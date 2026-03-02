# Metro Arrival Time Prediction

Perceptron-based metro schedule predictor with a command-line pipeline, SQLite export, evaluation metrics, and a Streamlit dashboard.

## What This Project Is

This project predicts station-by-station metro arrival times using a single-layer perceptron-style linear regressor.

It trains on route segment data and estimates:
- Segment travel time between stations
- Full trip arrival and departure times from a user-provided starting departure time

## What It Can Do

- Load metro route data from CSV into typed Python objects.
- Convert the CSV dataset into a SQLite database table.
- Build features from:
  - Distance from previous station
  - Average speed
  - Previous station dwell time
  - Derived runtime estimate
- Train a perceptron-style regression model with:
  - Feature scaling
  - Gradient descent
  - Optional L2 regularization
  - Early stopping by loss tolerance
- Evaluate model quality with `MAE`, `RMSE`, and `R2`.
- Generate a full predicted schedule (arrival + departure times) across all stations.
- Run an interactive Streamlit app with configurable training parameters.
- Validate behavior with unit and pipeline tests.

## Tech Stack

- Python 3.9+
- Streamlit
- SQLite (`sqlite3` from Python standard library)
- `unittest` for tests

## Repository Structure

```text
data/
  metro_line.csv
docs/
  architecture.md
  member_work_guide.md
scripts/
  run_demo.py
src/metro_perceptron/
  __init__.py
  data.py
  evaluation.py
  features.py
  model.py
  scheduler.py
tests/
  conftest.py
  test_features.py
  test_model.py
  test_pipeline.py
ui/
  streamlit_app.py
```

## Dataset Fields

`data/metro_line.csv` contains:
- `line_name`
- `station_order`
- `station_name`
- `distance_from_prev_km`
- `avg_speed_kmph`
- `dwell_time_min`
- `observed_segment_time_min`

## Setup

```bash
python -m venv .venv
```

Windows PowerShell:

```bash
.venv\Scripts\Activate.ps1
```

macOS/Linux:

```bash
source .venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

## Run Locally

### 1. Run the CLI Demo Pipeline

```bash
python scripts/run_demo.py --departure 08:30
```

What this does:
- Loads data from `data/metro_line.csv`
- Writes `data/metro_line.db`
- Trains the model
- Prints validation metrics
- Prints full predicted station schedule

### 2. Run the Streamlit App

```bash
python -m streamlit run ui/streamlit_app.py
```

Then open:

```text
http://localhost:8501
```

In the UI, you can:
- Change learning rate
- Change epochs
- Set starting departure time
- View model metrics and predicted station schedule

### 3. Run Tests

```bash
python -m unittest discover -s tests -p "test_*.py" -v
```

## Deploy to Streamlit Community Cloud

Streamlit Community Cloud deploys from GitHub, not from a local folder.

Steps:
1. Push code to a GitHub repository (public for free Community Cloud usage).
2. In Streamlit Community Cloud, click `New app`.
3. Select:
   - Repository: `lingadevaru-hp/metro-arrival-time-prediction`
   - Branch: `main`
   - Main file path: `ui/streamlit_app.py`
4. Click `Deploy`.

Streamlit automatically installs packages from `requirements.txt`.

## Team Coverage

This repository includes deliverables for:
- ML model logic
- Architecture design
- Dataset/database handling
- Implementation
- UI/documentation
- Testing/validation
