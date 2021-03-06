---
title: Vue d'ensemble des serveurs avec Azure Arc
description: Apprenez à utiliser les serveurs avec Azure Arc afin de gérer les serveurs hébergés en dehors d'Azure comme une ressource Azure.
keywords: Azure Automation, DSC, PowerShell, Desired State Configuration, Update Management, Change Tracking, inventaire, runbooks, Python, graphique, hybride
ms.date: 10/15/2020
ms.topic: overview
ms.openlocfilehash: 01de579d2e1ea84c0e9da4ceafbd33dbad4c6e27
ms.sourcegitcommit: 9b8425300745ffe8d9b7fbe3c04199550d30e003
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/23/2020
ms.locfileid: "92460850"
---
# <a name="what-is-azure-arc-enabled-servers"></a>Qu’est-ce qu’un serveur avec Azure Arc ?

Les serveurs avec Azure Arc vous permettent de gérer vos machines Windows et Linux hébergées en dehors d'Azure, sur votre réseau d'entreprise ou un autre fournisseur de cloud, de la même façon que vous gérez des machines virtuelles Azure natives. Quand une machine hybride est connectée à Azure, elle devient une machine connectée et est traitée comme une ressource dans Azure. Chaque machine connectée possède un ID de ressource, est gérée dans le cadre d’un groupe de ressources au sein d’un abonnement et tire parti des constructions Azure standard, comme Azure Policy et l’application d’étiquettes. Les fournisseurs de services qui gèrent l'infrastructure locale d'un client peuvent gérer ses machines hybrides (comme ils le font déjà avec les ressources Azure natives) dans différents environnements clients à l'aide d'[Azure Lighthouse](../../lighthouse/how-to/manage-hybrid-infrastructure-arc.md) avec Azure Arc.

Pour bénéficier de cette expérience avec vos machines hybrides hébergées en dehors d’Azure, vous devez installer Azure Connected Machine sur chaque machine que vous envisagez de connecter à Azure. Cet agent ne fournit aucune autre fonctionnalité et ne remplace pas l’agent Azure [Log Analytics](../../azure-monitor/platform/log-analytics-agent.md). L’agent Log Analytics pour Windows et Linux est nécessaire quand vous souhaitez superviser de manière proactive le système d’exploitation et les charges de travail en cours d’exécution sur la machine, gérer le système d’exploitation à l’aide de runbooks Automation ou de solutions comme Update Management ou utiliser d’autres services Azure tels qu’[Azure Security Center](../../security-center/security-center-introduction.md).

## <a name="supported-scenarios"></a>Scénarios pris en charge

Lorsque vous connectez votre machine à des serveurs avec Azure Arc, vous pouvez effectuer les tâches de surveillance et de gestion de la configuration suivantes :

- Affecter des [configurations invité Azure Policy](../../governance/policy/concepts/guest-configuration.md) à l’aide de la même expérience que lors de l’attribution de stratégie pour des machines virtuelles Azure. De nos jours, la plupart des stratégies de configuration d’invité ne s’appliquent pas aux configurations : elles auditent seulement les paramètres à l’intérieur de la machine. Pour comprendre le coût de l’utilisation de stratégies Guest Configuration dans Azure Policy avec des serveurs Arc, consultez le [guide des tarifs](https://azure.microsoft.com/pricing/details/azure-policy/) d’Azure Policy.

- Signalez les changements de configuration relatifs aux logiciels installés, aux services Microsoft, au registre et aux fichiers Windows ainsi qu'aux démons Linux sur des serveurs surveillés à l'aide d'Azure Automation [Change Tracking and Inventory](../../automation/change-tracking/overview.md).

- Surveillez les performances du système d’exploitation invité de votre machine connectée, et découvrez les composants de l’application afin de surveiller leurs processus et dépendances avec d’autres ressources que l’application communique à l’aide d’[Azure Monitor pour machines virtuelles](../../azure-monitor/insights/vminsights-overview.md).

- Simplifiez le déploiement avec d'autres services Azure tels qu'Azure Automation [State Configuration](../../automation/automation-dsc-overview.md) et un espace de travail Azure Monitor Log Analytics à l'aide des [extensions de machine virtuelle Azure](manage-vm-extensions.md) prises en charge pour votre machine Windows ou Linux non Azure. Cela comprend l’exécution de la configuration après déploiement ou de l’installation de logiciels à l’aide de l’extension de script personnalisé.

- Utilisez la fonctionnalité [Update Management](../../automation/update-management/update-mgmt-overview.md) d'Azure Automation pour gérer les mises à jour du système d'exploitation de vos serveurs Windows et Linux.

- Incluez vos serveurs non Azure pour la détection des menaces, et surveillez de manière proactive les menaces de sécurité potentielles à l'aide d'[Azure Security Center](../../security-center/security-center-introduction.md).

Les données de journal collectées et stockées dans un espace de travail Log Analytics à partir de la machine hybride contiennent désormais des propriétés spécifiques de la machine, telles qu’un ID de ressource. Cela peut être utilisé pour prendre en charge l’accès au journal de [contexte de ressource](../../azure-monitor/platform/design-logs-deployment.md#access-mode).

[!INCLUDE [azure-lighthouse-supported-service](../../../includes/azure-lighthouse-supported-service.md)]

## <a name="supported-regions"></a>Régions prises en charge

Pour obtenir la liste définitive des régions prises en charge dotées de serveurs avec Azure Arc, consultez la page [Produits Azure par région](https://azure.microsoft.com/global-infrastructure/services/?products=azure-arc).

Dans la plupart des cas, l’emplacement que vous sélectionnez au moment de créer le script d’installation doit être la région Azure géographiquement la plus proche de l’emplacement de votre ordinateur. Les données au repos sont stockées dans la zone géographique Azure englobant la région que vous spécifiez, ce qui peut aussi affecter votre choix de région si vous avez des contraintes en matière de résidence des données. Si la région Azure à laquelle votre ordinateur est connecté subit une panne, l’ordinateur connecté n’est pas affecté, mais les opérations de gestion effectuées avec Azure risquent de ne pas aboutir. En cas de panne régionale, si vous avez plusieurs emplacements qui prennent en charge un service géographiquement redondant, l’idéal est de connecter les machines de chaque emplacement à une région Azure distincte.

### <a name="agent-status"></a>État de l’agent

L’agent Connected Machine envoie des messages de pulsation au service de façon régulière (toutes les 5 minutes). Si le service cesse de recevoir ces messages de pulsation d’une machine, cette machine est considérée comme étant hors connexion, et l’état dans le portail est automatiquement remplacé par **Déconnectée** au bout de 15 à 30 minutes. À la prochaine réception d’un message de pulsation de l’agent Connected Machine, son état devient automatiquement **Connecté** .

## <a name="next-steps"></a>Étapes suivantes

Avant d'évaluer ou d'activer des serveurs avec Azure Arc sur plusieurs machines hybrides, consultez [Vue d'ensemble d'Azure Connected Machine Agent](agent-overview.md) pour en savoir plus sur les exigences et les détails techniques relatifs à l'agent, ainsi que sur les méthodes de déploiement.