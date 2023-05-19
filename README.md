# Real estate price prediction based on [Sberbank Russian Housing Market dataset](https://www.kaggle.com/c/sberbank-russian-housing-market) 

## Annotation  

This is a classic type of task machine learning is Linear Regression. 
**Random rainforest** and **Gradient Boosting** models were also used. 

The aim of the project is prediction price in house market of Moscow. 

## Structure of Github:

 - **tryings** - this is directory, which contains _jupyter notebooks_ with first tryings of solution, exploration of data and feature engineering 
 - **project** - this is the main directory, which contains solution and datasets     

## Input data

 - macro.csv - data about macroeconomic situation 
 - train.csv - train data
 - test.csv - test data without target value 
 - sample_submission.csv - data with values of test target  

## Solution  

### Used libs: <a name="1"></a>

- [Pandas](https://pandas.pydata.org/)
- [Numpy](https://numpy.org/) 
- [Seaborn](https://seaborn.pydata.org/) 
- [Matplotlib](https://matplotlib.org/)
- [Scipy](https://scipy.org/)
- [Category_encoders](https://contrib.scikit-learn.org/category_encoders/)
- [Scikit-learn](https://scikit-learn.org/stable/index.html) 
- [Xgboost](https://xgboost.ai/)

### 1. Cleaning dataset from null values 

- Dropping colums with null values percentage more than 40%
- Replacing null values with 'uknown' in categorial features and with mean value in numerical ones

### 2. Price adjustment for annual infaltion

Adjusting price with CPI (Consumer Price Index) using the following equation:
**adjusted_price = (price / CPI) * 100%**

### 3. Including features into the dataset

Only highly correlated features were included into the dataset. Every included column has been cleaned from outliers by IQR (Interquartile range) method.
- **Full square**

- **State** <br />
  The range of condition is from 1 to 4, where 4 is the best one, 1 is the worst
  
- **Distance from the infrastructure facilities** <br /> 
  The distance is the result of the average distance from all kind of infrastructure facitilites
  
- **Number of rooms** <br /> 
  Flats with the number of rooms more than 5 and less than 1 have been dropped out
  
- **Number of working population**

- **Distance from the Moscow center**

- **Distance from MKAD**

### 4. Standatization of the dataset and logarithm of the target before model training

Used method [StandardScaller](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.StandardScaler.html) from Scikit-learn 

### 5. Training model with numeric features
|  Model          |Score    |
|-----------------|---------|
|**Lasso**        |**-0.08**|
|Linear Regression|-124.98  |
|Random Forest    |-216.34  |
|Ridge            |-124.96  |

The best model is [Lasso](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.Lasso.html). 

### 6. Adding categorical features into the dataset
Only highly correlated features were included into the dataset.
- **Ecology factor** <br /> 
Ecology factor was decoded by one hot encoding (5 categories)

- **Sub area** <br /> 
Sub area was decoded by binary encoding (134 categories)


### 7. Training model with numeric and categirical features
|  Model          |Score    |
|-----------------|---------|
|**Lasso**        |**-0.08**|
|Linear Regression|-130.77  |
|Random Forest    |-220.37  |
|Ridge            |-130.77  |
|XGBboost         |-256.32  |
|Gradient Boosting|-197.14  |


### 8. Conclusion
Including the categorical features into the dataset didn't give any model improvement. The best model for our case of real estate pricing prediction is Lasso.
 
## Sources:

1. [Machine learning estate price](https://medium.com/@max.bobkov/machine-learning-moscow-flats-appraising-25a1e9f171db)

2. [Predicting real estate price](https://data4help.medium.com/predicting-real-estate-prices-255266ce2f43)

3. [Linear regression estimate results](https://habr.com/ru/articles/195146/)

4. [Cleaning dataset](https://proglib.io/p/moem-dataset-rukovodstvo-po-ochistke-dannyh-v-python-2020-03-27)

5. [Feature engineering](https://proglib.io/p/postroenie-i-otbor-priznakov-chast-1-feature-engineering-2021-09-15)

6. [Encoding categorical variables](https://medium.com/analytics-vidhya/heres-all-you-need-to-know-about-encoding-categorical-data-with-python-code-53e367a79b5c)

7. [XGboost Algorythm](https://medium.com/nuances-of-programming/%D0%B0%D0%BB%D0%B3%D0%BE%D1%80%D0%B8%D1%82%D0%BC-xgboost-%D0%BF%D1%83%D1%81%D1%82%D1%8C-%D0%BE%D0%BD-%D1%86%D0%B0%D1%80%D1%81%D1%82%D0%B2%D1%83%D0%B5%D1%82-%D0%B4%D0%BE%D0%BB%D0%B3%D0%BE-dc8c4eca3fbc)

8. [Python libs](#1)

