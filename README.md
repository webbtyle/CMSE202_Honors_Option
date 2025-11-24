# CMSE202_Honors_Option
This project builds a linear regression model to predict an MLB player’s next-season salary (in millions). The model uses three inputs:

Previous Salary
Previous Season WAR
Years of Service (YOS)

# Model Steps

1. Pre-process data:

Ensure all values used in the model are numeric (float or int).
Convert all salary values to a millions scale:

model_FS['PrevSalary_mil'] = model_FS['PrevSalary_updated'] / 1e6 \
model_FS['FinalSalary_mil'] = model_FS['FinalSalary_Updated'] / 1e6

2. Train_Test_Split the data using an 80/20 ratio and fit to an OLS regression model.
   
3. Evaluate model accuracy using MSE and RMSE on the test set. RMSE is used later when computing the salary prediction range.

4. Run the notebook from top to bottom, or run only:

Import cells
Data cleaning cells
MLB Salary Prediction Function cell

(Cells 1, 2, and 7)

# Prediction Function

Predicts a players given year salary and range (In Millions $) based on RMSE.

Parameters:
prev_salary_mil : (float) - Previous Salary in millions
war_prev : (float) - Previous season WAR
yos : (float) - Years of Service in YYDDD format 
model : Fitted OLS Regression Model
rmse : (float) - Model Calculated RMSE for Range Calculation

Example Usage
predict_salary(prev_salary_mil, war_prev, yos, model, rmse)
predict_salary(3.5, 2.06, 4.015, Millions_Salary_Model, rmse)

Example Output
Predicted Salary: 5.518 (In Millions $)
Salary Range: 4.318 - 6.718 (In Millions $)





