# Useful Pandas Commands

#Read and Write Data

###Read CSV
import pandas as pd

import numpy as np

df = pd.read_csv("...file_name.csv")

###Get data types:
df.dtypes

###Write csv:
df.to_csv("...file_name.csv")


#String

###Convert column to strings:

df["Notes"] = df["Notes"].astype(str)

*Can also use "int" and "float"*

###Convert string to all lower case:

df["Notes"] = df["Notes"].map(str.lower)

*Can also use .upper*


##Stripping Strings: 

###Strips all numbers from strings in dataframe column:

df['Last Name'] = df['Last Name'].map(lambda x: x.strip('0123456789'))

###Or, just from left and right:

df['result'] = df['result'].map(lambda x: x.lstrip('+-').rstrip('aAbBcC'))

###Strip white space from leading and trailing edge:

df["Address"] = df["Address"].map(str.strip)

###Strip using special characters:

line = "59-35"

import re

line = re.sub('[-]', '', line)

*Output: 5935*

#Drop Columns and Duplicates, Rename Columns and Elements

###By column name:

df = df.drop('First Name_x', 1)

###Drop duplicates and reset index:

df = df.drop_duplicates(['Group2']).reset_index(drop=True)

*Note: Always reset index after droping

###Just reset index

df = df.reset_index(drop=True)

###Renaming Columns

df = df.rename(columns={'Org.Level.4': 'org_level_4', 'Org.Level.4.Number': 'org_level_4_number'})

###Rename Elements

dfn['Boro'] =  dfn['Boro'].str.replace('BRO', 'BROOKLYN')

###Fill NaN with zeros

df = df.fillna(0)

#Merging data

###Simple merge, if keys in w1 and w2 are the same:

merged = pd.merge(w1, w2)

###If not same,  specify the key:

merged_all = pd.merge(merged, w3, left_on = "FULL NAME1", right_on = "FULL NAME2" )

###Concatinate 

frames = [df1, df2]

result = pd.concat(frames)

###Create DF and add rows of data

qn = pd.DataFrame(columns=('BIN', 'Boro Code', 'Boro', 'House Number', 'Street Name', 'Address', 'Latitude', 'Longitude'))

qn.loc[0] = ['NA','NA','NA', 'NA','NA','NA', 'NA','NA']

qn.loc[1] = ['NA','NA','NA', 'NA','NA','NA', 'NA','NA']

Note: Number of columns must match

#Loops and Assignments

###Turn chain assignments off:

pd.set_option('chained_assignment', None)

#Subsetting

geoCodeCheck = geoCodeCheck[geoCode['Street Name'] == 'knickerbocker avenue']


#Sort and reindex

####Sort by high risk ranking and reindex

export = export.sort_values(by = 'High Risk Ranking', ascending=False).reset_index(drop=False) 









