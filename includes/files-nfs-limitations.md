---
title: Fichier include
description: Fichier include
services: storage
author: roygara
ms.service: storage
ms.topic: include
ms.date: 09/15/2020
ms.author: rogarana
ms.custom: include file
ms.openlocfilehash: 866640d90c66dd82e8be61d221bc903907575454
ms.sourcegitcommit: 4bebbf664e69361f13cfe83020b2e87ed4dc8fa2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/01/2020
ms.locfileid: "91643406"
---
En préversion, NFS présente les limitations suivantes :

- NFS 4.1 ne prend actuellement en charge que les fonctionnalités obligatoires de la [spécification du protocole](https://tools.ietf.org/html/rfc5661). Les fonctionnalités facultatives, comme les délégations et les rappels de toutes sortes, les mises à niveau de verrous et les rétrogradations, ainsi que l’authentification et le chiffrement Kerberos ne sont pas prises en charge.
- Si la majorité de vos demandes sont centrées sur les métadonnées, la latence sera plus grande en comparaison avec les opérations de lecture/d’écriture/de mise à jour.
- Vous devez créer un nouveau compte de stockage pour pouvoir créer un partage NFS.
- Seules les API REST du plan de gestion sont prises en charge. Les API REST du plan de données ne sont pas disponibles, ce qui signifie que des outils comme l’Explorateur de stockage ne fonctionneront pas avec les partages NFS. Vous ne pourrez pas non plus parcourir les données de partage NFS dans le Portail Azure.
- Disponible uniquement pour le niveau Premium.
- Actuellement disponible uniquement avec le stockage localement redondant (LRS).

### <a name="azure-storage-features-not-yet-supported"></a>Fonctionnalités de stockage Azure pas encore prises en charge

En outre, les fonctionnalités Azure Files suivantes ne sont pas disponibles avec les partages NFS :

- Authentification basée sur l’identité
- Support Sauvegarde Azure
- Instantanés
- Suppression réversible
- Prise en charge complète du chiffrement en transit (pour plus d’informations, consultez [Sécurité NFS](../articles/storage/files/storage-files-compare-protocols.md#security))
- Azure File Sync (disponible uniquement pour les clients Windows, que NFS 4.1 ne prend pas en charge)