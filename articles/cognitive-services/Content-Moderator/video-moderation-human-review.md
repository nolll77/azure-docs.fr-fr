---
title: Modération de vidéo avec l’outil de révision - Content Moderator
titleSuffix: Azure Cognitive Services
description: Utilisez la modération de vidéo assistée par ordinateur et l'outil de révision pour modérer les contenus inappropriés
services: cognitive-services
author: PatrickFarley
manager: nitinme
ms.service: cognitive-services
ms.subservice: content-moderator
ms.topic: conceptual
ms.date: 07/20/2020
ms.author: pafarley
ms.openlocfilehash: 392cc06c6e0bce7ec2304da61033fc508d940bbb
ms.sourcegitcommit: 4b76c284eb3d2b81b103430371a10abb912a83f4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2020
ms.locfileid: "93143773"
---
# <a name="video-moderation-with-the-review-tool"></a>Modération de vidéo avec l’outil de révision

Utilisez la [modération de vidéo](video-moderation-api.md) assistée par ordinateur et l'[outil de révision](Review-Tool-User-Guide/human-in-the-loop.md) de Content Moderator pour modérer les vidéos et les transcriptions explicites (contenu destiné aux adultes) ou provocantes (contenu suggestif), et permettre à votre entreprise de bénéficier des meilleurs résultats.

## <a name="view-videos-under-review"></a>Afficher les vidéos en cours de révision

Dans le tableau de bord, sélectionnez l’une des files d’attente de révision dans le type de contenu vidéo. Cette opération démarre une révision et ouvre la page de modération de contenu vidéo.

> [!div class="mx-imgBorder"]
> ![Vue détaillée de la modération de vidéo dans l’outil de révision](./Review-Tool-User-Guide/images/video-moderation-detailed.png)

### <a name="review-count"></a>Nombre d’examens

Utilisez le curseur en haut à droite pour définir le nombre de révisions que vous souhaitez afficher dans la page.

### <a name="view-type"></a>Type de vue

Vous pouvez afficher les différentes entrées de contenu sous forme de vignettes ou dans une vue détaillée. La vue **Detail** vous permet de voir les images clés et d’autres informations sur la vidéo sélectionnée. 

> [!NOTE]
> Au lieu d’isoler des images à intervalles réguliers, le service de modération des vidéos identifie et isole des images qui sont potentiellement complètes et de bonne qualité. Cette fonctionnalité génère efficacement des images afin d’analyser le contenu explicite et suggestif au niveau de l’image.

La vue **Tiled** affiche chaque vidéo sous la forme d’une vignette unique. Sélectionnez le bouton de développement au-dessus d’une image vidéo pour agrandir cette vidéo et masquer les autres.

### <a name="content-obscuring-effects"></a>Effets de masquage du contenu

Utilisez les boutons bascule **Blur all** et **Black and white** pour définir ces effets de masquage du contenu. Ils sont activés par défaut. Dans la vue **Tiled** , vous pouvez basculer les effets individuellement pour chaque vidéo.

## <a name="check-video-details"></a>Vérifier les détails de la vidéo

Dans la vue **Detail** , le volet droit contient plusieurs onglets qui fournissent des détails sur la vidéo.

* Sélectionnez l’onglet **Notes** pour ajouter des notes personnalisées aux vidéos.
* Sélectionnez l’onglet **Transcript** pour voir la transcription de la vidéo ; le service extrait automatiquement une transcription de toute parole dans la vidéo. Lorsque vous sélectionnez une section de texte, le lecteur vidéo passe directement à cette partie de la vidéo.
* Sélectionnez l’onglet **Meta-data** pour afficher les métadonnées du fichier vidéo.
* Sélectionnez l’onglet **History** pour afficher l’historique de la révision, par exemple sa date de création et la manière dont elle a été modifiée.

> [!div class="mx-imgBorder"]
> ![Bouton Bulk Tags de modération de vidéo](./Review-Tool-User-Guide/images/video-moderation-video-details.png)

## <a name="apply-moderation-tags"></a>Appliquer des étiquettes de modération

