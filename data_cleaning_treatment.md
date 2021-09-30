#Purpose: Perform data cleaning and treatment using pandas and statistical functions

#Author: Magda Monteiro

#Date: July, 2021

#This data is from Kaggle.com

#--

'''To perform an exploratory data analysis, we first need to clean and treatment the data so that it becomes consistent. 
   This is one of the most important steps if you want to make quality decisions.'''

#--

#So, let's begin!

#first import the librarys of funcions 

#give a alias for the library

import pandas as pd
import statistics as sts

#later import the data

#give a name for your data. In this case im using "dataset" like name

#the name of the file that im using is "../input/dados-1/Churn.csv"

dataset = pd.read_csv("../input/dados-1/Churn.csv", sep = ";")

#for view the data,use the funcion:

dataset.head()

#to view the total of lines and columns, use the funcion:

dataset.shape

#for rename for the columns, use the funcion:

dataset.columns=["Id", "Score","State","Gender","Age","Patrimony","Balance", "Products","Temcartcredito","Active","Wage","Exited" ]

#to view 

dataset.head()

#some states are incorrectly named and in this case we will only need the PR, SC and RS state data.
#we can see the "state" column, assigning a variable to the formula and then calling that variable

grouped=dataset.groupby(['State']).size()
grouped

#to correct this, we will substitute the values for the mode
#since the state that is most repeated is RS, we will replace the data that is inconsistent with it,
#using the function below:

dataset.loc[dataset['State'].isin(['TD','SP','RP']),'State']='RS'

#to view 

grouped=dataset.groupby(['State']).size()
grouped

in the case of data referring to age, we need it to be within the range of 0 to 120 years
#first we will check for occurrences of values outside this range

dataset.loc[(dataset['Age'] < 0) | (dataset['Age'] > 120)]

#now, we calculate the median to replace the data that out of range.
#the median is less likely to have nonstandard values.
#for this, we will use the statistics library function

median=sts.median(dataset['Age'])

#to replace the data that out of range:

dataset.loc[(dataset['Age'] < 0) | (dataset['Age'] > 120)]=median

#to check if there are still values for the age range:

dataset.loc[(dataset['Age'] < 0) | (dataset['Age'] > 120)]

#to identify duplicate data, we search by ID

dataset[dataset.duplicated(['Id'],keep=False)]

# to delete duplicate ID

dataset.drop_duplicates(subset="Id",keep="first",inplace=True)

#to check if there are duplicate ID

dataset[dataset.duplicated(['Id'],keep=False)]

#to view the total of lines and columns,after delete duplicate ID
#note that before there were 999 lines and now it has 995
dataset.shape
