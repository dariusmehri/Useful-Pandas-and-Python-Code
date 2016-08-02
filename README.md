# Useful-Pandas-Commands

#Stripping 

Strips all numbers from column of strings:

df['Last Name'] = df['Last Name'].map(lambda x: x.strip('0123456789'))

Or, just from left and right:

df['result'] = df['result'].map(lambda x: x.lstrip('+-').rstrip('aAbBcC'))

Strip white space from leading and trailing edge:

df["Address"] = df["Address"].map(str.strip)
