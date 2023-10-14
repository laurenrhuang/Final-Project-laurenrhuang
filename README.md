# Project Overview

## Preview of Data and Preliminary Analysis

#### What does it include?
The dataset is on student performance in 2 secondary education Portuguese schools. There are many predictor variables, such
as school, sex, age, family size, mother’s education, father’s education, mother’s job, father’s job, travel time, study time,
failures, and more. The goal of training a model on this data will be to accurately predict a student’s G3 (final grade) based on their (G1) 1st
and (G2) 2nd period grades.

#### Where and how will you be obtaining it? Include the link and source.
The data is in csv format and comes from kaggle. The data is separated into 2 files, student performance in Math and Portuguese
classes.
https://www.kaggle.com/datasets/whenamancodes/student-performance?select=Portuguese.csv

#### About how many observations? How many predictors?
The Math data file has about 390-400 observations, and the Portuguese data file has about 650 observations. Both files have the same 30
predictors.

#### What types of variables will you be working with?
I’ll be working with independent variables(predictors) like school, age, travel time, study time, etc. and a dependent variable(s), which is
G1 (first period grade), G2 (second period grade) and G3 (final grade).

## Preview the data

It's good to know the variables we will be using in this project:

* `school`: student's school name (GP="Gabriel Pereira", MS="Mousinho da Silveira")

* `sex`: sex (1 if F="Female", 0 if M="Male")

* `age`: age in years

* `famsize`: greater than 3 (GT3) or less than or equal to 3 (LE3)

* `Pstatus`: parent's cohabitiation status (T="living together", A="apart")

* `Medu`: mother's education (0="none", 1="primary", 2="5th to 9th grade", 3="secondary", 4="high edu")

* `Fedu`: father's education (0="none", 1="primary", 2="5th to 9th grade", 3="secondary", 4="high edu")

* `Mjob`: mother's job

* `Fjob`: father's job

* `reason`: reason to choose this school (close to 'home', school 'reputation', 'course' preference or 'other')

* `guardian`: student's guardian (mother, father, other)

* `traveltime`: home to school travel time (1="<15 min.", 2="15 to 30 min.", 3="30 min. to 1 hour", or 4=">1 hour")

* `studytime`: weekly study time (1="<2 hours", 2="2 to 5 hours", 3="5 to 10 hours", or 4=">10 hours")

* `failures`: number of past class failures (n if 1<=n<3, else 0)

* `schoolsup`: extra educational support (yes, no)

* `famsup`: family educational support (yes, no)

* `paid`: extra paid classes within the course subject (yes, no)

* `activities`: extracurricular activities (yes, no)

* `nursery`: attended nursery school (yes, no)

* `higher`: wants to take higher education (yes, no)

* `internet`: internet access at home (yes, no)

* `romantic`: with a romantic relationship (yes, no)

* `famrel`: quality of family relationships (from 1="very bad" to 5="excellent")

