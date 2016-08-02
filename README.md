# Useful-Pandas-Commands

#Stripping 

Strips all numbers from column of strings:

df['Last Name'] = df['Last Name'].map(lambda x: x.strip('0123456789'))

Or, just from left and right:

df['result'] = df['result'].map(lambda x: x.lstrip('+-').rstrip('aAbBcC'))

Strip white space from leading and trailing edge:

df["Address"] = df["Address"].map(str.strip)

#String Commands

Convert column fro strings:

df["Notes"] = df["Notes"].astype(str)

Can also use "int" and "float"

Convert string to all lower case:

df["Notes"] = df["Notes"].map(str.lower)

Can also use .upper
