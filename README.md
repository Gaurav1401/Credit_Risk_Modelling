# Credit_Risk_Modelling

## Scorecard Model
**Monotonic binning** was done to calculate **WOE(Weight of Evidence)** values for the continuous variables using Pymob library. In order to understand the predictive power and each variable
and later **Information value(IV)** was also calculated by summing up the WOE values of all the bins for feature selsction purpose. <br>

**How to calculate WOE and IV:**
 - WOE = ln(%Y / %Obs)
 - IV = ∑((%Y- %Obs) * WOE)

**Steps to calculate WOE and IV:**
 - Split Continuous Independent Variable (x) into 10 or 20 buckets (call variable 'rank'). If you have categorical independent variable, you don't need to split as they are already categorized.
 - Calculate min and max of x by rank. Compute sum of target variable (y) by rank. Let’s name it as ‘SumY’.
 - Calculate total count and % of observations falling in each bucket of rank variable.
 - Calculate %Y which is calculated by SumY / ∑SumY.
 - WOE = ln(%Y / %Obs). %Obs represents percentage of observations (calculated in step 3)
 - IV = ∑((%Y- %Obs) * WOE) 
 

**Advantages of using WOE values**
 - It creates a separate bin for missing values ,i.e, imputation is not required.
 - It can easily treat outliers as the values get binned.
 
### Multicollinearity Detection
**Variance Inflation Factor (VIF)** was used to detect the multicollinearity among the independent variables. 
**Conclusion:** Multicollinearity did not exist among continuous variables.


**Logistic regression** model was used to calculate the probbability of the target variable which were later used to calculate the final **Credit Score**

## Tree Models

In order to implement Tree Models like **Decision Tree and Random Forest**, separate data preprocessing was done, since WOE values can't be used with such models.

### Missing value imputation
3000 records were having missing values of **loan_int_rate**, since loan_int_rate was dependent on **loan_grade**, so for each loan_grade median loan_int_rate was calculated and values were imputed accordingly.
Other missing value records were just dropped.

### Next Steps
Feature Encoding, Train Test Split and Hyperparameter Tuning using GridSearchCV was done on the dataset and model.

## Performance Metrics
 - **KS statistic:** It basically measures the degree of separation between the CDF’s of  two classes.
 - **ROC AUC:** It just gives the measurement of the area under the ROC curve made from predictions.
 - **Recall Score:** It basically tells proportion of correctly classified positives out of total positives.
 - **F1 Score:** It is just the weighted average of precision and recall.
 - **Capture rate:** It is the proportion of actual positives in each bin. Predicted probabilities are sorted and divided into 10 bins. A Good model shows staircase pattern from top to bottom in case of capture rate

## Results

**Logistic Regression (Using WOE)**
| Metric | Train    | Test    |
| :---:   | :---: | :---: |
| KS | 60.6   | 60.8   |
| ROC AUC | 0.74   | 0.73   |
| Capture Rate (10%) | 37.07   | 36.8   |
| Capture Rate (20%) | 62.97   | 62.1   |
| Recall | 0.534   | 0.52   |
| F1 Score | 0.62   | 0.61   |

**Decision Tree**
| Metric | Train    | Test    |
| :---:   | :---: | :---: |
| KS | 68.7   | 66.5   |
| ROC AUC | 0.85   | 0.84   |
| Capture Rate (10%) | 46.33  | 46.3   |
| Capture Rate (20%) | 73.9   | 72.2   |
| Recall | 0.76   | 0.75   |
| F1 Score | 0.75   | 0.74   |

**Random Forest**
| Metric | Train    | Test    |
| :---:   | :---: | :---: |
| KS | 64.2   | 62.8   |
| ROC AUC | 0.788   | 0.79   |
| Capture Rate (10%) | 43.65  | 44   |
| Capture Rate (20%) | 68.78   | 68.1   |
| Recall | 0.615   | 0.62   |
| F1 Score | 0.7   | 0.7   |
