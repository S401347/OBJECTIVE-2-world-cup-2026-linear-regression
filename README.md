# HIT140 Assessment 3 – Objective 2: Predicting FIFA World Cup 2026 Results with Linear Regression

Group project for HIT140 Foundations of Data Science.

We built two linear regression models using only information known before each match (FIFA ranking points, team form, rest days, travel, host advantage, stage and stadium altitude):

- **Model 2.1:** predicts the goal difference between the two teams in a match (104 rows, one per match)
- **Model 2.2:** predicts the number of goals scored by a team in a match (208 rows, one per team per match)

## Group members

- Subash Gautam (S397793)
- Aayush KC (S401347)
- Rubin Sunar (S399228)
- Kishmat Gautam (S398056)

## Files

- `WorldCup2026_Objective2.ipynb` – the notebook with the data cleaning, models and plots
- `Objective2_Group_Report.docx` – the written report
- `data/` – input and output data
  - `fbref_fixtures_2026.csv` – scores and fixtures for all 104 World Cup 2026 matches (FBref)
  - `fbref_fixtures_2022.csv` – scores and fixtures for World Cup 2022 (used for each team's starting form)
  - `fbref_extra_time_90min.csv` – 90-minute scores for the extra-time matches in 2026
  - `fbref_extra_time_90min_2022.csv` – 90-minute scores for the extra-time matches in 2022
  - `fifa_ranking_2026-06-11_raw.json` – FIFA World Ranking points, published 11 June 2026
  - `dataset_2_1_goal_difference.csv` – final dataset for Model 2.1
  - `dataset_2_2_team_goals.csv` – final dataset for Model 2.2
  - `summary_regression.csv` – summary of the regression results

## Results (test set)

| | Model 2.1 | Model 2.2 |
|---|---|---|
| Target | Goal difference | Goals scored by a team |
| Test R² | 0.460 | 0.237 |
| Test RMSE (goals) | 1.833 | 1.540 |

In both models the FIFA ranking points were the most important variables.

## How to run

1. Install Python 3 and the packages `pandas`, `numpy`, `matplotlib`, `scikit-learn` and `jupyter`.
2. Keep the `data` folder in the same folder as the notebook.
3. Open `WorldCup2026_Objective2.ipynb` in Jupyter and choose **Run All**.

## Data sources

- FBref – World Cup 2026 and 2022 scores and fixtures, and match reports
- FIFA/Coca-Cola Men's World Ranking, 11 June 2026
