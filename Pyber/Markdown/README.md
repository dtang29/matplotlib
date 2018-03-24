

```python
#import dependencies
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
```


```python
city_data = pd.read_csv("raw_data/city_data.csv")
ride_data = pd.read_csv("raw_data/ride_data.csv")

ride_data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Sarabury</td>
      <td>2016-01-16 13:49:27</td>
      <td>38.35</td>
      <td>5403689035038</td>
    </tr>
    <tr>
      <th>1</th>
      <td>South Roy</td>
      <td>2016-01-02 18:42:34</td>
      <td>17.49</td>
      <td>4036272335942</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Wiseborough</td>
      <td>2016-01-21 17:35:29</td>
      <td>44.18</td>
      <td>3645042422587</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Spencertown</td>
      <td>2016-07-31 14:53:22</td>
      <td>6.87</td>
      <td>2242596575892</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Nguyenbury</td>
      <td>2016-07-09 04:42:44</td>
      <td>6.28</td>
      <td>1543057793673</td>
    </tr>
  </tbody>
</table>
</div>




```python
grouped_rides = ride_data.groupby("city")
rides_per_city = grouped_rides["ride_id"].count()
average_fare = grouped_rides["fare"].mean()

df = pd.DataFrame({"Number of Riders": rides_per_city,
                  "Average Fare": average_fare})
df = df.reset_index()
df

merge = pd.merge(df, city_data, on="city")

urban = merge.loc[merge["type"] == "Urban"]
suburban = merge.loc[merge["type"] == "Suburban"]
rural = merge.loc[merge["type"] == "Rural"]

urban = plt.scatter(urban["Number of Riders"].values, urban["Average Fare"].values, s=urban["driver_count"].values**1.6, marker="o", facecolors="lightcoral", edgecolors="black", alpha=0.60, label="Urban")
suburban = plt.scatter(suburban["Number of Riders"].values, suburban["Average Fare"].values, s=suburban["driver_count"].values**1.6, marker="o", facecolors="LightSkyBlue", edgecolors="black", alpha=0.75, label="Suburban")
rural = plt.scatter(rural["Number of Riders"].values, rural["Average Fare"].values, s=rural["driver_count"].values**1.6, marker="o", facecolors="Gold", edgecolors="black", alpha=0.75, label="Rural")

plt.legend(handles=[urban, suburban, rural], loc="best")
plt.title("Pyber Ride Sharing Data")
plt.xlabel("Total Number of Rides (Per City)")
plt.ylabel("Average Fare ($)")

urban
```




    <matplotlib.collections.PathCollection at 0x109ba8080>




![png](output_2_1.png)



```python
merged = pd.merge(ride_data, city_data, on="city", how="left")
merged

city_data
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Nguyenbury</td>
      <td>8</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>East Douglas</td>
      <td>12</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>West Dawnfurt</td>
      <td>34</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Rodriguezburgh</td>
      <td>52</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>5</th>
      <td>South Josephville</td>
      <td>4</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>6</th>
      <td>West Sydneyhaven</td>
      <td>70</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Travisville</td>
      <td>37</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Torresshire</td>
      <td>70</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Lisaville</td>
      <td>66</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Mooreview</td>
      <td>34</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Smithhaven</td>
      <td>67</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Carrollfort</td>
      <td>55</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Port Josephfurt</td>
      <td>28</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Lake Jeffreyland</td>
      <td>15</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>15</th>
      <td>South Louis</td>
      <td>12</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>16</th>
      <td>West Peter</td>
      <td>61</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Kimberlychester</td>
      <td>13</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Alyssaberg</td>
      <td>67</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Sarabury</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Yolandafurt</td>
      <td>7</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Edwardsbury</td>
      <td>11</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>22</th>
      <td>New Andreamouth</td>
      <td>42</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>23</th>
      <td>New David</td>
      <td>31</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Arnoldview</td>
      <td>41</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Williamshire</td>
      <td>70</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Lisatown</td>
      <td>47</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>27</th>
      <td>New Aaron</td>
      <td>60</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Swansonbury</td>
      <td>64</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Fosterside</td>
      <td>69</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>96</th>
      <td>New Lynn</td>
      <td>20</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>97</th>
      <td>Port Jose</td>
      <td>11</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>98</th>
      <td>Johnland</td>
      <td>13</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>99</th>
      <td>West Tony</td>
      <td>17</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>100</th>
      <td>Port James</td>
      <td>3</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Campbellport</td>
      <td>26</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>102</th>
      <td>Port Guytown</td>
      <td>26</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>103</th>
      <td>Webstertown</td>
      <td>26</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>104</th>
      <td>Clarkstad</td>
      <td>21</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>105</th>
      <td>North Tracyfort</td>
      <td>18</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>106</th>
      <td>Martinmouth</td>
      <td>5</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>107</th>
      <td>New Jessicamouth</td>
      <td>22</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>108</th>
      <td>South Elizabethmouth</td>
      <td>3</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>109</th>
      <td>East Troybury</td>
      <td>3</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>110</th>
      <td>Kinghaven</td>
      <td>3</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>111</th>
      <td>New Johnbury</td>
      <td>6</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>112</th>
      <td>Erikport</td>
      <td>3</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>113</th>
      <td>Jacksonfort</td>
      <td>6</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>114</th>
      <td>Shelbyhaven</td>
      <td>9</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>115</th>
      <td>Matthewside</td>
      <td>4</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>116</th>
      <td>Kennethburgh</td>
      <td>3</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>117</th>
      <td>South Joseph</td>
      <td>3</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>118</th>
      <td>Manuelchester</td>
      <td>7</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>119</th>
      <td>Stevensport</td>
      <td>6</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>120</th>
      <td>North Whitney</td>
      <td>10</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>121</th>
      <td>East Stephen</td>
      <td>6</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>122</th>
      <td>East Leslie</td>
      <td>9</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>123</th>
      <td>Hernandezshire</td>
      <td>10</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>124</th>
      <td>Horneland</td>
      <td>8</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>125</th>
      <td>West Kevintown</td>
      <td>5</td>
      <td>Rural</td>
    </tr>
  </tbody>
