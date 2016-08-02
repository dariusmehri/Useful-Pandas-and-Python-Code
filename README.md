# Useful-Pandas-Commands

#Stripping 

Strips all numbers from column of strings:

df['Last Name'] = df['Last Name'].map(lambda x: x.strip('0123456789'))
