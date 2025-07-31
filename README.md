# Submission TSMixer ZKI-PH4
Authors:
Affiliation: Robert Koch Institute, Berlin, Germany
Corresponding author:

## Abstract
We built a model based on the Time Series Mixer (**TSMixer**), as proposed by Chen et al. (2023). After identifying the most important features for state-level predictions using TSMixer, we selected: `pdo`, `precip_min`, `pressure_min`, and `temp_min`. Since these features were unavailable during the forecast period, we used the multivariate foundation model **TiRex** (Auer et al., 2025) to forecast them over the relevant time window. These forecasts were then used as additional inputs to TSMixer for the final prediction task.

To install and work with TSMixer, simply pip install neuralforecast. For installing TiRex, please refer to the following Github repo:
https://github.com/NX-AI/tirex

## Contents
This README covers the following components of the project:

- Data processing
- Feature forecasting
- Model predictions

## Data Processing
All data was initially merged at the municipality level. The population for 2025 was estimated by taking the 2024 population and adding the difference between 2024 and 2023. After excluding the state of ES, data was aggregated to the state level. During aggregation:

- Population size and dengue cases were summed.

- Climate variables were aggregated using a weighted average based on the physical area of each municipality within the state.

- Weekly time-based features (`sin`, `cos`) were added.

Next, the data was split into training sets 1–3 and validation sets 1–3. All columns were normalized using min-max scaling, where each validation set was scaled using the distribution of its corresponding training set.

## Feature Forecasting
After state-level aggregation, each state had a time series for each feature in the training sets. These were used to forecast the remainder of the time series to span the validation sets using the TiRex model.

## Model Predictions
This section is currently a placeholder. Details to be added.

## Citations
Chen, Si-An, Chun-Liang Li, Nate Yoder, Sercan O. Arik, and Tomas Pfister (2023). TSMixer: An All-MLP Architecture for Time Series Forecasting. arXiv:2303.06053

Auer, Andreas, Patrick Podest, Daniel Klotz, Sebastian Böck, Günter Klambauer, and Sepp Hochreiter (2025). TiRex: Zero-Shot Forecasting Across Long and Short Horizons with Enhanced In-Context Learning. arXiv:2505.23719