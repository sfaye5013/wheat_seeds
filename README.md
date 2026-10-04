# 🌾 Classification des graines de blé

Application **Streamlit** qui classe une graine de blé parmi plusieurs
variétés à partir de ses caractéristiques physiques (aire, périmètre,
compacité, longueur et largeur du noyau, coefficient d'asymétrie, longueur du
sillon). Le modèle retenu est un **DBSCAN** (clustering basé sur la densité),
entraîné et exploré dans le notebook associé.

## Structure du projet

```
.
├── app.py                               # Application Streamlit (interface + inférence)
├── requirements.txt                     # Dépendances Python
├── data/
│   └── wheat_seeds_dataset.csv          # Jeu de données brut utilisé pour l'entraînement
├── models/
│   └── modele_dbscan.joblib             # Modèle DBSCAN entraîné (points cœurs, labels, eps, etc.)
├── outils/
│   └── utils.py                         # Fonctions utilitaires
└── Kmeans_On_Wheat_Seeds_Dataset.ipynb   # Exploration, préparation des données et entraînement des modèles
```

## Installation

```bash
python -m venv .venv
source .venv/bin/activate  # Windows : .venv\Scripts\activate
pip install -r requirements.txt
```

## Lancer l'application

```bash
streamlit run app.py
```

L'application permet de :

- Sélectionner des valeurs médianes ou l'un des exemples prédéfinis pour
  pré-remplir le formulaire.
- Saisir les caractéristiques d'une graine de blé.
- Obtenir sa classe prédite, ou un avertissement si la graine est atypique
  (point considéré comme une anomalie par DBSCAN).

## Entraînement du modèle

Le notebook `Kmeans_On_Wheat_Seeds_Dataset.ipynb` contient le pipeline de
préparation des données :

1. Analyse exploratoire (distributions, corrélations).
2. Normalisation des variables numériques.
3. Comparaison de plusieurs algorithmes de clustering (K-Means, DBSCAN).
4. Sélection du modèle DBSCAN, export des points cœurs, labels et paramètres
   (`eps`, valeurs par défaut, exemples) avec `joblib` dans `models/`.

## Jeu de données

`data/wheat_seeds_dataset.csv` contient 199 lignes avec les colonnes
suivantes :

| Colonne                      | Description                        |
|-------------------------------|-------------------------------------|
| `area A`                      | Aire du grain                      |
| `perimeter`                   | Périmètre du grain                 |
| `compactness`                 | Compacité (4·π·aire / périmètre²)  |
| `length of kernel`            | Longueur du noyau                  |
| `width of kernel`              | Largeur du noyau                   |
| `asymmetry coefficient`       | Coefficient d'asymétrie            |
| `length of kernel groove`     | Longueur du sillon du noyau        |

## Déploiement

Cette application est conçue pour être déployée sur **Streamlit Community
Cloud** :

1. Pousser ce dépôt sur GitHub.
2. Aller sur [share.streamlit.io](https://share.streamlit.io), se connecter
   avec GitHub.
3. Cliquer sur **New app**, sélectionner le dépôt, la branche `main` et le
   fichier `app.py`.
4. Déployer : l'application sera accessible via une URL publique du type
   `https://<nom-app>.streamlit.app`.
