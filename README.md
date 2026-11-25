# Global Disaster Impact Analysis Using EM-DAT

The [v5 analysis notebook](EMDAT_Disaster_Impact_Analysis_v5.ipynb) examines 16,697 event-country records from the Emergency Events Database (EM-DAT), covering 14,877 distinct disasters with start years from 2000 through 2025.

## What the notebook does

| Task | Outcome |
| --- | --- |
| Disaster type (A) | Classifies 21 eligible disaster types using geographic and seasonal predictors. |
| Relative severity (S2 and S3) | Classifies severity using deaths and people affected for S2, with inflation-adjusted damage added for S3. |
| Impact regression (C) | Estimates reported deaths, people affected and inflation-adjusted damage in three separate models. |

The primary evaluation uses development data through 2017 and a holdout beginning in 2018. Training and evaluation sets are disjoint at the disaster-event level. The notebook also compares event-grouped random splits and tests transfer to held-out countries. The resulting scores describe retrospective performance on reported outcomes.

## Data access

To reproduce this run, request the **13 March 2026 custom EM-DAT snapshot exported on 15 March 2026** from CRED/UCLouvain. Registration provides access to EM-DAT Public Data, which is updated regularly. A newer export can produce different cohorts and results. [EM-DAT Public Data](https://public.emdat.be/) · [Contact CRED](https://doc.emdat.be/docs/about/contact/) · [Data-sharing terms](https://doc.emdat.be/docs/additional-resources-and-tutorials/faq/)

Save the workbook as `dataset.xlsx` beside the notebook. The notebook reads the `EM-DAT Data` sheet. To use a workbook stored elsewhere, set `EMDAT_DATASET` to its path before running the notebook.

The SHA-256 checksum for the workbook used in the study is shown below.

```text
d1e873e53071fffe9264f81a40b2673b0785c6b032601ca177426d27808ce1d6
```

## Reproduce the analysis

The verified run used **Python 3.14.3** on Windows. From your local copy of the repository, save the dependency list below as `requirements.txt` and run these commands in PowerShell.

```powershell
py -3.14 -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

<details>
<summary>Pinned dependencies</summary>

```text
numpy==2.4.2
pandas==3.0.3
scipy==1.17.1
scikit-learn==1.8.0
xgboost==3.2.0
lightgbm==4.6.0
catboost==1.2.10
matplotlib==3.10.8
matplotlib-inline==0.2.1
seaborn==0.13.2
joblib==1.5.3
openpyxl==3.1.5
et-xmlfile==2.0.0
shap==0.51.0
numba==0.65.1
llvmlite==0.47.0
slicer==0.0.8
cloudpickle==3.1.2
threadpoolctl==3.6.0
pillow==12.1.1
ipython==9.10.0
ipykernel==7.2.0
nbformat==5.11.1
nbclient==0.11.0
jupyter-client==8.8.0
```

</details>

Open `EMDAT_Disaster_Impact_Analysis_v5.ipynb` in Jupyter or VS Code, select the `.venv` Python kernel, and run all cells in order.

The default `full` profile reproduces the study configuration. For a shorter test run, set `EMDAT_PROFILE` to `quick` before starting the notebook kernel. It uses fewer tuning trials and bootstrap resamples and can produce different results. Set `EMDAT_OUTPUT_DIR` to change where the notebook writes its results.

## Outputs

The full run writes tables, figures, model files, predictions, split manifests and configuration records to `outputs_v5_full/` by default. Some of these local outputs contain row-level EM-DAT information and are subject to the provider’s sharing terms.

## Cite the data

UCLouvain / CRED. *Emergency Events Database (EM-DAT) Public Data*. Brussels, Belgium. Custom snapshot dated 13 March 2026 and exported 15 March 2026. [EM-DAT Public Data](https://public.emdat.be/)

Delforge, D., et al. (2025). EM-DAT: the Emergency Events Database. *International Journal of Disaster Risk Reduction*, 124, 105509. [DOI](https://doi.org/10.1016/j.ijdrr.2025.105509)
