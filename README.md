![chain]()

# Machine Learning On-Chain Analysis of Bitcoin Price

---

## Background

In this project, we used three different machine learning models to identify key drivers of bitcoin prices and tested which model would yeild the most accurate results in predicting bitcoin prices. The models used were Perceptrons (Deep Learning), Random Forest Regressor (Ensemble Learning), and Lasso Regressor (Supervised Learning). 

We used the on-chain analysis framework provided by [Ark Invest](https://github.com/Jyou965/machine_learning_price_prediction_btc/blob/main/supporting_files/screenshots/ark%20framework.png) (the Ark Framework). 

We started with 27 on-chain metrics from Glassnode.com as well as the Fear & Greed Index from alternative.me and narrowed down the dimentions to 12, with ten years of daily history since 2011.

---

## Libraries and Dependancies

* [json](https://docs.python.org/3/library/json.html?highlight=json#module-json) - stands for JavaScript Object Notation. It is a lightweight data interchange format inspired by JavaScript object literal syntax.

* [requests](https://docs.python-requests.org/en/master/) - an elegant and simple HTTP library for Python, built for human beings.

* [pandas](https://pandas.pydata.org/docs/) - an open source, BSD-licensed library providing high-performance, easy-to-use data structures and data analysis tools for the Python programming language.

* [os](https://docs.python.org/3/library/os.html) - provides a portable way of using operating system dependent functionality.

* [dotenv](https://pypi.org/project/python-dotenv/) - reads key-value pairs from a .env file and can set them as environment variables.

* [matplotlib](https://matplotlib.org/) - a comprehensive library for creating static, animated, and interactive visualizations in Python.

* [hvplot](https://hvplot.holoviz.org/user_guide/Introduction.html) - provides a high-level plotting API built on HoloViews and Bokeh that provides a general and consistent API for plotting data in all the abovementioned formats.

* [numpy](https://numpy.org/doc/stable/) - the fundamental package for scientific computing in Python. It is a Python library that provides a multidimensional array object, various derived objects (such as masked arrays and matrices), and an assortment of routines for fast operations on arrays, including mathematical, logical, shape manipulation, sorting, selecting, I/O, discrete Fourier transforms, basic linear algebra, basic statistical operations, random simulation and much more.

* [scikit-learn](https://scikit-learn.org/stable/) - tools for predictive data analysis.

* [TensorFlow](https://www.tensorflow.org/api_docs) - an end-to-end open source machine learning platform.

* [keras](https://keras.io/guides/) - a Python deep learning API library that offers consistent & simple APIs, minimizes the number of user actions required for common use cases, and provides clear & actionable error messages. 

* [fbprophet](https://facebook.github.io/prophet/) - a procedure for forecasting time series data based on an additive model where non-linear trends are fit with yearly, weekly, and daily seasonality, plus holiday effects. It works best with time series that have strong seasonal effects and several seasons of historical data.

* [itertools](https://docs.python.org/3/library/itertools.html) - creates iterators for efficient looping.

* [panel](https://panel.holoviz.org/) - https://panel.holoviz.org/ - an open-source Python library that lets you create custom interactive web apps and dashboards by connecting user-defined widgets to plots, images, tables, or text.

* [datetime](https://docs.python.org/3/library/datetime.html) - supplies classes for manipulating dates and times.

---

## API

The API to Glassnode.com is hidden.  Users of this program need to set up their own APIs.

---

## Project Phases:
  
  ### Phase One: Cleaning Data, Correlation, Choosing Features for DataFrames
  
  By using the Ark Framework, we started with 27 features to further examine and build DataFrames for. We then used heat maps to illustrate correlations. Features that had high correlations with others and those that didn't have ten years of history were deleted. 12 features remained.  

  Below is a diagram of the metrics in relation to the Ark Framework.  Those in black are the 12 features that remained.  Those in red got eliminated due to high correlation with other features.  Those in green got eliminated due to not having ten years of historical data.

  ![features](https://github.com/Jyou965/machine_learning_price_prediction_btc/blob/main/supporting_files/screenshots/features.png)

  The correlations among the remaining features are demonstrated in the following chart.

  ![correlations](https://github.com/Jyou965/machine_learning_price_prediction_btc/blob/main/supporting_files/screenshots/correlations.png)
  
  ### Phase Two: Building Machine Learning Models
  
  As mentioned above, we used Perceptrons, Random Forest Regressor, and Lasso Regressor to do the analysis. In this phase, we built the Lasso Regressor model to evaluate the coefficients of the 12 features.  The other two models are built in Phase Four.

  ![lasso](https://github.com/Jyou965/machine_learning_price_prediction_btc/blob/main/supporting_files/screenshots/lasso%20coefficients.png)

  ### Phase Three: FB Prophet 
  
  We used FB Prophet to predict the price range of each feature on a given day (in this case, 2022-01-13). Yhat, yhat lower & yhat upper are captured.  We then used Itertools to iterate all 532,441 (=3^12) combinations of feature possibilities using the three captured values for each feature.

  ![FB](https://github.com/Jyou965/machine_learning_price_prediction_btc/blob/main/supporting_files/screenshots/prophet%203%20lines.png)
  ![FB](https://github.com/Jyou965/machine_learning_price_prediction_btc/blob/main/supporting_files/screenshots/prophet%20full.png)
    
  ### Phase Four: Applying Machine Learning Models to Make BTC Price Predictions
  
  For this step, we applied each machine learning model using the feature_predictions dataframe. Random Forrest Regressor predictions are worth the most attention because it is the most accurate model among the three based on model scores and back-testing accuracy, which will be illustrated in the following section.

  ![prediction](https://github.com/Jyou965/machine_learning_price_prediction_btc/blob/main/supporting_files/screenshots/prediction.png)

---

## Key Decisions, Results and Findings

1. During the process, we had three key strategic decisions to make:
    A. To predict BTC prices or returns: We tried both and decided to predict prices due to more reasonable results.  

    B. To use Lasso Regressor to select features or use correlations to manually select features:  We tried both.  Lasso Regressor singled out hash rate as the only feature to be used, which could be very insightful.  However, predictive results were not as good as using correlations to narrow down the number of features to 12.  As such, we chose the latter approach. But Lasso Regressor's initial selection of hash rate is well worth further investigation.
    
    C. To use train_test_split or TimeSeriesSplit:  We tried both and decided to use train_test_split due to better predictive results.

2. Model effectiveness and backtesting results: Random Forrest Regressor turned out to be the most accurate model among the three.

  Model scores:
  ![lassoScore](https://github.com/Jyou965/machine_learning_price_prediction_btc/blob/main/supporting_files/screenshots/lasso%20scores.png)
  ![rfScore](https://github.com/Jyou965/machine_learning_price_prediction_btc/blob/main/supporting_files/screenshots/rf%20scores.png)
  ![perceptronLayers](https://github.com/Jyou965/machine_learning_price_prediction_btc/blob/main/supporting_files/screenshots/perceptrons%20layers.png)
  ![perceptronScore](https://github.com/Jyou965/machine_learning_price_prediction_btc/blob/main/supporting_files/screenshots/perceptrons%20score.png)

  Back-testing results:
  ![lassBacktest](https://github.com/Jyou965/machine_learning_price_prediction_btc/blob/main/supporting_files/screenshots/lasso%20backtesting.png)
  ![rfBacktest](https://github.com/Jyou965/machine_learning_price_prediction_btc/blob/main/supporting_files/screenshots/rf%20backtesting.png)
  ![perceptronsBacktest](https://github.com/Jyou965/machine_learning_price_prediction_btc/blob/main/supporting_files/screenshots/perceptrons%20backtesting.png)

3. Key drivers of BTC prices:

  The following charts from Lasso Regressor and Random Forrest Regressor demonstrated that the top three drivers of BTC prices are Hash Rate, Circulating Supply and Transaction Volume, all of which fall into Network Health, the bottom level of the Ark Framework pyramid.  It also indicates that Network Effect is a bigger driver for BTC prices than stock-to-flow.
  
  ![lassocoefficient](https://github.com/Jyou965/machine_learning_price_prediction_btc/blob/main/supporting_files/screenshots/lasso%20coefficient.png)
  ![rf_importance](https://github.com/Jyou965/machine_learning_price_prediction_btc/blob/main/supporting_files/screenshots/rf%20importance.png)

  As mentioned earlier, the output by Lasso Regressor covers the 12 features manually selected.  When Lasso Regressor was given all 27 features to select from, it only kept hash rate.  Although the effectiveness of the model based on hash rate only was not as high, this response is well worth further research.
  
---

## Future Steps
   The predictive capabilities of the models depend on the availability of historical data for features, the configuration of FB Prophet, the ML model selection and model parameter settings. The following steps can be done to further improve the predictive power of the models:
   - Evaluate model selection or combination.
   - Look into Lasso Regressor's preliminary selection of hash rate as the only factor.
   - Examine how to get better results by predicting BTC returns instead of prices.
   - Better understand how parameters impact model results (X, y split; y as price or return).
   - Incorporate features with shorter history.
   - Adapt the model for Etherem and DeFi protocols.

For more information, please refer to the [presentation](https://github.com/Jyou965/machine_learning_price_prediction_btc/blob/main/supporting_files/project_presentation.pdf) in the repo.
