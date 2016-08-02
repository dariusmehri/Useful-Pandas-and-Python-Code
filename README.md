# Useful-Pandas-Commands



#String Commands

###Convert column to strings:

df["Notes"] = df["Notes"].astype(str)

*Can also use "int" and "float"*

###Convert string to all lower case:

df["Notes"] = df["Notes"].map(str.lower)

*Can also use .upper*


#Stripping 

###Strips all numbers from column of strings:

df['Last Name'] = df['Last Name'].map(lambda x: x.strip('0123456789'))

###Or, just from left and right:

df['result'] = df['result'].map(lambda x: x.lstrip('+-').rstrip('aAbBcC'))

###Strip white space from leading and trailing edge:

df["Address"] = df["Address"].map(str.strip)

#Drop Columns

###By column name:

df = df.drop('First Name_x', 1)

#Merging data

###Simple merge, this is if keys in w1 and w1 are the same:

merged = pd.merge(w1, w2)

###Use this to specify key:

merged_all = pd.merge(merged, w3, left_on = "FULL NAME1", right_on = "FULL NAME2" )




