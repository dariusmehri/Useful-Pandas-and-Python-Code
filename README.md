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

###Fuzzy logic string comparison:

s1 = "3243 IRWIN AVENUE BRONX" 
 
s2 = "3253 IRWIN AVENUE BRONX"

ratio =  SM(None, s1, s2).ratio()

####Returns a score based on similarity


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

###Stripping out numbers:

str = "h3110 23 cat 444.4 rabbit 11 2 dog"

str2 = [int(s) for s in str.split() if s.isdigit()]

*ouptut: [23, 11, 2]*

###Stripping out numbers, method 2

st = '132ND'

st = ''.join(c for c in st if c.isdigit())

*output: 132

###Stripping out special characters:

dfstaff["Name"] =  dfstaff["Name"].str.replace('[^\x00-\x7F]','')

### Remove the last element (or word) in a text string:

text = '272-276 Broadway New York NY 10007'

text.rsplit(' ', 1)[0]

#Drop Columns and Duplicates, Rename Columns and Elements

###By column name:

df = df.drop('First Name_x', 1)

###Drop duplicates and reset index:

df = df.drop_duplicates(['Group2']).reset_index(drop=True)

*Note: Always reset index after droping

###Drop duplicates based on more than one field:

df = df.drop_duplicates(subset=['Address', 'Boro']).reset_index(drop=True)

*drops rows where address and borough are the same*

###Just reset index

df = df.reset_index(drop=True)

###Renaming Columns

df = df.rename(columns={'Org.Level.4': 'org_level_4', 'Org.Level.4.Number': 'org_level_4_number'})

###Rename Elements

dfn['Boro'] =  dfn['Boro'].str.replace('BRO', 'BROOKLYN')

###Fill NaN with zeros

df = df.fillna(0)

###Drop row based on element type:

df = df[df["BORO"] != 0]

*drops all rows with 0*

###Drop row if contain string:

df2 = df2[df2.Address.str.contains("WEST END AVE") == False]

*drops all rows in Address field if contain WEST END AVE*

### Drop NaN using dropna:
df = df.dropna()

*this drops all rows with NaN*

### Drop NaN using is finite (numeric data):

df = df[np.isfinite(df['House Number'])]

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

###Subset  streets bounded by left and right x coord using mask

mask = (dfList['XCoord'] >= xy2[0]) & (dfList['YCoord'] <= xy1[0])

dfList_subset = dfList.loc[mask]


#Sort and reindex

####Sort by high risk ranking and reindex

export = export.sort_values(by = 'High Risk Ranking', ascending=False).reset_index(drop=False) 


####Sort and keep only those with duplicates

ids = dfInt["NODEID"]

dfInt2 = dfInt[ids.isin(ids[ids.duplicated()])].sort_values(by="NODEID")



#From List to Dataframe:

df = pd.DataFrame(dfList, columns=['BIN', 'Boro', 'Address'])

#Lists and Sets

###Create a list
list_block = []
    
    for i in range(0, len(df2)):
        list_block.append(df2["Block"][i])
   
   
###Create a set from a list     
    set_block = set(list_block)
  
###Sort the set
    set_block = sorted(set_block)


#Splitting and String Comparison with Two Dataframes

###This splits house number with "-" into two columns

location_df = df['h_no'].apply(lambda x: pd.Series(x.split(',')))

###Want to know if address one in df1 matches df2, if so tag the address

*Create a list of matching addresses in the dataframes:*

common_cols = list(set(df14.Address) & set(dfmn.Address))


dfmn["Corner"] = 0

dfmn["Corner"] = 0


for i in range(0, len(dfmn)):

    if dfmn["Address"][i] in common_cols:
    
        dfmn["Corner"][i] = 1
        
        

#Groupby 

####Add the total leave hours per person in new column called 'Correct Duration Sum'


lv['Correct Duration Sum'] = lv['Correct Duration'].groupby(lv['CityTime ID']).transform('sum')

####Sums by BIN and then year and sums up all of the other numeric variables:

qnG = qn.groupby(['BIN', 'Year']).sum()

####Reset back to dataframe:

qnG = qnG.add_suffix('_Count').reset_index()

#Datetime

### Get the difference in days
d = df2["Variance End Date"][j] - df2["Variance Start Date"][j]

diff = d.days

diff = int(diff)

#Data Frame Math Calculations

###Sum values in dataframe:

sum_trans = df3["Transaction Amount"].sum()

### Get min mor max in dataframe column:

df2["EucDistance"].min()



