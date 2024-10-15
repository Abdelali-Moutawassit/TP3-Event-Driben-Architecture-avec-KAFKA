# Activité Pratique N°3 - Event Driven Architecture avec Kafka

**Nom complet :** ABDELALI MOUTAWASSIT  
**Date :** 6 Octobre

## Table des matières
- [Introduction](#introduction)
- [Installation de Kafka](#installation-de-kafka)
- [Utilisation de Docker](#utilisation-de-docker)
- [Création des services](#création-des-services)
- [Conclusion](#conclusion)

## Introduction
Cette activité pratique a pour but d'explorer l'architecture Event Driven à l'aide de Kafka. Nous allons installer Kafka, l'utiliser avec Docker, et créer plusieurs services pour traiter des données en temps réel.

## Installation de Kafka

| Étape                              | Description                                                                 |
|------------------------------------|-----------------------------------------------------------------------------|
| 1. Télécharger Kafka               | Téléchargez la dernière version de Kafka depuis [Kafka Downloads](https://kafka.apache.org/downloads). |
| 2. Démarrer Zookeeper              | Exécutez la commande suivante dans le terminal :                           |
|                                    | `bin/zookeeper-server-start.sh config/zookeeper.properties`                |
| 3. Démarrer Kafka-server           | Exécutez la commande suivante dans le terminal :                           |
|                                    | `bin/kafka-server-start.sh config/server.properties`                       |
| 4. Tester avec Kafka-console-producer | Utilisez la commande suivante :                                           |
|                                    | `bin/kafka-console-producer.sh --topic test --bootstrap-server localhost:9092` |
| 5. Tester avec kafka-console-consumer | Utilisez la commande suivante :                                           |
|                                    | `bin/kafka-console-consumer.sh --topic test --from-beginning --bootstrap-server localhost:9092` |

## Utilisation de Docker

Pour exécuter Kafka avec Docker, suivez les étapes ci-dessous.

| Étape                              | Description                                                                 |
|------------------------------------|-----------------------------------------------------------------------------|
| 1. Créer le fichier `docker-compose.yml` | Créez un fichier `docker-compose.yml` avec le contenu suivant :            |
|                                    | ```yaml                                                                    |
|                                    | version: '2'                                                               |
|                                    | services:                                                                 |
|                                    |   zookeeper:                                                              |
|                                    |     image: wurstmeister/zookeeper:latest                                   |
|                                    |     ports:                                                                |
|                                    |       - "2181:2181"                                                        |
|                                    |   kafka:                                                                  |
|                                    |     image: wurstmeister/kafka:latest                                       |
|                                    |     ports:                                                                |
|                                    |       - "9092:9092"                                                        |
|                                    |     environment:                                                           |
|                                    |       KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181                             |
|                                    |       KAFKA_ADVERTISED_LISTENERS: INSIDE://kafka:9092,OUTSIDE://localhost:9092 |
|                                    |       KAFKA_LISTENER_SECURITY_PROTOCOL_MAP: INSIDE:PLAINTEXT,OUTSIDE:PLAINTEXT |
|                                    |       KAFKA_LISTENERS: INSIDE://0.0.0.0:9092,OUTSIDE://0.0.0.0:9092      |
|                                    | ```                                                                      |
| 2. Démarrer les conteneurs Docker  | Exécutez la commande suivante :                                           |
|                                    | `docker-compose up`                                                       |
| 3. Tester avec Kafka-console-producer | Utilisez la commande suivante :                                           |
|                                    | `docker exec -it <kafka-container-id> kafka-console-producer.sh --topic test --bootstrap-server localhost:9092` |
| 4. Tester avec kafka-console-consumer | Utilisez la commande suivante :                                           |
|                                    | `docker exec -it <kafka-container-id> kafka-console-consumer.sh --topic test --from-beginning --bootstrap-server localhost:9092` |

## Création des services

### 1. Service Producer KAFKA via un Rest Controller
- Créez un contrôleur REST qui envoie des messages à un topic Kafka.

### 2. Service Consumer KAFKA
- Créez un service qui consomme des messages d'un topic Kafka.

### 3. Service Supplier KAFKA
- Créez un service qui fournit des données à un topic Kafka.

### 4. Service de Data Analytics Real Time Stream Processing avec Kafka Streams
- Développez un service qui traite les flux de données en temps réel.

### 5. Application Web pour afficher les résultats
- Créez une application web qui permet d'afficher les résultats du traitement des données en temps réel.

## Conclusion
Cette activité pratique a permis d'apprendre à configurer et utiliser Kafka pour une architecture Event Driven. Nous avons également exploré l'utilisation de Docker pour simplifier le déploiement des services.

---

**Remarque :** Pour toute question ou assistance, veuillez contacter votre instructeur.
