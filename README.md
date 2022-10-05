# <p align="center">Rossmann Store Sales Prediction</p>

<p align="center">
    <img width="60%" src="https://raw.githubusercontent.com/eduardoffonseca/Rossman-Store-Sales/main/img/rosmann.png"> 
</p>

**Disclaimer:** The following business case is merely fictitious, based on a challenge from the Kaggle platform, using data from the Rossmann company to develop a data-driven solution.

**Kaggle Overview Description**[1]**:** Rossmann operates over 3,000 drug stores in 7 European countries. Currently, Rossmann store managers are tasked with predicting their daily sales for up to six weeks in advance. Store sales are influenced by many factors, including promotions, competition, school and state holidays, seasonality, and locality. With thousands of individual managers predicting sales based on their unique circumstances, the accuracy of results can be quite varied.

**Business Case:** To facilitate large-scale decision-making, Rossmann's CEO and CFO need to know the sales forecast for all their stores for the next six weeks, in order to define the necessary budget and prioritize which stores should be renovated so that sales be minimally affected in the short term and maximized in the long term. Given this scenario, it is extremely important to assertively forecast sales for the next six weeks.

# Solution Planning

In order to build a solution to this problem, in an orderly and easily understandable way, the Cross Industry Standard Process for Data Mining (CRISP-DM)[2] methodology was used. It consists of a six-step cyclic process, as shown in the figure below.

<p align="center">
    <img width="70%" src="https://www.datascience-pm.com/wp-content/uploads/2021/02/CRISP-DM.png"  style="background-color: white;"> 
</p>

## **I. Business Understanding**

Understand the reasons behind the business need. Understand why it is necessary to carry out sales predictions, determine available resources, project requirements and technologies and tools to be used.

## **II. Data Understanding**

The main objective of data understanding is to identify, collect, and analyze the data sets that can help to accomplish the project goals.

1. **Collect Initial Data:** Acquire the dataset from the company and load it into de analysis tool;

2. **Describe Data:** Examine the dataset and the documentation in order to understand properties such as data formats and number of records;

3. **Explore Data:** Examine the dataset in order to assess the relationship between features;

4. **Verify Data Quality:** Verify how "clean" the dataset is and document it, in order to be prepared for the next steps.

## **III. Data Preparation**

This step consists in select and prepare the final dataset for modeling.

1. **Data Cleaning:** Perform the treatment of missing values, outliers and inconsistent data and deciding whether to correct, impute, or remove erroneous values;

2. **Feature Engineering:** Based on existing features, derive new attributes that can be helpful in the description of the phenomenon to be modeled;

3. **Data Filtering:** Filter records and features that do not contain useful information for modeling;

4. **Exploratory Data Analysis:** Analytical exploration of data, in order to understand the business, generate insights through raised hypotheses and seek the most important variables for the Machine Learning Models;

5. **Data Preparation:** Transformation and preparation of the data so that the model algorithm can interpret them correctly;

6. **Feature Selection:** Selection of features to be used by the model, based on algorithms and user business perception.

## **IV. Modeling**

Build and assess of various machine learning models based on several different modeling techniques.

1. **Select Modeling Techniques:** Determine which regression algorithms will be tested;

2. **Build Models:** Creation and training of the selected models, using training and validation datasets, for cross-validation analysis;

3. **Assess Models:** Evaluation of the results obtained on the models training, based on cross-validation error metrics;

4. **Hyperparameter Fine Tuning:** Selection of the best hyperparameters of the chosen model, based on random parameters search;

5. **Final Model:** Creation of the model that will be used in production, based on the hyperparameter fine tuning.

## **V. Evaluation**

Model error assessment, interpreting the error in a business and a statistical way.

1. **Business Performance:** Interpretation of the error focused on the business case, showing best and worst case scenarios for the sales predictions.

2. **Machine Learning Performance:**  Interpretation of the error focused on statistics, comparing the result with the test dataset and evaluating the magnitude of the machine learning model error.

## **VI. Deployment**

Create a solution so that the customer can access the results of the trained final model.

1. **Production Deployment:** Deployment of the final model in a cloud environment, Heroku, loading the saved model and applying the required transformations on the dataset.

2. **Telegram Bot:** Deployment of a Telegram Bot, used as interface between the user and the deployed model on the cloud.

# Data Fields

## Kaggle dataset dictionary[1]

| Feature                       | Description                                                     |
| -------------------------------- | ------------------------------------------------------------ |
| Id | an Id that represents a (Store, Date) duple within the test set |
| Store | a unique Id for each store |
| Sales | the turnover for any given day (this is what you are predicting) |
| Customers | the number of customers on a given day |
| Open | an indicator for whether the store was open. |
| StateHoliday |  indicates a state holiday. Normally all stores, with few exceptions, are closed on state holidays. Note that all schools are closed on public holidays and weekends. |
| SchoolHoliday | indicates if the (Store, Date) was affected by the closure of public schools |
| StoreType | differentiates between 4 different store models |
| Assortment | describes an assortment level |
| CompetitionDistance | distance in meters to the nearest competitor store |
| CompetitionOpenSince[Month/Year] |  gives the approximate year and month of the time the nearest competitor was opened |
| Promo | indicates whether a store is running a promo on that day |
| Promo2 | Promo2 is a continuing and consecutive promotion for some stores |
| Promo2Since[Year/Week] | describes the year and calendar week when the store started participating in Promo2 |
| PromoInterval | describes the consecutive intervals Promo2 is started, naming the months the promotion is started anew. E.g. "Feb,May,Aug,Nov" means each round starts in February, May, August, November of any given year for that store |

## Features derived from the original dataset

