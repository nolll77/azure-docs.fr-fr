---
title: Clé gérée par le client dans Azure Monitor
description: Informations et étapes relatives à la configuration de CMK (Customer-Managed Key) pour chiffrer des données dans vos espaces de travail Log Analytics à l’aide d’une clé Azure Key Vault.
ms.subservice: logs
ms.topic: conceptual
author: yossi-y
ms.author: yossiy
ms.date: 09/09/2020
ms.openlocfilehash: 532d96163e2ec66730dc3fdf87f10904fd584224
ms.sourcegitcommit: ae6e7057a00d95ed7b828fc8846e3a6281859d40
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/16/2020
ms.locfileid: "92107995"
---
# <a name="azure-monitor-customer-managed-key"></a>Clé gérée par le client dans Azure Monitor 

Cet article fournit des informations générales et des étapes pour configurer des clés gérées par le client (CMK, Customer-Managed Keys) qui sont destinées à vos espaces de travail Log Analytics. Une fois la configuration effectuée, toutes les données envoyées à vos espaces de travail sont chiffrées au moyen de votre clé Azure Key Vault.

Nous vous recommandons de passer en revue les [Limitations et contraintes](#limitationsandconstraints) ci-dessous avant de procéder à la configuration.

## <a name="customer-managed-key-cmk-overview"></a>Vue d’ensemble des clés gérées par le client (CMK)

Le [chiffrement au repos](../../security/fundamentals/encryption-atrest.md) est une exigence de sécurité et de confidentialité courante dans les organisations. Vous pouvez laisser Azure gérer complètement le chiffrement au repos, mais vous disposez aussi de plusieurs options pour gérer étroitement le chiffrement ou les clés de chiffrement.

Azure Monitor veille à ce que toutes les données et requêtes enregistrées soient chiffrées au repos à l’aide de clés gérées par Microsoft (MMK). Azure Monitor fournit également une option de chiffrement à l’aide de votre propre clé qui est stockée dans votre [Azure Key Vault](../../key-vault/general/overview.md) et accessible à l’aide de l’authentification par [identité managée](../../active-directory/managed-identities-azure-resources/overview.md) attribuée par le système. Cette clé (CMK) peut être [protégée par un logiciel ou par un HSM matériel](../../key-vault/general/overview.md). L’utilisation du chiffrement par Azure Monitor est identique à celle du [chiffrement par Stockage Azure](../../storage/common/storage-service-encryption.md#about-azure-storage-encryption).

La capacité de clé gérée par le client est fournie sur des clusters Log Analytics dédiés et vous permet de révoquer l’accès à vos données à tout moment et de les protéger avec le contrôle [Lockbox](#customer-lockbox-preview). Pour vérifier que nous disposons de la capacité requise pour un cluster dédié dans votre région, votre abonnement doit nécessairement être autorisé au préalable. Avant de commencer à configurer une clé CMK, demandez à votre contact Microsoft d’autoriser votre abonnement.

Le [modèle de tarification des clusters Log Analytics](./manage-cost-storage.md#log-analytics-dedicated-clusters) utilise des réservations de capacité à partir de 1 000 Go/jour.

Les données ingérées au cours des 14 derniers jours sont également conservées dans le cache à chaud (SSD) afin d’optimiser l’utilisation du moteur de requête. Ces données restent chiffrées avec des clés Microsoft, quelle que soit la configuration de clé gérée par le client, mais votre contrôle sur les données SSD est sujet à une [révocation de clé](#cmk-kek-revocation). Nous travaillerons à l’implémentation de données SSD chiffrées avec clé CMK au cours de la seconde moitié de 2020.

## <a name="how-cmk-works-in-azure-monitor"></a>Fonctionnement de CMK dans Azure Monitor

Azure Monitor tire parti de l’identité managée attribuée par le système pour accorder l’accès à votre coffre de clés Azure. L’identité gérée attribuée par le système ne peut être associée qu’à une seule ressource Azure, tandis que l’identité du cluster Log Analytics est prise en charge au niveau du cluster. Cela exige que la capacité de clé CMK soit fournie sur un cluster Log Analytics dédié. Pour prendre en charge la capacité de clé CMK sur plusieurs espaces de travail, une nouvelle ressource *cluster* Log Analytics s’exécute en tant que connexion d’identité intermédiaire entre votre Key Vault et vos espaces de travail Log Analytics. Le stockage en cluster Log Analytics utilise l’identité gérée associée à la ressource *cluster* pour s’authentifier auprès de votre Azure Key Vault via Azure Active Directory. 

Après la configuration d’une clé CMK, toutes les données ingérées dans les espaces de travail liés à votre cluster dédié sont chiffrées à l’aide de votre clé stockée dans Key Vault. Vous pouvez dissocier les espaces de travail du cluster à tout moment. Les nouvelles données sont ingérées dans un stockage Log Analytics et chiffrées avec une clé Microsoft. Et vous pouvez interroger vos données, nouvelles et anciennes, sans la moindre difficulté.


![Vue d’ensemble de CMK](media/customer-managed-keys/cmk-overview.png)

1. Key Vault
2. Ressource *cluster* Log Analytics ayant une identité gérée avec des autorisations pour Key Vault. L’identité est propagée vers le stockage de cluster Log Analytics dédié sous-jacent.
3. Cluster Log Analytics dédié.
4. Espaces de travail liés à la ressource *cluster* pour le chiffrement par clé CMK

## <a name="encryption-keys-operation"></a>Opération de clés de chiffrement

Il existe trois types de clés impliquées dans le chiffrement des données de Stockage :

- **KEK** - Clé de chiffrement principale (CMK)
- **AEK**  : clé de chiffrement de compte
- **DEK**  : clé de chiffrement de données

Les règles suivantes s’appliquent :

- Les comptes de stockage de cluster Log Analytics génèrent une clé de chiffrement unique pour chaque compte de stockage, appelée clé de chiffrement de compte (AEK, Account Encryption Key).

- La clé AEK est utilisé pour dériver les clés DEK, clés utilisées pour chiffrer chaque bloc de données écrites sur le disque.

- Lorsque vous configurez votre clé dans Key Vault et que vous la référencez dans le cluster, Stockage Azure envoie des requêtes à votre Azure Key Vault pour envelopper et désenvelopper l’AEK afin d’effectuer des opérations de chiffrement et de déchiffrement de données.

- Votre clé KEK ne quitte jamais votre coffre de clés et, dans le cas d’une clé HSM, elle ne quitte jamais le matériel.

- Stockage Azure utilise l’identité managée associée à la ressource *cluster* pour s’authentifier et accéder à Azure Key Vault par le biais d’Azure Active Directory.

## <a name="cmk-provisioning-procedure"></a>Procédure de provisionnement de CMK

1. Autorisation de l’abonnement : la capacité de clé CMK est fournie sur des clusters Log Analytics dédiés. Pour vérifier que nous disposons de la capacité requise dans votre région, votre abonnement doit nécessairement être autorisé au préalable. Demandez à votre contact Microsoft d’autoriser votre abonnement.
2. Création du coffre de clés Azure et stockage de la clé
3. Création du cluster
4. Octroi d’autorisations d’accès à votre coffre de clés
5. Liaison d’espaces de travail Log Analytics

La configuration de clé CMK n’est pas prise en charge dans le portail Azure et l’approvisionnement est effectué par le biais de requêtes [PowerShell](https://docs.microsoft.com/powershell/module/az.operationalinsights/), [CLI](https://docs.microsoft.com/cli/azure/monitor/log-analytics) ou [REST](https://docs.microsoft.com/rest/api/loganalytics/).

### <a name="asynchronous-operations-and-status-check"></a>Opérations asynchrones et vérification de l’état

Certaines étapes de configuration s’exécutent de façon asynchrone, car elles ne peuvent pas être effectuées rapidement. Lors de l’utilisation de requêtes REST dans la configuration, la réponse retourne initialement un code d’état HTTP 200 (OK) et un en-tête avec la propriété *Azure-AsyncOperation* lorsqu’elle est acceptée :
```json
"Azure-AsyncOperation": "https://management.azure.com/subscriptions/subscription-id/providers/Microsoft.OperationalInsights/locations/region-name/operationStatuses/operation-id?api-version=2020-08-01"
```

Pour vérifier l’état de l’opération asynchrone, envoyez une requête GET dans la valeur d’en-tête *Azure-AsyncOperation*  :
```rst
GET https://management.azure.com/subscriptions/subscription-id/providers/microsoft.operationalInsights/locations/region-name/operationstatuses/operation-id?api-version=2020-08-01
Authorization: Bearer <token>
```

La réponse contient des informations sur l’opération et son *état* . Les valeurs possibles sont les suivantes :

L’opération est en cours
```json
{
    "id": "Azure-AsyncOperation URL value from the GET operation",
    "name": "operation-id", 
    "status" : "InProgress", 
    "startTime": "2017-01-06T20:56:36.002812+00:00",
}
```

L’opération de mise à jour de l’identificateur de clé est en cours.
```json
{
    "id": "Azure-AsyncOperation URL value from the GET operation",
    "name": "operation-id", 
    "status" : "Updating", 
    "startTime": "2017-01-06T20:56:36.002812+00:00",
    "endTime": "2017-01-06T20:56:56.002812+00:00",
}
```

La suppression du cluster est en cours : lorsque vous supprimez un cluster auquel des espaces de travail sont liés, l’opération de dissociation est effectuée pour chacun des espaces de travail de façon asynchrone et l’opération peut prendre du temps.
Cela ne s’applique pas lorsque vous supprimez un cluster sans espace de travail lié. Dans ce cas, le cluster est immédiatement supprimé.
```json
{
    "id": "Azure-AsyncOperation URL value from the GET operation",
    "name": "operation-id", 
    "status" : "Deleting", 
    "startTime": "2017-01-06T20:56:36.002812+00:00",
    "endTime": "2017-01-06T20:56:56.002812+00:00",
}
```

L’opération est terminée
```json
{
    "id": "Azure-AsyncOperation URL value from the GET operation",
    "name": "operation-id", 
    "status" : "Succeeded", 
    "startTime": "2017-01-06T20:56:36.002812+00:00",
    "endTime": "2017-01-06T20:56:56.002812+00:00",
}
```

L’opération a échoué
```json
{
    "id": "Azure-AsyncOperation URL value from the GET operation",
    "name": "operation-id", 
    "status" : "Failed", 
    "startTime": "2017-01-06T20:56:36.002812+00:00",
    "endTime": "2017-01-06T20:56:56.002812+00:00",
    "error" : { 
        "code": "error-code",  
        "message": "error-message" 
    }
}
```

### <a name="allowing-subscription-for-cmk-deployment"></a>Autorisation de l’abonnement pour le déploiement de la clé CMK

La capacité de clé CMK est fournie sur des clusters Log Analytics dédiés. Pour vérifier que nous disposons de la capacité requise dans votre région, votre abonnement doit nécessairement être autorisé au préalable. Utilisez vos contacts au sein de Microsoft pour fournir vos ID d’abonnement.

> [!IMPORTANT]
> La fonctionnalité CMK est régionale. Vos Azure Key Vault, le cluster et les espaces de travail Log Analytics liés doivent se trouver dans la même région, mais ils peuvent être dans des abonnements différents.

### <a name="storing-encryption-key-kek"></a>Stockage de la clé de chiffrement (KEK)

Créez un coffre de clés Azure, ou utilisez-en un existant, pour générer ou importer une clé à utiliser pour le chiffrement des données. Le coffre de clés Azure doit être configuré comme récupérable pour protéger votre clé et l’accès à vos données Azure Monitor. Vous pouvez vérifier cette configuration dans les propriétés de votre coffre de clés : les fonctionnalités de *suppression réversible* et de *protection contre la suppression définitive* doivent être activées.

![Paramètres de suppression réversible et de protection contre la suppression définitive](media/customer-managed-keys/soft-purge-protection.png)

Ces paramètres peuvent être mis à jour par le biais de l’interface CLI et de PowerShell :

- [Suppression réversible](../../key-vault/general/soft-delete-overview.md)
- La [protection contre la suppression définitive](../../key-vault/general/soft-delete-overview.md#purge-protection) protège contre la suppression forcée du secret ou du coffre, même après activation de la suppression réversible.

### <a name="create-cluster"></a>Créer un cluster

Suivez la procédure illustrée dans l’article sur les [Clusters dédiés](https://docs.microsoft.com/azure/azure-monitor/log-query/logs-dedicated-clusters#creating-a-cluster). 

> [!IMPORTANT]
> Copiez et enregistrez la réponse, car vous aurez besoin des détails aux étapes suivantes.

### <a name="grant-key-vault-permissions"></a>Octroi d’autorisations d’accès au coffre de clés

Mettez à jour votre Key Vault avec une nouvelle stratégie d’accès pour accorder des autorisations à votre cluster. Ces autorisations sont utilisées par le Stockage Azure Monitor sous-jacent pour le chiffrement des données. Ouvrez votre coffre de clés dans le portail Azure, puis cliquez sur « Stratégies d’accès », puis sur « + Ajouter une stratégie d’accès » pour créer une stratégie avec les paramètres ci-après :

- Autorisations de clé : sélectionnez « Obtenir », « Inclure la clé » et « Ne pas inclure la clé ».
- Sélectionner le principal : entrez le nom du cluster ou la valeur principal-id retournée dans la réponse à l’étape précédente.

![Octroi d’autorisations d’accès au coffre de clés](media/customer-managed-keys/grant-key-vault-permissions-8bit.png)

L’autorisation *Obtenir* est nécessaire pour vérifier que votre coffre de clés est configuré comme récupérable pour protéger votre clé et l’accès à vos données Azure Monitor.

### <a name="update-cluster-with-key-identifier-details"></a>Mettre à jour le cluster avec les détails de l’identificateur de clé

Toutes les opérations effectuées sur le cluster nécessitent l’autorisation Microsoft.OperationalInsights/clusters/write action. Cette autorisation peut être accordée via le Propriétaire ou le Contributeur qui contient l’action */write ou via le rôle Contributeur Log Analytics qui contient l’action Microsoft.OperationalInsights/* .

Cette étape met à jour le stockage Azure Monitor avec la clé et la version à utiliser pour le chiffrement des données. Une fois mise à jour, votre nouvelle clé est utilisée pour envelopper et désenvelopper la clé de stockage (AEK).

Sélectionnez la version actuelle de votre clé dans Azure Key Vault pour afficher les détails de l’identificateur de clé.

![Octroi d’autorisations d’accès au coffre de clés](media/customer-managed-keys/key-identifier-8bit.png)

Mettez à jour la propriété KeyVaultProperties du cluster avec les détails de l’identificateur de clé.

L’opération est asynchrone et peut prendre du temps.

```powershell
Update-AzOperationalInsightsCluster -ResourceGroupName "resource-group-name" -ClusterName "cluster-name" -KeyVaultUri "key-uri" -KeyName "key-name" -KeyVersion "key-version"
```

> [!NOTE]
> Vous pouvez mettre à jour les valeurs *sku* , *keyVaultProperties* ou *billingType* du cluster à l’aide de l’instruction PATCH.

```rst
PATCH https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.OperationalInsights/clusters/<cluster-name>?api-version=2020-08-01
Authorization: Bearer <token>
Content-type: application/json

{
   "identity": { 
     "type": "systemAssigned" 
     },
   "sku": {
     "name": "capacityReservation",
     "capacity": 1000
     },
   "properties": {
    "billingType": "cluster",
     "KeyVaultProperties": {
       "KeyVaultUri": "https://<key-vault-name>.vault.azure.net",
       "KeyName": "<key-name>",
       "KeyVersion": "<current-version>"
       }
   },
   "location":"<region-name>"
}
```

**Réponse**

200 OK et en-tête.
La propagation de l’identificateur de clé prend quelques minutes. Vous pouvez vérifier l’état de la mise à jour de deux manières :
1. Copiez la valeur de l’URL Azure-AsyncOperation à partir de la réponse et suivez les instructions de[contrôle de l’état des opérations asynchrones](#asynchronous-operations-and-status-check).
2. Envoyez une requête GET sur le cluster, puis examinez les propriétés *KeyVaultProperties* . Les détails de l’identificateur de clé récemment mis à jour doivent être retournés dans la réponse.

Une réponse à la requête GET doit ressembler à ceci lorsque la mise à jour de l’identificateur de clé est terminée :

```json
{
  "identity": {
    "type": "SystemAssigned",
    "tenantId": "tenant-id",
    "principalId": "principle-id"
    },
  "sku": {
    "name": "capacityReservation",
    "capacity": 1000,
    "lastSkuUpdate": "Sun, 22 Mar 2020 15:39:29 GMT"
    },
  "properties": {
    "keyVaultProperties": {
      "keyVaultUri": "https://key-vault-name.vault.azure.net",
      "kyName": "key-name",
      "keyVersion": "current-version"
      },
    "provisioningState": "Succeeded",
    "billingType": "cluster",
    "clusterId": "cluster-id"
  },
  "id": "/subscriptions/subscription-id/resourceGroups/resource-group-name/providers/Microsoft.OperationalInsights/clusters/cluster-name",
  "name": "cluster-name",
  "type": "Microsoft.OperationalInsights/clusters",
  "location": "region-name"
}
```

### <a name="link-workspace-to-cluster"></a>Lier un espace de travail à un cluster

Pour effectuer cette opération, vous devez disposer des autorisations « écrire » sur votre espace de travail et le cluster, ce qui implique notamment les actions suivantes :

- Dans l'espace de travail : Microsoft.OperationalInsights/workspaces/write
- Dans le cluster : Microsoft.OperationalInsights/clusters/write

> [!IMPORTANT]
> Cette étape ne doit être accomplie qu’une fois l’approvisionnement du cluster Log Analytics terminé. Si vous liez des espaces de travail et ingérez des données avant cet approvisionnement, les données ingérées sont définitivement supprimées.

Cette opération est asynchrone et peut durer un certain temps.

Suivez la procédure illustrée dans l’article sur les [Clusters dédiés](https://docs.microsoft.com/azure/azure-monitor/log-query/logs-dedicated-clusters#link-a-workspace-to-the-cluster).

## <a name="cmk-kek-revocation"></a>Révocation de clé CMK (KEK)

Vous pouvez révoquer l’accès aux données en désactivant votre clé ou en supprimant la stratégie d’accès du cluster dans votre Key Vault. Le stockage de cluster Log Analytics respecte toujours les modifications des autorisations de clé en maximum une heure. Il devient alors indisponible. Toutes les nouvelles données ingérées dans les espaces de travail liés à votre cluster sont définitivement supprimées. Les données sont donc inaccessibles et les requêtes adressées à ces espaces de travail échouent. Les données précédemment ingérées restent dans le stockage tant que votre cluster et vos espaces de travail ne sont pas supprimés. Les données inaccessibles sont régies par la stratégie de conservation des données et sont vidées à la fin de la durée de conservation. 

Les données ingérées au cours des 14 derniers jours sont également conservées dans le cache à chaud (SSD) pour optimiser l’utilisation du moteur de requête. Elles sont supprimées lors d’une opération de révocation de clé et devient également inaccessibles.

Le stockage sonde régulièrement votre Key Vault pour tenter de désencapsuler la clé de chiffrement et, une fois qu’il y a accès, l’ingestion et l’interrogation des données reprennent dans un délai de 30 minutes.

## <a name="cmk-kek-rotation"></a>Rotation de clé CMK (KEK)

La rotation de clé CMK nécessite une mise à jour explicite du cluster avec la nouvelle version de clé dans Azure Key Vault. Suivez les instructions de l’étape « Mettre à jour le cluster avec les détails de l’identificateur de clé ». Si vous ne mettez pas à jour les nouveaux détails de l’identificateur de clé dans le cluster, le stockage de cluster Log Analytics continue d’utiliser votre clé précédente pour le chiffrement. Si vous désactivez ou supprimez votre ancienne clé avant de mettre à jour la nouvelle dans le cluster, vous passez à l’état [révocation de clé](#cmk-kek-revocation).

Toutes vos données restent accessibles après l’opération de rotation de clé, car les données sont toujours chiffrées avec la clé de chiffrement de compte (AEK, Account Encryption Key), tandis que celle-ci est désormais chiffrée avec votre nouvelle version de clé de chiffrement de clé (KEK, Key Encryption Key) dans Key Vault.

## <a name="cmk-for-queries"></a>Clé CMK pour les requêtes

Le langage de requête utilisé dans Log Analytics est expressif et peut contenir des informations sensibles dans les commentaires que vous ajoutez aux requêtes ou dans la syntaxe de requête. Certaines organisations requièrent que ces informations soient protégées dans le cadre de la stratégie CMK et vous devez sauvegarder vos requêtes en les chiffrant avec votre clé. Azure Monitor vous permet de stocker des requêtes de *recherches enregistrées* et d’ *alertes de journal* chiffrées avec votre clé dans votre propre compte de stockage lorsque vous êtes connecté à votre espace de travail. 

> [!NOTE]
> Les requêtes Log Analytics peuvent être enregistrées dans différents magasins en fonction du scénario utilisé. Les requêtes restent chiffrées avec Microsoft Key (MMK) dans les scénarios suivants, quelle que soit la configuration de CMK : Classeurs dans Azure Monitor, tableaux de bord Azure, application logique Azure, Azure Notebooks et Automation Runbooks.

Lorsque vous apportez votre propre stockage (BYOS) et que vous le liez à votre espace de travail, le service charge les requêtes de *recherches enregistrées* et d’ *alertes de journal* dans votre compte de stockage. Cela signifie que vous contrôlez le compte de stockage et la [stratégie de chiffrement au repos](../../storage/common/customer-managed-keys-overview.md) à l’aide de la même clé que celle utilisée pour chiffrer les données dans le cluster Log Analytics ou d’une clé différente. Toutefois, vous êtes responsable des coûts associés à ce compte de stockage. 

**Considérations à prendre en compte avant de définir la clé CMK pour les requêtes**
* Vous devez disposer d’autorisations d’écriture pour votre espace de travail et votre compte de stockage.
* Veillez à créer votre compte de stockage dans la même région que celle où se trouve votre espace de travail Log Analytics.
* Les *recherches enregistrées* en stockage sont considérées comme des artefacts de service et leur format peut changer.
* Les *recherches enregistrées* existantes sont supprimées de votre espace de travail. Copiez toutes les *recherches enregistrées* dont vous avez besoin avant la configuration. Vous pouvez afficher vos *recherches enregistrées* à l’aide de [PowerShell](/powershell/module/az.operationalinsights/get-azoperationalinsightssavedsearch).
* L’historique des requêtes n’est pas pris en charge et vous ne pouvez pas voir les requêtes que vous avez exécutées.
* Vous pouvez lier un seul compte de stockage à l’espace de travail pour l’enregistrement des requêtes, mais il peut être utilisé pour les requêtes de *recherches enregistrées* et d’ *alertes de journal* .
* L’action d’épingler au tableau de bord n’est pas prise en charge.

**Configurer BYOS pour les requêtes de recherches enregistrées**

Liez un compte de stockage à *interroger* à votre espace de travail. Les requêtes de *recherches enregistrées* sont enregistrées dans votre compte de stockage. 

```powershell
$storageAccount.Id = Get-AzStorageAccount -ResourceGroupName "resource-group-name" -Name "storage-account-name"
New-AzOperationalInsightsLinkedStorageAccount -ResourceGroupName "resource-group-name" -WorkspaceName "workspace-name" -DataSourceType Query -StorageAccountIds $storageAccount.Id
```

```rst
PUT https://management.azure.com/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.OperationalInsights/workspaces/<workspace-name>/linkedStorageAccounts/Query?api-version=2020-08-01
Authorization: Bearer <token> 
Content-type: application/json
 
{
  "properties": {
    "dataSourceType": "Query", 
    "storageAccountIds": 
    [
      "/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Storage/storageAccounts/<storage-account-name>"
    ]
  }
}
```

Après la configuration, toute nouvelle requête *de recherche enregistrée* sera sauvegardée dans votre stockage.

**Configurer BYOS pour les requêtes d’alertes de journal**

Liez un compte de stockage pour les *alertes* à votre espace de travail. Les requêtes d’ *alertes de journal* sont enregistrées dans votre compte de stockage. 

```powershell
$storageAccount.Id = Get-AzStorageAccount -ResourceGroupName "resource-group-name" -Name "storage-account-name"
New-AzOperationalInsightsLinkedStorageAccount -ResourceGroupName "resource-group-name" -WorkspaceName "workspace-name" -DataSourceType Alerts -StorageAccountIds $storageAccount.Id
```

```rst
PUT https://management.azure.com/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.OperationalInsights/workspaces/<workspace-name>/linkedStorageAccounts/Alerts?api-version=2020-08-01
Authorization: Bearer <token> 
Content-type: application/json
 
{
  "properties": {
    "dataSourceType": "Alerts", 
    "storageAccountIds": 
    [
      "/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Storage/storageAccounts/<storage-account-name>"
    ]
  }
}
```

Après la configuration, toute nouvelle requête d’alerte sera sauvegardée dans votre stockage.

## <a name="customer-lockbox-preview"></a>Customer Lockbox (préversion)
Lockbox vous permet d’approuver ou de rejeter la demande d’un ingénieur Microsoft d’accéder à vos données lors d’une demande de support.

Dans Azure Monitor, vous disposez de ce contrôle sur les données des espaces de travail liés à votre cluster Log Analytics dédié. Le contrôle Lockbox s’applique aux données stockées dans un cluster Log Analytics dédié dans lequel elles sont maintenues isolées dans les comptes de stockage du cluster configurés dans votre abonnement protégé par Lockbox.  

En savoir plus sur [Customer Lockbox pour Microsoft Azure](../../security/fundamentals/customer-lockbox-overview.md)

## <a name="cmk-management"></a>Gestion de clé CMK

- **Obtenir tous les clusters dans un groupe de ressources**
  
  ```powershell
  Get-AzOperationalInsightsCluster -ResourceGroupName "resource-group-name"
  ```

  ```rst
  GET https://management.azure.com/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.OperationalInsights/clusters?api-version=2020-08-01
  Authorization: Bearer <token>
  ```

  **Réponse**
  
  ```json
  {
    "value": [
      {
        "identity": {
          "type": "SystemAssigned",
          "tenantId": "tenant-id",
          "principalId": "principal-Id"
        },
        "sku": {
          "name": "capacityReservation",
          "capacity": 1000,
          "lastSkuUpdate": "Sun, 22 Mar 2020 15:39:29 GMT"
          },
        "properties": {
           "keyVaultProperties": {
              "keyVaultUri": "https://key-vault-name.vault.azure.net",
              "keyName": "key-name",
              "keyVersion": "current-version"
              },
          "provisioningState": "Succeeded",
          "billingType": "cluster",
          "clusterId": "cluster-id"
        },
        "id": "/subscriptions/subscription-id/resourcegroups/resource-group-name/providers/microsoft.operationalinsights/workspaces/workspace-name",
        "name": "cluster-name",
        "type": "Microsoft.OperationalInsights/clusters",
        "location": "region-name"
      }
    ]
  }
  ```

- **Obtenir tous les clusters dans un abonnement**
  
  ```powershell
  Get-AzOperationalInsightsCluster
  ```

  ```rst
  GET https://management.azure.com/subscriptions/<subscription-id>/providers/Microsoft.OperationalInsights/clusters?api-version=2020-08-01
  Authorization: Bearer <token>
  ```
    
  **Réponse**
    
  La même réponse que pour « cluster dans un groupe de ressources », mais dans l’étendue d’un abonnement.

- **Mettre à jour la *réservation de capacité* dans un cluster**

  À mesure que le volume de données de vos espaces de travail liés change au fil du temps, vous souhaitez mettre à jour le niveau de réservation de capacité de manière appropriée. Suivez la [mise à jour du cluster](#update-cluster-with-key-identifier-details) et fournissez votre nouvelle valeur de capacité. Celle-ci peut varier entre 1000 et 3000 Go par jour par incréments de 100. Pour un niveau de réservation de capacité supérieur à 3000 Go par jour, adressez-vous à votre contact Microsoft pour l’activer. Notez que vous n’avez pas besoin de fournir le corps entier de la requête REST et que vous devez inclure la propriété sku :

  ```powershell
  Update-AzOperationalInsightsCluster -ResourceGroupName "resource-group-name" -ClusterName "cluster-name" -SkuCapacity "daily-ingestion-gigabyte"
  ```

  ```rst
  PATCH https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.OperationalInsights/clusters/<cluster-name>?api-version=2020-08-01
  Authorization: Bearer <token>
  Content-type: application/json

  {
    "sku": {
      "name": "capacityReservation",
      "Capacity": 1000
    }
  }
  ```

- **Mettre à jour la propriété *billingType* dans le cluster**

  La propriété *billingType* détermine l’attribution de facturation pour le cluster et ses données :
  - *cluster* (par défaut) : la facturation est attribuée à l’abonnement hébergeant votre ressource cluster.
  - *workspaces*  : la facturation est attribuée de façon proportionnée aux abonnements hébergeant vos espaces de travail.
  
  Suivez la [mise à jour du cluster](#update-cluster-with-key-identifier-details) et fournissez votre nouvelle valeur de billingType. Notez que vous n’avez pas besoin de fournir tout le corps de la requête REST et que vous devez inclure la propriété *billingType*  :

  ```rst
  PATCH https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.OperationalInsights/clusters/<cluster-name>?api-version=2020-08-01
  Authorization: Bearer <token>
  Content-type: application/json

  {
    "properties": {
      "billingType": "cluster",
      }  
  }
  ``` 

- **Dissocier l’espace de travail**

  Pour effectuer cette opération, vous devez disposer des autorisations d’écriture sur l’espace de travail et le cluster. Vous pouvez dissocier un espace de travail de votre cluster à tout moment. Les nouvelles données ingérées après l’opération de dissociation sont stockées dans le stockage Log Analytics et chiffrées avec une clé Microsoft. Vous pouvez interroger en toute transparence les données ingérées dans votre espace de travail avant et après la dissociation tant que le cluster est approvisionné et configuré avec une clé de Key Vault valide.

  Cette opération est asynchrone et peut durer un certain temps.

  ```powershell
  Remove-AzOperationalInsightsLinkedService -ResourceGroupName "resource-group-name" -Name "workspace-name" -LinkedServiceName cluster
  ```

  ```rest
  DELETE https://management.azure.com/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/microsoft.operationalinsights/workspaces/<workspace-name>/linkedservices/cluster?api-version=2020-08-01
  Authorization: Bearer <token>
  ```

  **Réponse**

  200 OK et en-tête.

  Les données ingérées après l’opération de dissociation sont stockées dans le stockage Log Analytics. Cela peut prendre jusqu’à 90 minutes. Vous pouvez vérifier l’état de dissociation de l’espace de travail de deux manières :

  1. Copiez la valeur de l’URL Azure-AsyncOperation à partir de la réponse et suivez les instructions de[contrôle de l’état des opérations asynchrones](#asynchronous-operations-and-status-check).
  2. Envoyez une requête [Workspaces – Get](/rest/api/loganalytics/workspaces/get) et observez la réponse. L’espace de travail dissocié n’a pas d’identificateur *clusterResourceId* sous *features* .

- **Vérifier l’état d’association de l’espace de travail**
  
  Effectuez une opération Get sur l’espace de travail et observez si la propriété *clusterResourceId* est présente dans la réponse sous *Fonctionnalités* . Un espace de travail lié comprend la propriété *clusterResourceId* .

  ```powershell
  Get-AzOperationalInsightsWorkspace -ResourceGroupName "resource-group-name" -Name "workspace-name"
  ```

- **Supprimer votre cluster**

  Pour effectuer cette opération, vous devez disposer des autorisations d’écriture sur le cluster. Une opération de suppression réversible est effectuée pour permettre la récupération de votre cluster, y compris ses données, dans un délai de 14 jours, que la suppression ait été accidentelle ou intentionnelle. Le nom du cluster reste réservé pendant la période de suppression réversible et vous ne pouvez pas l’utiliser pour un autre cluster. À l’issue la période de suppression réversible, le nom du cluster redevient disponible et votre cluster ainsi que ses données sont définitivement supprimés et ne peuvent pas être récupérés. Tout espace de travail lié est dissocié du cluster lors de l’opération de suppression. Les nouvelles données ingérées sont stockées dans le stockage Log Analytics et chiffrées avec une clé Microsoft. 
  
  L’opération de dissociation est asynchrone et peut prendre jusqu’à 90 minutes.

  ```powershell
  Remove-AzOperationalInsightsCluster -ResourceGroupName "resource-group-name" -ClusterName "cluster-name"
  ```

  ```rst
  DELETE https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.OperationalInsights/clusters/<cluster-name>?api-version=2020-08-01
  Authorization: Bearer <token>
  ```

  **Réponse**

  200 OK

- **Récupérer votre cluster et vos données** 
  
  Un cluster supprimé au cours des 14 derniers jours est dans un état de suppression réversible. Il est possible de le récupérer avec ses données. Étant donné que tous les espaces de travail ont été dissociés du cluster lors de sa suppression, vous devez réassocier vos espaces de travail après la récupération du chiffrement par clé CMK. Actuellement, cette opération de récupération est effectuée manuellement par le groupe de produits. Utilisez votre canal Microsoft pour les demandes de récupération.

## <a name="limitations-and-constraints"></a>Limitations et contraintes

- La clé CMK est prise en charge sur un cluster Log Analytics dédié, et convient pour des clients qui envoient au moins 1 To par jour.

- Le nombre maximal de clusters par région et abonnement est de 2

Le nombre maximal d’espaces de travail liés à un cluster est de 100

- Vous pouvez lier un espace de travail à votre cluster puis le dissocier si une clé CMK n’est pas requise pour l’espace de travail. Le nombre de liaisons d’espaces de travail sur un espace de travail particulier est limité à 2 sur une période de 30 jours.

- Vous ne devez lier un espace de travail à un cluster qu’APRÈS avoir vérifié que l’approvisionnement du cluster Log Analytics est terminé. Les données envoyées à votre espace de travail avant la fin de l’approvisionnement seront définitivement supprimées.

- Le chiffrement CMK s’applique aux données nouvellement ingérées après la configuration de CMK. Les données qui ont été ingérées avant la configuration de CMK demeurent chiffrées avec la clé Microsoft. Vous pouvez interroger les données ingérées avant et après la configuration de CMK de manière fluide.

- Le coffre de clés Azure doit être configuré comme récupérable. Les propriétés ci-après, qui ne sont pas activées par défaut, doivent être configurées à l’aide de l’interface CLI ou de PowerShell :<br>
  - [Suppression réversible](../../key-vault/general/soft-delete-overview.md)
  - La [protection contre le vidage](../../key-vault/general/soft-delete-overview.md#purge-protection) doit être activée pour bénéficier d’une protection contre la suppression forcée du secret ou du coffre, même après activation de la suppression réversible.

- Le déplacement d’un cluster vers un autre groupe de ressources ou abonnement n’est pas pris en charge.

- Votre Azure Key Vault, le cluster et les espaces de travail liés doivent se trouver dans la même région et dans le même locataire Azure Active Directory (Azure AD) mais peuvent être dans des abonnements différents.

- La liaison d’un espace de travail à un cluster échoue s’il est lié à un autre cluster

## <a name="troubleshooting"></a>Dépannage

- Comportement avec disponibilité du Key Vault
  - En temps normal, le Stockage met en cache la clé AEK pendant de courtes périodes et revient régulièrement dans Key Vault pour la désencapsulation.
    
  - Erreurs de connexion temporaires : le Stockage gère les erreurs temporaires (délais d’attente, échecs de connexion, problèmes DNS) en autorisant les clés à rester en cache pendant un peu plus de temps, compensant toute courte période d’indisponibilité. Les fonctionnalités de requête et d’ingestion se poursuivent sans interruption.
    
  - Une indisponibilité du site actif d’environ 30 minutes entraîne l’indisponibilité du compte de stockage. La fonctionnalité de requête est indisponible et les données ingérées sont mises en cache pendant plusieurs heures à l’aide de la clé Microsoft pour éviter la perte de données. Quand l’accès à Key Vault est restauré, la requête est disponible et les données mises en cache temporaires sont ingérées dans le magasin de données et chiffrées avec CMK.

  - Taux d’accès au Key Vault : la fréquence à laquelle le stockage Azure Monitor accède au Key Vault pour les opérations d’encapsulation (wrap) et de désencapsulation (unwrap) est comprise entre 6 et 60 secondes.

- Si vous créez un cluster et spécifiez la propriété KeyVaultProperties immédiatement, l’opération peut échouer, car la stratégie d’accès ne peut pas être définie tant que l’identité système n’a pas été attribuée au cluster.

- Si vous mettez à jour le cluster existant avec KeyVaultProperties et que la stratégie d’accès de clé « Obtenir » est manquante dans Key Vault, l’opération échoue.

- Si vous recevez une erreur de conflit lors de la création d’un cluster, il est possible que vous ayez supprimé votre cluster au cours des derniers 14 jours et qu’il se trouve dans une période de suppression réversible. Le nom du cluster reste réservé pendant la période de suppression réversible et vous ne pouvez pas l’utiliser pour un autre cluster. Le nom est libéré après la période de suppression réversible, lorsque le cluster est définitivement supprimé.

- Si vous mettez à jour votre cluster alors qu’une opération est en cours, l’opération échoue.

- Si vous ne parvenez pas à déployer votre cluster, vérifiez que votre Azure Key Vault, le cluster et les espaces de travail Log Analytics liés se trouvent dans la même région. Ils peuvent être liés à des abonnements différents.

- Si vous mettez à jour votre version de clé dans Key Vault et ne mettez pas à jour les détails de l’identificateur de clé dans le cluster, le cluster Log Analytics continue d’utiliser votre clé précédente et vos données deviennent inaccessibles. Mettez à jour les nouveaux détails de l’identificateur de clé dans le cluster pour reprendre l’ingestion des données et avoir la possibilité d’interroger les données.

- Certaines opérations sont longues et peuvent prendre du temps. Il s’agit des opérations de création du cluster, de mise à jour de la clé du cluster et de la suppression du cluster. Vous pouvez vérifier l’état de l’opération de deux manières :
  1. Lorsque vous utilisez REST, copiez la valeur de l’URL Azure-AsyncOperation à partir de la réponse et suivez les instructions de[vérification de l’état des opérations asynchrones](#asynchronous-operations-and-status-check).
  2. Envoyez une requête GET au cluster ou à l’espace de travail du cluster et observez la réponse. Par exemple, l’espace de travail dissocié n’a pas de *clusterResourceId* sous *features* .

- Pour obtenir du support et de l’aide concernant la clé gérée par le client, utilisez vos contacts dans Microsoft.

- Messages d’erreur
  
  Création de cluster :
  -  400 -- Le nom du cluster n’est pas valide. Le nom du cluster peut contenir les caractères a-z, A-Z, 0-9 et doit compter entre 3 et 63 caractères.
  -  400 -- Le corps de la demande a la valeur null ou est dans un format incorrect.
  -  400 -- Nom de SKU non valide. Définissez le nom de la SKU sur capacityReservation.
  -  400 -- La capacité a été fournie, mais la référence SKU n’est pas capacityReservation. Définissez le nom de la SKU sur capacityReservation.
  -  400 -- Xapacité manquante dans la SKU. Définissez la valeur de capacité sur 1 000 ou plus par degrés de 100 (Go).
  -  400 -- La capacité dans la SKU n’est pas comprise dans la plage. Doit être au minimum de 1 000 et jusqu’à la capacité maximale autorisée, disponible sous « Utilisation et coût estimé » dans votre espace de travail.
  -  400 -- La capacité est verrouillée pendant 30 jours. La réduction de la capacité est autorisée 30 jours après la mise à jour.
  -  400 -- Aucune SKU n’a été définie. Définissez le nom de la SKU sur capacityReservation et la valeur de capacité sur 1 000 ou plus par degrés de 100 (Go).
  -  400 -- L’identité a la valeur nul ou est vide. Définissez l’identité avec le type systemAssigned.
  -  400 -- Les KeyVaultProperties sont définies à la création. Mettez à jour les KeyVaultProperties après la création du cluster.
  -  400 -- Impossible d’exécuter une opération pour le moment. L’opération asynchrone est dans un état autre que réussi. Le cluster doit effectuer cette opération avant l’exécution d’une opération de mise à jour.

  Mise à jour d’un cluster
  -  400 -- Le cluster est en cours de suppression. L’opération asynchrone est en cours. Le cluster doit effectuer cette opération avant l’exécution d’une opération de mise à jour.
  -  400 -- Les KeyVaultProperties ne sont pas vides, mais leur format est incorrect. Consultez [mise à jour de l’identificateur de la clé](#update-cluster-with-key-identifier-details).
  -  400 -- Échec de validation de la clé dans Key Vault. Peut être dû à un manque d’autorisations ou à l’inexistence de la clé. Vérifiez que vous [avez défini la clé et la stratégie d’accès](#grant-key-vault-permissions) dans Key Vault.
  -  400 -- La clé n’est pas récupérable. La suppression réversible et la protection contre le vidage doivent être définis pour Key Vault. Consulter la [documentation sur Key Vault](../../key-vault/general/soft-delete-overview.md)
  -  400 -- Impossible d’exécuter une opération pour le moment. Attendez que l’opération asynchrone se termine et réessayez.
  -  400 -- Le cluster est en cours de suppression. Attendez que l’opération asynchrone se termine et réessayez.

  Obtention de cluster :
    -  404 -- Cluster introuvable, le cluster a peut-être été supprimé. Si vous essayez de créer un cluster portant ce nom et que cela génère un conflit, le cluster est supprimé de manière réversible pendant 14 jours. Vous pouvez contacter le support technique pour le récupérer ou utiliser un autre nom pour créer un nouveau cluster. 

  Suppression de cluster
    -  409 -- Impossible de supprimer un cluster en état d’approvisionnement. Attendez que l’opération asynchrone se termine et réessayez.

  Liaison d’un espace de travail :
  -  404 -- Espace de travail introuvable. L’espace de travail que vous avez spécifié n’existe pas ou a été supprimé.
  -  409 -- Opération de liaison ou de dissociation d’espace de travail en cours.
  -  400 -- Cluster introuvable, le cluster que vous avez spécifié n’existe pas ou a été supprimé. Si vous essayez de créer un cluster portant ce nom et que cela génère un conflit, le cluster est supprimé de manière réversible pendant 14 jours. Contactez le support technique pour le récupérer.

  Dissociation d’un espace de travail :
  -  404 -- Espace de travail introuvable. L’espace de travail que vous avez spécifié n’existe pas ou a été supprimé.
  -  409 -- Opération de liaison ou de dissociation d’espace de travail en cours.
