# Weather Prediction using Markov Chain and Monte Carlo Simulation

This project uses historical daily weather data (2000–2024) to simulate and predict the weather for the **next 30 days using:

- Markov Chain Model
- Adaptive Transition Matrix
- Monte Carlo Simulation

The project is implemented in **Python (Jupyter Notebook)** and uses probabilistic modeling to forecast future weather states based on historical transition patterns.

#Project Objective

The main goal of this project is to model weather as a **stochastic process** where the weather of the next day depends on the current day’s weather.

Using historical data, the project:

1. Converts weather conditions into discrete states
2. Builds transition probabilities
3. Creates an adaptive Markov transition matrix
4. Simulates future weather for 30 days
5. Estimates probabilities of extreme events

---

#Dataset

The dataset used is:

`india_2000_2024_daily_weather.xlsx`

It contains **daily weather data from 2000 to 2024** for multiple Indian cities.

#Features Used

- `city`
- `date`
- `temperature_2m_max`
- `rain_sum`
- `wind_speed_10m_max`

For this project, the model was built specifically for:

Mumbai



 # Weather State Classification

The continuous weather variables were converted into categorical states.

# Defined States

| Condition | Weather State |
|---|---|
| Wind speed ≥ 40 | Storm |
| Temperature ≥ 36°C | Heatwave |
| Rain ≥ 20 mm | Heavy Rain |
| Rain > 0 mm | Rainy |
| Temperature between 25–35°C | Sunny |
| Otherwise | Cloudy |

This conversion helps in applying the Markov Chain model effectively.


# Methodology

# 1. Data Segmentation

The historical dataset was divided into 3 time periods:

- Old: Before 2008
- Mid: 2008–2015
- New: 2016 onwards

This was done to capture changing weather trends over time.


# 2. Transition Matrix Construction

For each period, a transition matrix was created using:

```python
pd.crosstab(df["state"], df["next_state"], normalize="index")
```

This gives the probability of transitioning from one weather state to another.

# 3. Adaptive Transition Matrix

Instead of using a single fixed transition matrix, the project computes an **adaptive transition matrix** by averaging the three period-specific matrices:

This improves robustness by accounting for long-term climate variations.

# 4. Markov Prediction

Future states are predicted on the basis of adaptive transition matrix.

# 5. Monte Carlo Simulation

A 30-day weather sequence is simulated using random sampling from transition probabilities.

```python
np.random.choice(states, p=probs)
```

This allows generation of realistic future weather paths.

# Extreme Weather Probability

The model also calculates probability of extreme weather events:

- Heavy Rain
- Heatwave
- Storm

This can be useful for risk analysis and forecasting.

# Model Accuracy

The notebook includes a custom accuracy function that compares:

- actual next weather state
- predicted most probable next state

This provides a basic performance evaluation of the Markov model.

# Visualizations

The project includes:

#1. Transition Matrix Heatmap
A heatmap showing transition probabilities between weather states.

#2. 30-Day Weather Simulation Plot
A time-series style plot showing simulated weather states for future days.

## Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Jupyter Notebook

#Key Concepts Used

- Markov Chains
- Stochastic Processes
- Monte Carlo Simulation
- Probability Transition Matrix
- Time Series Weather Modeling
- Climate Trend Adaptation
