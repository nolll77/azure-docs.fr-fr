---
title: 'Tutoriel : Prise en main d’Azure Synapse Analytics - Surveiller votre espace de travail Synapse'
description: Dans ce tutoriel, vous allez apprendre à surveiller les activités dans votre espace de travail Synapse.
services: synapse-analytics
author: saveenr
ms.author: saveenr
manager: julieMSFT
ms.reviewer: jrasnick
ms.service: synapse-analytics
ms.subservice: monitoring
ms.topic: tutorial
ms.date: 10/15/2020
ms.openlocfilehash: d497ff1a829902c0623740f01a457e6496db2401
ms.sourcegitcommit: 8c7f47cc301ca07e7901d95b5fb81f08e6577550
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/27/2020
ms.locfileid: "92744958"
---
# <a name="monitor-your-synapse-workspace"></a>Surveiller votre espace de travail Synapse

Dans ce tutoriel, vous allez apprendre à surveiller les activités dans votre espace de travail Synapse. Vous pouvez surveiller les activités actuelles et historiques en relation avec SQL, Apache Spark et Pipelines. 

## <a name="introduction-to-the-monitor-hub"></a>Présentation du hub Monitor

Ouvrez Synapse Studio et accédez au hub **Monitor**. À cet emplacement, vous pouvez voir un historique de toutes les activités qui se produisent dans l’espace de travail et celles qui sont actuellement actives. 

* Sous **Intégration** , vous pouvez superviser les pipelines, les déclencheurs et les runtimes d’intégration.
* Sous **Activités** , vous pouvez surveiller les activités Spark et SQL. 

## <a name="integration"></a>Intégration

1. Accédez à **Intégration > Pipeline**. Dans cette vue, vous pouvez voir chaque exécution d’un pipeline dans votre espace de travail. 
1. Recherchez le pipeline que vous avez exécuté à l’étape précédente et cliquez sur son **nom**.
1. Vous pouvez maintenant voir la façon dont les activités individuelles dans ce pipeline s’exécutent.
1. Cliquez sur **Barre de navigation** vers le haut de Synapse Studio, cliquez sur **Toutes les exécutions de pipelines** pour revenir à la vue précédente.

## <a name="apache-spark-activities"></a>Activités Apache Spark

1. Accédez à **Intégration > Activités > Applications Apache Spark** . Vous pouvez maintenant voir toutes les applications Spark en cours d’exécution ou exécutées dans votre espace de travail.
1. Recherchez une application qui n’est plus en cours d’exécution et cliquez sur son **nom**. Vous pouvez maintenant voir les détails de l’application Spark.
1. Si vous êtes familiarisé avec Apache Spark, vous pouvez trouver l’interface utilisateur du serveur d’historique Apache Spark standard en cliquant sur **Serveur d’historique Spark**.

## <a name="sql-activities"></a>Activités SQL

1. Accédez à **Intégration > Activités > Requêtes SQL**.
1. Dans cette vue, vous pouvez voir les requêtes SQL.
1. Sélectionnez un **pool** à surveiller. Vous pouvez maintenant voir toutes les requêtes SQL en cours d’exécution ou exécutées dans votre espace de travail dans ce pool.
1. Recherchez une requête SQL spécifique et pointez la souris sur cet élément. Une icône de script SQL s’affiche.
1. Cliquez sur l’icône de script SQL pour afficher le texte complet de la requête SQL.

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Explorer le Centre de connaissances](get-started-knowledge-center.md)
