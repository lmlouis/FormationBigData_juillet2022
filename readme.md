# Formation Pratique Big data 

Formation vidéo suivit durant la période de Juillet 2022 animé par une chaine youtube 

# Outils et Versions ¶
* Apache Hadoop Version: 2.7.2
* Apache Spark Version: 2.2.1
* Containerisation : Docker Version 20.10.12
* IDE  : IntelliJ IDEA Version Community version 
* Langage  : Java Version ( open jdk 18 )
* Environnement : Linux (ubuntu 20.04 )

Hadoop 
------

un projet hadoop comprend deux grandes parties :
* `HDFS` (hadoop Distributed file system) : pour le stokage des données 
* `Map Reduce` & `YArn` :  pour le traitement de données 

### Principe 

* Diviser les données en blocks
* Sauvegarder les données dans des clusters ( avec replication de block)
* Traiter les données en paralelle directement dans leur lieu de stokage 

### Architecture HDFS 
architecture maitre / esclave
* Blocks enrégistrés dans des noeuds différends
* `Data node` (slave) : daemon sur chaque noeud du cluster 
* `Name node` (master) : daemon qui contient les meta-données et permet de retrouver les noeuds qui exécutent les blocks du même fichier


### Map Reduce 

* Patron d'architecture de dévéllopement permetant de `traiter les données` volumineuses de manière `paralèlle et distribuée`
* Utilise le `langage java` ( et récemement d'autres langages tels que python et ruby  )
* Divise le fichier et le parcours en parellèle 
#### Processus Map Reduce 
* `Mappers` : travailent en parallèle sur chacun des blocs du fichier à mapper on obtient en sorti un enrégistrement intermédiaire de données couple (clé/valeurs)
* `Mélange` (sélection de fiches réçu des mappers ) et `tri` (rangement selon un ordre au niveau de chaque reducer)  s'ensuit 
* `Reducers ` :  collectent les  données mélangées et les triées selon clé / valeur et effectue des traitement simples sur ces données  pour fournir des résultats finaux  
#### Composant Map Reduce 

`Map Reduce V1`
---

* `API` : pour l'écriture d'application map reduce 
* `Framework` :  service  permettant l'éxecution des jobs mapReduce, Shuffle/sort 
* `Resource Management` : infrastructure pour gérer des noeuds, allouer des resources et ordonnacer les jobs 

daemon
---
* JobTracker : Divise le travail sur les mapper et reducer, s'éxécutant sur différents noeuds 
* TaskTrackers : 
   * s'exécute sur chacun des noeuds pour exécuter la veritable tache map reduce 
   * choisit en générale de traiter (Map / Reduce) un bloc sur la même machine que lui 
   * si il est occuper alors tâche revient à un autre tracker qui utilise le même réseau (rare)

`Map Reduce V2`
---

* `Map Reduce V2` : sépare la gestion des resources de celle des tâches RM 
    * RM API
    * Framework 
* `Pas de notion de Slot` 
* `Yarn` :
    * Yarn API
    * Resource Management

daemon
---
* Resource Manager (RM): permet l'`ordonnancement` et l'`arbitrage` des resources entre plusieurs applications sur le `noeud master `
* Node Manager (NM) : communique avec le RM et `s'exécute` sur les noeuds esclaves 
* Container : est créer par le RM (à la demande) et se voit `allouer des resourcces` sur les noeuds esclaves 
* Application master (AM): il existe en un seul exemplaire par application, s'exécute sur un container démandes plusieurs containers pour exécuter les tâches de l'application 



