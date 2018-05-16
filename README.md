
# Read and Write Data

### Read CSV
import pandas as pd

import numpy as np

df = pd.read_csv("...file_name.csv")

### Get data types:
df.dtypes

### Write csv without index:
df.to_csv("...file_name.csv", index=False)

# Installing packages from tar.gz files

### Navigate to the directory containing the .tar.gz file from your command prompt and enter this command:

pip install my-tarball-file-name.tar.gz

# String

### Convert column to strings:

df["Notes"] = df["Notes"].astype(str)

*Can also use "int" and "float"*

### Convert string to all lower case:

df["Notes"] = df["Notes"].map(str.lower)

*Can also use .upper*

### Strip out all punctuations in strings, including brackets:

geoCodeAdd["STREET_NAME"] = geoCodeAdd["STREET_NAME"].str.replace('[^\w\s]','')

### Create new column category based on string in another column:

d['Type'] = np.where(d['Inspector Dept'].str.contains("Enforcement", case=False, na=False), 'Enforcement', 'Development')

### Create new column based on split in string in another column:

d["Inspector Department"] = d['Inspector Dept'].str.split().str[0]

### Fuzzy logic string comparison:

from difflib import SequenceMatcher as SM

s1 = "3243 IRWIN AVENUE BRONX" 
 
s2 = "3253 IRWIN AVENUE BRONX"

ratio =  SM(None, s1, s2).ratio()

#### Returns a score based on similarity

### Fuzzy logic explicit word matching:

s1 = 'Alphonso Marshall'

s2 = 'Marshall Alphonso'

set1 = set(s1.split(' '))

set2 = set(s2.split(' '))

if set1 == set2:

    print "True, same person"
    
else:

    print "False, not same person"

#### This prints out True

### Splitting strings based on capital letters in string:

import re

a = 'JohnHamilton'

re.findall('[A-Z][^A-Z]*', a)

#### Output is a list: ['John', 'Hamilton']

## Stripping Strings: 

### Get year from date that is in this format: 20101117:

df['Initial File Year'] = df['Initial File Date Raw'].apply(lambda x: x[:4])

### Strips all numbers from strings in dataframe column:

df['Last Name'] = df['Last Name'].map(lambda x: x.strip('0123456789'))

### Or, just from left and right:

df['result'] = df['result'].map(lambda x: x.lstrip('+-').rstrip('aAbBcC'))

### Strip white space from leading and trailing edge:

df["Address"] = df["Address"].map(str.strip)

### Or use loop and column names:
col_names = sorted(list(df.columns.values))

for i in range(0, len(col_names)):

    df[col_names[i]] = df[col_names[i]].astype(str)

for i in range(0, len(col_names)):

    df[col_names[i]] = df[col_names[i]].map(str.strip)

### Strip white spaces from leading and tailing edge in column

dfn = dfn.rename(columns=lambda x: x.strip())

### Strip using special characters:

line = "59-35"

import re

line = re.sub('[-]', '', line)

*Output: 5935*

### Stripping out numbers:

str = "h3110 23 cat 444.4 rabbit 11 2 dog"

str2 = [int(s) for s in str.split() if s.isdigit()]

*ouptut: [23, 11, 2]*

### Stripping out numbers, method 2

st = '132ND'

st = ''.join(c for c in st if c.isdigit())

*output: 132

### Stripping out special characters:

dfstaff["Name"] =  dfstaff["Name"].str.replace('[^\x00-\x7F]','')

### Remove the last element (or word) in a text string:

text = '272-276 Broadway New York NY 10007'

text.rsplit(' ', 1)[0]

# Drop Columns and Duplicates, Rename Columns and Elements

### Count the total NaN in dataframe:

df.isnull().sum()

### Sum NaN by column:

df["VEHICLE_NUMBER"].isnull().sum()

### By column name:

df = df.drop('First Name_x', 1)

### Drop duplicates and reset index:

df = df.drop_duplicates(['Group2']).reset_index(drop=True)

*Note: Always reset index after droping

