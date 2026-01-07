# f1-race-outcome-prediction
Scenario-based Formula 1 race outcome prediction using FastF1 data, machine learning, and pre-race weather assumptions.

Overview: 
This project is a scenario-driven Formula 1 race outcome prediction model built using historical race data, qualifying performance, team strength, driver statistics, and weather-related assumptions.
Rather than claiming real-time automation, this project focuses on pre-race simulation, answering the question:
“Given the information available before race day, what does a data-driven model predict?”
The project uses FastF1 for official F1 timing data and a Gradient Boosting Regressor to estimate expected race lap times for drivers.

Key Objectives: 
1) Predict relative race performance of drivers for a future Grand Prix
2) Study the impact of:
            A) Qualifying performance
            B) Team strength
            C) Driver consistency
            D) Weather conditions
3) Build a flexible model that can be re-run as race-day assumptions change

Data Sources:
1) FastF1 library
        A) Sector times
        B) Lap times
        C) Qualifying and race sessions
2) Official F1 timing data (via Ergast API through FastF1)

Feature Engineering:
The model uses the following features:
---------------------------------------------------------------------------------------------
|     Feature                          | Description                                        |
---------------------------------------------------------------------------------------------
|     QualifyingTime	               | Driver qualifying lap time                         |
|     TotalSectorTime            	   | Average sector performance from previous season    |
|     TeamPerformanceScore	   | Normalized constructor championship points         |
|     DriverPoints	               | Driver championship points                         |
|     RainProbability	               | Pre-race rain probability (manual input)           |
|     Temperature	               | Estimated race-day temperature                     |
|     LastYearWinner                   | Binary indicator for previous year’s race winner   |
---------------------------------------------------------------------------------------------

Weather Modeling Approach (Important)
1. Wet Performance Scores

Wet performance is not guessed or arbitrary.
         - A separate analysis (weather_performance.py) compares:
                         : Qualifying vs race lap times
                         : For a known wet race (Australia 2025)
         - A Wet Performance Score is computed for each driver
         - These scores are manually injected into the main model

 Why manual?

- Wet races are rare
- Live wet-performance APIs do not exist
- This mirrors how analysts use precomputed adjustment factors

"This is a deliberate engineering decision, not a limitation"

2. Rain Probability

             rain_probability = 0.75  # Updated manually before race day
- Rain probability is manually set based on publicly available forecasts
- The model is re-run as forecasts change

"This is scenario-based modeling, not real-time automation"

Modeling Technique: 
A) Model: Gradient Boosting Regressor
B) Target Variable: Average race lap time
C) Evaluation Metric: Mean Absolute Error (MAE)

The model focuses on relative driver performance, not exact finishing positions.

Outputs:
- Predicted race lap times per driver
- Visualizations:
        : Team performance vs predicted race time
        : Feature importance analysis
  
"These outputs help interpret why the model makes certain predictions"

How to Run:
1) Install dependencies:
              pip install fastf1 pandas numpy scikit-learn matplotlib
2) Run weather analysis (optional):
              python weather_performance.py
3) Run race prediction:
              python race_prediction.py


Future Improvements:
A) Expand training data across multiple races
B) Automate weather ingestion (API-based)
C) Add uncertainty intervals to predictions
D) Integrate strategy simulations

Author
Mehul Gupta
