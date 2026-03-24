# RFM (Recency, Frequency, Monetary) Analyse avec SQL et PowerBI
## 📊 Contexte du projet
### 🏢 Présentation de l’entreprise

Ce projet s’appuie sur un jeu de données fictif provenant de PrintifyCo, une entreprise e-commerce spécialisée dans les produits d’impression personnalisée.

PrintifyCo propose une large gamme de produits, notamment :

- Cartes de visite (Business Cards)

- Flyers promotionnels

- Posters

- Toiles imprimées (Canvas Prints)

- Albums photo (Photo Books)

- Cartes de vœux (Greeting Cards)

L’entreprise vend ses produits à des particuliers ainsi qu’à des petites entreprises souhaitant du matériel marketing ou des souvenirs personnalisés.

## 🎯 Problématique métier

L’équipe marketing de PrintifyCo souhaite mieux comprendre le comportement de ses clients afin de :

- Identifier les clients les plus fidèles

- Détecter les clients à risque de churn

- Cibler les campagnes marketing de manière plus efficace

- Augmenter la Customer Lifetime Value (CLV)

Pour répondre à ces besoins, l’équipe décide de mettre en place une analyse RFM (Recency, Frequency, Monetary).

## 📦 Description des données

Les données utilisées représentent les transactions clients sur une période donnée.

Chaque ligne correspond à une commande.

| Colonne     | Description                       |
| ----------- | --------------------------------- |
| OrderID     | Identifiant unique de la commande |
| CustomerID  | Identifiant unique du client      |
| OrderDate   | Date de la commande               |
| ProductType | Type de produit acheté            |
| OrderValue  | Montant de la commande (€)        |

Exemple: 
| OrderID    | CustomerID | OrderDate | ProductType | OrderValue |
| ----------- | -----------|-----------|----------- | ----------|
| ORDER00102 | CUST0038 | 2025-01-01 | Flyer          | 11.60 |
| ORDER00139 | CUST0025 | 2025-01-01 | Canvas Print   | 41.44 |
| ORDER00398 | CUST0161 | 2025-01-01 | Greeting Card  | 4.56  |

## 🧠 Objectif analytique

L’objectif est de segmenter les clients selon 3 dimensions :

- Recency (R) : nombre de jours depuis la dernière commande

- Frequency (F) : nombre total de commandes

- Monetary (M) : montant total dépensé

Ces métriques permettront de classer les clients en segments, par exemple :

- 🟢 Top Customers (Champions et loyal VIP)

- ⚠️ Clients à risque

- ❌ Clients perdus


## 🛠️ Stack technique

SQL (BigQuery) : transformation et calcul des métriques RFM

Power BI : visualisation et dashboard interactif

GitHub : documentation et versioning

## 📈 Cas d’usage

Grâce à cette analyse, PrintifyCo pourra :

- Lancer des campagnes ciblées (emailing, promos)

- Récompenser les meilleurs clients

- Réactiver les clients inactifs

- Optimiser ses revenus marketing


# ☁️ Ingestion des données dans le cloud (Google BigQuery)

Dans un premier temps, les fichiers CSV sont ingérés dans le data warehouse Google BigQuery.

Cette étape permet de centraliser les données transactionnelles dans un environnement scalable et performant, facilitant ainsi leur exploitation analytique.

## 🎯 Objectifs de l’ingestion

L’ingestion des données dans BigQuery répond à plusieurs enjeux :

- Centralisation des données
  - Regrouper l’ensemble des fichiers CSV dans un seul environnement de stockage structuré.

- Industrialisation de la logique métier
  - Implémenter les transformations directement en SQL pour garantir cohérence et traçabilité.

- Création de vues réutilisables
  - Mettre en place des vues SQL permettant de standardiser les calculs et de simplifier les analyses futures.

- Scalabilité
  - Permettre l’ajout continu de nouveaux fichiers CSV (historisation des données) sans refonte de l’architecture.

## 📦 Résultat attendu

À l’issue de cette étape, toutes les données sont :

- accessibles via SQL

- structurées et prêtes pour l’analyse

- facilement connectables à des outils de visualisation comme Power BI

## BigQuery

Création de nouveau projet intitulé `rfm-analysis-1337`
<img width="542" height="452" alt="image" src="https://github.com/user-attachments/assets/96074934-0b7b-42f5-9a52-2adb649e9089" />

Comme observé, ce dossier est vide, il faudra créer notre dataset comme ceci :
<img width="513" height="357" alt="image" src="https://github.com/user-attachments/assets/0f81cd42-f9a0-4cdc-8b4c-3ddc38ffc715" />
<img width="563" height="596" alt="image" src="https://github.com/user-attachments/assets/d2a83311-2285-44c8-943f-951668f8a76d" />

### Création des Tables
En cliquant sur la Database nouvellement créé, il nous faut créer nos table
<img width="1270" height="1264" alt="image" src="https://github.com/user-attachments/assets/89985fd8-90ee-4991-a71b-82f9f098aabd" />

Il nous faudra faire cela pour tout nos fichier csv.

Une fois le chargement de tout les fichiers fini, cela donne ceci :
<img width="266" height="422" alt="image" src="https://github.com/user-attachments/assets/594ba1fa-5f8a-40d6-964e-7af11fe8f2f2" />
