# Notebooks — Breast Cancer ML Experiments

This folder contains Jupyter notebooks that demonstrate data exploration, preprocessing, model development, evaluation, and lightweight demonstration workflows for breast-cancer classification experiments. The notebooks are intended to be clear, reproducible, and serve as a baseline for further development.

## Contents
- `_Breast_Cancer_Classification.ipynb` — End-to-end experiment: dataset inspection, preprocessing pipelines, model comparison, hyperparameter search, evaluation metrics and visualizations.
- `Breast_Cancer_Detection.ipynb` — Compact/focused notebook that illustrates exploratory analysis and one or two modeling approaches.
- `README.md` — This document.

## Goals
- Provide readable, runnable examples for breast-cancer classification.
- Demonstrate good practices: pipelines, reproducibility, clear evaluation.
- Provide a foundation for iterative improvement and productionization.

## Requirements
Recommended
- Python 3.8+
- The notebooks rely on standard data-science packages. Example minimal dependencies:
  - numpy
  - pandas
  - scikit-learn
  - matplotlib
  - seaborn
  - joblib
  - imbalanced-learn (optional)
  - jupyterlab / notebook

Pin versions for reproducibility. Preferably add a `requirements.txt` or `environment.yml` at the repository root. Example:
```
pip install -r ../requirements.txt
```

## Quick start — interactive
1. Create and activate your environment (example using pip):
   ```
   python -m venv .venv
   source .venv/bin/activate   # macOS / Linux
   .\.venv\Scripts\activate    # Windows
   pip install -r ../requirements.txt
   ```
2. Launch Jupyter:
   ```
   jupyter lab
   ```
   or
   ```
   jupyter notebook
   ```
3. Open the desired notebook in the `notebooks/` folder and run cells top-to-bottom. Start by running the top “environment / reproducibility” cell that prints versions and sets the random seed.

## Headless execution (CI / reproducible runs)
To execute notebooks non-interactively (useful for CI or regenerating outputs):
```
pip install -r ../requirements.txt
jupyter nbconvert --to notebook --execute notebooks/_Breast_Cancer_Classification.ipynb --ExecutePreprocessor.timeout=600 --output notebooks/_Breast_Cancer_Classification.executed.ipynb
```
To parameterize runs:
```
pip install papermill
papermill notebooks/_Breast_Cancer_Classification.ipynb notebooks/run.ipynb -p RANDOM_SEED 42
```

## Reproducibility checklist (recommended)
- Include a top cell that sets a deterministic seed and prints versions:
  - os.environ['PYTHONHASHSEED'], random.seed(), numpy.random.seed(), and consistent `random_state` in scikit-learn calls.
- Keep all imports in a single cell near the top.
- Use scikit-learn Pipelines and ColumnTransformer for preprocessing and modeling.
- Use stratified splits for classification:
  ```
  train_test_split(X, y, stratify=y, random_state=SEED)
  ```
- Save trained artifacts (models, preprocessing objects) with joblib in a `models/` directory.
- Label long-running cells (e.g., “(long)”) and optionally provide precomputed artifacts to load.

## Outputs & artifacts
- Place trained models and large generated artifacts in `models/`. If artifacts are too large for the repository, add them to an external storage service and include a download script.
- Add `models/` to `.gitignore` if you do not want to commit binary artifacts.

## Recommended project structure
- data/                — raw and processed data (or download script)
- notebooks/           — this folder (interactive notebooks)
- src/                 — reusable helper modules (plotting, metrics, data loaders)
- models/              — saved model artifacts (add to .gitignore if large)
- requirements.txt     — pinned pip deps
- environment.yml      — optional conda environment
- Dockerfile / binder/ — optional reproducible execution

## Suggested improvements (priority)
1. Add `requirements.txt` / `environment.yml` with pinned versions.
2. Move repeated helper code into `src/` and import from notebooks.
3. Convert preprocessing + model steps into scikit-learn Pipelines.
4. Add a small CI workflow to run notebooks (or nbconvert) on push/PR.
5. Provide a short tutorial cell at the top of each notebook: purpose, expected runtime, and how to skip long cells.

## If you want, I can
- Update this README in a branch and open a PR.
- Create `requirements.txt` or `environment.yml` from a working environment.
- Refactor `_Breast_Cancer_Classification.ipynb` to use pipelines, seeds, and externalized helper code in `src/`.
- Add a simple GitHub Actions workflow to run notebooks with `nbconvert`.

Please tell me which of the above actions you want me to do next (update README only, add requirements, refactor notebooks, or create CI).  
