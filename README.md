# Uber-price-forecasting-by-ML
The project used machine learning KNN and Random forest to forecast Uber price based on contributing variables.
## I. Introduction
Ride share services have become increasingly popular in the past decade. Uber and Lyft are leading companies in this field. To keep up with demand and increase profitability, these companies use dynamic pricing to encourage more drivers to pick up requests and keep up with demand. The pricing is greatly affected by the demand and supply of rides at a given time, dates or weather condition. 

The uber company try to analyze the prices of these ride-sharing apps and try to figure out what factors are driving the demand and how to use them as input to forecast the price of each ride. 

This project implemented 2 machine learning techniques (Random forest and KNN) to analyse and make prediction to the ride based on contributing variables. 

**Analysing tool: Rapid Miner software.**

**Datasets: Ride share train and Ride share test**
## II. Data pre-processing
### 1. Import and clean data
The datasets were imported into Rapid Miner system before conducting some basic transformations: 
![image](https://github.com/mistletoegoegoe/Uber-price-forecasting-by-ML/assets/121160527/8879fee0-3064-4e13-9115-fc2dda5a9dd0)
- Set role: Assigned Price column as dependent variable and attributes of time (hour, day, month), location (destination, distance), weather as independent variables
- Normalisation: Normalised the contributing attributes so that all variables had the similar scale from 0 to 1.
- Remove correlated attributes: By setting the correlation threshold to 0.95, removed all attributes that have the correlation index below this level.- 
### 2. Calculate weight for each independent variable
## III. Model training
### 1. Random forest
#### Model implementation
#### Parameters optimisation
### 2. KNN
#### Model implementation
#### Parameters optimisation
## IV. Model Evaluation
