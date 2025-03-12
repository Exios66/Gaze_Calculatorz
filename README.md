# Gaze Data Processing Pipeline

A comprehensive data pipeline for processing eye-tracking gaze data, calculating fixations, saccades, and metrics useful for Continuous Wavelet Transform (CWT) analysis.

## Features

- Load and preprocess raw gaze data
- Detect fixations and saccades using velocity-based or DBSCAN clustering methods
- Compute various gaze metrics including:
  - Fixation duration and dispersion
  - Saccade amplitude and velocity
  - Path complexity measures
  - Wavelet coefficients for CWT analysis
- Generate visualizations:
  - Gaze trajectory plots
  - Fixation and saccade maps
  - Velocity profiles
  - CWT scalograms
  - Gaze density heatmaps
- Save processed data for further analysis

## Installation

1. Clone this repository
2. Install the required dependencies:

```bash
pip install -r requirements.txt
```

## Usage

Basic usage:

```python
from gaze_data_processor import GazeDataProcessor

# Initialize the processor with the path to your gaze data file
processor = GazeDataProcessor("path/to/your/gaze_data.csv")

# Run the complete pipeline with default parameters
results = processor.run_pipeline()

# Or customize the pipeline parameters
results = processor.run_pipeline(
    velocity_threshold=100,  # pixels/sec
    min_fixation_duration=0.1,  # seconds
    min_saccade_velocity=300,  # pixels/sec
    use_dbscan=False  # Set to True to use DBSCAN clustering
)
```

## Input Data Format

The input CSV file should contain at minimum the following columns:

- `timestamp`: Time in milliseconds
- `x`: X-coordinate of gaze position
- `y`: Y-coordinate of gaze position

## Output

The pipeline generates several outputs in the `processed_data` directory:

- CSV files with processed data, fixations, and saccades
- Visualization images (PNG format)
- Metrics summary
- Wavelet data for CWT analysis

## Customizing the Pipeline

You can use individual methods of the `GazeDataProcessor` class to customize your analysis:

```python
processor = GazeDataProcessor("path/to/your/gaze_data.csv")

# Load and preprocess data
processor.load_data()

# Choose your fixation detection method
processor.detect_fixations_and_saccades()  # Velocity-based method
# OR
processor.detect_fixations_dbscan()  # DBSCAN clustering method

# Compute metrics
processor.compute_cwt_metrics()

# Generate visualizations
processor.visualize_results()

# Save processed data
processor.save_processed_data()
```

## CWT Analysis

The Continuous Wavelet Transform analysis is particularly useful for:

- Identifying patterns at different time scales
- Analyzing non-stationary signals
- Detecting transient events in gaze data
- Quantifying the time-frequency characteristics of eye movements

The pipeline computes wavelet coefficients, power spectra, and entropy measures that can be used for further CWT analysis.
