# Segmentation Client RFM + K-Means avec Gestion des Outliers  
### Analyse de segmentation clients sur le dataset **Online Retail II** (UCI)

![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![Pandas](https://img.shields.io/badge/Pandas-2.0%2B-3776AB)
![Scikit--learn](https://img.shields.io/badge/scikit--learn-KMeans-orange)
![License](https://img.shields.io/badge/License-MIT-green)

## Description du projet

Ce projet réalise une **segmentation client avancée** à partir du célèbre jeu de données **Online Retail II**, en combinant :

- L’approche classique **RFM** (Recency, Frequency, Monetary Value)
- Un **nettoyage rigoureux** des données (annulations, codes article spéciaux, valeurs manquantes…)
- Une **gestion intelligente des outliers** (clients très gros dépensiers ou très fréquents)
- Un **clustering K-Means** sur les données normalisées
- Une **interprétation métier actionable** avec 7 segments clients nommés

Le résultat : une segmentation marketing prête à être utilisée pour des campagnes ciblées (rétention, réactivation, upselling, fidélisation VIP…).

## Dataset utilisé

**Online Retail II**  
Lien : https://archive.ics.uci.edu/dataset/502/online+retail+ii

> Jeu de données réel de transactions d’un site e-commerce britannique (déc. 2009 – déc. 2011)  
> 1 067 371 lignes – 8 colonnes  
> Ventes de cadeaux et objets déco, principalement à des grossistes et particuliers

## Structure du projet
.
├── data/

│   └── online_retail_II.xlsx          # Dataset original

├── online-retail-data-clustering-personal.ipynb                     # Notebook complet (exploration → clustering)

├── requirements.txt                   # Dépendances

├── README.md                          # Ce fichier


## Segments clients obtenus (7 segments)

| Cluster | Nom          | Caractéristiques principales                                 | Stratégie marketing       |
|--------|--------------|----------------------------------------------------------------|----------------------------|
| 0      | **RETAIN**   | Bonnes dépenses, achats réguliers, parfois un peu anciens     | Fidélisation & engagement  |
| 1      | **RE-ENGAGE**| Faibles dépenses, peu fréquents, très anciens                 | Campagnes de réactivation  |
| 2      | **NURTURE**  | Clients récents mais faibles dépenses et fréquence            | Onboarding & nurturing     |
| 3      | **REWARD**   | Très bons clients, fréquents et récents                       | Programme VIP, cadeaux     |
| -1     | **PAMPER**   | Très gros panier mais peu fréquents (outliers Monetary)       | Offres premium, services+  |
| -2     | **UPSELL**   | Très fréquents mais faible panier moyen (outliers Frequency)  | Upsell & cross-sell        |
| -3     | **DELIGHT**  | Champions absolus : très gros + très fréquents                | Traitement VIP exclusif    |

## Principales étapes du notebook

1. **Exploration & nettoyage**
   - Suppression des annulations (`Invoice` commençant par "C")
   - Filtrage des codes article valides
   - Suppression des lignes sans `Customer ID`
   - Gestion des prix nuls ou négatifs

2. **Feature Engineering RFM**
   - `MonetaryValue` = Quantity × Price
   - `Frequency` = nombre de factures distinctes
   - `Recency` = jours depuis la dernière commande

3. **Détection et traitement des outliers** (méthode IQR sur Monetary & Frequency)

4. **Clustering K-Means** (k = 4 sur les clients "normaux")
   - Standardisation avec `StandardScaler`
   - Choix du k via Elbow + Silhouette

5. **Clustering spécifique des outliers** (3 segments supplémentaires)

6. **Visualisations**
   - Histogrammes & boxplots
   - Nuages de points 3D
   - Violins plots par cluster
   - Graphique récapitulatif avec effectifs + moyennes RFM

## Installation & exécution

```bash
git clone https://github.com/Toussema/online-retail-data-clustering-personal.git
cd online-retail-data-clustering-personal
pip install -r requirements.txt
jupyter notebook notebook.ipynb
