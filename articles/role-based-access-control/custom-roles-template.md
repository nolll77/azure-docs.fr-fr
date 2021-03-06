---
title: Créer un rôle Azure personnalisé à l’aide d’un modèle Azure Resource Manage - Azure RBAC
description: Découvrez comment créer un rôle Azure personnalisé à l’aide des modèles Azure Resource Manager et du contrôle d’accès en fonction du rôle Azure (Azure RBAC).
services: role-based-access-control,azure-resource-manager
author: rolyon
manager: mtillman
ms.service: role-based-access-control
ms.topic: how-to
ms.custom: subject-armqs
ms.workload: identity
ms.date: 06/25/2020
ms.author: rolyon
ms.openlocfilehash: bcf1966ffc326291448cb611d99390fe0d652151
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "85397997"
---
# <a name="create-an-azure-custom-role-using-an-azure-resource-manager-template"></a>Créer un rôle Azure personnalisé à l’aide d’un modèle Azure Resource Manager

Si les [rôles intégrés Azure](built-in-roles.md) ne répondent pas aux besoins spécifiques de votre organisation, vous pouvez créer vos propres [rôles personnalisés](custom-roles.md). Cet article décrit la procédure de création d’un rôle personnalisé à l’aide d’un modèle Resource Manager.

[!INCLUDE [About Azure Resource Manager](../../includes/resource-manager-quickstart-introduction.md)]

## <a name="prerequisites"></a>Prérequis

Pour créer un rôle personnalisé, vous devez disposer des éléments suivants :

