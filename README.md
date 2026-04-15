# Analyse des données des systèmes éducatifs — Expansion internationale d'Academy

## Contexte

**Academy** est une start-up EdTech spécialisée dans les formations en ligne pour les lycéens et étudiants. Dans le cadre d'une **expansion internationale**, ce projet réalise une analyse exploratoire des données de la Banque mondiale pour identifier les pays offrant le meilleur potentiel de marché.

## Objectifs

- Déterminer quels pays présentent les meilleures conditions pour l'implantation d'une plateforme EdTech
- Analyser les corrélations entre indicateurs éducatifs, économiques et démographiques
- Produire un classement des 10 pays à fort potentiel basé sur un score pondéré


## Données

Source : **World Bank EdStats** — base de données ouverte de la Banque mondiale sur les statistiques éducatives mondiales.

- ~1,5 million d'enregistrements
- Couvre la plupart des pays du monde
- Indicateurs éducatifs, économiques et démographiques

## Méthodologie

Le notebook est organisé en 4 parties :

### Partie 1 — Préparation des données
- Import des librairies et chargement des 5 fichiers CSV
- Exploration initiale (structure, doublons, valeurs manquantes)
- Suppression des colonnes vides

### Partie 2 — Nettoyage et filtrage
- Suppression des "faux pays" (agrégats régionaux, groupements mondiaux)
- Validation des codes ISO 3166 avec `pycountry`
- Sélection de 15 indicateurs pertinents pour l'EdTech
- Réduction temporelle (2000–2025)
- Construction d'une matrice **pays × indicateurs** (moyenne sur les années)
- Conservation des pays avec au moins 6 indicateurs renseignés

### Partie 3 — Analyse statistique
- Calcul des corrélations de **Pearson** et **Spearman**
- Heatmaps pour identifier les indicateurs redondants (r > 0,7)
- Décision motivée de conserver tous les indicateurs malgré les corrélations

### Partie 4 — Scoring et recommandations
- Distribution des indicateurs clés (histogrammes + KDE)
- **Méthode 1** : pays apparaissant le plus souvent dans les Top 5 par indicateur
- **Méthode 2** : score global pondéré avec normalisation Min-Max

| Indicateur | Poids | Justification |
|---|---|---|
| PIB par habitant (USD) | 30 % | Capacité d'achat pour services EdTech |
| Utilisateurs Internet (%) | 25 % | Maturité numérique, accès aux formations en ligne |
| Population en âge secondaire | 15 % | Volume du marché cible |
| Population en âge supérieur | 15 % | Volume du marché cible |
| Durée scolarité secondaire | 7,5 % | Valeur culturelle de l'éducation |
| Durée scolarité supérieure | 7,5 % | Valeur culturelle de l'éducation |

- Carte **Choropleth interactive** (Plotly) des Top 10 pays

## Résultat

Un classement des **10 pays à fort potentiel** d'expansion pour Academy, basé sur une combinaison de richesse économique, maturité numérique et taille du marché éducatif.

## Prérequis

```bash
pip install pandas numpy matplotlib seaborn scikit-learn plotly pycountry
```

Ou via le fichier de configuration :

```bash
pip install -r pyproject.toml
```

## Utilisation

1. Cloner le dépôt
2. Installer les dépendances
3. Ouvrir `1_notebook.ipynb` dans Jupyter Notebook ou JupyterLab
4. Exécuter les cellules dans l'ordre

