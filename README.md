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
- Remove correlated attributes: By setting the correlation threshold to 0.95, removed all attributes that have the correlation index below this level.
- Data type transformation: Changed Price from Numeric to Polynomial because the function to calculate the weight of contributing attributes does not work with Numeric data (details in next part).
### 2. Calculate weight for each independent variable
- Function used: Weight by Information Gain to identify the extent of independent variables' contribution to the value of dependent variable.
![image](https://github.com/mistletoegoegoe/Uber-price-forecasting-by-ML/assets/121160527/5290a66c-4e83-413d-8cac-270dbbaff4af)
- Result:
  
  ![image](https://github.com/mistletoegoegoe/Uber-price-forecasting-by-ML/assets/121160527/2e2557ed-12b3-44a2-9412-b72e2523b65f)
## III. Model training
### 1. Random forest
#### Model implementation
![image](https://github.com/mistletoegoegoe/Uber-price-forecasting-by-ML/assets/121160527/e1e4b63c-8466-4a5c-ab0c-67158592f073)
### Model interpretation: 
- The first line is to setup the training model, the second line is to test the model on test dataset.
- In the model, after transform the data by operators (Set Role, Select Relevant attributes, Filter non-missing values, Normalise, Remove correlated attributes), it passes the operator called Cross Validation.

Cross validation is a technique used in machine learning to evaluate the performance of a model. It involves dividing the available data into multiple folds or subsets, using one of these folds as a validation set, and training the model on the remaining folds. Then, it helps to compare and select an appropriate model for the specific predictive modeling problem.

Che Cross Validation is also used in order to avoid model overfitting. The number of folds in this operator is kept at 10 as the optimal number.

- In the Cross validation, a model of Random Forest is set up (see the image below):
  ![image](https://github.com/mistletoegoegoe/Uber-price-forecasting-by-ML/assets/121160527/5c2b0e40-f86e-4d04-8493-c1f94aecc0ca)
  ### The intially model's parameters selection
  ![image](https://github.com/mistletoegoegoe/Uber-price-forecasting-by-ML/assets/121160527/875e7a73-4461-40c0-95b7-db77c03d4e0c)

  ### The model explanation:
  - A RF model is implemented on training dataset.
  - Then, this model will use test dataset as the input to calculate the performance of the model.
  - The process will iterate several times by Cross validation technique to find out the most appropriate one.
### 2. Parameters optimisation
-	Optimize Parameters operator to choose the optimal parameters for Random Forest model (number of trees and maximal depth). In this step, the maximal depth and minimal gain of the decision tree model were chosen to be optimized. In the Optimize parameter window, the parameters settings were set up as below.

 	![image](https://github.com/mistletoegoegoe/Uber-price-forecasting-by-ML/assets/121160527/5270cc3a-d86d-4a26-b9f5-5aba6f5445e9)

 	![image](https://github.com/mistletoegoegoe/Uber-price-forecasting-by-ML/assets/121160527/e80c0a4a-d97d-4c11-b596-2666071803a2)

- The final result after comparing those ranges is that the optimal combination of maximal depth and the number of trees is 70 and 9. Thus, these parameters are used to train the model.
  
  ![image](https://github.com/mistletoegoegoe/Uber-price-forecasting-by-ML/assets/121160527/0046d573-ff42-4be7-a277-0be057743d40)


### 2. KNN
#### Model implementation
#### Parameters optimisation
## IV. Model Evaluation
