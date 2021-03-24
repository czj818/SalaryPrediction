# Salary Prediction For Better Compensation Strategy

## Introduction


Employee retention is an important task for HR/Talent Acquisition Team. One of the solution is to offer competitive salaries to employees. 	The mean or median of the salary are not good enough to indicate the actual salary because people with more years of experiences might deserve more. The salary prediction model gives a better idea to talent acquisition team of  the amount of compensation people deserve. The dataset includes features such as company Id, Job Type, Education level, Major, Industry, years of experience, miles from Metropolis and the corresponding salary. This model not only predicts employees's salaries but also gives the important factors that determine the salary.

![Alt text](https://www.moneyunder30.com/wp-content/uploads/2016/08/114__best-salary-information-websites-648x364-c-default.jpg)

The training dataset contains 1M records.
There are total of 9 attributes in the dataset and salary is our dependent variable:

- jobId: Unique job identifier for each job posting.
- companyId: Company this posting belongs to. There are total of 63 companies.
- jobType: Type of the job, such as Vice President or Janitor.
- degree: Educational degree, such as high school or masters.
- major: Majored in, such as none or business.
- industry: Which industry this job will be performed in, such as health or oil.
- yearsExperience: In years, range between 0 and 24 years.
- milesFromMetropolis: Distance from a metro area.
- salary: In U.S dollars, and reported in 1000s.


## Exploratory Data Analysis

First, let's look at the statistical metrics for salary. The median salary is \$114,000,  the mean is \$116,0618 and the maximum salary is \$301,000. From the box plot below, there are many salaries exceed the upper bound of IQR. However, these are legitimate data after examination, not outliers. The distribution plot shows a slightly skewed distribution with a longer right tail.

![Alt Text](https://github.com/czj818/SalaryPrediction/blob/main/image/box:hist.png)

### Degree V.S. Salary

According to the box plot of salaries for different education levels, it is apparent that with or without a college degree is associated with the salaries. Without a college degree, people are more difficult to have a high salary job compare to those who have a college degree.  The median of the salary increases as the education degree goes up.

![Alt Text](https://github.com/czj818/SalaryPrediction/blob/main/image/degree.png)

### Salaries for different Job Types in different industry

After ranked job types from Janitor to CEO, the trend that the higher job type level leads to the higher compensation is obvious. Furthermore, the oil and finance industries give better compensations than other industries for the same job type. For example, oil and finance give the highest median salary to janitor position, even higher than the 75 percentile salary in Auto, Education and Service industry.
 
 ![Alt Text](https://github.com/czj818/SalaryPrediction/blob/main/image/industry.png)
 
 ### Salaries for different Majors in different industry
 
Web, Finance and Oil industry give higher salaries to engineering, math and business major students.  The Education, Service and Auto industries seems have similar salaries to different major employees. Intuitively, healthcare industry pays more to chemistry and biological students. None major students are less paid, might because they do not have a college degree.
 
 ![Alt Text](https://github.com/czj818/SalaryPrediction/blob/main/image/major.png)

### Work Experience \& Miles from Metropolis

Intuitively, the more work experience people have the more they get paid. There is a positive correlation showed below. The line represents the mean salary and the opaque area represent the 1 standard deviation area.

The plot on the left shows a negative correlation between miles from metropolis and salaries. People in metropolis area tend to have higher salaries because of the higher living cost compare to rural area.

 ![Alt Text](https://github.com/czj818/SalaryPrediction/blob/main/image/exp.png) |  ![Alt Text](https://github.com/czj818/SalaryPrediction/blob/main/image/metro.png)
 
 ### Correlation Heatmap
 
 Gives a general idea of correlations between variables. The degree is highly associated with major, might need to consider the VIF if collinearity happens.
 
 ![Alt Text](https://github.com/czj818/SalaryPrediction/blob/main/image/corr.png)
 
 ## Models
 
 ### Preprocessing
 
 Because 5 categorical variables and two of them job type and degree have level scale inherently, I used ordinal encoding (label encoding) for job type and degree, and one hot encoding for the rest. I used median of salary to impute the missing value and a robust scaler because the data has some extreme data-points.
 
 ### Models
 
 - Linear Regression
 - Principle Analysis Component + Linear Regression
 - Random Forest
 - Gradient Boosting
 - XGBoost
 
 I used 2-fold cross validation and selected the one with the lowest Mean Squared Error. 
 
 ### Best Model
 
 The best model is the xgboost with 355 MSE.
 
 ### Feature Importance
 Here I select the top five key features that affect the prediction of salary the most.
 The most important factor in determine salary is job type. almost twice as important as the second factor. Other important factors include major_NONE, years of experience, degree, and industry_education.
 
  ![Alt Text](https://github.com/czj818/SalaryPrediction/blob/main/important_features.png)
 
 