---
title: 'Tutoriel : Démarrer l’analyse avec Spark'
description: Dans ce tutoriel, vous allez voir comment analyser des données avec Apache Spark.
services: synapse-analytics
author: saveenr
ms.author: saveenr
manager: julieMSFT
ms.reviewer: jrasnick
ms.service: synapse-analytics
ms.subservice: spark
ms.topic: tutorial
ms.date: 07/20/2020
ms.openlocfilehash: ec6af7c23f781d25114794066a228adbfe7528d0
ms.sourcegitcommit: 30505c01d43ef71dac08138a960903c2b53f2499
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/15/2020
ms.locfileid: "92093614"
---
# <a name="analyze-with-apache-spark"></a>Analyser avec Apache Spark

## <a name="analyze-nyc-taxi-data-in-blob-storage--using-spark"></a>Analyser les données NYC Taxi situées dans le Stockage Blob à l’aide de Spark

Dans ce tutoriel, vous allez découvrir les étapes de base permettant de charger et d’analyser des données avec Apache Spark pour Azure Synapse.

1. Dans le hub **Données**, cliquez sur **Ajouter une nouvelle ressource**(bouton plus situé au-dessus de **Lié**) >> **Parcourir les exemples**. Recherchez **NYC Taxi & Limousine Commission - yellow taxi trip records**, puis cliquez dessus. Au bas de la page, appuyez sur **Continuer**, puis sur **Ajouter un jeu de données**. Maintenant, dans le hub **Données** situé en dessous de **Lié**, cliquez avec le bouton droit sur **Stockage Blob Azure >> Exemples de jeux de données >> nyc_tlc_yellow**, puis sélectionnez **Nouveau notebook**.
1. Un notebook sera créé avec le code suivant :
    ```
    from azureml.opendatasets import NycTlcYellow

    data = NycTlcYellow()
    data_df = data.to_spark_dataframe()
    display(data_df.limit(10))
    ```
1. Dans le notebook, choisissez un pool Spark dans le menu **Attacher à**.
1. Cliquez sur **Exécuter** dans la cellule.

## <a name="load-the-nyc-taxi-data-into-the-spark-nyctaxi-database"></a>Charger les données NYC Taxi dans la base de données Spark appelée nyctaxi

Des données sont disponibles dans une table dans **SQLDB1**. Chargez-les dans une base de données Spark nommée **nyctaxi**.

1. Dans Synapse Studio, accédez au hub **Développer**.
1. Sélectionnez **+**  > **Notebook**.
1. En haut du notebook, définissez la valeur **Joindre à** sur **Spark1**.
1. Sélectionnez **Ajouter du code** pour ajouter une cellule de code du notebook, puis collez le texte suivant :

    ```scala
    %%spark
    spark.sql("CREATE DATABASE IF NOT EXISTS nyctaxi")
    val df = spark.read.sqlanalytics("SQLDB1.dbo.Trip") 
    df.write.mode("overwrite").saveAsTable("nyctaxi.trip")
    ```

1. Accédez au hub **Données**, cliquez avec le bouton droit sur **Bases de données**, puis sélectionnez **Actualiser**. Vous devez maintenant voir ces deux bases de données :

    - **SQLDB1** (pool SQL)
    - **nyctaxi** (Spark)

## <a name="analyze-the-nyc-taxi-data-using-spark-and-notebooks"></a>Analyser les données des taxis de New York à l’aide de Spark et des notebooks

1. Retournez dans votre notebook.
1. Créez une nouvelle cellule de code et entrez le texte suivant. Exécutez ensuite la cellule pour afficher les données NYC Taxi que nous avons chargées dans la base de données Spark **nyctaxi**.

   ```py
   %%pyspark
   df = spark.sql("SELECT * FROM nyctaxi.trip") 
   display(df)
   ```

1. Exécutez le code suivant pour effectuer la même analyse que celle faite précédemment avec le pool SQL **SQLDB1**. Ce code enregistre les résultats de l’analyse dans une table nommée **nyctaxi.passengercountstats** et crée une visualisation des résultats.

   ```py
   %%pyspark
   df = spark.sql("""
      SELECT PassengerCount,
          SUM(TripDistanceMiles) as SumTripDistance,
          AVG(TripDistanceMiles) as AvgTripDistance
      FROM nyctaxi.trip
      WHERE TripDistanceMiles > 0 AND PassengerCount > 0
      GROUP BY PassengerCount
      ORDER BY PassengerCount
   """) 
   display(df)
   df.write.saveAsTable("nyctaxi.passengercountstats")
   ```

1. Dans les résultats de la cellule, sélectionnez **Graphique** pour afficher les données visualisées.

## <a name="customize-data-visualization-with-spark-and-notebooks"></a>Personnaliser la visualisation des données avec Spark et des notebooks

Vous pouvez contrôler le rendu des graphiques à l’aide de notebooks. Le code suivant présente un exemple simple. Il utilise les bibliothèques populaires **matplotlib** et **seaborn**. Le code effectue le rendu dans le même type de graphique en courbes que les requêtes SQL que nous avons exécutées précédemment.

```py
%%pyspark
import matplotlib.pyplot
import seaborn

seaborn.set(style = "whitegrid")
df = spark.sql("SELECT * FROM nyctaxi.passengercountstats")
df = df.toPandas()
seaborn.lineplot(x="PassengerCount", y="SumTripDistance" , data = df)
seaborn.lineplot(x="PassengerCount", y="AvgTripDistance" , data = df)
matplotlib.pyplot.show()
```



## <a name="load-data-from-a-spark-table-into-a-sql-pool-table"></a>Charger des données à partir d’une table Spark dans une table de pools SQL

Nous avions copié les données de la table **SQLDB1.dbo.Trip** du pool SQL dans la table Spark **nyctaxi.trip**. Ensuite, dans Spark, nous avions agrégé les données dans la table Spark **nyctaxi.passengercountstats**. Nous allons maintenant copier les données de **nyctaxi.passengercountstats** dans une table du pool SQL appelée **SQLDB1.dbo.PassengerCountStats**.

Exécutez la cellule suivante dans votre notebook. La table Spark agrégée est de nouveau copiée dans la table du pool SQL.

```scala
%%spark
val df = spark.sql("SELECT * FROM nyctaxi.passengercountstats")
df.write.sqlanalytics("SQLDB1.dbo.PassengerCountStats", Constants.INTERNAL )
```

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Analyser des données avec SQL à la demande](get-started-analyze-sql-on-demand.md)


