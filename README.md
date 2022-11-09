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
General
./mf i <bot-name> create ...................... Create/Init an instance
./mf i <bot-name> trade ....................... Start Instance
./mf i <bot-name> stop ........................ Stop Instance
./mf i <bot-name> pairs <quote> ............... List available exchange pairs
./mf i <bot-name> configs-pairs <quote> ....... Set TMP pairs, from configs
./mf i <bot-name> data <days-count> ........... Download data for backtests & hyperopt
./mf i <bot-name> reset ....................... Reset instance data
./mf i <bot-name> remove ...................... Remove instance
./mf i <bot-name> logs ........................ Tail running instance Freqtrade logs

./mf ui start ................................. Start UI
./mf ui stop .................................. Stop UI

./mf i <bot-name> backtesting <from-date> ................................ Run Backtest (<from-date> Format: 20211102)
./mf i <bot-name> hyperopt <file> <spaces> <epochs> <freqai> <from-date>.. Run HyperOpt & FreqAI
```


### Create a new Freqtrade instance

Suppose you want to create an instance named `unicorn`

```
./mf i unicorn create
```

Now you need to configure your instance parameters from `./instances/unicorn.sh`

## Backtesting

```
./mf i unicorn data 10 # Download 10 days of data for `unicorn` instance
./mf i unicorn backtesting # Let's backtest!
```

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