* `freetime`: free time after school (1="very low to 5="very high")

* `goout`: going out with friends (1="very low to 5="very high")

* `Dalc`: workday alcohol consumption (1="very low to 5="very high")

* `Walc`: weekend alcohol consumption (1="very low to 5="very high")

* `health`: current health status (from 1="very bad" to 5="very good")

* `absences`: number of school absences

* `G1`: first period grade (0 to 20)

* `G2`: second period grade (0 to 20)

* `G3`: final grade (0 to 20, heavily depends on G1 and G2) (this is what we'll be predicting!)

### Research Questions

#### Why would this model be useful?

The goal of this model is to try and predict a student's final G3 grade based on previous grades, familial relationships, and environmental factors. 
Hopefully having these results will give educators, staff, and family an idea of where to target resources to support students. 
For students, a grade prediction would give them a better idea of their current performance.

#### What variable(s) are you interested in predicting? What question(s) are you interested in answering?
I am interested predicting G3 final grades from G1 (first period grades) and G2 (second period grades) and other familial/environmental factors.
I also hope to understand the relationship between each predictor and the students’ grades.
I would pose questions such as: 
- What is the relationship between a mother or father’s education and the student’s final grade?
- What is the relationship between a mother or father’s job and the student’s final grade? 
- What is the relationship between the distance between school and home and student’s final grade?

#### Name your response/outcome variable(s) and briefly describe it/them.
My response/outcome variable will be G3, which is a student's final grade.
I will need to train my model on the predictor variables, including school, age, family size, study time, failures, etc. and G1, G2 grades.

#### Will these questions be best answered with a classification or regression approach?
For my dataset, it can be challenging to tell whether or not regression or classification will be more effective. I will test both methods to check.
While the student grades are on a numerical scale of 0 to 20, students can only recieve grades which are whole numbers.
(the grading scale does not have partial grades, ex. 0.25, 0.5, 0.75, etc.)

#### Which predictors do you think will be especially useful?
Predictors like school, travel time, study time, failures will be most useful because they can tell us the direct impact on the
outcome. Other predictors such as mother’s education, father’s education, mother’s job, father’s job may help reveal the importance/value of
parental guidance or familial emphasis on education, but because these are qualitative traits, it is harder to quantify their impact on
student performance.

#### Is the goal of your model descriptive, predictive, inferential, or a combination? Explain.
I believe the goal of my model is predictive. I am using existing student data and background information to make a prediction about the grade a student recieves.

## Model Building and Evaluation:
1. Read in and clean the data
2. Exploratory Data Analysis
   - Make plots to visualize.
   - Investigate any correlation between variables.
   - Decide how to split the data into training and testing sets.
     - Method 1: Merge Maths and Portuguese datasets, then split into training and testing datasets.
     - Method 2: Use Portuguese dataset for training, Maths dataset for testing.
3. Try both Regression and Classification methods (on the training datasets)
   - Regression (will predict a numerical value for the students' G3 grade)
     - Linear regression
   - Classification (will predict Pass/Fail for students' G3 grade)
     - Logistic Regression
     - Linear Discriminant Analysis (LDA)
     - Quadratic Discriminatn Analysis (QDA)
4. Repeat Step 3 for both method 1 and method 2 of splitting data.
5. Analyze the ROC curves and AUC values resulting from each method, choose the best performing model.
   * Note: How to interpret model performance from ROC curves and AUC values?
     The more a ROC curve looks like a "right angle," the closer it is to being a "perfect classifier."
     AUC stands for "area under the (ROC) curve." The closer the AUC value is to 1, the more accurate the model is.
   - Overall, the classification models performed better than regression models.
   - The best performing model was Logistic Regression.
7. Conduct k-fold cross validation on the best performing model so far (Logistic Regression) to check if model accuracy increases.
   - Try 10 folds. Interestingly, no improvement on model accuracy.
9. Let's try 3 more models. These models could be set to either regression or classification mode, but we choose to go with classification because earlier we saw that
    classification methods tend to be more accurate than regression methods for our goals.
     - Elastic Net Tuning
     - Decision Tree
     - Boosted Tree
11. Repeat Step 9 for both method 1 and method 2 of splitting data.
    - Out of these three models, the Boosted Tree model performed best.
12. Compare the ROC curves and AUC values from all the models and data splitting methods we tried out.
    - the Boosted Tree model using Method 1 (merging Maths and Portuguese datasets) of data splitting gave the highest AUC value.
13. Fit the testing dataset to the Boosted Tree model using Method 1 of data splitting.
    - 0.9044586 accuracy and 0.968298 roc_auc on the testing dataset

## Conclusion

- While there was initial concern of how the outcome variable (G3 final grades) would perform under a Regression vs. Classification model, this was remedied by the introduction of "Fail" and "Pass" labels on G3 grades.
  This classification labeling system worked extremely well, producing accuracies and roc_auc values of mostly 0.9 or upwards.
- Is Method 1 or 2 of data splitting better? We discovered that most models performed better when using Method 1 (merge Maths and Portuguese datasets).
  This implies that there is some detectable difference between the Maths and Portuguese datasets, such that when a model is only trained on one of the datasets,
  it has some difficulty predicting the other. Finding this difference would require more exploration.

### Next Steps

- To take the analysis further, I might try fitting a random forest model and/or k nearest neighbors. The boosted tree did the best, better than the individual decision tree model,
  which is most likely a result of collecting knowledge from fitting several trees instead of just one. (In which case, a random forest would also likely give great results)
  I would also explore why the accuracy and roc_auc values decreased after conducting k-fold cross validation on the logistic regression model.
- The variables that most heavily influence a student's G3 grades are their G1, G2 grades, past failures, and alcohol consumption (moreso weekend alcohol consumption).
  Mother's education and Father's education are correlated among themselves, but their respective relationships with G3 grades would need to be further investigated.

### Personal Thoughts
This was an exciting project to work on, I greatly enjoyed it because of my love for exploring the intersection between statistics, data, education, and the ways each field can enhance one another.
Working with grades data and observing which factors heavily impact performance is a great first step in targeting the needs and kinds of resources needed to support students.
One of my goals for the future is to use data analysis methods to better understand the needs and backgrounds of students, which will hopefully help me find ways to motivate and help them excel in their careers.
