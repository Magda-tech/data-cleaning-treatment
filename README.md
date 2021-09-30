#Purpose: perform data cleaning and treatment using pandas and statistical functions
#Author: Magda Monteiro
#Date: July, 2021
#This data is from 

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
