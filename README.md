# <p align="center"> Internship task </p>

***Warning - codes are commented in the polish language***

The main task of the intership was to determinate what kind of variables correlates the most with the shadow economy/informal work. Data was taken from [BKL](https://www.parp.gov.pl/component/site/site/bilans-kapitalu-ludzkiego) which is Balance of Human Capital. It is a unique Polish and European monitoring of demand for competences on the labor marker. I came across two different surveys: population and entrepreneurs. In this case, I focused on the population data since only this questionnaire included questions about participation in the shadow economy. The questionnaire has more than 500 questions about the people job, informal work, working abroad, education level, marriage status and many, many more. 

Imported data frame had 902 columns and 2533 rows. Therefore, the first thing I focused on was matching the columns to individual questions. After that, I have decided to select thos that could be potentially useful in the current analysis. (f.e.: the negligible correlation of the variable "participation in the internship" meant that this variable was not taken into account when considering the further impact of the variable on the development of the model)

***Explained variable*** - The first challenge encountered was to create a variable that would allow us to examine the relationships. For this purpose, the variable Y was determined based on two questions:
- ***J6*** - During the last 12 months, has it happened that you received part of the remuneration for contract work informally? (0 - no, 1 - yes)
- ***N1*** - Have you taken up such gainful (informal) work in the last 12 months? (0 - no, 1 - yes)
Variable Y was a merger of affirmative answers for the examined objects.
#

# <p align="center"> The course of the study </p>
### EDA - Explained variable imbalance
The first encountered serious problem was lack of proper balance of the explained variable. As you can see below, only 5% of the respondents answered the question in the affirmative. This is a relatively small percentage of people. The main problem of the respondents' research is the tendency to keep some data secret. 

 <p align="center"> <img src = https://user-images.githubusercontent.com/31701880/180861934-5045e391-8a9d-4d9a-a4dc-6a3aba218e3f.png width="600" height="400"></p>

### EDA - Variables selection
In this case, I tried to limit myself to variables that required any response from the respondent. The selection of variables was carried out using an expert method based on publicly available studies, as well as with the help of the potential correlation between the variables. In this task, we had a lot of categorical variables and one or two numerical variables. Some of the categorical variables had NULL values (the question might not apply to a given person). That was the reason to create binary variables. This allowed me to "somehow" get rid of potential NULLs, but one should also consider a different approach to such situations. Among the nominal variables, only the age variable was taken which takes values from 18 to 70. (I excluded the income variable due to very large missing data - more than 50% of the value would have to be supplemented, which is not very effective)

The first main set of variables was:
- Y - dependent variable denoting belonging or not to the gray zone
- woj - Voivodship from which the observation was taken
- place_4k - city / village type divided into 4 categories (village, city up to 20k, city 20-100k, city with more than 100k citizens)
- age - age of the surveyed people
- age_3k - age of the surveyed people broken down into 3 categories
- age_4k - age of the surveyed people broken down into 4 categories
- m2 - gender of the examined person
- wykszt_4k - education divided into 4 categories (secondary, basic vocational, higher, lower secondary and less)
- matura - whether the person had a full-time certificate
- p1 - is it running a business
- p1_typ - type of business activity
- p14 - how your income has changed in recent years
- c1 - Have you helped in the last 12 months in a family business or farming activity for free?
- c2 - Are you still doing this work, or has it already been completed or temporarily interrupted?
- y1 - Have you worked abroad in the past 12 months?
- y1_1 - How many months did you work?
- y2 - Are you going to work abroad in the next 12 months?
- g1 - has a job and performs / is absent or has a break
- s1 - Are you looking for any other job, apart from the one you are currently doing?
- m5 - What is your current marital status? (maybe divided into smaller categories?
- m6 - Do you have a child?
- m9_1 - Earnings ranges

After full EDA, I have included only part of the above variables. Some of them had less impact than it was thought at the beggining. (a bit of data manipulation, etc)

- Wiek - the age of the examined person
- Woj-zachodnie - does the respondent's province belong to one of the provinces of the Western Bloc (1 - yes, 0 no)
- Miejsce_4k_wieś - does the respondent come from a village (1-yes, 0 no)
- Age_3k_18-35 - is the respondent's age in the range of 18-35 (1-yes, 0 no)
- M2_male - respondent's gender (1 - male, 0 - female)
- Wykszt_4k_ Wyższa - whether the person has higher education (1 - yes, 0 - no)
- Matura_tak - does the person have a high school diploma (1 - yes, 0 - no)
- P1_tak - Does the person run a business (1 - yes, 0 - no)
- C1_tak - Have you helped in the family business in the last 12 months (here the variable can potentially also be part of the dependent variable) (1 - yes, 0 - no)
- Y1_tak - work abroad in the last 12 months (1 - yes, 0 - no)
- Y2_ Definitely no - Does he intend to work abroad in the next 12 months (1 - no, 0 - yes / he doesn't know)
- G1_ has a job - Does it have a job (1 - yes, 0 - no)
- S1_tak - Is he looking for a job in addition to what he has (1 - yes, 0 - no)
- M5_zamężny / żonata - Is he / she married (1 - yes, 0 - no)
- M6_no - Does the person have a child (1 - no, 0 - yes)


### Methods used
#### SMOTE Algorithm
In order to create decision trees and random forests, it is first of all necessary to take care of the appropriate balance of the explained variable. For this purpose, the SMOTE algorithm was used, thanks to which additional records supplementing the tested feature were created.

SMOTE algorithm point by point:
1) We choose a random example of an observation for the minority class.
2) We find the k nearest neighbors for the selected observation (from the point above).
3) We choose one of these neighbors and place a synthetic point anywhere on the line connecting the considered point with its neighbor.
4) We repeat the above steps until the data is balanced.

Explained variable after the SMOTE:
 <p align="center"> <img src = https://user-images.githubusercontent.com/31701880/180874951-8166960a-ef4f-4e0e-a939-119fe20fe31d.png width="600" height="400"></p>


#### Decision tree (and random forest)
Considering the structure of the obtained data, as well as the high level of categorization of variables (almost all variables are categorical), I decided to use the algorithms of decision trees and random forests. This choice was made due to the possibility of easy verification how individual variables affect the decision-making of the created model. Additionally, it is very banal to determine the influence of parameters on the explained variable (for example using the Gini index).

Parameters of the decision tree have been chosen by the following method:
 <p align="center"> <img src = https://user-images.githubusercontent.com/31701880/180876360-e8596a10-f295-4224-8c3f-46d18e0dbe93.png width="600" height="400"></p>

The selected decision tree has 14 levels, which may lead to an overfitting of the model. However, the previously tested parameters did not have a sufficient value of the F1 index to be able to adopt them without any major doubts.

#### Cross validation
Cross-validation involves breaking a data set into k subsets (k-fold validation) and then taking one of them in turn as a test data set and using the rest as a training data set. Accuracy assessment consists in calculating the arithmetic mean of the model accuracy and other such indicators.

### Model classification
<p align="center"> <img src = https://user-images.githubusercontent.com/31701880/180878343-e291fe54-e35a-472c-8300-ea736b44f71e.png width="600" height="400"></p>

- ACC = ~91%
- TPR = ~ 80% 
- FPR = ~ 7,3%
- TNR = ~ 92,7%
- FNR = ~ 20%

### Parameters importance
<p align="center"> <img src = https://user-images.githubusercontent.com/31701880/180881930-5648a480-c5a6-445d-af4d-c3f634fcbce1.png width="600" height="400"></p>


# <p align="center"> Conclusions </p>


