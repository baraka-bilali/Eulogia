# Projet Eulogia — Groupe 2 : Clustering K-Means

Guide pas à pas pour installer l'environnement, les bibliothèques Python et exécuter le notebook de clustering K-Means sur les données électriques africaines.

---

## Sommaire

1. [Prérequis](#1-prérequis)
2. [Structure du projet](#2-structure-du-projet)
3. [Installation de Python](#3-installation-de-python)
4. [Installation des bibliothèques](#4-installation-des-bibliothèques)
5. [Exécuter le projet dans Cursor](#5-exécuter-le-projet-dans-cursor)
6. [Exécuter le projet en ligne de commande (alternative)](#6-exécuter-le-projet-en-ligne-de-commande-alternative)
7. [Résultats attendus](#7-résultats-attendus)
8. [Dépannage](#8-dépannage)

---

## 1. Prérequis

Avant de commencer, assurez-vous d'avoir :

| Outil | Version minimale | Vérification |
|-------|------------------|--------------|
| **Python** | 3.10 ou plus récent | `python --version` |
| **pip** | inclus avec Python | `pip --version` |
| **Cursor** (ou VS Code) | dernière version | — |
| **Extension Jupyter** | pour Cursor/VS Code | installée automatiquement à l'ouverture d'un `.ipynb` |

> **Système testé :** Windows 10/11 — les commandes PowerShell sont utilisées ci-dessous.

---

## 2. Structure du projet

```
Eulogia/
├── README.md                                          ← ce fichier
├── Donnees_Electricite_preparees_KMeans_CORRIGE.xlsx  ← données (obligatoire)
├── Groupe2_KMeans.ipynb                               ← notebook principal
└── outputs/                                           ← graphiques et exports (créé à l'exécution)
    ├── kmeans_evaluation_k2_10.png
    ├── kmeans_pca_k4.png
    ├── kmeans_heatmap_k4.png
    ├── kmeans_silhouette_k4.png
    ├── kmeans_affectation_k4.xlsx
    ├── kmeans_profils_moyens_k4.xlsx
    └── kmeans_metriques_k2_10.xlsx
```

---

## 3. Installation de Python

### Étape 3.1 — Vérifier si Python est déjà installé

Ouvrez un terminal dans Cursor : **Terminal → New Terminal** (ou `Ctrl + ù`).

```powershell
python --version
```

Si vous voyez `Python 3.10.x` (ou supérieur), passez à l'étape 4.

### Étape 3.2 — Installer Python (si nécessaire)

1. Allez sur [https://www.python.org/downloads/](https://www.python.org/downloads/)
2. Téléchargez **Python 3.12** (ou la dernière version stable)
3. Lancez l'installateur
4. **Cochez impérativement** : `Add Python to PATH`
5. Cliquez sur **Install Now**
6. Fermez et rouvrez le terminal, puis vérifiez :

```powershell
python --version
pip --version
```

---

## 4. Installation des bibliothèques

Placez-vous dans le dossier du projet :

```powershell
cd D:\BECKER\Eulogia
```

### Étape 4.1 — Installer toutes les dépendances en une commande

```powershell
pip install pandas openpyxl scikit-learn matplotlib seaborn jupyter nbconvert
```

| Bibliothèque | Rôle dans le projet |
|--------------|---------------------|
| `pandas` | Lecture et manipulation des données Excel |
| `openpyxl` | Moteur de lecture des fichiers `.xlsx` |
| `scikit-learn` | Algorithme K-Means, PCA, score de silhouette |
| `matplotlib` | Création des graphiques (coude, PCA, heatmap) |
| `seaborn` | Graphiques statistiques (heatmaps, palettes) |
| `jupyter` | Exécution des notebooks `.ipynb` |
| `nbconvert` | Exécution automatique du notebook en ligne de commande |

> `numpy` et `scipy` sont installés automatiquement comme dépendances de `pandas` et `scikit-learn`.

### Étape 4.2 — Vérifier que tout est installé

```powershell
python -c "import pandas, openpyxl, sklearn, matplotlib, seaborn; print('Toutes les bibliothèques sont OK')"
```

Vous devez voir : `Toutes les bibliothèques sont OK`

### Étape 4.3 — (Optionnel) Créer un environnement virtuel

Recommandé si vous travaillez sur plusieurs projets Python :

```powershell
cd D:\BECKER\Eulogia
python -m venv venv
.\venv\Scripts\Activate.ps1
pip install pandas openpyxl scikit-learn matplotlib seaborn jupyter nbconvert
```

> Si PowerShell bloque l'activation, exécutez une fois :
> `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned`

---

## 5. Exécuter le projet dans Cursor

### Étape 5.1 — Ouvrir le dossier

1. Dans Cursor : **File → Open Folder**
2. Sélectionnez `D:\BECKER\Eulogia`

### Étape 5.2 — Ouvrir le notebook

1. Dans l'explorateur de fichiers (barre latérale gauche), cliquez sur **`Groupe2_KMeans.ipynb`**
2. Si Cursor propose d'installer l'extension **Jupyter**, acceptez

### Étape 5.3 — Sélectionner le kernel Python

1. En haut à droite du notebook, cliquez sur **Select Kernel**
2. Choisissez **Python 3.x** (celui où vous avez installé les bibliothèques)
3. Si vous utilisez un environnement virtuel, sélectionnez `./venv/Scripts/python.exe`

### Étape 5.4 — Vérifier le chemin des données

Dans la **2e cellule de code** du notebook, vérifiez que le chemin correspond à votre machine :

```python
BASE_DIR = Path(r"D:/BECKER/Eulogia")
```

Si vous avez copié le projet ailleurs, modifiez ce chemin. Exemple :

```python
BASE_DIR = Path(r"C:/Users/VotreNom/Documents/Eulogia")
```

### Étape 5.5 — Exécuter le notebook

| Action | Raccourci / bouton |
|--------|-------------------|
| Exécuter une cellule | `Shift + Entrée` ou bouton ▶ |
| Exécuter toutes les cellules | **Run All** (en haut du notebook) |
| Redémarrer le kernel | **Kernel → Restart** |

**Exécution complète :** cliquez sur **Run All** — toutes les cellules doivent s'exécuter sans erreur (environ 30 secondes).

### Étape 5.6 — Confirmer que ça fonctionne

Après **Run All**, vous devez voir :

- Un tableau avec **54 pays** et **25 variables**
- Les métriques K-Means pour **k = 2 à 10**
- Des **graphiques** affichés sous les cellules (coude, silhouette, PCA, heatmap)
- Un message final : `Fichiers exportés dans : D:\BECKER\Eulogia\outputs`

---

## 6. Exécuter le projet en ligne de commande (alternative)

Si vous préférez ne pas utiliser l'interface Cursor, exécutez le notebook depuis le terminal :

```powershell
cd D:\BECKER\Eulogia
python -m jupyter nbconvert --to notebook --execute Groupe2_KMeans.ipynb --output Groupe2_KMeans_executed.ipynb
```

Pour lancer Jupyter dans le navigateur :

```powershell
cd D:\BECKER\Eulogia
python -m jupyter notebook
```

Puis ouvrez `Groupe2_KMeans.ipynb` dans le navigateur qui s'ouvre.

---

## 7. Résultats attendus

### Fichiers générés dans `outputs/`

| Fichier | Contenu |
|---------|---------|
| `kmeans_evaluation_k2_10.png` | Courbes inertie (coude) et silhouette |
| `kmeans_pca_k4.png` | Visualisation PCA des 4 clusters |
| `kmeans_heatmap_k4.png` | Profils normalisés par cluster |
| `kmeans_silhouette_k4.png` | Distribution des scores de silhouette |
| `kmeans_affectation_k4.xlsx` | Liste des 54 pays avec leur cluster |
| `kmeans_profils_moyens_k4.xlsx` | Profils moyens par cluster |
| `kmeans_metriques_k2_10.xlsx` | Tableau des métriques k=2 à 10 |

### Résultat principal

- **k retenu : 4 clusters**
- Cluster 0 : 11 pays émergents (Ghana, Nigeria, Kenya…)
- Cluster 1 : Afrique du Sud (puissance industrielle)
- Cluster 2 : Égypte (géant fossile)
- Cluster 3 : 41 pays à basse consommation

---

## 8. Dépannage

### `ModuleNotFoundError: No module named 'pandas'`

Les bibliothèques ne sont pas installées sur le kernel sélectionné :

```powershell
pip install pandas openpyxl scikit-learn matplotlib seaborn
```

Puis redémarrez le kernel : **Kernel → Restart**.

---

### `FileNotFoundError` sur le fichier Excel

Le chemin `BASE_DIR` dans le notebook ne correspond pas à l'emplacement réel du projet. Modifiez la 2e cellule de code :

```python
BASE_DIR = Path(r"VOTRE/CHEMIN/VERS/Eulogia")
```

---

### Le kernel ne démarre pas dans Cursor

1. Installez l'extension **Jupyter** : `Ctrl+Shift+X` → recherchez "Jupyter" → Install
2. Redémarrez Cursor
3. Rouvrez le notebook et resélectionnez le kernel

---

### `pip` est reconnu mais pas `python`

Essayez avec `py` à la place :

```powershell
py --version
py -m pip install pandas openpyxl scikit-learn matplotlib seaborn jupyter
```

---

### Erreur réseau lors de `pip install`

Réessayez avec un timeout plus long, ou installez les paquets un par un :

```powershell
pip install pandas
pip install openpyxl
pip install scikit-learn
pip install matplotlib
pip install seaborn
```

---

### Les graphiques ne s'affichent pas

Vérifiez que `matplotlib` est bien installé et que la cellule contenant `plt.show()` a bien été exécutée. Redémarrez le kernel et relancez **Run All**.

---

## Contact / Groupe 4

Ce notebook est produit par le **Groupe 2** (K-Means). Transmettez le notebook et le dossier `outputs/` au **Groupe 4** pour l'assemblage du notebook final et la rédaction du rapport PDF.
