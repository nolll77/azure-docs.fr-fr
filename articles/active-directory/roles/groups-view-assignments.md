---
title: Afficher les rôles attribués à un groupe dans Azure Active Directory | Microsoft Docs
description: Découvrez la façon dont les rôles attribués à un groupe peuvent être consultés à l’aide du centre d’administration Azure AD. La consultation des groupes et des rôles attribués est une autorisation utilisateur par défaut.
services: active-directory
author: curtand
manager: daveba
ms.service: active-directory
ms.workload: identity
ms.subservice: users-groups-roles
ms.topic: article
ms.date: 07/27/2020
ms.author: curtand
ms.reviewer: vincesm
ms.custom: it-pro
ms.collection: M365-identity-device-management
ms.openlocfilehash: e578c90a05085df33c2d547402256cfc38229aa3
ms.sourcegitcommit: 28c5fdc3828316f45f7c20fc4de4b2c05a1c5548
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92373137"
---
# <a name="view-roles-assigned-to-a-group-in-azure-active-directory"></a>Afficher les rôles attribués à un groupe dans Azure Active Directory

Cette section décrit la façon dont les rôles attribués à un groupe peuvent être consultés à l’aide du centre d’administration Azure AD. La consultation des groupes et des rôles attribués est une autorisation utilisateur par défaut.

1. Connectez-vous au [centre d’administration Azure AD](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) avec les informations d’identification d’un compte administrateur ou non-administrateur.

1. Sélectionnez le groupe qui vous intéresse.

1. Sélectionnez **Rôles attribués** . Vous pouvez maintenant voir tous les rôles Azure AD attribués à ce groupe.

   ![Afficher tous les rôles attribués à un groupe sélectionné](./media/groups-view-assignments/view-assignments.png)

## <a name="using-powershell"></a>Utilisation de PowerShell

### <a name="get-object-id-of-the-group"></a>Obtenir l’ID d’objet du groupe

```powershell
Get-AzureADMSGroup -SearchString “Contoso_Helpdesk_Administrators”
```

### <a name="view-role-assignment-to-a-group"></a>Afficher l’attribution de rôle d’un groupe

```powershell
Get-AzureADMSRoleAssignment -Filter "principalId eq '<object id of group>" 
```

## <a name="using-microsoft-graph-api"></a>Utilisation de l’API Microsoft Graph

### <a name="get-object-id-of-the-group"></a>Obtenir l’ID d’objet du groupe

```powershell
GET https://graph.microsoft.com/beta/groups?$filter displayName eq ‘Contoso_Helpdesk_Administrator’ 
```

### <a name="get-role-assignments-to-a-group"></a>Obtenir les attributions de rôles d’un groupe

```powershell
GET https://graph.microsoft.com/beta/roleManagement/directory/roleAssignments?$filter=principalId eq
```

## <a name="next-steps"></a>Étapes suivantes

- [Utiliser des groupes cloud pour gérer les attributions de rôles](groups-concept.md)
- [Résolution des problèmes des rôles attribués aux groupes cloud](groups-faq-troubleshooting.md)
