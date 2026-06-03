# PREDICTELEC - Orchestration des pipelines de données et de prévisions photovoltaïques

## Présentation du projet

PREDICTELEC est une plateforme de prévision de production d'électricité photovoltaïque.

L'objectif du projet est de collecter, centraliser et exploiter plusieurs sources de données afin de prédire la production future des centrales photovoltaïques :

* données météorologiques observées ;
* prévisions météorologiques ;
* données de production électrique ;
* caractéristiques techniques des centrales ;
* informations géographiques des stations météorologiques.

Le projet a été réalisé dans le cadre d'un mémoire de fin d'études en Intelligence Artificielle et Data Science.

---

## Problématique

La qualité des prévisions photovoltaïques dépend directement de la disponibilité et de la fraîcheur des données.

Plusieurs milliers de mesures doivent être récupérées quotidiennement depuis différentes sources externes.

Avant ce projet, ces traitements étaient déclenchés par des tâches système planifiées (crontab), ce qui rendait difficile :

* le suivi des exécutions ;
* la gestion des erreurs ;
* la reprise automatique des traitements ;
* l'analyse des performances.

L'objectif a donc été d'industrialiser l'ensemble du pipeline de données.

---

## Solution mise en œuvre

L'orchestration des traitements a été réalisée avec Apache Airflow.

Airflow permet :

* de planifier les traitements ;
* de suivre leur exécution ;
* de relancer automatiquement les tâches en échec ;
* de paralléliser les traitements ;
* d'obtenir une traçabilité complète des opérations.

L'ensemble est déployé sous Docker afin de garantir la reproductibilité de l'environnement.

---

## Architecture générale

Le système repose sur plusieurs composants :

### Apache Airflow

Pilote l'ensemble des traitements de données.

### PostgreSQL

Stocke :

* les données métier du projet ;
* les métadonnées d'exécution Airflow.

### Redis

Permet la gestion des files d'attente des tâches parallèles.

### Celery Executor

Répartit les traitements entre plusieurs workers afin d'accélérer les exécutions.

### Grafana et Prometheus

Assurent la supervision de la plateforme.

---

## Pipelines automatisés

### Mise à jour des structures

Récupération des informations relatives :

* aux centrales photovoltaïques ;
* aux stations météorologiques associées.

### Mise à jour des données météo observées

Collecte des mesures réelles utilisées pour l'entraînement des modèles.

### Mise à jour des données de production

Import des historiques de production électrique.

### Récupération des prévisions météo

Collecte massive des prévisions de :

* température ;
* rayonnement solaire ;
* nébulosité ;
* vent.

Ces données sont utilisées pour alimenter les futurs modèles prédictifs.

---

## Optimisations réalisées

L'un des principaux défis du projet concernait le temps de récupération des prévisions météo.

Pour réduire les temps de traitement :

* les requêtes ont été réparties entre plusieurs comptes d'accès API ;
* les traitements ont été parallélisés grâce à Airflow et Celery ;
* les limites de consommation imposées par l'API ont été respectées.

Cette approche a permis de réduire significativement les temps d'exécution tout en garantissant la stabilité du système.

---

## Compétences mises en œuvre

* Data Engineering
* Apache Airflow
* Docker
* PostgreSQL
* Python
* Automatisation de pipelines
* Orchestration de traitements
* Monitoring et observabilité
* Gestion de la parallélisation
* Industrialisation d'un projet de Data Science


