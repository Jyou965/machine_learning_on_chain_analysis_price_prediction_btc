# Project Two: Machine Learning On-Chain Analysis to Predict Bitcoin Prices

__________________________________________________________________________

# Background

In this project, we used three different machine learning models to predict bitcoin prices and test which one would yeild the most accurate results. The models used were Perceptrons (Deep Learning), Random Forest (Ensemble Learning), and Lasso Regression (Supervised Learning). We attempted to account for all three levels of the On-Chain Analysis Framework (shown below) by focusing our analysis on features included in all levels. 

![Screen-Shot-2021-04-07-at-8 31 22-PM](https://user-images.githubusercontent.com/81061058/126056173-80aee8c4-4cdf-43c9-b756-e60ddbe00a2d.jpg)


__________________________________________________________________________

# Libraries and Setup 

We imported many of the libraries that are used often in class, like Pandas, but we added a few notable ones to perform the machine learning analysis. Lasso, Linear Regression, and Logistic Regression from the sklearn.linear_model were also included, and so were train_test_split and TimeSeriesSplit from the sklearn.model_selection library. A full list of the imported libraries is included in the first section of the main_code file. 

After importing the required libraries, we imported and used the glassnode.com API key, making sure to define the coin as BTC. 


___________________________________________________________________________

# Project Phases:
  
  ## Phase One: Cleaning Data, Correlation, Choosing Features for DataFrames
  
  By using the On-Chain Analysis Framework, we defined 27 features to further examine and build DataFrames for. We then used heat maps to illustrate correlation and deleted features that didn't have enough history. After cleaning, we were left with 12 features to create data frames for, with the hope that using the ML models with them would yeild the best results. 
  
  ## Phase Two: Building Machine Learning Models
  
  As mentioned above, we used Perceptrons, Random Forest, and Lasso Regression to do our analysis. We found three key features that seemed to have the most correlation with BTC price: Circulating Supply, Hash Rate, and Transaction Count. All three features fall into Network Health, the bottom level of the Bitcoin pyramid.
  
  ## Phase Three: FaceBook Prophet 
  
   Loaded FB Prophet into notebook by using "from fbprophet import Prophet". It created 532,441 combinations of feature possibilities.
    
  ## Phase Four: Applying Machine Learning Models 
  
  For this step, we applied each machine learning model using the feature_predictions dataframe. We used train_test_split for Random Forest, and two hidden layers with Perceptrons.
  
  
