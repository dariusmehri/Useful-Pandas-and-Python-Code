# Useful-Pandas-Commands

#Stripping 

Strips all numbers from column of strings
w3['Last Name'] = w3['Last Name'].map(lambda x: x.strip('0123456789'))
