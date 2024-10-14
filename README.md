 # Crypto Trading Bot with Gradient Boosting Strategy

This project implements an automated crypto trading bot using a Gradient Boosting model. The bot performs backtesting on historical data and integrates with Google Cloud services (BigQuery and Pub/Sub) for data storage and trade notifications.

## Prerequisites

1. **Python Environment**: Ensure you have Python 3.x installed.
2. **Google Cloud Account**: 
   - You need to create a Google Cloud project and enable the **BigQuery API**.
   - Set up a **Service Account** and download the credentials file.

## Setup Instructions

### 1. Install Dependencies

To install the necessary dependencies, run the `install_dependencies.ipynb` notebook.

### 2. Account Setup

Before running the bot, you need to set up your credentials and environment:

1. **Create an `.env` file**:
   - Run the following command in your terminal to create an empty `.env` file:
     ```bash
     touch .env
     ```

2. **Generate and Store Account Details**:
   - Open and execute the `account_generation.ipynb` notebook. This will automatically generate your **Orderly** account credentials and store them in the `.env` file.

### 3. Training the Model

To train the model:

1. Update your **Google Cloud credentials path** and **project ID** in the `training.ipynb` notebook:
   - Set the path to your service account credentials JSON file in the notebook.
   - Set your Google Cloud **Project ID** in the notebook.

2. Run the `training.ipynb` notebook. This will:
   - Fetch historical market data.
   - Train the Gradient Boosting model using technical indicators.
   - Store the model and scaler files locally.

### 4. Running the Strategy (Backtesting)

To backtest the strategy:

1. Make sure to update the **Google Cloud credentials path** and **project ID** in the `backtesting.ipynb` notebook, similar to the training step.

2. Run the `backtesting.ipynb` notebook to execute the backtest. This notebook will:
   - Fetch historical market data.
   - Apply the trained Gradient Boosting model to generate buy/sell signals.
   - Store results in BigQuery and send trade notifications via Pub/Sub.

### Notes:
- **Google Cloud API Setup**: Ensure you have enabled the **BigQuery API** in your Google Cloud Console:
  1. Go to the **API & Services Dashboard** in the Google Cloud Console.
  2. Search for "BigQuery API" and click **Enable**.

- You will also need to update the Pub/Sub **Topic** in the backtesting notebook for trade notifications, ensuring you have the appropriate topic set up in your Google Cloud project.

## Workflow

1. **Data Fetching**: Historical market data is fetched from a crypto exchange (e.g., Binance).
2. **Feature Engineering**: Technical indicators like SMA, EMA, MACD, RSI, and ATR are calculated.
3. **Model Training**: The Gradient Boosting model is trained using the engineered features.
4. **Backtesting**: The strategy is backtested on historical data using the **Empyreal SDK**.
5. **Trade Notifications**: For each buy/sell action taken during backtesting, a message is sent to a Pub/Sub topic for real-time monitoring.

## Key Files

- `install_dependencies.ipynb`: Installs all required Python libraries.
- `account_generation.ipynb`: Generates Orderly account credentials and stores them in the `.env` file.
- `training.ipynb`: Trains the machine learning model and saves it locally.
- `backtesting.ipynb`: Runs the strategy on historical data and sends trade notifications.

## Dependencies

- **pandas**: Data manipulation and analysis
- **pandas-ta**: Technical analysis indicators
- **scikit-learn**: Machine learning algorithms
- **joblib**: Model serialization
- **ccxt**: Crypto exchange APIs
- **Empyreal SDK**: For backtesting strategies
- **google-cloud-bigquery**: For interacting with BigQuery
- **google-cloud-pubsub**: For sending trade notifications

## Google Cloud Integration

1. **BigQuery**: Used for storing historical market data and trade logs for further analysis.
2. **Pub/Sub**: Used for sending real-time trade notifications whenever the bot takes a buy/sell action.

## Bot Performance Statistics
- **Starting Position**: 70000$
- **Duration**: 13 days 23:00:00
- **Exposure Time**: 99.40%
- **Equity Final**: $73,922.92
- **Equity Peak**: $74,784.34
- **Return**: 5.60%
- **Buy & Hold Return**: -1.85%
- **Return (Ann.)**: 345.30%
- **Volatility (Ann.)**: 83.82%
- **Sharpe Ratio**: 4.12
- **Sortino Ratio**: 43.38
- **Calmar Ratio**: 94.03
- **Max Drawdown**: -3.67%
- **Avg. Drawdown**: -1.42%
- **Max. Drawdown Duration**: 3 days 15:00:00
- **Avg. Drawdown Duration**: 1 day 01:00:00
- **Number of Trades**: 80
- **Win Rate**: 52.5%
- **Best Trade**: 3.01%
- **Worst Trade**: -1.53%
- **Avg. Trade**: 0.08%
- **Max. Trade Duration**: 1 day 10:00:00
- **Avg. Trade Duration**: 0 days 05:00:00
- **Profit Factor**: 1.37
- **Expectancy**: 0.08%
- **SQN**: 0.93
- **Kelly Criterion**: 0.14
