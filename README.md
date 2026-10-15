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

### Main data files (used to fit the models)

| File | Rows | Description |
|---|---|---|
| `data/dataset_2_1_goal_difference.csv` | 104 | One row per match. Target: `goal_diff` (team1 goals minus team2 goals). Predictors: both teams' FIFA points, and differences in goals-for form, goals-against form, points form, rest days, travel and host status. |
| `data/dataset_2_2_team_goals.csv` | 208 | Two rows per match, one per team. Target: `goals`. Predictors: team and opponent FIFA points, team goals-for form, opponent goals-against form, rest difference, host at home, knockout, altitude. |

### Raw input files

- `data/fbref_fixtures_2026.csv` – scores and fixtures for all 104 World Cup 2026 matches (FBref)
- `data/fbref_fixtures_2022.csv` – scores and fixtures for World Cup 2022 (used for each team's starting form)
- `data/fbref_extra_time_90min.csv` – 90-minute scores for the extra-time matches in 2026
- `data/fbref_extra_time_90min_2022.csv` – 90-minute scores for the extra-time matches in 2022
- `data/fifa_ranking_2026-06-11_raw.json` – FIFA World Ranking points, published 11 June 2026

### Output file

- `data/summary_regression.csv` – summary of the regression results (rows, CV R², CV RMSE, baseline RMSE, adjusted R²)

## How the main data files are built

1. Load the match results. For extra-time games, use the 90-minute score instead of the final score.
2. Create one row per team per match (goals for, goals against, points).
3. Add pre-match variables for each team, using only games played before that match:
   - **Form:** average goals scored, goals conceded and points in earlier games. It starts from the 2022 World Cup average as one extra game, so first matches have a form difference of 0.
   - **FIFA points:** from the ranking JSON.
   - **Rest days:** days since the team's previous match.
   - **Travel:** distance in km from the previous venue.
   - **Altitude and host at home:** from the stadium table (host at home = team's country matches the venue's country).
   - **Knockout:** 1 for any round other than the group stage.
4. Join the opponent's values to each row.
5. Reshape into the two datasets:
   - **2.1** keeps one row per match, with most predictors as differences between the two teams.
   - **2.2** keeps both team rows, with the team's and opponent's values as separate predictors.

## Results

Test set (80/20 split):

| | Model 2.1 | Model 2.2 |
|---|---|---|
| Target | Goal difference | Goals scored by a team |
| Test R² | 0.460 | 0.237 |
| Test RMSE (goals) | 1.833 | 1.540 |

10-fold cross-validation (from `summary_regression.csv`):

| | Model 2.1 | Model 2.2 |
|---|---|---|
| CV R² | 0.305 | 0.176 |
| CV RMSE | 1.671 | 1.255 |
| Baseline RMSE | 2.022 | 1.392 |

In both models the FIFA ranking points were the most important variables.

## How to run

1. Install Python 3 and the packages `pandas`, `numpy`, `matplotlib`, `seaborn`, `scipy`, `statsmodels`, `scikit-learn` and `jupyter`.
2. Keep the `data` folder in the same folder as the notebook.
3. Open `WorldCup2026_Objective2.ipynb` in Jupyter and choose **Run All**.

## Data sources

- FBref – World Cup 2026 and 2022 scores and fixtures, and match reports
- FIFA/Coca-Cola Men's World Ranking, 11 June 2026
