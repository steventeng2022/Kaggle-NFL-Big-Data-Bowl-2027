# NFL Big Data Bowl 2027 — Beyond the stopwatch

A reproducible receiver study asking whether sensor-measured speed during the Combine 40-yard dash adds information beyond official measurements when evaluating rookie NFL route movement.

[View the notebook](nfl_big_data_bowl_2027.ipynb) · [Open in Google Colab](https://colab.research.google.com/github/steventeng2022/Kaggle-NFL-Big-Data-Bowl-2027/blob/main/nfl_big_data_bowl_2027.ipynb) · [Competition](https://www.kaggle.com/competitions/nfl-big-data-bowl-2027)

## Run in Kaggle

1. Download this notebook or import it into a Kaggle Notebook.
2. Attach **NFL Big Data Bowl 2027** using **Add Input**.
3. Select CPU and **Run All**. Internet access is unnecessary once the data is attached.

Results are written to `/kaggle/working/receiver_speed`. The final cell creates `/kaggle/working/receiver_speed_results.zip`; download it from the Output panel. In Colab, use the Files panel to download the results bundle.

## Run in Colab or locally

Obtain access to the official competition data on Kaggle and extract its CSV files into one folder. In Colab, upload that folder or mount the Drive folder containing it.

For a local environment, install the dependencies:

```bash
python -m pip install -r requirements.txt
```

Open the notebook and set `DATA_DIR_OVERRIDE` in its configuration cell to the extracted competition folder. Run all cells. Local results are written to `receiver_speed_outputs/`.

The game tracking files are large. CPU is sufficient; allow time for the first scan. A source-validated cache accelerates reruns in the same session.

## Analysis

- Header and drill-label detection, duplicate-frame checks, and explicit coverage diagnostics.
- Three-frame speed smoothing, complete snap-to-release windows, and equal rookie-season exposure.
- Within-player repeatability across Combine attempts and disjoint sets of NFL games.
- Four baseline/model comparisons trained on 2023–2024, with 2025 held out; an earlier 2023→2024 check is reported separately.
- A route-context sensitivity using route type and release duration. Training-player adjustments are fitted on other players; holdout adjustments use training data only.
- Conditional bootstrap intervals plus primary-outcome intervals that refit both models on resampled training players.
- Five PNG/SVG figures, a computed research summary, and a downloadable ZIP with output hashes.
- Explicit skipped-model reports when fixed sample-size requirements are not met.

The notebook keeps primary, sensitivity, and exploratory outcomes distinct. The analysis is observational; route movement is not an overall talent score.

## Validation and results

Notebook structure and Python syntax were checked. All code cells passed 19 behavioral checks on generated fixtures. The checks cover drill-column variants, chunk boundaries, duplicate frames, incomplete route windows, cache consistency, missing events, empty cohorts, repeatability, refitted uncertainty, and training/holdout separation.

To reproduce the checks without competition data:

```bash
python -m pip install -r requirements-dev.txt
python tests/smoke_notebook.py
```

Fixtures and results are created in a temporary directory. To keep the generated diagnostic charts, pass `--artifacts /path/to/test-output`. These generated results are for checking code behavior and are not competition findings.

The saved Kaggle version 4 run used the official competition input and pipeline 3.0.0. Its 56 eligible receivers comprise 20 from 2023, 20 from 2024, and 16 from 2025. On the 2025 holdout, adding tracking reduced MAE from **0.1929 to 0.1921 yd/s** (0.38%). The 95% interval with model refitting was **[-0.0481, 0.0321] yd/s**, so the incremental benefit is inconclusive.

Read the [project write-up](writeup/kaggle_project_description.md) for methods, results, figures, and limitations. The original aggregate tables and figures are in [writeup/official_run](writeup/official_run). All 25 output hashes were verified against the run manifest. Raw competition files were not rerun locally; the source notebook keeps its stored outputs empty.

[Executed Kaggle notebook](https://www.kaggle.com/code/steventeng2022/nfl-big-data-bowl-2027) — this was marked Private when last inspected. A public executed notebook is required for a competition submission.

## Write-up and media

- [Project description](writeup/kaggle_project_description.md)
- [Kaggle form details](writeup/kaggle_basic_details.txt)
- [560 × 280 cover](writeup/kaggle_cover_560x280.png)
- [Media gallery and captions](writeup/media_gallery.md)

The project description embeds five official-run figures and one results table. For Kaggle, upload the figures and replace the relative image paths with Kaggle image links.

## Data and attribution

Competition data is provided by The National Football League through Kaggle. Obtain it from the [official data page](https://www.kaggle.com/competitions/nfl-big-data-bowl-2027/data) and follow its license and competition rules.

This repository contains the analysis code. A competition entry also needs a reviewed write-up and an executed notebook, following the [official submission requirements](https://www.kaggle.com/competitions/nfl-big-data-bowl-2027/overview).
