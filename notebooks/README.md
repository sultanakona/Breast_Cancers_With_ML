# Notebooks — Breast_Cancers_With_ML

This directory contains Jupyter notebooks that walk through data exploration, preprocessing, model training, evaluation, and simple deployment steps for breast cancer detection/classification experiments.

## Contents
- `_Breast_Cancer_Classification.ipynb` — End-to-end notebook that explores the dataset, builds preprocessing pipelines, compares classifiers, performs hyperparameter tuning, and reports evaluation metrics and plots.
- `Breast_Cancer_Detection.ipynb` — Focused notebook for a single modeling approach or a shorter experiment (visualization + single model training/evaluation).
- `README.md` — This file.

## Purpose
These notebooks are intended to:
- Demonstrate preprocessing and modeling choices for breast cancer classification.
- Provide reproducible experiments and easy-to-follow evaluation.
- Serve as a base for further model improvements and productionization.

## Requirements and Environment
Recommended:
- Python 3.8+
- Install dependencies:
  ```
  pip install -r ../requirements.txt
  ```
  or if you prefer conda:
  ```
  conda env create -f ../environment.yml
  conda activate <env-name>
  ```

Minimal required packages:
- numpy
- pandas
- scikit-learn
- matplotlib
- seaborn
- joblib
- imbalanced-learn (optional if resampling is used)
- jupyterlab / notebook

(If `requirements.txt` or `environment.yml` are missing from the repo root, generate them with `pip freeze > requirements.txt` from a working environment.)

## How to run the notebooks
Open in Jupyter:
1. Install dependencies (see above).
2. From the repository root:
   ```
   jupyter lab
   ```
   or
   ```
   jupyter notebook
   ```
3. Open the notebook files from the `notebooks/` folder and run cells top-to-bottom.

Run headlessly (for CI or reproducible runs):
```
pip install -r ../requirements.txt
jupyter nbconvert --to notebook --execute notebooks/_Breast_Cancer_Classification.ipynb --ExecutePreprocessor.timeout=600 --output notebooks/_Breast_Cancer_Classification.executed.ipynb
```
Or use papermill to parameterize and execute:
```
papermill notebooks/_Breast_Cancer_Classification.ipynb notebooks/_Breast_Cancer_Classification.runned.ipynb -p some_param value
```

## Reproducibility notes
- Each notebook contains (or should contain) a reproducibility cell that sets a global random seed and prints package versions. Ensure you do not rely on unpinned package versions for reproducible results.
- All long-running or computationally expensive cells are optional; to reproduce quickly, look for cells labeled as `(long)` and skip them, or load saved model artifacts if provided in `models/`.

## Recommended project organization (suggested)
- data/                — raw and processed data (keep raw data out of VCS if large; provide data download script)
- notebooks/           — this folder
- models/              — trained model artifacts (add to .gitignore if large)
- src/                 — reusable helper functions and modules
- requirements.txt     — pinned pip dependencies
- environment.yml      — pinned conda environment (optional)
- Dockerfile or binder/ — for fully reproducible runtime (optional)

## Tips to improve these notebooks (quick checklist)
- Add a top-level description and short TL;DR.
- Keep imports in a single cell at the top.
- Use sklearn Pipelines & ColumnTransformer.
- Use stratified splits and set `random_state`.
- Save small helper functions to `src/` and import them (keeps notebooks readable).
- Visualize class imbalance and show ROC/PR curves for best models.
- Save final model with joblib and provide instructions to load it.

## Contact / Next steps
If you'd like, I can:
- Apply the recommended notebook refactor (create a branch + PR with the improved notebook).
- Add a `requirements.txt`, `models/` folder, and a small `src/` module for helper functions.
- Add Binder / GitHub Actions to execute notebooks automatically.
This folder contains Jupyter notebooks.
