# STA-309
# Author: Ryan Zrelak
# Course: STA 309
# Date: May 2026

# Spotify Popularity Analysis (2010–2019)
This project analyzes the Spotify Streaming Insights dataset to understand which musical features influence a song’s popularity. The analysis includes data preprocessing, exploratory data analysis, a five‑plot dashboard, predictive modeling, model comparison, and a final interpretation of results. All analysis and code are contained in 309finalfianl.Rmd.

# Part 1 — Data Pre‑Processing
- Loaded the dataset directly from GitHub
- Explored structure, dimensions, and variable types
- Created a derived categorical variable for musical mode (Major → Yes, Minor → No)
- Selected Popularity as the response variable
- Identified five predictors: Danceability, Energy, Valence, Decibel, and Mode

This ensured the dataset was clean, consistent, and ready for modeling.

# Part 2 — Exploratory Data Analysis & Dashboard
# A dashboard of five visualizations was created to explore how popularity relates to each predictor:

- Popularity vs Energy

- Popularity vs Danceability

- Popularity vs Valence

- Popularity vs Decibel

- Popularity by Mode (boxplot)

These plots reveal trends, patterns, and potential nonlinear relationships.
A PNG of the dashboard is included as dashboard.png.

# Part 3 — Predictive Modeling
# Three predictive models were trained using 5‑fold cross‑validation:

# Full Linear Regression
– Uses all predictors
– Provides interpretability and a baseline

# Subset Linear Regression
– Uses only Energy + Danceability
– Tests whether a simpler model performs competitively

# Random Forest
– Tree‑based, nonlinear model
– Captures interactions and complex patterns

Each model includes a rationale and interpretation in the R Markdown file.

# Part 4 — Model Comparison
Models were compared using MAE, RMSE, and R².
A comparison plot was generated using bwplot(model_results).

# Summary of Findings:  
- Random Forest performed best across all metrics
- Full Linear Regression performed moderately well
- Subset Linear Regression performed the worst

This indicates that popularity depends on multiple interacting features, and nonlinear models capture these relationships more effectively.

#Final Interpretation
The analysis shows that Energy and Danceability are consistently the strongest predictors of popularity. Popularity is not purely linear, and the Random Forest model provides the most accurate predictions. However, external factors such as marketing, artist fame, and playlist placement are not included in the dataset, limiting predictive power. Overall, the project demonstrates how musical attributes relate to popularity and how different modeling approaches compare in predictive performance.