La tâche principale d’une révision de vidéo consiste à appliquer ou à supprimer des étiquettes de modération sur des vidéos ou des parties de vidéos.

### <a name="bulk-tagging"></a>Étiquetage en bloc

La barre d’outils **Bulk Tags** vous permet d’ajouter des étiquettes à plusieurs vidéos sélectionnées en même temps. Sélectionnez une ou plusieurs vidéos, sélectionnez les étiquettes que vous souhaitez appliquer, puis cliquez sur **submit**. 

> [!div class="mx-imgBorder"]
> ![Bouton Bulk Tags de modération de vidéo](./Review-Tool-User-Guide/images/video-moderation-bulk-tags.png)


### <a name="key-frame-tagging"></a>Étiquetage d’image clé

Vous pouvez également ajouter des étiquettes de modération à des images clés spécifiques. Sélectionnez les images dans le volet de vignettes d’images clés, puis sélectionnez **Keyframe tags +** pour appliquer les étiquettes souhaitées.

> [!NOTE]
> Si le service n’a pas pu extraire les images clés, le volet de vignettes d’images affiche **No frames available** , et l’option permettant de sélectionner les images clés est grisée. Dans ce cas, vous ne pouvez appliquer des étiquettes qu’à la vidéo dans son ensemble (à l’aide du bouton **Video tags +** ).

> [!div class="mx-imgBorder"]
> ![Vue détaillée de la modération de vidéo dans l’outil de révision](./Review-Tool-User-Guide/images/video-moderation-tagging-options.png)

## <a name="put-a-review-on-hold"></a>Mettre une révision en attente

Le bouton **Hold** en bas du volet de vidéo vous permet de mettre en attente une révision afin de pouvoir la récupérer et la terminer ultérieurement, par exemple si elle nécessite une consultation par un autre membre ou responsable de l’équipe qui n’est pas disponible actuellement. 

Vous pouvez afficher les vidéos en attente en cliquant sur le bouton **Hold** en haut de l’écran. Le volet Hold est affiché à droite. À partir de là, vous pouvez sélectionner plusieurs révisions en attente et les replacer dans la file d’attente ou définir leur heure d’expiration. Passé le délai préconfiguré, les révisions en attente sont replacées dans la file d’attente. Sélectionnez **Save** pour commencer le compte à rebours à partir du délai d’expiration actuellement sélectionné.

> [!div class="mx-imgBorder"]
> ![Vue détaillée de la modération de vidéo dans l’outil de révision](./Review-Tool-User-Guide/images/video-moderation-hold.png)

## <a name="submit-a-review"></a>Soumettre une révision

Une fois que vous avez appliqué vos étiquettes, sélectionnez le bouton **Submit** en bas du volet de vidéo. Si vous avez étiqueté plusieurs vidéos, vous pouvez les soumettre en tant que révision unique ou en tant que révisions distinctes.

## <a name="limbo-state"></a>État Limbo

Une fois que vous avez soumis une révision, la vidéo passe à l’état **Limbo** , que vous pouvez afficher en sélectionnant le bouton **Limbo** en haut de l’écran. Les vidéos restent à l’état Limbo pour une durée préconfigurée (que vous pouvez modifier dans le menu en bas) ou jusqu’à ce qu’elles soient révisées à nouveau ou envoyées manuellement.

Une fois que les vidéos expirent de l’état Limbo, leurs évaluations sont marquées comme achevées.

## <a name="next-steps"></a>Étapes suivantes

- Consultez le [démarrage rapide pour la modération des vidéos](video-moderation-api.md).
- Découvrez comment générer des [revues de vidéos](video-reviews-quickstart-dotnet.md) pour vos réviseurs à partir de résultats modérés.
- Ajoutez des [revues de la transcription de la vidéo](video-transcript-reviews-quickstart-dotnet.md) à vos révisions de vidéos.
- Consultez le tutoriel détaillé sur le développement d’une [solution complète de modération de vidéos](video-transcript-moderation-review-tutorial-dotnet.md).