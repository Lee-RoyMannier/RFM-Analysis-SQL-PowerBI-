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

## Création de notre table RAW

Dans un premier temps, nous regroupons l’ensemble des tables de ventes mensuelles dans une table unique afin de centraliser les données.
```
-- Setp 1 : Append all monthly sales tables together

CREATE OR REPLACE TABLE `rfm1337.sales.raw_sales_2025` AS
  SELECT OrderID, CustomerID, OrderDate, ProductType, OrderValue FROM `sales.sales202501`
  UNION ALL
  SELECT OrderID, CustomerID, OrderDate, ProductType, OrderValue FROM `sales.sales202502`
  UNION ALL
  SELECT OrderID, CustomerID, OrderDate, ProductType, OrderValue FROM `sales.sales202503`
  UNION ALL
  SELECT OrderID, CustomerID, OrderDate, ProductType, OrderValue FROM `sales.sales202504`
  UNION ALL
  SELECT OrderID, CustomerID, OrderDate, ProductType, OrderValue FROM `sales.sales202505`
  UNION ALL
  SELECT OrderID, CustomerID, OrderDate, ProductType, OrderValue FROM `sales.sales202506`
  UNION ALL
  SELECT OrderID, CustomerID, OrderDate, ProductType, OrderValue FROM `sales.sales202507`
  UNION ALL
  SELECT OrderID, CustomerID, OrderDate, ProductType, OrderValue FROM `sales.sales202508`
  UNION ALL
  SELECT OrderID, CustomerID, OrderDate, ProductType, OrderValue FROM `sales.sales202509`
  UNION ALL
  SELECT OrderID, CustomerID, OrderDate, ProductType, OrderValue FROM `sales.sales202510`
  UNION ALL
  SELECT OrderID, CustomerID, OrderDate, ProductType, OrderValue FROM `sales.sales202511`
  UNION ALL
  SELECT OrderID, CustomerID, OrderDate, ProductType, OrderValue FROM `sales.sales202512`
```

### 📊 Préparation des données pour l’analyse RFM
Maintenant que nos données sont centralisées, nous pouvons préparer les indicateurs nécessaires à l’analyse RFM (Recency, Frequency, Monetary).

🎯 Objectif

Calculer pour chaque client :

- Recency : nombre de jours écoulés depuis le dernier achat

- Frequency : nombre total de commandes

- Monetary : montant total dépensé (€)

Afin de structurer la logique métier et de rendre les calculs réutilisables, nous créons une vue dans Google BigQuery, en utilisant une requête SQL ainsi qu'une CTE.

Dans cette étape, nous construisons une vue analytique permettant de calculer les métriques RFM pour chaque client. Une date d’analyse fixe est définie (2026-01-01) afin de garantir la reproductibilité des résultats. Pour chaque client, nous calculons la recency (nombre de jours depuis le dernier achat), la frequency (nombre total de commandes) et le monetary (montant total dépensé).
Ensuite, nous ajoutons un système de ranking à l’aide de fonctions analytiques (ROW_NUMBER) afin de positionner chaque client relativement aux autres sur chaque dimension (récence, fréquence et valeur). Cette vue constitue la base analytique pour le scoring RFM.
```
CREATE OR REPLACE VIEW `rfm1337.sales.rfm_metrics`
AS
WITH current_date AS (
  SELECT DATE('2026-01-01') as analysis_date 
),
rfm as (
  SELECT
    CustomerID,
    MAX(OrderDate) as last_order_date,
    DATE_DIFF((SELECT analysis_date FROM current_date), MAX(OrderDate), DAY) as recency,
    COUNT(OrderID) as frequency,
    SUM(OrderValue) as monetary
  FROM
    `rfm1337.sales.raw_sales_2025` 
  GROUP BY CustomerID
)

SELECT
  rfm.*,
  ROW_NUMBER() OVER(ORDER BY recency ASC) as r_rank,
  ROW_NUMBER() OVER(ORDER BY frequency DESC) as f_rank,
  ROW_NUMBER() OVER(ORDER BY monetary DESC) as m_rank,
FROM
  rfm;

```

🔢 Attribution des scores RFM (déciles)

Une fois les classements établis, nous transformons ces rangs en scores grâce à la fonction NTILE(10), qui permet de répartir les clients en 10 groupes (déciles). Chaque client reçoit ainsi un score de 1 à 10 pour chacune des dimensions R, F et M.
Un score élevé indique une meilleure performance (client récent, fréquent et à forte valeur). Cette étape permet de normaliser les métriques et de faciliter la segmentation client.

```
CREATE OR REPLACE VIEW `rfm1337.sales.rfm_scores` 
AS
SELECT
  *,
  NTILE(10) OVER(ORDER BY r_rank DESC) as r_score,
  NTILE(10) OVER(ORDER BY f_rank DESC) as f_score,
  NTILE(10) OVER(ORDER BY m_rank DESC) as m_score
FROM 
  `rfm1337.sales.rfm_metrics`

```

