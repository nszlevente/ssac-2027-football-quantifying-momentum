# Football PDE Analysis

This repository contains the analysis pipeline for studying behavioural change following Psychological Disruption Events (PDEs) and Positive Flow Events (PFEs). The project covers event detection, behavioural metrics, control windows, individual-level analyses andseverity analysis.

## Repository contents

The notebooks are organised into a standard event-level pipeline and a PDE-based individual-level pipeline. See [REPRODUCE.md](REPRODUCE.md) for the dependency-aware execution order.

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
- `12_analyse_severity.ipynb`: Analyses the severity and correlations of PDE event types.

## Data source and usage

The analysis uses open football event data made available by StatsBomb. The data are available from the [StatsBomb Open Data repository](https://github.com/statsbomb/open-data). The download notebook retrieves the data and stores a local offline copy in `sb_offline_data/`.

Please follow the StatsBomb Open Data terms and attribution requirements when reusing the data.

## Output structure

All generated artefacts are grouped by analysis family and processing stage.

### PDE event-level outputs

- `output/pde/catalogue/events_raw.csv`: all detected PDE candidates before isolation and full-window filtering
- `output/pde/catalogue/events_filtered.csv`: isolated PDEs with complete pre/post analysis windows
- `output/pde/catalogue/events_with_metrics.csv`: PDE events enriched with pre-event, post-event, and change metrics
- `output/pde/controls/controls.csv`: cross-match control windows matched to PDE events
- `output/pde/controls/controls_with_metrics.csv`: control windows enriched with the same behavioural metrics
- `output/pde/analysis/`: PDE behavioural-change heatmaps and severity-correlation results

### PFE event-level outputs

- `output/pfe/catalogue/events_raw.csv`: all detected PFE candidates before filtering
- `output/pfe/catalogue/events_filtered.csv`: isolated PFEs with complete analysis windows
- `output/pfe/catalogue/events_with_metrics.csv`: PFE events enriched with behavioural metrics
- `output/pfe/controls/controls.csv`: cross-match control windows matched to PFE events
- `output/pfe/controls/controls_with_metrics.csv`: metric-enriched PFE control windows
- `output/pfe/analysis/`: PFE behavioural-change figures

### Individual-level outputs

This branch must be run after the standard PDE event-level branch has produced the required PDE catalogues and metrics.

- `output/individual/catalogue/protagonists_raw.csv`: player/event records before final protagonist filtering
- `output/individual/catalogue/protagonists_master.csv`: final individual PDE event catalogue
- `output/individual/controls/controls_catalogue.csv`: player-level control windows
- `output/individual/controls/control_catalogue_with_metrics.csv`: metric-enriched player-level controls
- `output/individual/analysis/`: individual change, contagion, coverage, and mixed-effects model tables and figures

## Output naming conventions

- `_raw` identifies rows before filtering.
- `_filtered` identifies isolated or full-window event rows.
- `_with_metrics` identifies metric-enriched tables.
- `.csv` files contain tabular results, `.png` files contain figures, and `.md` files contain human-readable summaries.

## Reproducibility notes

- Use the Python environment described in `requirements.txt`.
- The download notebook requires network access and uses the permitted StatsBomb open-data source.
- Several stages are computationally intensive and may require substantial memory and storage.
