# AI-Course

Cours et TP d'introduction à l'intelligence artificielle — JUNIA M1.

## Environnement

Le PDF `AI_M1_00_Setup The Course Environment.pdf` demande un environnement
Python avec Jupyter et NumPy. Il présente Conda comme exemple et accepte
d'autres gestionnaires : ce projet utilise **uv et Python 3.12**.

Les dépendances sont installées dans **`.venv`**, propre à ce dossier :

| Outil | Utilisation |
| --- | --- |
| Jupyter Notebook et JupyterLab | Ouvrir et exécuter les notebooks des TP |
| ipykernel | Exécuter Python dans les notebooks, notamment dans VS Code |
| NumPy | Tableaux et calcul numérique |
| pandas | Manipulation de données et fichiers CSV |
| SciPy | Calcul scientifique |
| Matplotlib | Graphiques |
| scikit-learn | Algorithmes de machine learning |

TensorFlow et Keras sont cités comme exemples dans le PDF, mais ne sont pas
nécessaires à ce premier setup. Ils pourront être ajoutés si un TP les demande.

## TP ajoutés

- `notebooks/01_cours.ipynb` : régression linéaire sur le CSV du professeur.
- `notebooks/College Admission Labwork.ipynb` : classification des admissions,
  avec données d'entraînement et de test.
- `notebooks/IRIS Decision Tree.ipynb` : arbre de décision et forêt aléatoire sur
  le jeu Iris intégré à scikit-learn.

Les correspondances entre notebooks et CSV sont rappelées dans `data/README.md`.

## Lancer depuis le terminal (PowerShell)

Ouvre PowerShell puis lance :

```powershell
cd "C:\Users\Theo\Documents\GitHub\AI-Course"
uv sync --locked
uv run jupyter lab
```

`uv sync --locked` installe les versions enregistrées dans `uv.lock` si nécessaire.
JupyterLab ouvre ensuite ton navigateur. Ouvre
`notebooks/00_verification.ipynb`, puis exécute toutes les cellules pour vérifier
le fonctionnement de Python, des bibliothèques et des graphiques.

Pour utiliser l'interface Jupyter Notebook présentée dans le cours :

```powershell
uv run jupyter notebook
```

Lance une seule de ces deux interfaces à la fois. Si le navigateur ne s'ouvre
pas automatiquement, utilise l'adresse locale affichée dans le terminal.
Garde le terminal ouvert pendant la session. Pour arrêter le serveur, appuie
sur **Ctrl+C**, puis confirme si demandé.

Pour lancer un fichier Python (remplace le nom par celui de ton fichier) :

```powershell
uv run python mon_script.py
```

Avec `uv run`, tu n'as pas besoin d'activer `.venv` manuellement, ni de modifier
la politique d'exécution PowerShell.

## Lancer depuis VS Code

1. Ouvre VS Code et choisis **Fichier > Ouvrir le dossier**, puis `AI-Course`.
2. Les extensions **Python** (Microsoft) et **Jupyter** (Microsoft) sont nécessaires ;
   elles sont aussi recommandées dans `.vscode/extensions.json`.
3. Avec **Ctrl+Maj+P**, lance **Python: Select Interpreter** et sélectionne
   `.venv\Scripts\python.exe` (Python 3.12). Si nécessaire, utilise
   **Enter interpreter path** pour le choisir. Ce chemin est préconfiguré dans
   les paramètres du dossier.
4. Ouvre `notebooks/00_verification.ipynb`. En haut à droite, clique sur
   **Select Kernel / Sélectionner le noyau**, puis **Python Environments** et
   l'environnement `.venv` de ce projet.
5. Clique sur **Run All / Tout exécuter**. Pour exécuter une cellule seule,
   utilise **Maj+Entrée**.

VS Code peut exécuter les notebooks directement : inutile de lancer un serveur
Jupyter dans le navigateur pour cette utilisation.

Dans le terminal intégré (**Terminal > Nouveau terminal**), les mêmes commandes
`uv run ...` fonctionnent. Vérifie que le terminal est bien dans `AI-Course`.

Si la commande `code` est disponible dans ton terminal, tu peux aussi ouvrir le
projet avec `code .`. Sinon, utilise le menu de VS Code indiqué ci-dessus.

## Ajouter une bibliothèque ou réinstaller

### Notebooks et Git

Le filtre Git **nbstripout** est configuré sur ce PC pour ce dépôt. Il retire
automatiquement les résultats, les compteurs d'exécution et les métadonnées
d'exécution de la version des notebooks enregistrée par Git. Les résultats
restent visibles dans tes fichiers locaux. Le code et les cellules Markdown
restent suivis normalement, y compris avec VS Code ou GitHub Desktop.

Après un nouveau clone (ou si tu déplaces le dossier), active le filtre une fois :

```powershell
uv sync --locked
uv run nbstripout --install --attributes .gitattributes
```

Cette activation est locale à chaque clone : `.gitattributes` est partagé par
Git, mais la configuration du filtre ne l'est pas. Pour vérifier l'activation :

```powershell
uv run nbstripout --status
```

Si des résultats étaient déjà présents dans un ancien commit, leur suppression
apparaîtra une première fois lors du prochain ajout du notebook à un commit.
Ensuite, une simple réexécution ne changera plus le contenu enregistré par Git.
Les notebooks affichés sur GitHub auront donc leur code et leur texte, sans
les résultats ni les graphiques générés.

### Dépendances

Pour ajouter une dépendance, par exemple seaborn :

```powershell
uv add seaborn
```

uv met à jour `pyproject.toml`, `uv.lock` et l'environnement. Redémarre le noyau
du notebook après une modification des bibliothèques.

Sur un autre PC équipé de uv, récupère le dépôt puis lance `uv sync --locked`.
uv utilise Python 3.12 et peut le télécharger s'il manque. Les fichiers
`pyproject.toml`, `uv.lock` et `.python-version` doivent être conservés dans Git ;
`.venv` et les caches sont ignorés.

Si `uv` n'est pas reconnu sous Windows, ouvre un nouveau terminal. Au besoin,
remplace `uv` dans les commandes par `& "$env:USERPROFILE\.local\bin\uv.exe"`.
