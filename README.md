# Sparkify Capstone Project

## Table of Contents
- [Introduction](#introduction)
- [Scope](#scope)
- [Datasets](#datasets)
- [Technologies](#technologies)
- [Outcome](#outcome)
- [Resources](#resources)

## Introduction:
This project focuses on a music streaming application called "Sparkify."  
We have a dataset that provides information about users and their activities within the app.  
In this project, we will work with a subset of the data to explore various features and develop a machine learning model to predict user churn.  
The goal is to understand user behavior and build a model that can identify users at risk of leaving the app.

## Scope:
In this project, we aim to predict user churn based on the dataset.  
Churn is defined as the event when a user submits a "Cancellation Confirmation" request.  
By predicting which users are likely to churn, we can identify the key factors that contribute to their decision to leave the app.  
This understanding will allow us to implement strategies to reduce churn, such as offering personalized promotions or incentives to users identified as at-risk.  
The ultimate goal is to retain more users and improve overall engagement with the app.

This repository contains the following files:
- **Sparkify.ipynb**: The notebook containing the code used for analysis and building the model.

## Datasets:
The dataset includes the following fields:

- **ts**: Timestamp, when this event was recorded in milliseconds
- **userId**: Unique identifier for each user
- **firstname**: First name of user
- **lastname**: Last name of user
- **location**: City
- **gender**: "F" for female, "M" for male
- **registration**: Timestamp of subscription
- **level**: "free" or "paid"
- **page**: Webpage visited, or button clicked
- **method**: HTTP Method "GET" or "POST"
- **status**: HTTP Response Code "200", "307", "404"
- **userAgent**: Browser and operating system used
- **sessionId**: Session events
- **auth**: Current status of authentication "Logged In", "Logged Out"
- **song**: Title of song
- **length**: Length of song in seconds
- **artist**: Artist performing the song

## Technologies:

- **PySpark** version: 3.5.0
- **regex** version: 2.2.1
- **numpy** version: 1.26.3
- **pandas** version: 2.1.4
- **matplotlib** version: 3.8.2
- **seaborn** version: 0.13.1

These libraries provided the necessary tools for data processing, machine learning model building, evaluation, and visualization of results.

## Outcome:

### Model Evaluation and Prediction Results

#### Dataset Overview:
The model was trained on user activity data, including features like "Help," "Downgrade," "Error," and various others. The goal was to predict whether a user would churn, with the target variable being "Churn."

#### Data Split:
- **Training set**: 70%
- **Validation set**: 15%
- **Test set**: 15%

### Model Performance:

1. **Gradient Boosting (GBT)**:
    - **F1 Score on Validation**: 0.70  
    Although it performed decently, the F1 score is not the best compared to other models.

2. **Random Forest (RF)**:
    - **F1 Score on Validation**: 0.86  
    - **Best RF Model after Hyperparameter Tuning (Grid Search)**:
        - **F1 Score**: 0.82
    - **Final Test Set F1 Score**: 79.39%
    
    - **Confusion Matrix**:
        ```
        [[20.  0. ]
         [ 4.  1. ]]
        ```
    This model performed the best overall, with a high F1 score, demonstrating its ability to balance precision and recall effectively. The confusion matrix shows that it identified 1 churned user correctly but misclassified 4 others as not churned.

3. **Decision Tree (DT)**:
    - **F1 Score on Validation**: 0.72  
    The decision tree was also a strong contender, but it did not outperform the random forest.

### Feature Importance (for Random Forest):
The most important features for predicting churn are:
- **max(registration_ts_diff_days)** (Importance: 0.258)
- **avg(length)** (Importance: 0.105)
- **Thumbs Down** (Importance: 0.096)
- **Thumbs Up** (Importance: 0.088)
- **count(DISTINCT sessionId)** (Importance: 0.079)

These features had the most influence on the model’s predictions, with user engagement metrics (e.g., session length and thumbs up/down) and registration-related metrics being the key contributors.

### Conclusion:
The **Random Forest model** with hyperparameter tuning is the best model for predicting churn in this case, yielding a **final F1 score of 79.39%** on the test set. The **max(registration_ts_diff_days)** feature played the most important role in this prediction.

Moving forward, we can further tune the model or incorporate additional features for even better performance. However, based on current results, the Random Forest model is the most reliable for churn prediction.

## Resources:
Blog link: [Sparkify Churn Prediction Project](https://medium.com/@shadynayel/sparkify-churn-prediction-project-0d4f191a3e91)