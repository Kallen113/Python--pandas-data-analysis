# Python--pandas-data-analysis
'''Python code for: Importing Excel data, rename variables, melt columns, and run plots'''

#The following is Python code from a project I started on January 8, 2018:


Created on Mon Jan  8 00:27:13 2018

@author: Owner
"""

import pandas as pd
import statsmodels.api as sm
import pylab as pl
import numpy as np
import matplotlib.mlab as mlab
import matplotlib.pyplot as plt
import statsmodels.formula.api as smf
import warnings



df_reg = pd.read_csv('C:\\Users\\Owner\\Documents\\World_Bank_data_on_GDP_percapita_1995to2015.csv')

'''imports all data (i.e., from each column) from a given CSV file.'''

df_reg.columns
#displays a list of the different column names.

df_reg.shape
#Displays the dataset's total number of rows and columns.

print (df_reg.head())
#displays the observations from the first 5 rows of the data (here, known as a data frame) from imported Excel file.

df_reg
#displays all observations (as many as Python deems reasonable to display: here- the 1st and last years of data).
df_reg.rename(columns = {'Country Name' : 'Country'}, inplace=True)
#Renames variable Country Name to Country for ease of reference and to help prevent the other code from failing (i.e., no spaces).
#NOTE: A single line of code can be used to rename multiple variables simultaneously. 
#How? Just list the variable names and renamed variable names right after the 1st renamed variable.

df_reg.describe()
#computes summary statistics for each variable

df_reg.sort_values('Country')
#Sorts the dataset's variables by countries by alphabetical order.

df_reg['Country'].sort_values(ascending=False)
#Sorts the country observations in reverse alphabetical order.

df_reg['Country']
#Displays the original order of the observations.


df_reg= pd.melt(df_reg, id_vars=["Country"])
'''Rearranges the dataframe to be "stacked" and merged by the Country variable (i.e., country names).'''

df_reg
#displays the data for this newly merged dataframe.
'''Code works fine for this purpose of getting it into a wide format with only a single variable.'''



df_reg.rename(columns = {'variable' : 'Year'}, inplace=True)
#Renames variable 'variables' to Year.

df_reg.rename(columns = {'value' : 'GDP_percap'}, inplace=True)
#Renames variable to GDP_percap.

df_reg.columns
#Displays the names of the columns, and its # of rowsx # of columns.

'''The following code implements various plots:'''

df_reg.hist(column= "GDP_percap", bins=50)
'''Implements a histogram of the GDP_percap variable.
#Notice the data are heavily skewed to the right, meaning the mean is likely
much higher than the median. 

Thus, the wealthier countries, 
representing a relatively small % of the sample size,are driving
up the global average of GDP per-capita. In reality, most countries 
are low to medium income (i.e., somewhat to much less wealthy).'''

df_reg.plot.bar()
#Implments a bar chart.

df_reg.plot.box()
'''Implements a box plot. Similar to the histogram, notice how the
data are heavily skewed, and most of the distribution lies
within the lower to mid income countries. The higher-income countries
are far above the global average of GDP per capita.'''


df_reg.plot("Year","GDP_percap")
'''Implements a plot comparing GDP per-capita over time, from
1995 to 2015 (i.e., the full duration of the data).
Notice there is a sloid increasing trend in GDP per-capita
over time, with the exception of one recession and one recent period
(2009-2010 for the recession and 2012-2014).'''
