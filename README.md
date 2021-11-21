# Problem Statement
You are working as a data scientist with HR Department of a large insurance company focused on sales team attrition. Insurance sales teams help insurance companies generate new business by contacting potential customers and selling one or more types of insurance. The department generally sees high attrition and thus staffing becomes a crucial aspect.

To aid staffing, you are provided with the monthly information for a segment of employees for 2016 and 2017 and tasked to predict whether a current employee will be leaving the organization in the upcoming two quarters (01 Jan 2018 - 01 July 2018) or not, given:
  1. Demographics of the employee (city, age, gender etc.)
  2. Tenure information (joining date, Last Date)
  3. Historical data regarding the performance of the employee (Quarterly rating, Monthly business acquired, designation, salary)

Private Leaderboard Rank - 1 </br>
Public Leaderboard Rank - 3

# Approach
Formulating the problem into a Machine Learning and transforming the data was the most challenging part. A snapshot of the data is provided under

![image](https://user-images.githubusercontent.com/19322337/142776001-aba1421a-c20a-4758-83bf-14bf91c62c6a.png)

As the objective was to predict if an employee will leave the organization in the upcoming two quarters, the target variable was taken such that if an employee leaves the organization within 180 days of review it was taken was 1 and 0 otherwise i.e., if the last working day is 25-11-2017 and a review was conducted on 01-05-2017(208 days prior), target would be 0 and for the next review conducted on 01-06-2017(177 days prior), the target would be 1. The training data was taken only till 01-08-2017 as a full 180 days was required for prediction. The predictions had to be done at review level for each employee otherwise there would not be sufficient data and the changes in employee performace/behaviour might be difficult to catch if data was minimized to one row per employee.

# Feature Engineering

A total of 21 features were engineered and 9 were used from the initial data provided. The basic idea behind the feature engineering was that the following factors affected the churn of an employee:
  1. Months since employee joined and changes in salary/designation throughout (more recent would cause churn)
  2. The cumulative salary earned and the cumulative business value and relation between these
  3. Change in quarterly ratings and mean rating over time
  4. Average tenure/salary of employees in a particular city, education level and gender
  5. Male/Female ratio and their average ages

# Model Building

CatBoost algorithm was used along with 5 fold stratified sampling. Using optuna to tune hyperparameters resulted in ovefitting due to scarcity in data. Hence, did not use any hyperparameters. The evaluation metric used was F1 score.

# Model Selection

One of the most important aspect was to choose the model for the final submission. There were instances when my local score would increase but the score on the public leaderboard would decrease. However, I did trust my local score and go with the one that gave me a good local score (I also had to take into consideration where I had got high local scores due to overfitting and not select those submissions). I ended up selected a submission which gave me a local score of 0.7914 and public score of 0.7219 which gave a private score of 0.75059 over a submission which gave me a local score of 0.78399 and a public score of 0.7292 which would have given me a private score of 0.7417 resulting in dropping a couple of places in the private leaderboard.
