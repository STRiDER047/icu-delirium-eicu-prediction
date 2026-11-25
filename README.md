# ICU Delirium / Acute Encephalopathy Proxy Modeling from Multi-Center EHR Data

This repository contains the reproducible analysis notebook and derived feature dataset supporting our study on machine learning modeling of ICU delirium/acute encephalopathy using routinely collected first-24-hour multi-center electronic health record (EHR) data.

## Repository Contents
* **`eICU_Delirium_Revision_Colab_FullCode.ipynb`**: Complete, pre-executed Google Colab notebook (`N_REPEATS = 3` × 5-fold patient-grouped `StratifiedGroupKFold`) comparing Logistic Regression (`LR`), Random Forest (`RF`), XGBoost (`XGB`), and a PyTorch Multi-Layer Perceptron (`MLP`). The notebook reproduces:
  1. **Label & Timing Verification:** Reconstruction of the 220 positive stays, diagnosis component breakdown, first-diagnosis timing (`diagnosisoffset`), and cohort/hospital counts (2,155 stays, 1,709 patients, 186 hospitals).
  2. **Ablation, Resampling & Imputation Analyses:** Feature-set ablation (`demographics`, `values_only`, `indicators_only`, `both`, `ind_no_demo`), class-imbalance comparison (`none`, `weights`, `SMOTE`, `undersampling`), imputation sensitivity (`train_median`, `test_median`, `random_draw`), MLP protocol fairness check (`es15` vs. `fixed` epochs), and record-level vs. patient-grouped splitting.
  3. **Statistical & Metric Checks:** Paired Nadeau–Bengio tests, per-fold class counts (0 patient overlap), and verification that hard-label AUROC equals balanced accuracy.
  4. **Clinical & Generalizability Evaluation:** Pooled out-of-fold patient-cluster bootstrap 95% CIs, probability calibration (slope, intercept, Brier score), alert-rate operating points (5%, 10%, 20%, 30%), hospital-grouped validation (`GroupKFold`), 24-hour landmark analysis (`n = 1,369`, 22 post-24h positives), and pre-imputation feature summaries.
* **`corrected_unitstay_level_features_eicu_v2.csv`**: Derived unit-stay-level feature table (2,155 ICU stays, 57 columns) extracted from the first 24 hours of ICU admission.

## Primary Data Source (PhysioNet)
The raw data supporting this study are openly available on PhysioNet (**eICU Collaborative Research Database Demo, version 2.0.1**) without credentialing requirements:
* **PhysioNet URL:** https://physionet.org/content/eicu-crd-demo/2.0.1/

To respect PhysioNet's distribution guidelines and maintain a single authoritative source, raw eICU tables are not redistributed in this repository. Please download the raw demo archive directly from PhysioNet to run the full notebook.

## How to Run
1. Open `eICU_Delirium_Revision_Colab_FullCode.ipynb` in **Google Colab** (or Jupyter Notebook).
2. Run the package installation cell, then upload `corrected_unitstay_level_features_eicu_v2.csv` and the zipped eICU-CRD Demo v2.0.1 archive from PhysioNet when prompted.
3. Execute the remaining cells sequentially (`N_REPEATS = 3` matches the paper; set `N_REPEATS = 1` for a quick test run). All generated CSV tables are saved to `/content/outputs` and packaged as `outputs.zip`.

## Authors
Hani Alnami, Faris Ghazwani, Eyad Makhasha, Abdulrahman Mahzari, and Meshal Zaylie  
*Department of Computer Science, College of Engineering and Computer Science, Jazan University, Saudi Arabia.*
