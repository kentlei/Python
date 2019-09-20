# Python
#learn

import numpy as np
import pandas as pd
from scipy import stats, integrate
import matplotlib as mpl
import matplotlib.pyplot as plt
import seaborn as sns
%matplotlib inline

df = pd.read_excel(r'L:\kentlei\Python data\2778price.xlsx', skiprows=6, na_values='NAN', parse_dates
                   =['Date']).set_index('Date')
print(df.head(10))

df1 = pd.read_excel(r'L:\kentlei\Python data\2778price.xlsx', sheet_name='Champion', skiprows=6, na_values='NAN', parse_dates
                   =['Date']).set_index('Date')
HSI = pd.read_excel(r'L:\kentlei\Python data\2778price.xlsx', sheet_name='HSI', skiprows=6, na_values='NAN', parse_dates
                   =['Date']).set_index('Date')


HSI['% Change'] = HSI['PX_LAST'].pct_change()
combined_listings = pd.concat([df1, HSI])
res = pd.merge(df1, HSI, on=['Date'])

print(HSI.head(10))
print(combined_listings.head(10))
print(res.head(10))

#####begin to draw picture
plt.figure(figsize=(50,50))
df[['PX_LAST', 'PX_VOLUME']].plot(secondary_y='PX_VOLUME', title='2778.HK')


res[['PX_LAST_x', 'PX_LAST_y']].plot(secondary_y='PX_LAST_y', title='2778 vs HSI')
plt.xlabel('Date')
plt.ylabel('Price')
plt.show()

##use seaborn
sns.set_style('white')
sns.distplot(df['PX_LAST'], hist=False, rug=True, kde_kws={'shade':True})
plt.show()

sns.regplot(data=res, x='PX_LAST_y', y='PX_LAST_x')
plt.show()


# Set the style to white
sns.set_style('white')
# Create a regression plot
sns.lmplot(data=df,
           x='PX_LAST',
           y='PX_VOLUME')

# Remove the spines
sns.despine()
# Show the plot and clear the figure
plt.show()
plt.clf()


# Set style, enable color code, and create a magenta distplot
sns.set(color_codes=True)
sns.distplot(df['PX_LAST'], color='m')
# Show the plot
plt.show()
