# **Project name:** synthetic financial time series generation
## Brief

Generate synthetic market data (returns, volatility paths) using GANs, for stress-testing and back-testing when historical data is limited.

## Rough scope

Week 1: research + pull data and learn and document the stylised facts of financial returns (e.g fat tails, volatility, clustering, absence of autocorrelations in returns)

Week 2: build a GAN and train it

Week 3: validate against real world data using statistical analysis

Week 4: upload github repo

## Working notes
**Motivation for project**
What's the point of sythetic data?

- synethtic datacan be used to test investment strategy against alternate histories (backtest overfitting)
- stress-testing investment strategies

What am I trying to do?
- test whether synthetic data can be generated that is statisically similar to real market data while

## Objectives
1. Characterise relevant stylised facts of real financial return data
2. Build a baseline generator (GARCH or VAE) to compare GAN performance to (to show if using GANs improves on simpler methods)
3. Build a GAN-based generator for synthetic return series
4. Rigourously valdiate generated series against real-data benchmark, employing named statistical tests
5. Evaluate generated data for real use-cases (e.g. backtesting, stress-testing, risk estimation)

## Glossary of terms

- stylised facts: empirical characteristics observed across a range of instruments, markets and time periods. [link]("http://rama.cont.perso.math.cnrs.fr/pdf/empirical.pdf")
    - absence of autocorrelation (measure of how similar a data point in a time series is to its own past values across different time gaps) except for very small intraday time scales (<= 20 mins)
    - heavy tails: a probability distribution with a tail that goes to zero more slowly than exponential distribution, meaning very large values are more likely i.e. high kurtosis with extreme outliers (the tail follows a power-law/Pareto-like shape with a tail index between 2 and 5 for most datasets)
    - gain/loss asymmetry: higher drawdowns compared to upward movement (stocks to go down faster than up)
    - aggregational Gaussianity: as the time scale is increased, return distribution approaches Gaussian
    - intermittency: high degree of variability at any time-scale, quantified by the presence of irregular bursts in time series
    - volatility clustering: different measures of vaolity display a positive autocorrelation over several days i.e. high volatility events tend to cluster in time, occuring together, while steadiness is clustered in time as well
    - conditional heavy tails: after correcting for volatility clustering via GARCH models, tails are less heavy (but still heavy)
    - slow decay of autocorrelation in absolute returns: if you take the absolute return and just focus on the *size* of the price move, there is strong autocorrelation which decays slowly (*can* be interpreted as sign of long-range dependence, also indicates volatility clustering) (the decay is roughly power-law with an exponent between 0.2 and 0.4)
    - leverage effect: most measures of volatility are negatively correlated with returns of the asset
    -   volume/volatility correlation: trading volume (total nuber of shares, contracts or units of an asset traded within specific time period) is postiviely-correlated with all measures of volatility
    - assumetry in time scales: coarse-grained measurs of volatility predict fine-scale volatility better than the other way around i.e. it is easier to scale down prediction than up

    **NOTE**
    Quantify early:
    1. Absence of autocorrelation in raw returns
    2. heavy tails (kurtosis + tail index)
    3. volatility clustering (autocorrelation of squared/absolute returns)
    4. slow decay of autocorrelation in absolute terms

    Maybe quantify:
    1. gain/loss asymmetery (comparing magnitude of drawdowns vs upward moves)
    2. aggregational gaussianity - aggregate retrusn to weekly monthly visually approach normal
    3. leverage eggect - correlating volatility with returns

    Maybe after GARCH if i use GARCH:
    1. conditional heavy tails: testing tails on residuals compated to before GARCH

    Difficult:
    1. volume/volatility correlation - requires trading volume data
    2. intermittency
    3. asymmetry in time scales
        both difficult to formalise quantitatively



- stationarity: distribution does not vary over time
    for any set of time instants 
- GAN : get from FYP report
- VAE (variational autoencoder) : a generative model that learns a compressed representation of data and can generate new samples from it
- GARCH: a classical statistical model built to capture volatility clustering
- TCN (temporal convolotuional network): convolutions in time
- Backtest overfitting: when a strategy is tuned so closely to historical data that it fails to generalise to new/future conditions
- risk-neutral distribution: a mathematically-adjsuted probaility distribution used specifically for pricing options consistency (out of scope)
- Ljung-Box test: a fomrla statistical test for whether autocorrelation is present in time series
- Sharpe ratio: a measure of investment return relative to risk taken (out of scope)

## Methodology
### Objective 1 - *Characterise relevant stylised facts of real financial return data*

1. extract and process S&P500 historical daily return data
2. Compute and visualise these core stylised facts:
    - Absence of autocorrelation in raw returns
    - heavy tails (kurtosis + tail index)
    - volatility clustering (autocorrelation of squared/absolute returns)
    - slow decay of autocorrelation in absolute terms
3. Output a quantiative benchmark to compare synthetic series to


Objective 2: Build a baseline generator (GARCH or VAE) to compare GAN performance to (to show if using GANs improves on simpler methods)
Objective 3: Build a GAN-based generator for synthetic return series
Objective 4: Rigourously valdiate generated series against real-data benchmark, employing named statistical tests
Objective 5: Evaluate generated data for real use-cases (e.g. backtesting, stress-testing, risk estimation)


## Bibliography
[QuantGAN]("https://arxiv.org/abs/1907.06673")

[Applications of synthetic financial data in portfolio and risk modelling]("https://arxiv.org/html/2512.21798v1#bib.bib8")

[When fake data beats real data]("https://medium.com/@ifor/when-fake-data-beats-the-real-thing-what-finance-is-learning-from-synthetic-data-experiments-cc99f2d41024")

[Empirical properties of asset returns]("http://rama.cont.perso.math.cnrs.fr/pdf/empirical.pdf")
