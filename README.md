# Stock Prediction of ingredients for Maven Pizzas

## Project Description
In this project we aim to predict the stock of the next week for the Maven Pizzas shop. For that, we have a dataset with 
every pizza sold in 2015, and the ingredients used in each pizza.  
To adjust the problem to reality, we'll try to predict the stock for a week, using data only until a number of days before.
If they need to make the order of ingredients on Thursday, we'll only use data until that day.

## DATA:
- We clean the data and make a data quality report in [pizzas_2015.ipynb](pizzas_2015.ipynb)

## PREDICTION:
- We'll use a XGBoost Regressor to predict the stock of each ingredient each day of the week.
- Then we'll find a margin of error for each ingredient (the mean absolute error) and add it to overestimate the stock
of that day just enough to avoid running out of ingredients.
- Finally we'll sum up all the ingredients and margins of each day of the week to get the total stock for the week.
- Predictions are made in [predict_ingredients_2015.ipynb](predict_ingredients_2015.ipynb)

## ETL:
- We automate this task with Airflow and Docker. Every day it triggers a DAG that
picks the current day, extracts the data and the model, makes a prediction and outputs it 
in csv format into the io/ folder.
- It simulates as if the year were 2015, picking the current day and month and changing the year to 2015.
- The DAG is in [dags/predict_2015_tag.py](dags/predict_ingredients.py)

## To Run:
    > docker-compose up --build
    > docker-compose start (if it's already built)