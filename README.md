# Quantitative Trading with High-Frequency Trading Framework

This repository provides a framework for **Quantitative Trading** strategies, focusing on the development of **Alpha Algorithms** systems. It allows users to backtest and simulate trading strategies with historical market data and execute those strategies in real-time and works with any timeframe.

## Key Features

- **Backtesting Engine**: Test your trading strategies using historical data before live deployment.
- **Strategy Implementation**: Implement custom trading strategies.
- **Real-time Trading Simulation**: Simulate the trading process in real time.
- **Risk Management**: Includes tools to incorporate risk management strategies (e.g., stop-loss, take-profit).
- **Data Analysis**: Analyze the performance of strategies using various financial metrics.

  

## Installation

Clone the repository and install the dependencies:

        git clone https://github.com/stephen-njiu/QuantitativeTrading.git
        cd QuantitativeTrading
       pip install -r requirements.txt

## Backtesting
To run a backtest using historical market data, use the backtest.py script. You can implement your strategy and adjust parameters to suit your needs.

## Live Trading
For live trading simulations or actual execution, use the `live_trading.ipynb` script using Oanda broker
* You can modify the `oanda.cfg` file to include your trading settings, account details, and API keys for real-time market data.

## Supported Data Types
* OHLC Data: Open, High, Low, Close, format, essential for backtesting strategies.
* Real-time Data: API-driven data for live trading.

## Custom Strategy Example
* To create a custom strategy, extend the Strategy class and implement the required functions.
* Here’s an example of a simple moving average crossover strategy:
 
```    
from strategy import Strategy

class MovingAverageCrossover(Strategy):
    def __init__(self, short_window=50, long_window=200):
       self.short_window = short_window
        self.long_window = long_window
    
    def init(self):
        self.short_ma = self.I(self.sma, self.data.Close, self.short_window)
        self.long_ma = self.I(self.sma, self.data.Close, self.long_window)
    
    def next(self):
        if self.short_ma > self.long_ma and not self.position:
            self.buy()
        elif self.short_ma < self.long_ma and self.position:
            self.sell()
```

### To run a backtest with this strategy:
`python backtest.py --strategy MovingAverageCrossover`


## Contributing
Contributions are welcome! If you have ideas or improvements, feel free to open an issue or submit a pull request.
1. Fork the repository.
2. Create a feature branch (git checkout -b feature-new-strategy).
3. Commit your changes (git commit -m 'Add a new strategy').
4. Push to the branch (git push origin feature-new-strategy).
5. Open a pull request.


## License
This project is licensed under the MIT License - see the LICENSE file for details.
