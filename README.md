# Use regression tree models to predict sales 
## Business Problem: Using data about several different attributes of grocery stores and supermarkets, predict the total sales generated by the stores 

**Author: Jacob Wang**

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