🧮 Calcul du score RFM global

Dans cette étape, nous agrégeons les scores individuels (R, F et M) afin de calculer un score RFM total. Ce score est obtenu en faisant la somme des trois composantes, ce qui permet d’obtenir une vision globale de la valeur client.
Ce score global est ensuite utilisé pour classer les clients du plus performant au moins performant, facilitant ainsi l’identification des profils à forte valeur et des clients à risque.

```
CREATE OR REPLACE VIEW `rfm1337.sales.rfm_total_scores`
AS
SELECT
  CustomerID,
  recency,
  frequency,
  monetary,
  r_score,
  f_score,
  m_score,
  (r_score + f_score + m_score) as rfm_total_score
FROM
  `rfm1337.sales.rfm_scores`
ORDER BY rfm_total_score DESC

```

🎯 Segmentation client (table prête pour la BI)

Enfin, nous créons une table finale prête à être exploitée dans un outil de visualisation comme Power BI.
Les clients sont segmentés en différentes catégories métier (Champions, Loyal VIPs, At Risk, etc.) en fonction de leur score RFM total. Cette segmentation permet de traduire les résultats analytiques en insights business directement exploitables par les équipes marketing.

Cette table constitue le livrable final du projet, optimisé pour la création de dashboards et la mise en place de stratégies de ciblage client.

```
-- Step 5: BI ready rfm segments table
CREATE OR REPLACE TABLE `rfm1337.sales.rfm_segments_final`
AS
SELECT
  CustomerID,
  recency,
  frequency,
  monetary,
  r_score,
  f_score,
  m_score,
  rfm_total_score,
  CASE
    WHEN rfm_total_score >= 28 THEN 'Champions'
    WHEN rfm_total_score >= 24 THEN 'Loyal VIPs'
    WHEN rfm_total_score >= 20 THEN 'Potential loyalists'
    WHEN rfm_total_score >= 16 THEN 'Promissing'
    WHEN rfm_total_score >= 12 THEN 'Engaged'
    WHEN rfm_total_score >= 8 THEN 'Requires Attention'
    WHEN rfm_total_score >= 4 THEN 'At Risk'
    ELSE 'Lost/Inactive'
  END as segment
FROM
  `rfm1337.sales.rfm_total_scores`
ORDER BY rfm_total_score DESC
```

On peut test cette nouvelle table avec :
```
SELECT
  segment,
  count(*)
FROM
  `rfm1337.sales.rfm_segments_final`
GROUP BY segment;
```
<img width="381" height="238" alt="image" src="https://github.com/user-attachments/assets/a7d9e84a-e8c8-4a28-bab8-c763d0996f24" />

## 📊 Visualisation des données avec Power BI
Dans cette dernière étape, les données préparées dans Google BigQuery sont connectées à Power BI afin de créer un dashboard interactif.

La connexion directe à BigQuery permet d’exploiter la table finale rfm_segments_final, optimisée pour la BI, sans nécessiter de transformations supplémentaires côté Power BI. Cela garantit une source de vérité unique et des données toujours à jour.

Le dashboard permet de visualiser les segments clients, d’analyser la distribution des scores RFM et d’identifier rapidement les profils à forte valeur ou à risque. Ces visualisations facilitent la prise de décision et permettent de transformer les résultats analytiques en actions marketing concrètes.

<img width="1771" height="991" alt="image" src="https://github.com/user-attachments/assets/70d17c90-0147-4dbd-9bf9-b880c0271b64" />

# 📊 Analyse du dashboard RFM
1. 🎯 Potentiel de conversion élevé

Une grande partie des clients se situe dans les segments Engaged et Promising, indiquant une base client active avec un fort potentiel de montée en gamme.

2. 💰 Concentration de la valeur

Les segments Champions et Loyal VIPs représentent une part réduite des clients mais concentrent probablement une part significative du chiffre d’affaires.

3. ⚠️ Risque de churn modéré

Environ 24% des clients sont classés At Risk ou Requires Attention, ce qui nécessite des actions marketing ciblées pour éviter leur perte.

4. ✅ Bonne rétention globale

Le faible nombre de clients Lost/Inactive indique une bonne capacité de rétention.

🚀 Recommandations (niveau senior / recruteur 🔥)
🟢 Champions & VIPs

Offres exclusives

Programme de fidélité

Early access produits

🟡 Engaged / Promising

Email marketing ciblé

Upsell / cross-sell

Réduction limitée dans le temps

🟠 At Risk

Campagnes de réactivation

Remises personnalisées

Relance email automatisée

🔴 Lost

Campagne “win-back”

Survey pour comprendre le churn
