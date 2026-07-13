<div align="center">

# Analyse Prédictive du Désabonnement des Clients Bancaires
### Projet de Business Intelligence — ETL avec CloverDX & Reporting interactif avec Looker Studio

*Legends Banque — Girls Project*

![CloverDX](https://img.shields.io/badge/ETL-CloverDX-00A19A)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?logo=mysql&logoColor=white)
![Looker Studio](https://img.shields.io/badge/Looker_Studio-4285F4?logo=looker&logoColor=white)
![Google Sheets](https://img.shields.io/badge/Google_Sheets-34A853?logo=googlesheets&logoColor=white)
![Kaggle](https://img.shields.io/badge/Dataset-Kaggle-20BEFF?logo=kaggle&logoColor=white)
![Modèle](https://img.shields.io/badge/Mod%C3%A8le-%C3%89toile-orange)

**Projet académique — Ingénierie Informatique et Technologies Emergentes (2ITE)**

École Nationale des Sciences Appliquées d'El Jadida — Université Chouaïb Doukkali

Année universitaire **2024-2025**

</div>

---

## ⚡ En un coup d'œil

| | |
|---|---|
| 📉 **20,4 %** de taux de désabonnement global | 👥 **10 000** clients analysés |
| 🌍 **3 pays** couverts (France, Allemagne, Espagne) | 🔁 Pipeline **ETL complet** avec CloverDX |
| ⭐ Modélisation en **schéma étoile** (1 fait + 3 dimensions) | 📊 **6 tableaux de bord interactifs** sous Looker Studio |
| 🗓️ **4,9 ans** de fidélité moyenne avant désabonnement | 🧬 Analyse croisée : âge, genre, solde, produits, activité |

---

## Sommaire
- [Description](#-description)
- [Contexte et problématique](#-contexte-et-problématique)
- [Objectifs du projet](#-objectifs-du-projet)
- [Méthodologie](#-méthodologie)
- [Chaîne décisionnelle](#-chaîne-décisionnelle)
- [Architecture applicative](#️-architecture-applicative)
- [Modélisation en étoile](#-modélisation-en-étoile)
- [Processus ETL avec CloverDX](#-processus-etl-avec-cloverdx)
- [Reporting & visualisation](#-reporting--visualisation)
- [Dashboards Looker Studio](#-dashboards-looker-studio)
- [Principaux insights](#-principaux-insights)
- [Stack technique](#️-stack-technique)
- [Jeu de données](#-jeu-de-données)
- [Structure du dépôt](#-structure-du-dépôt)
- [Documentation](#-documentation)
- [Auteures](#-auteures)

---

## Description

Ce projet de Business Intelligence analyse le **désabonnement (churn)** des clients d'une banque de détail à partir d'un dataset public Kaggle de 10 000 clients. L'objectif est de comprendre les facteurs qui poussent un client à quitter la banque, d'identifier les profils à risque, et de restituer ces analyses sous forme de **tableaux de bord interactifs** pour aider les décideurs à agir.

Le pipeline complet part de l'extraction du dataset brut, passe par un **processus ETL structuré sous CloverDX** (nettoyage, transformation, modélisation en étoile), un chargement dans **MySQL**, puis une restitution visuelle via **Looker Studio** (anciennement Google Data Studio).

---

## Contexte et problématique

Le désabonnement client est un enjeu stratégique majeur pour les banques : conserver un client coûte bien moins cher que d'en acquérir un nouveau, et un taux de churn élevé dégrade à la fois les revenus et la réputation de l'établissement.

**Problématique centrale :**
> *Quels sont les facteurs qui influencent le désabonnement des clients dans une banque de détail, et comment peut-on anticiper et réduire ce phénomène ?*

Sous-questions traitées :
- Quels profils de clients sont les plus susceptibles de se désabonner ?
- Quels facteurs géographiques, démographiques et comportementaux jouent un rôle clé ?
- Quelles actions préventives peuvent limiter le désabonnement ?

---

## Objectifs du projet

- **Analyser** les comportements de désabonnement et en identifier les tendances.
- **Identifier** les segments de clients à risque.
- **Structurer** les données dans un modèle en étoile adapté à l'analyse rapide.
- **Restituer** les résultats via des tableaux de bord clairs et interactifs pour la prise de décision.

---

## Méthodologie

L'analyse suit une démarche structurée en quatre grandes étapes :

<img width="890" height="103" alt="processus-etl" src="https://github.com/user-attachments/assets/05c3aa3d-7fbe-4edc-989c-798b8d747744" />

1. **Exploration des données** : inspection de la structure du dataset, détection des valeurs manquantes.
2. **Transformation et nettoyage** : traitement des valeurs manquantes, normalisation, encodage des variables catégorielles — via **CloverDX**.
3. **Analyse statistique** : mise en évidence des tendances et facteurs de risque par croisement de dimensions.
4. **Visualisation et reporting** : tableaux de bord interactifs sous **Looker Studio**.

---

## Chaîne décisionnelle

La chaîne décisionnelle représente le processus complet de transformation des données brutes en informations exploitables pour la prise de décision.

<img width="842" height="298" alt="chaine-decisionnelle" src="https://github.com/user-attachments/assets/fec5d1b6-cb83-4621-a6f1-5c3d280662fa" />

Collecte → Nettoyage & transformation → Analyse → Visualisation → Prise de décision.

---

## Architecture applicative

Le flux applicatif global part de la source de données (Kaggle) jusqu'au reporting final (Looker Studio), en passant par l'ETL (CloverDX) et le stockage (MySQL + Google Sheets).

<img width="3120" height="1836" alt="architecture-applicative" src="https://github.com/user-attachments/assets/8abbb126-4dd8-43cf-957e-2beee899fc45" />

- **Source** : dataset Kaggle *Bank Customer Churn* au format CSV.
- **ETL** : CloverDX pour l'extraction, la transformation et le chargement.
- **Stockage** : MySQL (requêtage structuré) + Google Sheets (connecteur natif Looker Studio).
- **Reporting** : Looker Studio pour les tableaux de bord interactifs.

> 📌 Note technique : la connexion directe MySQL → Looker Studio ayant posé des difficultés de synchronisation, les données ont été exportées vers **Google Sheets** comme solution de contournement, avant d'être connectées à Looker Studio via son connecteur natif.

---

## Modélisation en étoile

Le modèle en étoile a été retenu pour sa simplicité et son efficacité sur les requêtes analytiques : une table de faits centrale entourée de trois dimensions.

<img width="3840" height="3109" alt="modele-etoile" src="https://github.com/user-attachments/assets/ba2b5ac8-5796-46c9-b54e-af0ce057c34b" />

| Table | Rôle | Champs clés |
|---|---|---|
| **Fact_Desabonnement** | Table de faits | CreditScore, Balance, NumberOfProduct, Tenure, Exited + clés étrangères |
| **Customer** | Dimension client | CustomerId, Surname, Age, Gender, Salary, HasCreditCard, IsActiveMember |
| **Geography** | Dimension géographique | GeographyId, Country |
| **Date** | Dimension temporelle | DateId, Date |

Ce choix évite la complexité inutile d'un modèle en flocon ou en constellation, tout en restant facilement extensible si de nouvelles dimensions sont nécessaires.

---

## Processus ETL avec CloverDX

Le pipeline ETL est organisé en **3 jobs CloverDX** successifs :

1. **Filtrage des données** — `FlatFileReader` → `Filter` (suppression des enregistrements avec champs null) → `FlatFileWriter`.
2. **Extraction des dimensions** — `FlatFileReader` → `Combine` → `Map` (un par dimension) → `ExtSort` → `Dedup` → `DatabaseWriter` (insertion dans Customer, Geography, Date).
3. **Chargement de la table de faits** — `FlatFileReader` → `LookupJoin` (récupération des clés étrangères via des requêtes SQL sur les dimensions) → `DatabaseWriter` (insertion dans Fact_Desabonnement).

**Composants clés utilisés :** FlatFileReader/Writer, Filter, Combine, Map, ExtSort, Dedup, DatabaseWriter, LookupJoin.

---

##  Reporting & visualisation

Les données sont restituées sous Looker Studio à travers des **scorecards** (indicateurs clés), des **graphiques** (barres, courbes, radar, treemap) et une **carte géographique**, organisés en 6 sections thématiques.

---

## Dashboards Looker Studio

### 1. Indicateurs globaux

<img width="3750" height="2813" alt="Rapport_Désabonnement_260707_095747_page-0001" src="https://github.com/user-attachments/assets/352fc823-f6b7-4257-bd9a-83491bd725b7" />

Taux de désabonnement global (20,4 %), total de clients distincts (10,0 k), nombre moyen de produits par client (1,5), analyse triangulaire (Exited / Tenure / HasCreditCard) et jauge du volume total de désabonnements (2,0 k).

### 2. Répartition par pays et par date

<img width="3750" height="2813" alt="Rapport_Désabonnement_260707_095747_page-0002" src="https://github.com/user-attachments/assets/f21d26fb-1892-410e-bb69-c2af52bbbb27" />

Allemagne (814) et France (810) concentrent la majorité des désabonnements, loin devant l'Espagne (413). Carte géographique et détail chronologique par jour.

### 3. CreditScore et durée d'adhésion (Tenure)

<img width="3750" height="2813" alt="Rapport_Désabonnement_260707_095747_page-0003" src="https://github.com/user-attachments/assets/92ee1e5b-6407-42d3-a14e-65cfafc20b99" />

Durée moyenne de fidélité avant désabonnement : **4,9 ans**, avec une répartition assez uniforme des départs sur l'ensemble des durées d'adhésion.

### 4. Nombre de produits et solde bancaire

<img width="3750" height="2813" alt="Rapport_Désabonnement_260707_095747_page-0004" src="https://github.com/user-attachments/assets/8d595f8b-d504-4587-9101-a366943e9bc9" />

Les clients avec un seul produit bancaire représentent l'immense majorité des désabonnements (1 409 sur 2 037), suggérant qu'un portefeuille de produits diversifié fidélise davantage.

### 5. Répartition par genre et âge

<img width="3750" height="2813" alt="Rapport_Désabonnement_260707_095747_page-0005" src="https://github.com/user-attachments/assets/22ff1a9e-0c66-4621-b631-e63c207cc142" />

Les femmes représentent 55,9 % des désabonnements. Le pic de désabonnement se situe dans la tranche 40-50 ans, avec un maximum à 46 ans.

### 6. Statut d'activité et possession de carte de crédit

<img width="3750" height="2813" alt="Rapport_Désabonnement_260707_095747_page-0006" src="https://github.com/user-attachments/assets/30f8717e-ac7e-4204-9aee-0dccc8b61965" />

Les clients **inactifs** se désabonnent nettement plus (1 302 cas) que les clients actifs. La possession d'une carte de crédit ne montre en revanche pas d'impact direct significatif sur le churn.

---

## Principaux insights

- **Portefeuille de produits** : posséder un seul produit bancaire est le facteur le plus associé au désabonnement — la diversification des produits pourrait réduire le churn.
- **Engagement client** : les clients inactifs se désabonnent beaucoup plus que les clients actifs → l'activation/engagement est un levier clé de rétention.
- **Géographie** : Allemagne et France concentrent la majorité des départs malgré une base de clients comparable, ce qui justifie des actions de rétention ciblées par marché.
- **Âge** : la tranche 40-50 ans est la plus exposée au churn — des campagnes de fidélisation ciblées pourraient être envisagées pour ce segment.
- **Solde bancaire** : les soldes nuls ou très faibles sont associés à davantage de désabonnements.
- **Carte de crédit** : sa possession seule n'explique pas le churn, contrairement à d'autres facteurs comportementaux.

---

## Stack technique

| Domaine | Outils |
|---|---|
| **Source de données** | Kaggle (Bank Customer Churn Prediction Dataset) |
| **ETL** | CloverDX |
| **Stockage** | MySQL, Google Sheets |
| **Visualisation / Reporting** | Looker Studio (Google Data Studio) |

---

## Jeu de données

| Caractéristique | Valeur |
|---|---|
| Source | [Kaggle — Bank Customer Churn Prediction](https://www.kaggle.com/datasets/santoshd3/bank-customers) |
| Lignes | 10 000 clients |
| Colonnes | 14 |
| Cible | `Exited` (1 = désabonné, 0 = actif) |

**Champs principaux :** CustomerId, Surname, CreditScore, Geography, Gender, Age, Tenure, Balance, NumOfProducts, HasCrCard, IsActiveMember, EstimatedSalary, Exited.

---

## Structure du dépôt

```
analyse-desabonnement-bancaire-bi/
├── data/ # données nettoyées (sortie du job de filtrage)
│   └── Customer.csv
│   └── Date.csv
│   └── Fact_Desabonnement.csv
│   └── Geography.csv             
│
├── etl/
│   │── dimension_Unique_job.grf      
│   │── Fait_job.grf    
│   │── Filtering_job.grf          
│   └── Read_data_job.grp
│
└── README.md
```

---

## Auteur

**DRIHAM Siham**
Ingénieure d'État en Big Data
🔗 [LinkedIn](https://www.linkedin.com/in/siham-driham-955838238/) · 📧 [sihamdriham@gmail.com]

---

</div>
