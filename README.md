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

ORDER00102 | CUST0038 | 2025-01-01 | Flyer          | 11.60
ORDER00139 | CUST0025 | 2025-01-01 | Canvas Print   | 41.44
ORDER00398 | CUST0161 | 2025-01-01 | Greeting Card  | 4.56

## 🧠 Objectif analytique

L’objectif est de segmenter les clients selon 3 dimensions :

- Recency (R) : nombre de jours depuis la dernière commande

- Frequency (F) : nombre total de commandes

- Monetary (M) : montant total dépensé

Ces métriques permettront de classer les clients en segments, par exemple :

- 🟢 Champions

- 💎 Clients fidèles

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