### Drop duplicates based on more than one field:

df = df.drop_duplicates(subset=['Address', 'Boro']).reset_index(drop=True)

*drops rows where address and borough are the same*

### Drop duplicates based on element in another column, this drops all rows of data except if value in INSPECTION_ID equals the value in INSPECTION_ID.1

dn = dn[dn['INSPECTION_ID'] == dn["INSPECTION_ID.1"]]

### Just reset index

df = df.reset_index(drop=True)

### Renaming Columns

df = df.rename(columns={'Org.Level.4': 'org_level_4', 'Org.Level.4.Number': 'org_level_4_number'})

### Rename Elements

dfn['Boro'] =  dfn['Boro'].str.replace('BRO', 'BROOKLYN')

### Fill NaN with zeros

df = df.fillna(0)

### Replace string in all columns:

d = d.replace(["None"], [""]) 

df = df.replace(['very bad', 'bad', 'poor', 'good', 'very good'], [1, 2, 3, 4, 5]) 

### Drop row based on element type:

df = df[df["BORO"] != 0]

*drops all rows with 0*

### Drop row if contain string:

df2 = df2[df2.Address.str.contains("WEST END AVE") == False]

*drops all rows in Address field if contain WEST END AVE*

### Drop NaN, works for categorical variables:

df = df[pd.notnull(df['Distressed'])]

### Drop NaN using dropna:
df = df.dropna()

*this drops all rows with NaN*

### Drop NaN based on row:

df = df.dropna(subset = ['BIN'])

### Drop NaN using is finite (only works for numeric data):

df = df[np.isfinite(df['House Number'])]

### Move columns, this moves last column to first colum:

cols = nodesGephi.columns.tolist()

cols = cols[-1:] + cols[:-1]

nodesGephi = nodesGephi[cols]

# Merging data

### Simple merge, if keys in w1 and w2 are the same:

merged = pd.merge(w1, w2)

### If not same,  specify the key:

merged_all = pd.merge(merged, w3, left_on = "FULL NAME1", right_on = "FULL NAME2" )

### Left-outer join

http://stackoverflow.com/questions/21786490/pandas-left-outer-join-multiple-dataframes-on-multiple-columns

### Concatinate 

frames = [df1, df2]

result = pd.concat(frames)

### Create DF and add rows of data

qn = pd.DataFrame(columns=('BIN', 'Boro Code', 'Boro', 'House Number', 'Street Name', 'Address', 'Latitude', 'Longitude'))

qn.loc[0] = ['NA','NA','NA', 'NA','NA','NA', 'NA','NA']

qn.loc[1] = ['NA','NA','NA', 'NA','NA','NA', 'NA','NA']

Note: Number of columns must match

# Loops and Assignments

### Turn chain assignments off:

pd.set_option('chained_assignment', None)

# Subsetting

geoCodeCheck = geoCodeCheck[geoCode['Street Name'] == 'knickerbocker avenue']

### Subset  streets bounded by left and right x coord using mask

mask = (dfList['XCoord'] >= xy2[0]) & (dfList['YCoord'] <= xy1[0])

dfList_subset = dfList.loc[mask]

### Subset using two elements in column:

df = df[(df['closing_price'] >= 99) & (df['closing_price'] <= 101)]

### Subset using a list (this removes all rows of data not in list):

df = df[df['Name'].isin(nameList)]

### Or, remove all those in list (removes all items in the list):

dpsub = dp[~dp['BIN'].isin(binList)]

### Drop all rows except for rows where two fields are equal:

df2 = df[df['INSPECTION_ID'] == df["INSPECTION_ID.1"]]

# Sort and reindex

#### Sort by high risk ranking and reindex

export = export.sort_values(by = 'High Risk Ranking', ascending=False).reset_index(drop=False) 

#### Sort python list, from high to low:

sorted(ratio_list, reverse=True)


#### Sort and keep only those with duplicates

ids = dfInt["NODEID"]

dfInt2 = dfInt[ids.isin(ids[ids.duplicated()])].sort_values(by="NODEID")

