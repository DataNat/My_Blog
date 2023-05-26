---
layout: post
title: 'Classification Problem of Bank’s Telemarketing Campaign'
tags: [Classification, Machine Learning, SMOTE]
featured_image_thumbnail:
featured_image: assets/images/posts/2019/cover.jpeg
featured: true
hidden: true
---

## Introduction

Retail banks collect term deposits as part of their core business investment products. Banks generate a profit by lending funds held in deposit accounts for a higher rate than it pays the customer. Therefore, banks emphasize their marketing efforts to attract customers to deposit funds. Although most marketing channels are transitioning to a digital form and telemarketing campaigns are fading away, there is still space in advertising to utilize the phone as a tool for remote marketing. While remote marketing is moving gradually into robocalls, prospects still prefer to talk to a human rather than a robot-speaking voice.

In finance, an individual who buys a term deposit is called a subscriber. Subscription refers to a potential investor signing up for an investment vehicle agreement involving cash flow and money transfer. Different elements, such as a personal financial situation or high-interest rate, which makes the cost of borrowing more appealing, affect the subscription decision of the prospect. As such, banks benefit from data analysis and prediction models to optimize their campaigns by targeting certain segments of individuals.

## Dataset and Methodology

Our data on individuals have been taken from UCI machine learning repository online from May 2008 to November 2010. The dataset includes 45,211 observations from a Portuguese retail bank for which it has dependent variables, whether the prospect subscribes to a term deposit or not, and the independent variables are listed below.

### Feature List

| Feature    | Description                                                                                           |
|------------|-------------------------------------------------------------------------------------------------------|
| Age        | Age of the customer (numeric)                                                                         |
| Job        | Type of job (categorical)                                                                             |
| Marital    | Marital status (categorical)                                                                          |
| Education  | Educational level (categorical)                                                                       |
| Default    | Has credit in default? (categorical)                                                                  |
| Housing    | Has housing loan? (categorical)                                                                       |
| Loan       | Has personal loan? (categorical)                                                                      |
| Contact    | Contact communication type (categorical)                                                              |
| Month      | Last contact month of the year (categorical)                                                          |
| Day of Week| Last contact day of the week (categorical)                                                            |
| Duration   | Last contact duration, in seconds (numeric)                                                           |
| Campaign   | Number of contacts performed during this campaign and for this client (numeric, includes last contact) |
| Pdays      | Number of days that passed by after the client was last contacted from a previous campaign (numeric)   |
| Previous   | Number of contacts performed before this campaign and for this client (numeric)                       |
| Poutcome   | Outcome of the previous marketing campaign (categorical)                                              |
| Emp.var.rate| Employment variation rate - quarterly indicator (numeric)                                             |
| Cons.price.idx| Consumer price index - monthly indicator (numeric)                                                   |
| Cons.conf.idx| Consumer confidence index - monthly indicator (numeric)                                              |
| Euribor3m  | Euribor 3 month rate - daily indicator (numeric)                                                      |
| Nr.employed| Number of employees - quarterly indicator (numeric)                                                   |

## Bank Marketing Predictive Model

We use Python as a programming language utilizing the tools of Scikit-learn for our machine learning approach. We are employing the following classified algorithms: Logistic Regression, Decision Tree, Random Forest, and XGBoost for our prediction.

### Purpose

Our goal is to build a model to predict if a prospect will subscribe to a term deposit campaign. Using historical data, we built a model to predict future investors in bank term deposits in order to develop a targeted telemarketing strategy for the Bank of Portugal.

### Data Analysis and Coding Technicalities

We analyzed the data to determine the rate of subscribers per category within each feature. We used a loop function to calculate the percentage of subscribers from prospects contacted. We extracted a data set for each feature and the subscribed column. In the second part of the loop function, we plotted the results for each feature.

### Age

Seniors (ages 65 to 98) have a subscription rate three times as much as Older Adults (ages 56–65) and Young adults (ages 17–35). Middle Aged Adults (ages 36–65) have the lowest rate of subscription at 8.65%.

  <img src="assets/images/posts/2019/age.png" alt="Age">

### Occupation

Students and retired individuals were twice or three times more likely to subscribe than any other profession. Unemployed and administration professionals were the next highest group, ranging from 11.3% to 13% rate of subscribers, whereas the rest of the groups were less than 11.31%.

 <img src="assets/images/posts/2019/job.png" alt="Job">

### Method of Communication

