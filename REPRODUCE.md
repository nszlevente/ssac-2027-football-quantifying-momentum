# Reproduction guide

This guide describes how to recreate the analysis outputs from a clean local environment.

## 1. Requirements

- Python 3.13 or a compatible Python version supported by the listed packages
- A Jupyter Notebook or JupyterLab installation
- Network access for the data-download notebooks
- Sufficient disk space for the local StatsBomb data cache and generated outputs

Install the Python dependencies described in `requirements.txt`:

## 2. Data source and acquisition

The event data come from the [StatsBomb Open Data repository](https://github.com/statsbomb/open-data).

Run `00_download_standard_data.ipynb` to download and cache standard event data.

The notebooks store local files in:

- `sb_offline_data/`

## 3. Pipeline order

Run the notebooks from the repository root. The `MODE` cells in notebooks `03` and `04` select either `PDE` or `PFE`; run those notebooks once for each event family when both sets of results are required.

### Common preparation

1. `00_download_standard_data.ipynb`

### PDE branch

Run this branch first if individual-level analyses are required:

1. `01_detect_pde_events.ipynb`
2. `03_calculate_behavioural_metrics.ipynb` with `MODE = 'PDE'`
3. `04_find_cross_match_controls.ipynb` with `MODE = 'PDE'`
4. `05_detect_behavioural_change.ipynb` with `MODE = 'PDE'`

The PDE branch must finish through notebook `05` before starting the individual branch. Notebook `12_analyse_severity.ipynb` depends on the PDE metric and control outputs, so it should be run after notebook `04` and before or after the individual branch.

### PFE branch

Run this branch independently after the common preparation:

1. `02_detect_pfe_events.ipynb`
2. `03_calculate_behavioural_metrics.ipynb` with `MODE = 'PFE'`
3. `04_find_cross_match_controls.ipynb` with `MODE = 'PFE'`
4. `05_detect_behavioural_change.ipynb` with `MODE = 'PFE'`

### Individual branch

Run only after the PDE branch has produced the standard PDE catalogues and metric-enriched outputs:

1. `06_extract_individual_events.ipynb`
2. `07_calculate_individual_metrics.ipynb`
3. `08_find_individual_controls.ipynb`
4. `09_analyse_contagion.ipynb`
5. `10_analyse_individual_change.ipynb`
6. `11_fit_mixed_effects_model.ipynb`

## 4. Expected outputs

The pipeline writes derived tables and figures under `output/`:

- `output/pde/catalogue/`: raw, filtered, and metric-enriched PDE event tables
- `output/pde/controls/`: PDE cross-match controls and metric-enriched controls
- `output/pde/analysis/`: PDE behavioural-change figures and severity results
- `output/pfe/catalogue/`: raw, filtered, and metric-enriched PFE event tables
- `output/pfe/controls/`: PFE cross-match controls and metric-enriched controls
- `output/pfe/analysis/`: PFE behavioural-change figures
- `output/individual/catalogue/`: raw and final individual protagonist catalogues
- `output/individual/controls/`: individual control catalogues before and after metric enrichment
- `output/individual/analysis/`: contagion, coverage, individual-change, and mixed-effects results

The output tables use the following conventions:

- `_raw`: rows before filtering
- `_filtered`: isolated or full-window event rows
- `_with_metrics`: metric-enriched tables
