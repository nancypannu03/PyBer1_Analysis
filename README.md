# PyBer_Analysis
## Overview
- In this Project, we will assist Maria in performing certain Pandas functions with Python language to collect, clean and represent the data. We will be using functions of Pandas library such as groupby, isnull(), dropna(), duplicated(), etc, to clean and organize the data. And handover Maria a better representation of the given data.
## Student_Data_Challenge_Code

[Student Data Challenger Code](Student_Data_Challenge_Starter_Code/Student_Data_Challenge_Starter_Code.ipynb) <br/>

### Import required dependencies
 import pandas as pd
 
 import os

### Deliverable 1: Collect the Data

#### Create the path and import the data
full_student_data = os.path.join('../Resources/new_full_student_data.csv')

student_df = pd.read_csv(full_student_data)

#### Verify that the data was properly imported
student_df.head()

### Deliverable 2: Prepare the Data

#### Check for null values
student_df.isnull()

#### Drop rows with null values and verify removal
student_df.isnull().sum()

student_df=student_df.dropna()

student_df.isnull().sum()

#### Check for duplicated rows
student_df.duplicated().sum()


#### Drop duplicated rows and verify removal
student_df= student_df.drop_duplicates()

student_df.duplicated().sum()


#### Check data types

student_df.dtypes

dtype: object

#### Examine the grade column to understand why it is not an int
student_df['grade']

#### Remove the non-numeric characters and verify the contents of the column
​
student_df['grade'] = student_df['grade'].str.replace('th', '')

student_df['grade']
​
student_df['grade'] = student_df['grade'].astype(int)
student_df.dtypes

### Deliverable 3: Summarize the Data

#### Display summary statistics for the DataFrame
student_df.describe()

#### Display the mean math score using the mean function
student_df['math_score'].mean()

#### Store the minimum reading score as min_reading_score
min_reading_score = student_df['reading_score'].min()
min_reading_score

### Deliverable 4: Drill Down into the Data

#### Use loc to display the grade column
student_df.loc[:, "grade"]
​
#### Use `iloc` to display the first 3 rows and columns 3, 4, and 5.
student_df_iloc = student_df.iloc[0:3, 3:6]

student_df_iloc

#### Select the rows for grade nine and display their summary statistics using `loc` and `describe`.

student_df_grade9 = student_df.loc[student_df["grade"] == 9].describe()

student_df_grade9

####  Store the row with the minimum overall reading score as `min_reading_row`
####  using `loc` and the `min_reading_score` found in Deliverable 3.

min_reading_row = student_df.loc[student_df["reading_score"] == min_reading_score]

min_reading_row
​

#### Use loc with conditionals to select all reading scores from 10th graders at Dixon High School.
​
student_df_grade10 = student_df.loc[(student_df["grade"] == 10) & (student_df["school_name"] == "Dixon High School"),'school_name':'reading_score']
student_df_grade10
​
#### Find the mean reading score for all students in grades 11 and 12 combined.
student_df['reading_score'].loc[(student_df['grade'] == 11) | (student_df['grade'] == 12)].mean() 
​
74.90038089192188
#### Find the mean math score for all students in grades 11 and 12 combined.
student_df['math_score'].loc[(student_df['grade'] == 11) | (student_df['grade'] == 12)].mean()
​
63.25853039200117

### Deliverable 5: Make Comparisons Between District and Charter Schools

#### Use groupby and mean to find the average reading and math scores for each school type.
student_group_df = student_df.groupby("school_type").mean()
student_group_df.loc[: , ["school_budget"]]
​
avg_student_scores_by_grade = student_df.groupby("school_type").mean()
avg_student_scores_by_grade.loc[:, ["math_score", "reading_score"]] 

#### Use the `groupby`, `count`, and `sort_values` functions to find the
#### total number of students at each school and sort from most students to least students.
​
student_count_df = student_df.rename(columns={'student_name':'student_count'})
student_count_by_school_df = student_count_df.groupby("school_name").count()
student_count_by_school_df.loc[:,['student_count']].sort_values('student_count',ascending=False)

#### The average math scores for each combination of grade and school type are displayed. 
​
student_avg_df = student_df.groupby(["school_type","grade"]).mean().round()
student_avg_df.loc[:,["math_score"]]
​
### Deliverable 6: Summarize Your Findings
#### Write a few sentences to describe any discoveries that you made while performing your analysis. 

- From the analysis we can depict that the public schools have more average school budget than the charter schools. The average reading scores of both the schools (public and charter ) are more than the average math scores.
- By using the groupby, count, and sort_values functions we can conclude that Montgomery High School has the highest number of students followed by Green High         School.
- By using the 'groupby' , 'mean' functions we can deduce that the average math scores for the charter schools(of grade 9 t0 12) is more than the public schools.

#### Include any additional analysis that you believe would be worthwhile.

- Additional analysis can be done by applying the groupby, count functions on school type and reading score to obtain more detailed analysis on the project.
- We can group the charter and public schools in order to obtain the the total student count for each category. This will assist in deep dive of the school budget on the categorical levels.
