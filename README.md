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

**Cross validation is a technique used in machine learning to evaluate the performance of a model. It involves dividing the available data into multiple folds or subsets, using one of these folds as a validation set, and training the model on the remaining folds. Then, it helps to compare and select an appropriate model for the specific predictive modeling problem.**

**Cross Validation is also used in order to avoid model overfitting. The number of folds in this operator is kept at 10 as the optimal number.**

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

  ![image](https://github.com/mistletoegoegoe/Uber-price-forecasting-by-ML/assets/121160527/63ffa98d-c848-49f6-92c6-13cf7d73b564)


### 2. KNN
#### Model implementation
![image](https://github.com/mistletoegoegoe/Uber-price-forecasting-by-ML/assets/121160527/94f488fc-db48-4437-adf8-3af989748c90)

### Model interpretation: 
- The first line is to setup the training model, the second line is to test the model on test dataset.
- In the model, after transform the data by operators (Set Role, Select Relevant attributes, Filter non-missing values, Normalise, Remove correlated attributes), it passes the operator called Cross Validation.
- In the Cross validation, a model of KNN is set up (see the image below):
  ### The intially model's parameters selection
  ![image](https://github.com/mistletoegoegoe/Uber-price-forecasting-by-ML/assets/121160527/f62f87de-ab83-4e7f-8b2a-07fbc803658d)

 ### The model explanation:
  - A KNN model is implemented on training dataset.
  - Then, this model will use test dataset as the input to calculate the performance of the model.
  - The process will iterate several times by Cross validation technique to find out the most appropriate one.  
### 2. Parameters optimisation
Likewise the RF model, in this setup, Parameter optimisation are also utilised.
  ![image](https://github.com/mistletoegoegoe/Uber-price-forecasting-by-ML/assets/121160527/27284862-c126-4149-a1e0-d161a84ed9ba)

- To optimize parameters used in KNN model using Optimize parameter operator. In this step, the k value was chosen to be optimized. The k-value is set from 1 to 100 as the window below. The reason to choose this range to test k-value is that the maximum k is equal to the square root of the number of records in the train dataset.

  ![image](https://github.com/mistletoegoegoe/Uber-price-forecasting-by-ML/assets/121160527/b272c48b-4327-4c38-b57b-2cbb5bff1519)

- This is the result of running optimize operator with k-value:
  ![image](https://github.com/mistletoegoegoe/Uber-price-forecasting-by-ML/assets/121160527/79525e6e-867f-4ee1-9496-d2118cbc77ee)

## IV. Prediction and Model Evaluation
### 1. KNN Prediction
![image](https://github.com/mistletoegoegoe/Uber-price-forecasting-by-ML/assets/121160527/7ab6fab4-5a97-42fe-8c8f-6b75de352c41)

The chart of actual price and predicted price after KNN model: 

![image](https://github.com/mistletoegoegoe/Uber-price-forecasting-by-ML/assets/121160527/ec81ad8a-26c8-40a9-8918-cbb4aa88d23a)


### 2. Random forest Prediction
The prediction of Price after running Random Forest model:
![image](https://github.com/mistletoegoegoe/Uber-price-forecasting-by-ML/assets/121160527/23cc94ee-d2b9-44ec-abb8-308a5384b4d1)

The chart of actual price and predicted price after Random Forest model: 

![image](https://github.com/mistletoegoegoe/Uber-price-forecasting-by-ML/assets/121160527/874a13b5-fd28-462f-aeff-14b09d835aec)

### 3. Models comparison
In this project, Root mean square error (RMSE) and mean absolute error (MAE), Mean relative error (MRE) and Mean square error (MSE) are used as performance indicators for models prediction.

The table of RMSE, MAE< MRE, MSE of RF and KNN models: 

  |               | RMSE  | MAE             | MRE               | MSE                |
|---------------|-------|-----------------|-------------------|--------------------|
| KNN           | 8.863 | 7.127 +/- 5.269 | 56.52% +/- 58.11% | 78.558 +/- 143.483 |
| Random Forest | 8.554 |  7.025+/- 4.881 | 56.86% +/- 59.01% | 73.719 +/- 98.361  |

#### Result interpretations: 
-	Root Mean Square Error: The KNN model (8.863) is slightly higher than Random Forest (8.554). It is the one sign which indicates that Random Forest performs better than KNN in predicting the label variable. 
-	Mean absolute error: This metric is quite similar in both models. In addition, the fluctuations of this measure are large for both, specifically 7.025  for Random Forest and 7.127 for KNN. This indicates that the variation between actual price and predicted price is quite far in general. Thus, the performance of both models is not very good in prediction of the independent variable. However, the Random Forest is a little lower than KNN.
-	Mean Relative Error: The mean relative error in both models is around 56-57%. This number is quite high for a machine learning model performance. Thus, the conclusion can be drawn from this indication is that both models did not do well in prediction task. However, the uncertainty in MRE is also high (+/- 59.01% and +/- 58.01% for Random Forest and KNN model, respectively). That indicates both these models are not persistently predicting. Some records might be very close predictions, some might be not. 
-	Mean Square error: Random Forest has a lower MSE than KNN (73.719 and 78.558, respectively), meaning that it is more accurate in predicting the price. However, the standard deviation for both are large (143.483 for KNN model, and 98.361 for Random Forest model), which indicates that these models did not do the prediction stably. They can predict very closely, however, in some cases, they can do it very badly. 

In conclusion, it can be seen that Random forest performs better than KNN in price prediction task. However, both models still have many errors. Therefore, if we need to choose one between them, Random forest will be a better choice.  

