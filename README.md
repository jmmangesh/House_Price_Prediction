## House Price Prediction for Snohomish County, WA

Residential property sales in the Snohomish County (Washington) are public and offer useful information of the housing features via FTP Portal `ftp://ftp.snoco.org/assessor/property_sales/`. The **objective** of this exercise is to predict the continuous output variable i.e. **Sale Price of Single-Family Houses in Snohomish County, WA** using the categorical and numerical features available in property sale dataset. The raw dataset had 104k sales records with 51 columns spanning across 5+ years. After de-duplicating and outlier removal the processed dataset had: 45k records and 10 features. 1.5k property sale records (with sales in May-2021 onwards) were used in testing the accuracy of the predictions. 

For simplifying and **automating the feature processing and model training**, I’ve used **AutoGluon**. Using this feature, I’ve set the training time limit to 3 minutes. For evaluation, I’ve converted the **Sale Price to log 10 values**. This will make sure model training treats the prediction errors for high priced houses similar to low priced houses. For regression task, the evaluation function is set to **Mean Squared Error**. During 3 minutes AutoGluon evaluated 11 models and chose **WeightedEnsemble_L2** as the best performing one based on the score_val. If we need to reduce the prediction time, then **XGBoost** would give similar accuracy in lower time.
Converting the Log Values back to normal Sale Prices, and the accuracy of prediction of a known datapoint was ~8%. And the overall RMSE for Log Values was 0.08. Below are the key **features ranked by their importance** (with significant P-Values):
  1.	**Built Area** of the House in Sq. Ft.
  2. **Grade or Quality** of the House
  3. 	**School District**

In the correlation analysis **Bedrooms** had higher correlation coefficient of 0.45 with Sale Price. However, Bedrooms also had a high correlation of 0.61 with Built Area. And can cause high-collinearity. Thus, the importance of Bedrooms is lower.

Surprisingly, the **Sale Year** was NOT significant or important in prediction. This seems contrary to the +20% YoY market trend in Snohomish County. I think this is probably due to the fact that **historical sale price values are not adjusted for the appreciation**. To verify this logic, if we plot Price/Built Sq. Ft across years, then we can see that overall real estate prices have gone up with each year.
