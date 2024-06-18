# EPL Match Prediction Program "FootForecast"

## Overview

This program predicts the outcomes of English Premier League (EPL) matches using historical data and various statistical features. It processes raw match data, performs feature engineering, and calculates necessary metrics for prediction models.

## Features

- **Data Cleaning and Transformation**: Preprocesses match data to add target labels and relevant features.
- **Feature Engineering**: Computes various statistics such as goal differences, team effectiveness, average points, and head-to-head stats.
- **Team Statistics**: Analyzes team performance over seasons to determine status and trends.
- **Match Prediction**: Uses historical data to predict match outcomes.

## Setup

### Prerequisites

- Python 3.x
- pandas
- numpy
- os

### Installation

1. Clone the repository:
   ```bash
   git clone <repository_url>
   cd <repository_directory>
   ```
2. Install required packages:
   ```bash
   pip install pandas numpy
   ```

## Usage

### Configuration

Edit the configuration variables at the beginning of the script:

- **League Configuration**:
  ```python
  league_name, code = "Premier_league", "E0"
  FIRST_SEASON_YEAR, LAST_SEASON_YEAR = 5, 23
  N = 5  # Last number of seasons to calculate new features
  ```

- **Important Columns**:
  ```python
  selected_columns = [
      'Div', 'Date', 'HomeTeam', 'AwayTeam', 'FTHG', 'FTAG', 'FTR', 'HTHG', 'HTAG', 'HTR', 'HS', 'AS', 'HST', 'AST', 'HY', 'AY', 'HR', 'AR',
      f'HPTS_avg_{N}', f'APTS_avg_{N}', f'H_gd_{N}', f'A_gd_{N}', f'H_eff_{N}', f'A_eff_{N}', f'HST_avg_{N}', f'AST_avg_{N}', 'target'
  ]
  ```

### Data Processing

1. **Data Cleaning**:
   ```python
   def data_cleaner(df: pd.DataFrame):
       df_copy = df.copy()
       df_copy["target"] = np.where(df_copy["FTR"] == "H", 0, np.where(df_copy["FTR"] == "A", 2, 1))
       return df_copy
   ```

2. **Feature Engineering**:
   - Calculate seasonal and rolling metrics.
   - Compute average points, goal differences, effectiveness, etc.
   - Example functions:
     ```python
     def calc_avg_points(df: pd.DataFrame, window=5):
         # Compute average points over a rolling window
         # Implementation here
     ```

### Directory Setup

Ensure the output folder exists:
```python
output_folder = f"dataset/processed/"
if not os.path.exists(output_folder):
    os.makedirs(output_folder)
```

### Running the Script

Execute the script to process data and generate predictions:
```bash
python script_name.py
```

## Functions

### Core Functions

- **find_season_name**: Constructs season names based on start year and league code.
- **get_all_team_matches**: Retrieves all matches for a specified team.
- **calculate_final_table**: Computes the final league table for a season.
- **data_transformation**: Applies all necessary transformations to the dataset.

### Utility Functions

- **calc_team_status**: Calculates the status of teams based on past seasons.
- **calc_h2h_stats**: Computes head-to-head statistics for teams.

### Example Function Call

To calculate and transform data for a season:
```python
df = pd.read_csv("path_to_csv")
transformed_df = data_transformation(df, selected_columns, N)
transformed_df.to_csv(f"{output_folder}/processed_season.csv", index=False)
```

## Notes

- Adjust the configuration variables according to your dataset and requirements.
- Ensure that all necessary packages are installed and up-to-date.

