# Early Detection of Maternal Supraphysiological Hypercholesterolemia

This repository contains the computational workflows supporting the study:

> **Early Detection of Maternal Supraphysiological Hypercholesterolemia: Development and Internal Validation of a Machine Learning Model and Characterization of First-Trimester Atherogenic Biomarkers**

The project evaluates whether routinely collected first-trimester clinical and biochemical variables contain sufficient information to discriminate women who subsequently develop maternal supraphysiological hypercholesterolemia (MSPH) at term.

The repository includes the configuration files, analysis notebooks, machine-learning workflows, model-evaluation procedures, interpretability analyses, figures, and aggregate computational outputs used in the study.

---

## Study overview

The computational workflow comprises:

- harmonization and preparation of the analytical cohort;
- exploratory characterization of first-trimester clinical and biochemical variables;
- evaluation of alternative preprocessing strategies;
- benchmarking of multiple classical machine-learning classifiers;
- repeated internal validation across alternative partitioning strategies;
- stability-oriented model selection;
- evaluation of the final Linear Discriminant Analysis model;
- model interpretation using SHAP and permutation-based feature importance;
- generation of the figures and aggregate results reported in the manuscript.

The prediction task uses **11 first-trimester predictors**:

- maternal age;
- weight;
- height;
- body mass index;
- fasting glycemia;
- systolic blood pressure;
- diastolic blood pressure;
- total cholesterol;
- triglycerides;
- HDL cholesterol;
- LDL cholesterol.

MSPH was defined using **third-trimester total cholesterol > 290 mg/dL**. Third-trimester lipid measurements were used exclusively to define the outcome and were not included among the model predictors.

---

## Final model

The final manuscript-level model is based on **Linear Discriminant Analysis (LDA)** using the predefined first-trimester predictors.

In the internal evaluation reported in the manuscript, the final model achieved:

| Metric | Performance |
|---|---:|
| ROC-AUC | 0.77 |
| PR-AUC | 0.52 |
| Accuracy | 0.75 |
| Sensitivity | 0.62 |
| Specificity | 0.79 |
| MCC | 0.40 |

Threshold-dependent metrics were calculated using a fixed operating threshold of **0.60**.

Model outputs should be interpreted as **discrimination scores rather than calibrated estimates of absolute MSPH risk**. The model has undergone internal validation only and requires external validation before clinical use.

---

## Repository structure

The public repository preserves the computational structure used during the project while excluding restricted participant-level data and local development files.

```text
.
├── configs/
├── notebooks/
├── results/
├── .gitignore
├── environment.yaml
├── LICENSE
└── README.md
```

### `configs/`

Configuration files defining the analytical and machine-learning workflows, including dataset representations, preprocessing strategies, model configurations, validation schemes, and related computational settings.

### `notebooks/`

Jupyter notebooks used for data preparation, exploratory analysis, model development and evaluation, sensitivity analyses, interpretability analyses, and manuscript figure generation.

### `results/`

Aggregate computational outputs generated during the project, including figures, exploratory summaries, model-evaluation outputs, and result tables used to document the analyses reported in the manuscript.

---

## Getting started

### 1. Clone the repository

```bash
git clone https://github.com/kren-ai-lab/MSPH_classification_models.git
cd MSPH_classification_models
```

### 2. Create the Conda environment

The repository provides an `environment.yaml` file containing the computational dependencies required by the analysis notebooks and model-development workflows.

```bash
conda env create -f environment.yaml
```

Activate the environment with:

```bash
conda activate msph-ml
```

### 3. Launch the notebooks

```bash
jupyter lab
```

If the environment needs to be registered explicitly as a Jupyter kernel, run:

```bash
python -m ipykernel install --user --name msph-ml --display-name "Python (MSPH-ML)"
```

---

## Computational environment

The analyses were developed using **Python 3.12**.

The principal package versions used for the analyses reported in the manuscript are:

- NumPy 1.26.4
- pandas 2.2.2
- SciPy 1.13.1
- scikit-learn 1.5.1
- imbalanced-learn 0.12.3
- SHAP 0.46
- Matplotlib 3.9.1
- Seaborn 0.13.2

The environment also includes the supporting packages required by the repository workflows, including `openpyxl` for Excel input, `pyarrow` for Parquet files, `joblib` for serialized model objects, and the Jupyter environment required to execute the notebooks.

The complete environment definition is provided in [`environment.yaml`](environment.yaml).

---

## Data availability

**Individual-level participant data are not included in this public repository.**

The clinical datasets used to construct the analytical cohorts are excluded because of ethical and privacy restrictions associated with the original studies. This includes raw data, processed participant-level datasets, and other files containing individual clinical observations.

The complete preprocessing and model-development workflows therefore require authorized access to the study data. Authorized users can restore the private `data/` directory locally using the original project structure. The directory is intentionally excluded from the public repository and should remain outside version control.

Researchers interested in accessing de-identified study data should contact the corresponding authors. Data requests will be considered subject to the conditions of the original informed consent, institutional ethics approval, and applicable data-sharing requirements.

### Data requests

**Dr. Andrea Leiva**  
Facultad de Ciencias para el Cuidado de la Salud  
Universidad San Sebastián  
Santiago, Chile  
E-mail: [andrea.leiva@uss.cl](mailto:andrea.leiva@uss.cl)

**Dr. Sebastián E. Illanes**  
Faculty of Medicine  
Universidad de los Andes  
Santiago, Chile  
E-mail: [sillanes@uandes.cl](mailto:sillanes@uandes.cl)

---

## Reproducibility

Randomized model-development procedures were executed using predefined random seeds and configuration-controlled workflows.

The repository documents the analysis definitions used for:

- dataset variants;
- preprocessing strategies;
- classifier configurations;
- validation schemes;
- model-selection criteria;
- final-model evaluation;
- model interpretability.

Because participant-level data are restricted, complete rerunning of analyses that require individual observations requires authorized access to the original datasets. Aggregate outputs, analysis workflows, configurations, and manuscript figure-generation resources are provided to support transparency and reproducibility of the reported computational analyses.

---

## Code and computational questions

For questions related to the repository, computational workflow, machine-learning analyses, or code, please contact:

**Dr. David Medina-Ortiz**  
Department of Computer Engineering  
Universidad de Magallanes  
Punta Arenas, Chile  
E-mail: [david.medina@umag.cl](mailto:david.medina@umag.cl)

---

## Citation

If you use this repository or its computational workflows, please cite the associated manuscript:

> **XXX**

Final bibliographic information will be added following publication.

---

## License

The source code and computational materials in this repository are distributed under the **MIT License**.

See [`LICENSE`](LICENSE) for details.

---

## Disclaimer

This repository accompanies a research study focused on the development and internal validation of a prediction model for MSPH.

The model is intended for **research use only**. It has not been externally validated and should not be used as a standalone diagnostic tool or to guide clinical decisions without additional validation.
