# Football PDE Analysis

This repository contains the analysis pipeline for studying behavioural change following Psychological Disruption Events (PDEs) and Positive Flow Events (PFEs). The project covers event detection, behavioural metrics, control windows, individual-level analyses, spatial analysis using StatsBomb 360 data, severity analysis, and predictive modelling.

## Repository contents

The numbered notebooks are intended to be read and run in order:

- `00_download_standard_data.ipynb`: Downloads and stores StatsBomb match data offline.
- `01_detect_pde_events.ipynb`: Detects PDE events and creates raw and filtered catalogues.
- `02_detect_pfe_events.ipynb`: Detects PFE events and creates raw and filtered catalogues.
- `03_calculate_behavioural_metrics.ipynb`: Calculates behavioural metrics before and after events.
- `04_find_cross_match_controls.ipynb`: Finds cross-match control windows and calculates their metrics.
- `05_detect_behavioural_change.ipynb`: Compares behavioural change before and after events and against controls.
- `06_extract_individual_events.ipynb`: Extracts affected players and individual PDE events.
- `07_calculate_individual_metrics.ipynb`: Calculates individual player behavioural metrics within event windows.
- `08_find_individual_controls.ipynb`: Creates and enriches player-level controls for individual events.
- `09_analyse_contagion.ipynb`: Analyses the spread of behavioural change between players.
- `10_analyse_individual_change.ipynb`: Analyses individual performance and behavioural change.
- `11_fit_mixed_effects_model.ipynb`: Fits mixed-effects statistical models for individual changes.
- `12_download_360_data.ipynb`: Downloads StatsBomb 360 match and freeze-frame data.
- `13_calculate_spatial_metrics.ipynb`: Calculates spatial and pitch-control metrics for PDE360 events.
- `14_analyse_spatial_change.ipynb`: Analyses and visualises spatial behavioural change.
- `15_analyse_severity.ipynb`: Analyses the severity and correlations of PDE event types.
- `16_build_predictive_models.ipynb`: Fits and compares predictive models and creates the final figures and report.

See [REPRODUCE.md](REPRODUCE.md) for setup and execution instructions.

## Data source and usage

The analysis uses open football event and 360 data made available by StatsBomb. The download notebooks retrieve the data and store local offline copies in `sb_offline_data/` and `sb_offline_360_data/`.

## Output structure

All generated artefacts are grouped by analysis family and processing stage.

### PDE

- `output/pde/catalogue/`: detected event catalogues and event-level master tables
- `output/pde/controls/`: cross-match control windows and metric-enriched controls
- `output/pde/analysis/`: behavioural, severity, and statistical analysis results

### Individual

- `output/individual/catalogue/`: protagonist catalogues
- `output/individual/controls/`: player-level control windows and enriched controls
- `output/individual/analysis/`: individual, contagion, and mixed-effects results

### PDE360

- `output/pde360/catalogue/`: 360-degree PDE catalogues
- `output/pde360/controls/`: 360-degree control windows and enriched controls
- `output/pde360/analysis/`: spatial metrics and spatial comparison results

### Prediction

- `output/prediction/`: prediction summaries, figures, and hyperparameter tuning results

## Output naming conventions

- `_raw` identifies rows before filtering.
- `_filtered` identifies isolated or full-window event rows.
- `_with_metrics` identifies metric-enriched tables.
- `.csv` files contain tabular results, `.png` files contain figures, and `.md` files contain human-readable summaries.

## Reproducibility notes

- Use the Python environment described in `requirements.txt`.
- The download notebooks require network access and valid access to the permitted StatsBomb data source.
- Several stages are computationally intensive and may require substantial memory and storage.
