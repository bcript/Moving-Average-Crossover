## IMPORT MODULES
import yfinance as yf
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd

# Crossover strategy
TICKER = 'SPY'
LOOKBACK = 10000
FAST = 20
SLOW = 50
# get ticker data 
def get_data():
    df = yf.download(TICKER, period='33y')
    df.columns = df.columns.get_level_values(0)

    return df.iloc[-LOOKBACK:, :]


# add ma to df
def add_ma(df, fast, slow):
    df[f'{fast}_ma'] = df['Close'].rolling(fast).mean()
    df[f'{slow}_ma'] = df['Close'].rolling(slow).mean()

    # plot chart
    plt.plot(df['Close'])
    plt.plot(df[f'{fast}_ma'])
    plt.plot(df[f'{slow}_ma'])
    plt.legend([f'{TICKER} Close Price', f'{fast}_ma', f'{slow}_ma'])
    plt.title('MA Crossover Strategy')

    return df

# add strategy
def add_strategy(df, fast, slow):
    # long when fast > slow else short
    df['Strategy'] = np.where(df[f'{fast}_ma'] > df[f'{slow}_ma'], 1, 0)
    df['Strategy'] = df['Strategy'].shift(1)
    return df

# test strategy
def test_strategy(df, fast, slow):
    df['asset_returns'] = (1 + df['Close'].pct_change()).cumprod() - 1
    df['strategy_returns'] = (1 + df['Close'].pct_change() * df['Strategy']).cumprod() - 1

    plt.figure()
    plt.plot(df['asset_returns'])
    plt.plot(df['strategy_returns'])
    plt.legend(['Asset Cumilative Returns', 'Strategy Cumilative Returns'])
    plt.title('Moving Average Crossover Strategy')

    return df

def calculate_stats(df):
    ## calculation of sharpe ratio
    # daily returns from strategy
    daily_returns = df['Close'].pct_change() * df['Strategy']
    
    # risk-free rate
    rf = 0

    # Sharpe ratio calculation
    sharpe_ratio = (daily_returns.mean() - rf) / daily_returns.std()
    sharpe_ratio_annual = sharpe_ratio * np.sqrt(252) # assume 252 trading days SPY

    ## calculation of sortino ratio
    # calculation of downside returns
    downside_returns = daily_returns[daily_returns < 0]

    # Sortino ratio calculation
    sortino_ratio = (daily_returns.mean() - rf) / downside_returns.std()
    sortino_ratio_annual = sortino_ratio * np.sqrt(252)

    ## calculation of kelly criterion
    wins = daily_returns[daily_returns > 0]
    losses = downside_returns # same thing

    b = wins.mean() / abs(losses.mean())
    p = len(wins) / len(daily_returns.dropna())
    q = 1-p
    kelly_criterion = ((b * p) - q) / b

    ## calculation of cagr
    # let start value be 1
    start_value = 1
    end_value = (1 + (df['Close'].pct_change() * df['Strategy'])).cumprod().iloc[-1]

    # number of years in backtest
    num_years = len(df) / 252
    cagr = ((end_value / start_value) ** (1 / num_years)) - 1

    return float(sharpe_ratio_annual), float(sortino_ratio_annual), f'{float(kelly_criterion)*100}%', f'{float(cagr)*100}%'

def main():
    df = get_data()
    df = add_ma(df, FAST, SLOW)
    df = add_strategy(df, FAST, SLOW)
    print(calculate_stats(df))
    df = test_strategy(df, FAST, SLOW)
   
    return df

# get benchmark bench
df = get_data()
num_years = len(df) / 252
start_bench = 1
end_bench = (1 + df['Close'].pct_change()).cumprod().iloc[-1]
benchmark_cagr = ((end_bench / start_bench) ** (1 / num_years)) - 1

print(f'{benchmark_cagr*100}%')

# get average wins and losses
df = main()
daily_returns = df['Close'].pct_change() * df['Strategy']
wins = daily_returns[daily_returns > 0]
losses = daily_returns[daily_returns < 0]

print(f'Win rate: {len(wins)/len(daily_returns.dropna()):.2%}')
print(f'Avg win: {wins.mean():.5f * 100}%}')
print(f'Avg loss: {losses.mean():.5f * 100}%}')
df
