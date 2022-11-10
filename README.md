# MultiFreq - The FreqTrade Docker Manager 

* Create a new Freqtrade instance with WebUI in one command line 🚀
* Run multiple instances with the individual config files
* Support HyperOpt and FreqAI functionality

### Requirements

* [Binance Account](https://www.binance.com/en/futures/ref/48577931)
* [Docker](https://www.docker.com/)

### Install
```
git clone https://github.com/nomad5am/MultiFreq.git
cd MultiFreq
./mf
```

### Configure & Customize

* Adapt basic private generated files into `./configs/private`
* Use or add your strategies into `./strategies`

## Usage

Just use `./mf` from your Trading Bot directory.

```
New Instance            ./mf i <instance> create
Start Instance          ./mf i <instance> trade
Stop Instance           ./mf i <instance> stop
List Available Pairs    ./mf i <instance> pairs <quote>
Create Pairs List       ./mf i <instance> configs-pairs <quote> 
Download Candle Data    ./mf i <instance> data <number-days> <candles> (Format: 5m_15m_1h_1d)
Reset instance data     ./mf i <instance> reset
Remove instance         ./mf i <instance> remove 
Freqtrade Logs          ./mf i <instance> logs

Run Backtest            ./mf i <instance> backtesting <from-date> (Format: 20211102)
Run HyperOpt            ./mf i <instance> hyperopt <loss_file> <spaces> (Format: buy_sell_roi) <freqai> <from-date> 

Start Web UI            ./mf ui start 
Stop Web UI             ./mf ui stop
```


### Create a new Freqtrade instance

Suppose you want to create an instance named `unicorn`

```
./mf i unicorn create
```

Now you need to configure your instance parameters from `./instances/unicorn.sh`

## Backtesting

```
./mf i unicorn data 10          # Download 10 days of data for `unicorn` instance
./mf i unicorn backtesting      # Let's backtest!
```

## CREDITS

🙏 Thank you [Ph3nol](https://github.com/Ph3nol/FT-Trading-Bot) for starting this project. 
You provided an incredible boilerplate for more things to come!

## DISCLAIMER

Do not risk money which you are afraid to lose. 
**USE THIS APPLICATION AT YOUR OWN RISK.** THE AUTHORS AND ALL AFFILIATES ASSUME NO RESPONSIBILITY ABOUT YOUR TRADING RESULTS.


### (Re)Build reference Docker images

```
docker pull freqtradeorg/freqtrade:stable
docker buildx build --no-cache --push --platform linux/amd64 \
    --file .docker/freqtrade/Dockerfile \
    --tag ph3nol/freqtrade:latest .

# Update .docker/freqtrade-ui/Dockerfile UI archive version before building Docker image
docker buildx build --no-cache --push --platform linux/amd64 \
    --file .docker/freqtrade-ui/Dockerfile \
    --tag ph3nol/freqtrade-ui:latest .
```