- autorisations nécessaires pour créer des rôles personnalisés, par exemple, [Propriétaire](built-in-roles.md#owner) ou [Administrateur de l’accès utilisateur](built-in-roles.md#user-access-administrator) ;

## <a name="create-a-custom-role"></a>Créer un rôle personnalisé

Pour créer un rôle personnalisé, vous spécifiez un nom de rôle, des autorisations et l’emplacement où le rôle peut être utilisé. Dans cet article, vous créez un rôle nommé « Custom Role - RG Reader » avec des autorisations de ressources qui peuvent être affectées au niveau d’une étendue d’abonnement ou moins.

### <a name="review-the-template"></a>Vérifier le modèle

Le modèle utilisé dans cet article provient des [Modèles de démarrage rapide Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/subscription-deployments/create-role-def). Le modèle dispose de quatre paramètres et d’une section de ressources. Les quatre paramètres sont :

- Le tableau des actions avec la valeur par défaut ["Microsoft.Resources/subscriptions/resourceGroups/read"]
- Le tableau des notActions avec une valeur par défaut vide
- Le nom du rôle avec la valeur par défaut « Role personnalisé - Lecteur RG »
- Description du rôle avec la valeur par défaut « Déploiement de niveau abonnement d’une définition de rôle »

La ressource définie dans le modèle est :

- [Microsoft.Authorization/roleDefinitions](/azure/templates/Microsoft.Authorization/roleDefinitions)

L’étendue d’attribution de ce rôle personnalisé est définie sur l’abonnement actuel.

:::code language="json" source="~/quickstart-templates/subscription-deployments/create-role-def/azuredeploy.json":::

### <a name="deploy-the-template"></a>Déployer le modèle

Procédez comme suit pour déployer le modèle précédent.

1. Connectez-vous au [portail Azure](https://portal.azure.com).

1. Ouvrez Azure Cloud Shell pour PowerShell.

1. Copiez et collez le script suivant dans Cloud Shell.

    ```azurepowershell
    $location = Read-Host -Prompt "Enter a location (i.e. centralus)"
    [string[]]$actions = Read-Host -Prompt "Enter actions as a comma-separated list (i.e. action1,action2)"
    $actions = $actions.Split(',')

    $templateUri = "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/subscription-deployments/create-role-def/azuredeploy.json"

    New-AzDeployment -Location $location -TemplateUri $templateUri -actions $actions
    ```

1. Entrez un emplacement pour le déploiement, tel que *centralus*.

1. Entrez une liste d’actions pour le rôle personnalisé sous la forme d’une liste séparée par des virgules, telle que *Microsoft.Resources/resources/read,Microsoft.Resources/subscriptions/resourceGroups/read*.

1. Si nécessaire, appuyez sur Entrée pour exécuter la commande New-AzDeployment.

    La commande [New-AzDeployment](/powershell/module/az.resources/new-azdeployment) déploie le modèle pour créer un rôle personnalisé.

    Vous devez obtenir une sortie similaire à la suivante :

    ```azurepowershell
    PS> New-AzDeployment -Location $location -TemplateUri $templateUri -actions $actions
    
    Id                      : /subscriptions/{subscriptionId}/providers/Microsoft.Resources/deployments/azuredeploy
    DeploymentName          : azuredeploy
    Location                : centralus
    ProvisioningState       : Succeeded
    Timestamp               : 6/25/2020 8:08:32 PM
    Mode                    : Incremental
    TemplateLink            :
                              Uri            : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/subscription-deployments/create-role-def/azuredeploy.json
                              ContentVersion : 1.0.0.0
    
    Parameters              :
                              Name               Type                       Value
                              =================  =========================  ==========
                              actions            Array                      [
                                "Microsoft.Resources/resources/read",
                                "Microsoft.Resources/subscriptions/resourceGroups/read"
                              ]
                              notActions         Array                      []
                              roleName           String                     Custom Role - RG Reader
                              roleDescription    String                     Subscription Level Deployment of a Role Definition
    
    Outputs                 :
    DeploymentDebugLogLevel :
    ```

## <a name="review-deployed-resources"></a>Vérifier les ressources déployées

Procédez comme suit pour vérifier que le rôle personnalisé a été créé.

1. Exécutez la commande [Get-AzRoleDefinition](/powershell/module/az.resources/get-azroledefinition) pour lister le rôle personnalisé.

    ```azurepowershell
    Get-AzRoleDefinition "Custom Role - RG Reader" | ConvertTo-Json
    ```

    Vous devez obtenir une sortie similaire à la suivante :

    ```azurepowershell
    {
      "Name": "Custom Role - RG Reader",
      "Id": "11111111-1111-1111-1111-111111111111",
      "IsCustom": true,
      "Description": "Subscription Level Deployment of a Role Definition",
      "Actions": [
        "Microsoft.Resources/resources/read",
        "Microsoft.Resources/subscriptions/resourceGroups/read"
      ],
      "NotActions": [],
      "DataActions": [],
      "NotDataActions": [],
      "AssignableScopes": [
        "/subscriptions/{subscriptionId}"
      ]
    }
    ```

1. Dans le portail Azure, ouvrez votre abonnement.

1. Dans le menu de gauche, cliquez sur **Contrôle d’accès (IAM)** .

1. Cliquez sur l’onglet **Rôles**.

1. Définissez la liste **Type** sur **CustomRole**.

1. Vérifiez que **Rôle personnalisé - Lecteur RG** est listé.

   ![Nouveau rôle personnalisé dans le portail Azure](./media/custom-roles-template/custom-role-template-portal.png)

## <a name="clean-up-resources"></a>Nettoyer les ressources

Pour supprimer le rôle personnalisé, procédez comme suit.

1. Exécutez la commande suivante pour supprimer le rôle personnalisé.

    ```azurepowershell
    Get-AzRoleDefinition -Name "Custom Role - RG Reader" | Remove-AzRoleDefinition
    ```

1. Entrez **Y** pour confirmer la suppression du rôle personnalisé.

## <a name="next-steps"></a>Étapes suivantes

- [Comprendre les définitions de rôles Azure](role-definitions.md)
- [Démarrage rapide : Ajouter une attribution de rôle Azure à l’aide d’un modèle Azure Resource Manager](quickstart-role-assignments-template.md)
- [Documentation sur les modèles ARM](../azure-resource-manager/templates/index.yml)
