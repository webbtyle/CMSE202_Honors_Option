# MLB Salary Prediction Model Report

# The Question

Question: Can we predict/estimate the future salary of an arbitration eligible player in MLB using past season performance metrics and other factors like age, experience, and more?

# Methods

First I cleaned all the data which was harder than I figured as there were a lot of variables that should've been floats where single characters were turning them to objects like commas or () in the salary columns. After cleaning I ran an inital Regression on the entire dataset to pick out the highest correlating factors and remove any unnecessary ones. That led to picking the top 3 highest performing factors being prev_salary, prev_WAR, and YOS. Next I ran the regression using just those three factors and realized there was the multicollinearity issue. I resolved that by scaling my salaries to be in millions (1 million vs 1000000) resulting in the low condition number and more normal coefficients. Then with my initial model working I ran a Train_Test_Split function from the sklearn library to split my original data into training and testing sets with an 80/20 split. Then with my split dataset I trained the model again with the three factors chosen before and the training dataset. With my new predictions from the training data I calculated the mean squared error (MSE) using the test_data and predictions with the Root Mean Squared Error (RMSE) coming out to approximately 1.2 Million $. With my RMSE calculated and my model trained I moved on to creating the more user-friendly predict_salary function. 

# Results

The predict_salary function takes inputs of prev_salary, prev_WAR, YOS, model, and RMSE and spits out both a straight predicted salary number as well as a range calculated using RMSE. After running it through a few real world trials with random Arbitration Eligible players from between 2011-2025 to match the parameters of the data my model was trained on I noticed a few different patterns. 

1. The model performs better when the previous and predicted salary < 10 Million
2. Even when a player posts a bad season (low WAR) the model has trouble predicting a decrease in salary in future years
3. The model tends to smooth over the possibility of big spikes in salary even when a player performs exceedingly well (high WAR)

# Discussion

I have a few theories that I think could explain the results above

1. As seen with the Actual vs. Predicted plot the model tends to undershoot any salaries above 10 Million which explains why it works better overall with salaries below 10 M
2. Because salary declines are rare in the training data, the model seems to have trouble identifying the factor values under which salary should decrease
3. Big increases in salary often depend on factors not explored in my model like contract re-negotiations, incentive, team budgets, players leverage in arbitration cases, etc. Since the dataset is mostly made up of players with more steady increases in salary its more biased towards predicting small changes and has trouble learning when jumps in WAR should or should not drastically affect Final Salary.

# Conclusion

This project demonstrates that a simple Linear Regression model using previous salary, previous WAR, and YOS can provide a decent estimate for future arbitration eligible player salaries. The model performs decently well for lower and mid range salaries but struggles in rare cases like salary declines and sharp increases between years. These limitations suggest that salary prediction in MLB arbitration requires more factors not represented in the current data. In the future if I were to continue this project I would look to add factors like talent disparity among different positions, team budgets, and other player performance metrics to get a more flexible model as well as test different regression methods. 