The rate of subscription for people contacted by cellular phone is 10% higher than for those contacted on a regular phone.

 <img src="assets/images/posts/2019/contact.png" alt="Contact">

### Building Predictive Models

After data cleaning and exploration, We prepared the data for prediction using the following models: Logistic Regression, Decision Tree, Random Forest, and XGBoost. Since our data is unbalanced, with only 11% of individuals subscribing to a term deposit, we employed the Synthetic Minority Over-Sampling Technique (SMOTE-NC) on our training data. SMOTE-NC helps address the class imbalance by generating synthetic samples for the minority class, improving the performance of our models in predicting term deposit subscriptions.

 <img src="assets/images/posts/2019/smote.png" alt="SMOTE">

### Score and Pipeline Function

We built a function that captures the classified models, trains them, and produces the scoring results (Accuracy, Precious Recall, and F1_Score). We added an “if statement” with a display element to have the option to not display when unnecessary.

 <img src="assets/images/posts/2019/split.png" alt="Split">

We utilized a pipeline to streamline the necessary steps for data processing before implementing our predictive models. This pipeline was particularly beneficial during the data splitting process, ensuring that information from the training data did not leak into the unseen testing data.

Within the pipeline, we incorporated a function that allowed for looping when employing different classified models. Our dataset consisted of both numerical and categorical variables. To handle this, we separated the data into numerical and categorical subsets. The numerical subset underwent StandardScaler() transformation, while the categorical subset was encoded using OneHotEncoder() to convert it into a numerical format.

As the data passed through the pipeline, it underwent the necessary transformations, including StandardScaler() and OneHotEncoder(). The processed data was then used to train the model and generate predictive values for both the testing and training data. Finally, the model scores were calculated based on these predictions.

 <img src="assets/images/posts/2019/pipeline.png" alt="Pipeline">

### Hyperparameter Tuning

In this project, we placed a strong emphasis on the F1 score as it takes into consideration both false positive and false negative predictions. By doing so, we aimed to minimize the cost of pursuing leads that have little potential for a positive return on investment, as well as avoid missed opportunities to gain clients who are likely to subscribe to the term deposit campaign.

To optimize our model, we performed hyperparameter tuning on the Random Forest algorithm using GridSearch. The following parameter grid was used:

```python
param_grid_rf = {
    'model__n_estimators': [100, 300, 600, 900, 1200],
    'model__max_features': [2, 4, 6, 8, 10, 12, 14],
    'model__max_depth': [50, 100, 200],
    'model__criterion': ['gini', 'entropy']
}

grid_clf_rf = GridSearchCV(pipeline_rf, param_grid_rf, scoring='accuracy',
                           cv=3, n_jobs=-1, verbose=2)

GridSearchCV suggested the following criteria, which produced the following results:
{
    'model__criterion': 'gini',
    'model__max_depth': 200,
    'model__max_features': 14,
    'model__n_estimators': 900
}
```

### Resutls 

 ```
Training_Accuracy: 0.9960036496350365
Test_Accuracy: 0.8729356906936079
Precision: 0.8685113598591178
Recall: 0.8729356906936079
F1_Score: 0.8706234452833183
```
 <img src="assets/images/posts/2019/results.png" alt="Results">

The model generated the following features of importance:

 <img src="assets/images/posts/2019/features_imp.png" alt="Features_imp">



### Conclusions

In this project, we implemented data analysis and predictive classified models to predict term deposit subscriptions at a Portuguese banking institution. With an F1 Score of 0.871 using Random Forest, the following business recommendations are:

- Pay close attention to socioeconomic data, including the 3 Month Euribor rate and Consumer Confidence Index.
- Target telemarketing calls toward selecting individuals who belong to a specific age group and occupation. Seniors, Students, and Retired Individuals are more likely to subscribe to a term deposit.
- Conduct the campaign during specific months. March, September, and October have been shown to have a higher rate of subscriptions.

For more details, you can refer to the complete article and resources:

- [Bank Marketing Dataset - UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/bank+marketing)
- [Decision Support Systems, Elsevier, 62:22–31, June 2014](https://doi.org/10.1016/j.dss.2014.03.001)
- [Scikit-learn Pipeline Documentation](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.Pipeline.html)
- [Feature Importances in Sklearn Pipeline](https://stackoverflow.com/questions/38787612/how-to-extract-feature-importances-from-an-sklearn-pipeline)
- [Investopedia: Financial Instrument](https://www.investopedia.com/terms/f/financialinstrument.asp)