| Feature                       | Description                                                     |
| -------------------------------- | ------------------------------------------------------------ |
| Day (sin/cos) | Cyclic way of expressing the number of the day |
| Day of Week (sin/cos) | Cyclic way of expressing the day of week |
| Week of Year (sin/cos) | Cyclic way of expressing the number of the week |
| Month (sin/cos) | Cyclic way of expressing the number of the month |
| Competition Time Month | The number of months since the store has competition |
| Promo Time Week | The number of weeks since the Promo2 has been active for each store |

# Tools Used
 
 - Python;
 - Python Libraries: Pandas, numpy, seaborn, matplotlib, scikit learn, xgboost, boruta, pickle;
 - Jupyter Notebook;
 - Github;
 - Heroku Cloud;
 - Flask e Python API's;
 - Telegram BOT API.

 # Exploratory Data Analysis
 
 During the exploratory data analysis, some insights were discovered, which can contribute to understanding the business problem. Here the main insights found are shown:

 - **Stores with more competitors should sell less:** Through the data it was discovered that this hypothesis is **False**. It is shown that stores with CLOSER competitors have, on average, similar sales when compared to other stores.
 
 <p align="center">
    <img width="100%" src="https://raw.githubusercontent.com/eduardoffonseca/Rossman-Store-Sales/main/img/competitors_sales_2.png"  style="background-color: white;"> 
</p>

 - **Stores should sell more before the 10th of each month:** Through the data it was discovered that this hypothesis is **True**. On average, stores sells more before the 10th of each month, as shown in the image below.

<p align="center">
    <img width="100%" src="https://raw.githubusercontent.com/eduardoffonseca/Rossman-Store-Sales/main/img/sales_before_10.png"  style="background-color: white;"> 
</p>

 - **Stores should sell less during school holidays:** Through the data it was discovered that this hypothesis is **False**. On average, Stores sell more during school holidays, as shown in the image below.

<p align="center">
    <img width="100%" src="https://raw.githubusercontent.com/eduardoffonseca/Rossman-Store-Sales/main/img/school_holiday_12.png"  style="background-color: white;"> 
</p>

 # Machine Learning Models Assessment

In this work, five different models were used to deliver the sales predictions desired:
- Average Model, used as a baseline result. This shows what managers could deliver without looking into the data;
- Linear Regression;
- Regularized Linear Regression (Lasso);
- Random Forest Regressor;
- XGBoost Regressor. 

To assess the performance of each model, a 5 fold cross-validation (CV) was carried out. The result were evaluated comparing different error metrics of each model. The metrics used were:

- **Mean Absolute error (MAE):** Shows the mean absolute error of the model and its standard deviation.
- **Mean Absolute percentage error (MAPE):** Shows the percentage of the MAE.
- **Root mean squared error (RMSE):** The root of the mean error raised to the square. It is a good metric to evaluate the performance of the algorithm but it is not as good to translate to share holders.

## Cross-Validation Model Results

| Model Name | MAE CV   | MAPE CV      | RMSE CV |
|-----------|---------|-----------|---------|
| Random Forest Regressor | 838.18 +/- 218.74 | 0.12 +/- 0.02	| 1256.87 +/- 319.67 |
| XGBoost Regressor | 1048.45 +/- 172.04 | 0.14 +/- 0.02   | 1513.27 +/- 234.33 |
| Linear Regression | 2081.73 +/- 295.63 | 0.3 +/- 0.02   | 2952.52 +/- 468.37 |
| Regularized Linear Regression | 2116.38 +/- 341.5 | 0.29 +/- 0.01 | 3057.75 +/- 504.26 |

Due to Performance issues on my Machine, despite the Random Forest Model showing the best results for the Cross-Validation Performance, The second best Model, **XGBoost Regressor** was used to develop the solution for this Regression Problem.

 ## Final Model (Hyperparameter Fine-Tuning)

| Model Name | MAE | MAPE | RMSE |
| ---- | :----: | :----: | :----: |
| XGBoost Regressor | 645.65 | 0.093 | 942.244 |
| Average Model | 1354.80 | 0.455 | 1835.135 |

According to the prediction model, an improvement of approximately **52%** was obtained when comparing the MAE of the model with the baseline Average Model. This improvement can be shown to the share holders using the best and worst case scenarios of the model for the next six weeks sales of all stores. These scenarios were calculated using the sum of predictions for all stores and the MAPE of the model.

| Scenario | Values |
|-----------|---------|
| Predictions | $283,727,626.23 |
| Worst Scenario | $257,458,781.08 |
| Best Scenario | $309,996,471.37 |


# Model Deployment

One of the main goal of this project is to present the model results in a easy way, so that share holders can access the results without the need of any programming interface. With this in mind, a Telegram BOT API was used, which queries the model, deployed on the Heroku Cloud, and deliver the result instantly. To access the bot, just click in the image below.


[<img width="30%" src="https://img.shields.io/badge/Telegram-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white">](https://t.me/rossmann_eff_bot)

To use the bot insert "/" + the number of the desired store, as shown in the example video below.

<p align="center">
    <img width="30%" src="https://raw.githubusercontent.com/eduardoffonseca/Rossman-Store-Sales/main/img/bot_Telegram.gif"  style="background-color: white;"> 
</p>

# Conclusion

The results obtained showed a satisfactory result when compared to the baseline model. The use of the XGBoost Regressor model proved to be the right choice when assessing the time to train and deploy the model and the results obtained. As next steps, another cycle of the CRISP-DM methodology can be started, evaluating new hypothesis, creating new features and investigating the stores where the error metrics were high, in order to improve the model performance.

# References

[1] Kaggle - [Rossmann Store Sales Data](https://www.kaggle.com/competitions/rossmann-store-sales/data)

[2] Data Science Process Alliance - [What is CRISP-DM](https://www.datascience-pm.com/crisp-dm-2/)