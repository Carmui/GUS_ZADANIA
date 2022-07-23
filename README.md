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
### EDA - Exploratory Data Analysis


#

# <p align="center"> Conclusions </p>