#### Sort a list of list, first item is string, second item is numeric:

from operator import itemgetter

ratio_list = sorted(ratio_list, key=itemgetter(1), reverse=True)

#### Sort columns by name:

df = df.reindex_axis(sorted(df.columns), axis=1)

# From List to Dataframe:

df = pd.DataFrame(dfList, columns=['BIN', 'Boro', 'Address'])

# Lists and Sets

### Create a list
list_block = []
    
    for i in range(0, len(df2)):
        list_block.append(df2["Block"][i])

### Create a list from dataframe column:

dateList = df2['Date'].tolist()

   
### Create a set from a list     
    set_block = set(list_block)
    
### Removing any element with numbers from a list:

text = [x for x in text if not any(c.isdigit() for c in x)] 
  
### Sort the set
    set_block = sorted(set_block)
    
### Create a categorical variable based on items in list:

frame = pd.DataFrame({'a' : ['the cat is blue', 'the sky is green', 'the dog is black']})

mylist =['dog', 'cat', 'fish']

pattern = '|'.join(mylist)

frame["TF"] = frame.a.str.contains(pattern)

### Remove empty elements in list:

a = filter(None, a)

### Replacing elements in list using list comprehension

a=[1,"",3,1,3,2,1,1]

a = ["NA" if x=="" else x for x in a]

#### Replaces empty elements with 'NA'

### List intersections, produces list of common elements between list1 and list2

x = list(set(list1).intersection(list2))

### Replace words or names in a list using a dictionary:

words = flist

final_string = ', '.join(str(nameDic.get(word, word)) for word in words)


### Sort a list of strings, from largest to smallest:

matchList.sort(key = lambda s: len(s), reverse=True )

### Remove empty space in a list:

name_list = ['ALEX PERA', ' ', 'VAL TOL']

name_list = [x for x in name_list if x != ' ']

### From list of lists to list:

oList = sum(oList, [])

# Map Function

### Create a list of titles and last names:

people = ['Dr. Christopher Brooks', 'Dr. Kevyn Collins-Thompson', 'Dr. VG Vinod Vydiswaran', 'Dr. Daniel Romero']

def split_title_and_name(person):

    return person.split()[0] + " " + person.split()[-1]

list(map(split_title_and_name, people))

# Append Dataframe

all_data = pd.DataFrame()

all_data = all_data.append(df,ignore_index=False)


# Splitting and String Comparison with Two Dataframes

### This splits house number with "-" into two columns

location_df = df['h_no'].apply(lambda x: pd.Series(x.split(',')))

### Want to know if address one in df1 matches df2, if so tag the address

*Create a list of matching addresses in the dataframes:*

common_cols = list(set(df14.Address) & set(dfmn.Address))


dfmn["Corner"] = 0

dfmn["Corner"] = 0


for i in range(0, len(dfmn)):

    if dfmn["Address"][i] in common_cols:
    
        dfmn["Corner"][i] = 1
        
        

# Groupby 

#### Add the total leave hours per person in new column called 'Correct Duration Sum'


lv['Correct Duration Sum'] = lv['Correct Duration'].groupby(lv['CityTime ID']).transform('sum')

#### Sums by BIN and then year and sums up all of the other numeric variables:

qnG = qn.groupby(['BIN', 'Year']).sum()

#### Reset back to dataframe:

qnG = qnG.add_suffix('_Count').reset_index()


#### Groupby, count number of jobs and sum all other variables:

dfG = (df.groupby('BIN_Number').agg({'Job_Number':'count', 'AHV_Grants': 'sum', 'Initial_Da':'sum', 'Additional':'sum'}).reset_index().rename(columns={'Job_Number':'Job_Number_count'}) )

#### Groupby and sum strings in row, this first creates a series and then needs to be converted to dataframe:

f = rank_title.groupby('Name')['Title'].apply(lambda x: "{%s}" % ', '.join(x))

X = pd.DataFrame(f)

X = X.reset_index(drop=False)

# Datetime

