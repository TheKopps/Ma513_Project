
# NER4Cyber-IPSA - Adrien Monteiro - Diego De Sousa

## Description
NER4Cyber-IPSA est un projet de reconnaissance d'entités nommées (NER) appliqué au domaine de la cybersécurité. Ce projet utilise un modèle pré-entraîné BERT pour effectuer une classification des entités à partir de données textuelles. Le projet est conçu pour entraîner, valider et tester un modèle sur des ensembles de données spécifiques à des tâches NER dans le cadre de la cybersécurité.

## Fonctionnalités principales
1. **Entraînement du modèle** : Chargement et prétraitement des données, ajustement des poids de classes pour gérer les déséquilibres, et entraînement du modèle BERT.
2. **Validation** : Évaluation des performances après chaque époque en utilisant les métriques de classification NER.
3. **Test** : Prédiction des entités nommées sur des données de test, suivi d'un export des résultats au format JSONLines.
4. **Sauvegarde** : Conservation du modèle, du tokenizer et des étiquettes uniques pour une réutilisation future.

## Installation

### Prérequis
- Python 3.8 ou supérieur
- CUDA (facultatif, mais recommandé pour accélérer l'entraînement avec GPU)
- Bibliothèques Python :
  - `transformers`
  - `torch`
  - `tqdm`
  - `seqeval`
  - `json`

### Installation des dépendances
Utilisez `pip` pour installer les dépendances nécessaires :

```bash
pip install torch transformers tqdm seqeval
```

## Utilisation

### Entraînement du modèle
1. Placez vos fichiers de données d'entraînement et de validation (`NER-TRAINING.jsonlines` et `NER-VALIDATION.jsonlines`) dans le chemin spécifié.
2. Configurez les hyperparamètres (chemins des fichiers, nombre d'époques, etc.) dans `train_model_v5`.
3. Exécutez le script d'entraînement :

   ```bash
   python train_model_v5.py
   ```

4. Le modèle et le tokenizer seront sauvegardés dans le répertoire spécifié (par défaut : `saved_model`).

### Test du modèle
1. Placez votre fichier de données de test (`NER-TESTING.jsonlines`) dans le chemin spécifié.
2. Exécutez le script de test :

   ```bash
   python test_model_v5.py
   ```

3. Les prédictions seront sauvegardées dans un fichier `NER-PREDICTIONS.jsonlines`.

### Structure des données
Chaque fichier JSONLines doit contenir des entrées avec les champs suivants :
- `unique_id` : Identifiant unique pour chaque exemple.
- `tokens` : Liste des mots/tokens de la phrase.
- `ner_tags` : Liste des étiquettes correspondantes (facultatif pour les données de test).

### Exemples de fichiers
#### Fichier d'entraînement (`NER-TRAINING.jsonlines`)
```json
{"unique_id": "1", "tokens": ["This", "is", "a", "test"], "ner_tags": ["O", "O", "O", "B-TEST"]}
```

#### Fichier de test (`NER-TESTING.jsonlines`)
```json
{"unique_id": "2", "tokens": ["Another", "example"]}
```

## Résultats
Les performances sont évaluées avec des métriques comme le rapport de classification (`seqeval`) et les pertes d'entraînement/validation. Les résultats finaux incluent des prédictions sauvegardées sous forme JSONLines.

## Structure du projet
```
NER4Cyber-IPSA/
├── train_model_v5.py        # Script pour l'entraînement
├── test_model_v5.py         # Script pour le test
├── saved_model/             # Répertoire contenant le modèle sauvegardé
├── Data/
│   ├── NER-TRAINING.jsonlines    # Données d'entraînement
│   ├── NER-VALIDATION.jsonlines  # Données de validation
│   ├── NER-TESTING.jsonlines     # Données de test
│   ├── NER-PREDICTIONS.jsonlines # Prédictions générées
└── README.md                # Documentation du projet
```

## Contributions
Les contributions sont les bienvenues ! Si vous souhaitez ajouter des fonctionnalités ou améliorer les performances, n'hésitez pas à soumettre une pull request.

## Licence
Ce projet est sous licence MIT. Voir le fichier `LICENSE` pour plus d'informations.
