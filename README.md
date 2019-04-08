# Using-Data-Aggregation-to-Analyse-Obama-s-Approval-Rating-from-2008-to-2017
#### Scatter graph, with median and percentile plots, displaying Obama's approval ratings from 2008 to 2017, using data imported from a CSV file. This was formatted for Jupyter Notebook.

![Using Data Aggregation to Analyse Obama's Approval Ratings](https://user-images.githubusercontent.com/48648985/55397104-53466880-553d-11e9-8c1d-f2494a23feb5.png)




#### Importing the libraries and modules:
import pandas as pd
from matplotlib import pyplot as plt

#### Importing the data from a .csv file:
data = pd.read_csv('obama.csv', parse_dates=['year_month'])
#### Using the parse_dates functions will instruct pandas to interpret the year's month as 
####  a series time stamps instead of as a string. A series of time stamps is needed to plot a
####  time series graph.
data.head()

![01 parse dates function to group data](https://user-images.githubusercontent.com/48648985/55742446-9e71e700-5a27-11e9-9752-ce5f523e2c30.png)

plt.plot(data.year_month, data.approve_percent, 'o', markersize=2, alpha=0.3)
plt.show()

![02 Showing basic time series scatter plot](https://user-images.githubusercontent.com/48648985/55743913-71bfce80-5a2b-11e9-90d4-5100a1f5ed9e.png)


#### To aggregate the data and summarise it, one method that is effective is to use the mean
####  approval percentage for each month. This can be acheived by using the groupby function:

data.groupby('year_month').mean()

#### This shows the mean approval percentage adn mean disapproval percentage for each month.

#### To show the mean:
data_mean = data.groupby('year_month').mean()
#### To also show the median as well as the mean:
data_median = data.groupby('year_month').median()


plt.plot(data_mean.index,data_mean.approve_percent, 'red')
#### data_mean.index provides the year's month column, treated as an index column in the 
####  data_mean data frame.

plt.plot(data_median.index, data_median.approve_percent, 'green')

plt.legend(['Mean', 'Median'])

#### These data_mean and median lines can be shown along side the oringal scatter graph data 
####  points by plotting:

plt.plot(data.year_month, data.approve_percent, 'o', markersize=2, alpha=0.3)


plt.show()

### Ploting the main graph:

#### To find the 25th and 75th percentiles:

data_25 = data.groupby('year_month').quantile(0.25)
data_75 = data.groupby('year_month').quantile(0.75)

fig = plt.figure(figsize=(18, 12), dpi= 80, facecolor='w', edgecolor='k')

plt.plot(data_75.index, data_75.approve_percent, 'green')
plt.plot(data_median.index, data_median.approve_percent, 'red')
plt.plot(data_25.index, data_25.approve_percent, 'blue')
plt.plot(data.year_month, data.approve_percent, 'o', markersize=2, alpha=0.8)

plt.legend(['75th Percentile', 'Median', '25th Percentile'])
plt.xlabel('Y E A R', fontsize='20', color='forestgreen')
plt.ylabel('A P P R O V A L %', fontsize='20', color='forestgreen')
plt.title('O B A M A \'S     A P P R O V A L     R A T I N G    %', fontsize='28', 
          color='forestgreen')
plt.show()