</table>
<p>126 rows × 3 columns</p>
</div>




```python
#Create a pie chart - % of total fares by city type


#Get the sum of the fares of the 'grouped by city' data
total_fares = grouped_rides["fare"].sum()

#Store the total fares by city into a dataframe and reset index to prep for a merge with city data
total_fares_city_df = pd.DataFrame({"Total Fares": total_fares}).reset_index()

#Merge the total_fares_df and the city_data to bring in the city types
total_fares_merge = pd.merge(total_fares_city_df, city_data, on="city")

#Merge will generate duplicates in City column. Drop them.
total_fares_merge = total_fares_merge.drop_duplicates(subset=["city"])

#Group the new dataframe by type
grouped_type_fares = total_fares_merge.groupby("type")

#Get the sum of the total fares of the 'grouped by city type' data
fares_by_city_type = grouped_type_fares["Total Fares"].sum()

#Store the total fares by city type into a new dataframe
total_fares_city_type = pd.DataFrame({"Total Fares": fares_by_city_type}).reset_index()
explode = (0,0,0.1)

colors = ["gold", "lightskyblue", "lightcoral"]


#total_fares_merge.to_csv("raw_data/test.csv")
plt.pie(total_fares_city_type["Total Fares"].values, explode=explode, labels=total_fares_city_type["type"].values, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=140)
plt.title("% of Total Fares by City Type")


```


![png](output_4_0.png)



```python
#Create a pie chart - % of total rides by city type

#Get the count of ids of the 'grouped by city' data
total_rides = grouped_rides["ride_id"].count()

#Store the total rides by city into a dataframe and reset index to prep for a merge with city data
total_rides_city_df = pd.DataFrame({"Total Rides": total_rides}).reset_index()

#Merge the total_rides_df and the city_data to bring in the city types
total_rides_merge = pd.merge(total_rides_city_df, city_data, on="city")

#Merge will generate duplicates in City column. Drop them.
total_rides_merge = total_rides_merge.drop_duplicates(subset=["city"])

total_rides_merge
#Group the new dataframe by type
grouped_type = total_rides_merge.groupby("type")

#Get the sum of the total rides of the 'grouped by city type' data
rides_by_city_type = grouped_type["Total Rides"].sum()


#Store the total rides by city type into a new dataframe
total_rides_city_type = pd.DataFrame({"Total Rides": rides_by_city_type}).reset_index()
total_rides_city_type

#Define the attritbutes for the pie parameters
explode = (0,0,0.1)
colors = ["gold", "lightskyblue", "lightcoral"]

plt.pie(total_rides_city_type["Total Rides"].values, explode=explode, labels=total_rides_city_type["type"].values, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=140)
plt.title("% of Total Rides by City Type")


```




    Text(0.5,1,'% of Total Rides by City Type')




![png](output_5_1.png)



```python
#Create a pie chart - % of total drivers by city type


#Get the sum of the total drivers of the 'grouped by city type' data
drivers_by_city_type = grouped_type["driver_count"].sum()

#Store the total drivers by city type into a new dataframe
total_drivers_city_type = pd.DataFrame({"Total drivers": drivers_by_city_type}).reset_index()
total_drivers_city_type

#Define the attritbutes for the pie parameters
explode = (0,0,0.1)
colors = ["gold", "lightskyblue", "lightcoral"]

plt.pie(total_drivers_city_type["Total drivers"].values, explode=explode, labels=total_drivers_city_type["type"].values, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=140)
plt.title("% of Total Drivers by City Type")
```




    Text(0.5,1,'% of Total Drivers by City Type')




![png](output_6_1.png)


3 Observable Trends:

1. People living in urban cities are more likely to take Pyber and their average fare is lower than suburban and rural areas.
2. There are more drivers in the urban cities most likely due to demand for pyber services in urban areas.
3. Rides in rural areas have a much higher fare due to the fact that there is less demand for those services. 
