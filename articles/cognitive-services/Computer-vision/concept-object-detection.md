---
title: Détection d’objets - Vision par ordinateur
titleSuffix: Azure Cognitive Services
description: Découvrez les concepts liés à la fonctionnalité Détection d’objets de l’API Vision par ordinateur - utilisation et limites.
services: cognitive-services
author: PatrickFarley
manager: nitinme
ms.service: cognitive-services
ms.subservice: computer-vision
ms.topic: conceptual
ms.date: 04/17/2019
ms.author: pafarley
ms.custom: seodec18
ms.openlocfilehash: 3957e15a09bd7e7ecd814d169451af3241108b64
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "80131675"
---
# <a name="detect-common-objects-in-images"></a>Détecter des objets courants dans des images

La détection d’objets est similaire au [balisage](concept-tagging-images.md), mais l’API retourne les coordonnées de cadre englobant (en pixels) pour chaque objet trouvé. Par exemple, si une image contient un chien, un chat et une personne, l’opération de détection liste ces objets ainsi que leurs coordonnées dans l’image. Vous pouvez utiliser cette fonctionnalité pour traiter les relations entre les objets dans une image. Elle vous permet également de déterminer s’il existe plusieurs instances de la même balise dans une image.

L’API Détection applique des balises en fonction des objets ou éléments vivants identifiés dans l’image. Il n’existe actuellement aucune relation formelle entre la taxonomie des balises et la taxonomie de détection d’objets. À un niveau conceptuel, l’API Détection recherche uniquement les objets et les éléments vivants, tandis que l’API Balise peut également inclure des termes contextuels tels que « intérieur », qui ne peuvent pas être localisés avec des cadres englobants.

## <a name="object-detection-example"></a>Exemple de détection d’objet

La réponse JSON suivante illustre ce que retourne Vision par ordinateur lors de la détection d’objets dans l’exemple d’image.

![Une femme utilisant un appareil Microsoft Surface dans une cuisine](./Images/windows-kitchen.jpg)

```json
{
   "objects":[
      {
         "rectangle":{
            "x":730,
            "y":66,
            "w":135,
            "h":85
         },
         "object":"kitchen appliance",
         "confidence":0.501
      },
      {
         "rectangle":{
            "x":523,
            "y":377,
            "w":185,
            "h":46
         },
         "object":"computer keyboard",
         "confidence":0.51
      },
      {
         "rectangle":{
            "x":471,
            "y":218,
            "w":289,
            "h":226
         },
         "object":"Laptop",
         "confidence":0.85,
         "parent":{
            "object":"computer",
            "confidence":0.851
         }
      },
      {
         "rectangle":{
            "x":654,
            "y":0,
            "w":584,
            "h":473
         },
         "object":"person",
         "confidence":0.855
      }
   ],
   "requestId":"a7fde8fd-cc18-4f5f-99d3-897dcd07b308",
   "metadata":{
      "width":1260,
      "height":473,
      "format":"Jpeg"
   }
}
```

## <a name="limitations"></a>Limites

Les limites de la détection d'objet doivent impérativement être prises en compte afin d'éviter ou d'atténuer les effets des faux négatifs (objets manqués) et des détails limités.

* Les tout petits objets (moins de 5 % de l'image) ne sont généralement pas détectés.
* Les objets proches les uns des autres (piles d'assiettes, par exemple) ne sont généralement pas détectés.
* Les objets ne sont pas différenciés par marque ou nom de produit (différents types de sodas sur une étagère de magasin, par exemple). Toutefois, vous pouvez obtenir des informations sur les marques figurant sur une image à l'aide de la fonctionnalité [Détection de marque](concept-brand-detection.md).

## <a name="use-the-api"></a>Utilisation de l’API

La fonctionnalité de détection d'objet fait partie de l'API [Analyser l'image](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa). Vous pouvez appeler cette API via un SDK natif ou via des appels REST. Incluez `Objects` dans le paramètre de requête **visualFeatures**. Ensuite, lorsque vous obtenez la réponse JSON complète, analysez simplement la chaîne de contenu de la section `"objects"`.

* [Démarrage rapide : SDK .NET Vision par ordinateur](./quickstarts-sdk/client-library.md?pivots=programming-language-csharp)
* [Démarrage rapide : Analyser une image (API REST)](./quickstarts/csharp-analyze.md)