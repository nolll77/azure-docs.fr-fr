---
title: Paramètres DNS du Pare-feu Azure (préversion)
description: Vous pouvez configurer le pare-feu Azure avec les paramètres de serveur DNS et de proxy DNS.
services: firewall
author: vhorne
ms.service: firewall
ms.topic: how-to
ms.date: 06/30/2020
ms.author: victorh
ms.openlocfilehash: 09ffac4f19d50d9a386110e1b89f8f147652a2cd
ms.sourcegitcommit: 33368ca1684106cb0e215e3280b828b54f7e73e8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/16/2020
ms.locfileid: "92132004"
---
# <a name="azure-firewall-dns-settings-preview"></a>Paramètres DNS du pare-feu Azure (préversion)

> [!IMPORTANT]
> Les paramètres DNS du Pare-feu Azure sont actuellement en version préliminaire publique.
> Cette préversion est fournie sans contrat de niveau de service et n’est pas recommandée pour les charges de travail de production. Certaines fonctionnalités peuvent être limitées ou non prises en charge. Pour plus d’informations, consultez [Conditions d’Utilisation Supplémentaires relatives aux Évaluations Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

Vous pouvez configurer un serveur DNS personnalisé et activer le proxy DNS pour le pare-feu Azure. Vous pouvez configurer ces paramètres lorsque vous déployez le pare-feu ou plus tard à partir de la page **Paramètres DNS**.

## <a name="dns-servers"></a>Serveurs DNS

Un serveur DNS gère et résout les noms de domaine en adresses IP. Par défaut, le Pare-feu Azure utilise Azure DNS pour la résolution de noms. Le paramètre **Serveur DNS** vous permet de configurer vos propres serveurs DNS pour la résolution de noms du Pare-feu Azure. Vous pouvez configurer un ou plusieurs serveurs.

### <a name="configure-custom-dns-servers-preview"></a>Configurer des serveurs DNS personnalisés (préversion)

1. Sous **Paramètres** du pare-feu Azure, sélectionnez **Paramètres DNS**.
2. Sous **Serveurs DNS**, vous pouvez taper ou ajouter des serveurs DNS existants qui ont été précédemment spécifiés dans votre réseau virtuel.
3. Sélectionnez **Enregistrer**.
4. Le pare-feu dirige désormais le trafic DNS vers le ou les serveurs DNS spécifiés pour la résolution de noms.

:::image type="content" source="media/dns-settings/dns-servers.png" alt-text="Serveurs DNS":::

## <a name="dns-proxy-preview"></a>Proxy DNS (version préliminaire)

Vous pouvez configurer le Pare-feu Azure pour qu’il agisse comme proxy DNS. Un proxy DNS agit comme un intermédiaire pour les requêtes DNS des machines virtuelles clientes à un serveur DNS. Si vous configurez un serveur DNS personnalisé, vous devez activer le proxy DNS pour éviter les incompatibilités de résolution DNS et activer le filtrage de nom de domaine complet dans les règles de réseau.

Si vous n’activez pas le proxy DNS, les requêtes DNS du client peuvent se déplacer vers un serveur DNS à une heure différente ou retourner une réponse différente de celle du pare-feu. Le proxy DNS place le Pare-feu Azure sur le trajet des demandes du client pour éviter toute incohérence.

La configuration du proxy DNS nécessite trois étapes :
1. Activez le proxy DNS dans les paramètres DNS du Pare-feu Azure.
2. Éventuellement, configurez votre serveur DNS personnalisé ou utilisez la valeur par défaut fournie.
3. Enfin, vous devez configurer l’adresse IP privée du Pare-feu Azure en tant qu’adresse DNS personnalisée dans les paramètres du serveur DNS de votre réseau virtuel. Cela garantit que le trafic DNS est dirigé vers le Pare-feu Azure.

### <a name="configure-dns-proxy-preview"></a>Configurer un proxy DNS (version préliminaire)

Pour configurer le proxy DNS, vous devez configurer le paramètre des serveurs DNS de votre réseau virtuel pour utiliser l’adresse IP privée du pare-feu. Ensuite, activez le proxy DNS dans les **paramètres DNS** de la stratégie de Pare-feu Azure.

#### <a name="configure-virtual-network-dns-servers"></a>Configurer les serveurs DNS du réseau virtuel

1. Sélectionnez le réseau virtuel dans lequel le trafic DNS sera routé via le Pare-feu Azure.
2. Sous**Paramètres**, sélectionnez **Serveurs DNS**.
3. Sélectionnez **Personnalisé** sous **Serveurs DNS**.
4. Saisissez l’adresse IP privée du pare-feu.
5. Sélectionnez **Enregistrer**.
6. Redémarrez les machines virtuelles connectées au réseau virtuel, afin que les nouveaux paramètres de serveur DNS leur soient assignés. Les machines virtuelles continuent d’utiliser leurs paramètres DNS actifs jusqu’à ce qu’elles soient redémarrés.

#### <a name="enable-dns-proxy-preview"></a>Activer un proxy DNS (préversion)

1. Sélectionnez votre pare-feu Azure.
2. Sous **Paramètres**, sélectionnez **Paramètres DNS**.
3. Le **proxy DNS** est désactivé par défaut. Lorsqu’il est activé, le pare-feu écoute le port 53 et transfère les requêtes DNS aux serveurs DNS configurés.
4. Vérifiez la configuration des **serveurs DNS** pour vous assurer que les paramètres sont adaptés à votre environnement.
5. Sélectionnez **Enregistrer**.

:::image type="content" source="media/dns-settings/dns-proxy.png" alt-text="Serveurs DNS":::

## <a name="next-steps"></a>Étapes suivantes

[Filtrage de nom de domaine complet dans les règles de réseau](fqdn-filtering-network-rules.md)
