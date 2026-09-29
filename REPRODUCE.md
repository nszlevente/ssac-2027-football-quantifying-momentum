# Reproduction guide

This guide describes how to recreate the analysis outputs from a clean local environment.

## 1. Requirements

- Python 3.13 or a compatible Python version supported by the listed packages
- A Jupyter Notebook or JupyterLab installation
- Network access for the data-download notebooks
- Sufficient disk space for the local StatsBomb data cache and generated outputs

Install the Python dependencies described in `requirements.txt`:

## 2. Data acquisition

Run `00_download_standard_data.ipynb` to download and cache standard event data. Run `12_download_360_data.ipynb` to download and cache StatsBomb 360 data.

The notebooks store local files in:

- `sb_offline_data/`
- `sb_offline_360_data/`

## 3. Pipeline order

Run the notebooks in this order:

1. `00_download_standard_data.ipynb`
2. `01_detect_pde_events.ipynb`
3. `02_detect_pfe_events.ipynb`
4. `03_calculate_behavioural_metrics.ipynb`
5. `04_find_cross_match_controls.ipynb`
6. `05_detect_behavioural_change.ipynb`
7. `06_extract_individual_events.ipynb`
8. `07_calculate_individual_metrics.ipynb`
9. `08_find_individual_controls.ipynb`
10. `09_analyse_contagion.ipynb`
11. `10_analyse_individual_change.ipynb`
12. `11_fit_mixed_effects_model.ipynb`
13. `12_download_360_data.ipynb`
14. `13_calculate_spatial_metrics.ipynb`
15. `14_analyse_spatial_change.ipynb`
16. `15_analyse_severity.ipynb`
17. `16_build_predictive_models.ipynb`

## 4. Expected outputs

The pipeline writes derived tables and figures under `output/`:

- `output/pde/`: PDE catalogues, controls, and analysis results
- `output/pfe/`: PFE catalogues and controls
- `output/individual/`: protagonist, player-control, contagion, and mixed-effects results
- `output/pde360/`: 360-degree catalogues, controls, and spatial analysis results
- `output/prediction/`: predictive-model summaries, figures, and tuning results

The output tables use the following conventions:

- `_raw`: rows before filtering
- `_filtered`: isolated or full-window event rows
- `_with_metrics`: metric-enriched tables
