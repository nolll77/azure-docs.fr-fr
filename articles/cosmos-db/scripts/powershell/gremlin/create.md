---
title: Script PowerShell pour créer une base de données et un graphe d’API Gremlin Azure Cosmos DB
description: Script Azure PowerShell - Azure Cosmos DB - Créer une base de données et un graphique pour l’API Gremlin
author: markjbrown
ms.service: cosmos-db
ms.subservice: cosmosdb-graph
ms.topic: sample
ms.date: 05/13/2020
ms.author: mjbrown
ms.openlocfilehash: 9be92ca8c976de7157f5602699ed64fdce78aaa6
ms.sourcegitcommit: 3bcce2e26935f523226ea269f034e0d75aa6693a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/23/2020
ms.locfileid: "92489215"
---
# <a name="create-a-database-and-graph-for-azure-cosmos-db---gremlin-api"></a>Créer une base de données et un graphique pour Azure Cosmos DB - API Gremlin

[!INCLUDE [updated-for-az](../../../../../includes/updated-for-az.md)]

[!INCLUDE [sample-powershell-install](../../../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a>Exemple de script

[!code-powershell[main](../../../../../powershell_scripts/cosmosdb/gremlin/ps-gremlin-create.ps1 "Create a database and graph for Gremlin API")]

## <a name="clean-up-deployment"></a>Nettoyer le déploiement

Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources et toutes les ressources associées.

```powershell
Remove-AzResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a>Explication du script

Ce script utilise les commandes suivantes. Chaque commande du tableau renvoie à une documentation spécifique.

| Commande | Notes |
|---|---|
|**Azure Cosmos DB**| |
| [New-AzCosmosDBAccount](/powershell/module/az.cosmosdb/new-azcosmosdbaccount) | Crée un compte Cosmos DB. |
| [New-AzCosmosDBGremlinDatabase](/powershell/module/az.cosmosdb/new-azcosmosdbgremlindatabase) | Crée une base de données d’API Gremlin. |
| [New-AzCosmosDBGremlinConflictResolutionPolicy](/powershell/module/az.cosmosdb/new-azcosmosdbgremlinconflictresolutionpolicy) | Crée une stratégie de résolution de conflit d’écriture d’API Gremlin. |
| [New-AzCosmosDBGremlinGraph](/powershell/module/az.cosmosdb/new-azcosmosdbgremlingraph) | Crée un graphe d’API Gremlin. |
|**Groupes de ressources Azure**| |
| [Remove-AzResourceGroup](/powershell/module/az.resources/remove-azresourcegroup) | Supprime un groupe de ressources, y compris toutes les ressources imbriquées. |
|||

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur Azure PowerShell, consultez la [documentation Azure PowerShell](/powershell/).