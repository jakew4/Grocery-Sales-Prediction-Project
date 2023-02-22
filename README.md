# Grocery Sales Prediction Project
## Business Problem: Using data about several different attributes of grocery stores and supermarkets, predict the total sales generated by the stores 

* Author: **Jacob Wang**
* **Coding Dojo Data Science Project 1**

## Data: 
* Variable Name	Description
* Item_Identifier	- Unique product ID
* Item_Weight	- Weight of product
* Item_Fat_Content	- Whether the product is low fat or regular
* Item_Visibility	- The percentage of total display area of all products in a store allocated to the particular product
* Item_Type	- The category to which the product belongs
* Item_MRP - Maximum Retail Price (list price) of the product (in rupees)
* Outlet_Identifier -	Unique store ID
* Outlet_Establishment_Year	- The year in which store was established
* Outlet_Size	- The size of the store in terms of ground area covered
* Outlet_Location_Type -	The type of area in which the store is located
* Outlet_Type	- Whether the outlet is a grocery store or some sort of supermarket
* Item_Outlet_Sales	- Sales of the product in the particular store. This is the target variable to be predicted.

## Methods: 
* Cleaned data by removing duplicates, imputing missing values, and correcting any inconsistencies in categorical data 
* Prepared exploratory/explanatory graphs to further analyze data and visualize different trends in the data
* Preprocessed and prepared data for machine learning models 

## Results: 
### Item MRP vs. Total Sales (by outlet type)
![salesPredGraph1 (1)](https://user-images.githubusercontent.com/112730629/197611411-15bd389d-1bbc-43c5-bcfd-628dda9db811.png)
> As can be expected, Item MRP certainly has a direct effect on total sales. Higher item prices equate to higher sales. In addition, the type of outlet also influences sales. As the outlet type increases in size, so do total sales. 

### Outlet Sales and Outlet Establishment Year
![salesVsYeargraph](https://user-images.githubusercontent.com/112730629/197611672-5bed9627-8ada-4f5c-b853-53428f21beee.png)
> According to this graph, the most profitable outlet location is also the oldest, having been established in 1985. There was little variation in outlet sales other than what looks like around 1997, when outlet sales dipped below 500.

### Linear Regression Feature Coefficents
![top3coeffs](https://user-images.githubusercontent.com/112730629/214708538-5423f8ea-fb7b-49e3-a668-ee5558cc0a8f.png)
* Our top 3 most impactful features were Outlet_Type_Grocery_Store, Outlet_Type_SupermarketType3 and Outlet_Type_SupermarketType1
* Basically, the type of outlet/store determined the sales of that establishment.
* If the outlet/store type was a grocery store, sales would typically drop by 1500.
* If the store was a Supermarket Type3, sales would increase by 1500.
* Type1 typically increased sales by around 250.
* (currency is Rupees)

### RandomForest Feature Importances
![most5importances](https://user-images.githubusercontent.com/112730629/214708777-d62908bf-f3f4-4133-825b-b2355d0ff271.png)
* The 5 features graphed above had the most impact on outlet sales according to the RandomForest. Item_MRP had the most impact, followed by whether or not the store was a grocery store. Item_Weight also was in the top 5 most important features for determining sales.

### SHAP Summary Plots
![sumPlot_bar](https://user-images.githubusercontent.com/112730629/215018388-b6ab51f8-7a8e-47dd-b566-9a675cb4a928.png)
* Many of the same features are found in both the RandomForest feature importance graph and the SHAP summary bar plot.
* The only variation in the top 5 is that the feature importances include Item_Type_Household as the 4th most impactful feature.
  * In contrast, the SHAP importances include Item_Visibilty as the 3rd most impactful feature and does not include Item_Type_Household
* The feature importances also have Supermarket_Type3 ranked higher
  * While Supermarket_Type3 is also present in the top 5 SHAP importances, it is the 4th most important

### SHAP Dot Plot
![sumplot_dot](https://user-images.githubusercontent.com/112730629/215018607-46c72a11-0bd0-417a-93eb-5aacc66ffbbf.png)
* According to our dot plot the Item_MRP is our most impactful feature and very highly correlated with sales.
  * The higher the MRP, the higher the target value (outlet sales)
  * If Item_MRP decreases, so does outlet sales
* The next most impactful feature is whether or not the store in question is a grocery store.
  * If it is, sales are expected to drop dramatically. If not, then sales will likely increase.
* Our 3rd most impactful feature is whether or not the store is a Supermarket Type3.
  * Supermarkets (and especially those that are type3) produce much higher sales than grocery stores.

### SHAP Force Plots
#### High Sales Example
![shap_max_sales](https://user-images.githubusercontent.com/112730629/215221592-4cca4f9e-6d66-47d5-9512-46fc881caa44.png)
* According to our force plot, the base value for sales is 2,156 rupees.
* The store sales for this particular example is 8,422.74 rupees.
* The most influential factors that contributed to increasing store sales were the Item_MRP, the fact that the store was a Supermarket Type3, and that it was NOT a grocery store.
 * The Item_MRP for this example was one of the highest item price values we have (260.6)
  * The max Item_MRP was 264.72

#### Low Sales Example
![shap_low_sales](https://user-images.githubusercontent.com/112730629/215221726-93908852-ea18-44c1-8d2d-4b78131365eb.png)
* This example yielded an expected sales value close to the lowest observed sales amount
* The fact that the store was a grocery store and that the Item_MRP was one of the lowest contributed the most to the low sales value

### LIME Local Explanations
#### High Sales Example
![lime_max_sales](https://user-images.githubusercontent.com/112730629/215221801-4214970f-565f-42b8-a445-8213a142f91b.png)
* According to our LIME Explanation, the most important feature that contributed to our model's prediction was that the store in question was NOT a grocery store.
* The Item_MRP was the second most influential feature - this makes sense as a higher MRP typically yielded higher sales
 * Our expected sales value (8,422.74) is one of the higher store sales amounts
* The store being a Supermarket Type3 also contributed heavily to the high sales value

#### Low Sales Example
![lime_low_sales](https://user-images.githubusercontent.com/112730629/215221844-7914206b-5852-4db2-b69b-a29a69c0b8c4.png)
* Our LIME explanations very closely mirror information from the SHAP Force plots
* According to our LIME Explanation, the example in question returned such a low sales value mainly because the store was a grocery store.
* The Item_MRP value being close to the minimum value observed also contributed heavily to the low sales amount
* The fact that the store in question was NOT a Supermarket Type3 was also very influential in the model's prediction




## Model
* Tested both linear regression and regression tree models. 
* Regression tree model returned much better regression metrics 
* * R2 scores - training: 0.54
*             - testing: 0.48
* * RMSE score - training: 136.78
*              - testing : 1667.62

## Recommendations: 
The business should proceed with the regression tree model to predict sales. The R2 scores imply that the model can explain roughly 50% of the variation in sales. The RMSE scores suggest that while the average error of the model is relatively high, they are still much lower than the RMSE scores of the linear regression model. 

### For futher information:
For any additional questions, please contact **jacob.wang0@gmail.com**