### Convert date into pandas datetime:

df['DATE_SCHEDULED'] = pd.to_datetime(df['DATE_SCHEDULED'])

### Convert string to datetime:

start_date = str(1) + '-' + str(1) + '-' + str(2016)

from dateutil import parser

start_date = parser.parse(start_date)

start_date = start_date.date()

### Remove time from datetime:

db["DATE_INSPECTION"] = db["DATE_INSPECTION"].apply(lambda x: x.date())

### Remove date from datetime:

df['Inspection Time'] = df["Inspection Time"].apply( lambda d : d.time() )


### Get the difference in days
d = df2["Variance End Date"][j] - df2["Variance Start Date"][j]

diff = d.days

diff = int(diff)

### Get the difference in hours:

print pd.Timedelta(d["Next_Login"][0] - d["Crash_Time_EST"][0]).seconds / 3600.0

### Create week number based on date, year, month and day are integers:

df["Week Number"][i] = datetime.date(year, month, day).isocalendar()[1]

### Subset with date time and masking:

start_time = str(lv["Start Time"][i].month) + '-' + str(lv["Start Time"][i].day) + '-' + str(lv["Start Time"][i].year)
 
end_time = str(lv["End Time"][i].month) + '-' + str(lv["End Time"][i].day) + '-' + str(lv["End Time"][i].year)

mask = (wd['workdays'] >= start_time) & (wd['workdays'] <= end_time)

wd_subset = wd.loc[mask]

### Print current date and time:

from datetime import datetime

print str(datetime.now())

### Plus or minus days in date range:

insp_date = df["DATE_INSPECTION"][0]

d = datetime.timedelta(days = 2)

minus2 = insp_date - d

plus2 = insp_date + d

mask = (all_data2['Date'] >= minus2) & (all_data2['Date'] <= plus2)

dfpm2 = all_data2.loc[mask]



# Dataframe Math and Stats Calculations

### Sum values in dataframe:

sum_trans = df3["Transaction Amount"].sum()

### Get min mor max in dataframe column:

df2["EucDistance"].min()

### Summary stats, continuous vars only:

df.describe().transpose()

### Multiply all floats by 100 to convert into percent

#### Get datatypes first then convert

dr.dtypes

dr[dr.select_dtypes(include=['float']).columns] *= 100

#### Round all numbers in df to two decimal places:

dr = dr.round(2)

# Dictionaries

### From dataframe to dictionary, df with fields "bin" and "WallArea SqFt"

dwsDic = dwsG.set_index('bin')['WallArea SqFt'].to_dict()

### Replace all values column based on dictionary:

di = {1: "A", 2: "B"}

df = df.replace({"col1": di})


### Creating flag using dictionaries, this creates a Y/N flag where Y is in flag if job number in column, N if not:

dic_s = {'7398378':'Y', '7398310':'Y'}

df['Flag'] = df['Job Number'].map(dic_s).fillna('N')


# Try

    for i in range(0, len(dfdn)):
         print "terracot address", dfdn["AddressMatch"][i]
    try: 
        print "dic list", d2[dfdn["AddressMatch"][i]] 
    except KeyError, e:
        print e



# Useful Websites:

#### 12 Useful Pandas Commands

https://www.analyticsvidhya.com/blog/2016/01/12-pandas-techniques-python-data-manipulation/

#### Pivoting in Pandas:

http://pandas.pydata.org/pandas-docs/stable/reshaping.html

#### Pivot with name, year, sum of variable (creates index with name, colums are date, values are duration in hours):

p = resultG.pivot_table(index='Name', columns='Month-Year', values='Duration Hours_Count')

#### Pivot and sum values

st = st.pivot_table(index='BIN Number', columns='Permit Sub Type',values='Value', aggfunc=np.sum)


#### List comprensions:

https://www.python-course.eu/list_comprehension.php

http://www.secnetix.de/olli/Python/list_comprehensions.hawk

https://www.analyticsvidhya.com/blog/2016/01/python-tutorial-list-comprehension-examples/


