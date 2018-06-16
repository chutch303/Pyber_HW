

```python
from matplotlib import pyplot as plt
%matplotlib inline
import seaborn as sns
import pandas as pd
```


```python
city_df = pd.read_csv("raw_data/city_data.csv")
ride_df= pd.read_csv("raw_data/ride_data.csv")
```


```python
city_df.head()
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
      <td>Richardfort</td>
      <td>38</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Williamsstad</td>
      <td>59</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Port Angela</td>
      <td>67</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Rodneyfort</td>
      <td>34</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>West Robert</td>
      <td>39</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python
# number of cities. length = 120
city_df['city'].value_counts()
```




    South Marychester       1
    East Kaylahaven         1
    Williamsonville         1
    West Hannah             1
    Port Shane              1
    West Christopherberg    1
    Rogerston               1
    South Karenland         1
    New Paulville           1
    South Jack              1
    Williamsview            1
    West Samuelburgh        1
    Nicolechester           1
    Sotoville               1
    North Richardhaven      1
    South Brenda            1
    North Barbara           1
    South Latoya            1
    Robertport              1
    New Jacobville          1
    Newtonview              1
    Pattyland               1
    Martinezhaven           1
    Jerryton                1
    South Phillip           1
    South Teresa            1
    North Jason             1
    East Kentstad           1
    Josephside              1
    West Heather            1
                           ..
    Johnton                 1
    Amandaburgh             1
    Lake Scott              1
    Karenberg               1
    Royland                 1
    Lake Omar               1
    Veronicaberg            1
    North Holly             1
    Karenside               1
    Brandonfort             1
    Roberthaven             1
    Raymondhaven            1
    Barronchester           1
    West Patrickchester     1
    Lake Jonathanshire      1
    Barajasview             1
    North Jeffrey           1
    South Jennifer          1
    Lake Jamie              1
    Rodriguezview           1
    Davidfurt               1
    Lake Latoyabury         1
    Randallchester          1
    South Michelleport      1
    North Jasmine           1
    Bethanyland             1
    West Robert             1
    New Raymond             1
    East Aaronbury          1
    Erikaland               1
    Name: city, Length: 120, dtype: int64




```python
ride_df.head()
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
      <td>Lake Jonathanshire</td>
      <td>2018-01-14 10:14:22</td>
      <td>13.83</td>
      <td>5739410935873</td>
    </tr>
    <tr>
      <th>1</th>
      <td>South Michelleport</td>
      <td>2018-03-04 18:24:09</td>
      <td>30.24</td>
      <td>2343912425577</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Port Samanthamouth</td>
      <td>2018-02-24 04:29:00</td>
      <td>33.44</td>
      <td>2005065760003</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Rodneyfort</td>
      <td>2018-02-10 23:22:03</td>
      <td>23.44</td>
      <td>5149245426178</td>
    </tr>
    <tr>
      <th>4</th>
      <td>South Jack</td>
      <td>2018-03-06 04:28:35</td>
      <td>34.58</td>
      <td>3908451377344</td>
    </tr>
  </tbody>
</table>
</div>




```python
# average fare for each city
city_avg_fare = ride_df.groupby('city').fare.mean()
```


```python
# number of rides per city
city_ride_count = ride_df['city'].value_counts()
```


```python
# number of drivers per city
city_driver_count = city_df['driver_count']
```


```python
joined_df = pd.merge(ride_df, city_df, how='left', on=['city'])
joined_df.head()
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
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Lake Jonathanshire</td>
      <td>2018-01-14 10:14:22</td>
      <td>13.83</td>
      <td>5739410935873</td>
      <td>5</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>South Michelleport</td>
      <td>2018-03-04 18:24:09</td>
      <td>30.24</td>
      <td>2343912425577</td>
      <td>72</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Port Samanthamouth</td>
      <td>2018-02-24 04:29:00</td>
      <td>33.44</td>
      <td>2005065760003</td>
      <td>57</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Rodneyfort</td>
      <td>2018-02-10 23:22:03</td>
      <td>23.44</td>
      <td>5149245426178</td>
      <td>34</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>South Jack</td>
      <td>2018-03-06 04:28:35</td>
      <td>34.58</td>
      <td>3908451377344</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python
#assigning each city type to a color
#then using a dict lookup on the value in the dataframe to assign the city type a color?
city_colors = {'Urban':'lightcoral','Suburban':'gold','Rural':'lightskyblue'}
#create new column in city_df using city types to assign colors:
city_df['color'] = city_df['type'].apply(lambda x: city_colors[x])
```


```python
#group by colors and create a scatter plot in order to get legend for three different types
city_type_group = city_df.groupby('type')

```


```python
plt.figure(figsize=(10, 10), dpi=80)
plt.scatter(city_ride_count, city_avg_fare, s=city_driver_count*10, color=city_df['color'], alpha=0.5, linewidths=1)
plt.xlabel('Total Ride Count per City')
plt.ylabel('Average Fare ($)')
plt.title('Pyber Ride Sharing Data')

#need a legend for color type
#plt.legend(loc = "upper right")
```




    Text(0.5,1,'Pyber Ride Sharing Data')




![png](output_11_1.png)



```python
#% of Total Fares by City Type
fare_group = joined_df.groupby('type').fare.sum()
plt.pie(fare_group, 
        explode=(0, 0, 0.1), 
        colors = ('lightskyblue', 'gold', 'lightcoral'), 
        labels = ('Rural', 'Suburban', 'Urban'), 
        shadow=True, 
        startangle=90, 
        autopct='%1.1f%%')
plt.axis('equal')
plt.title('Percent of Total Fares by City Type')
```




    Text(0.5,1,'Percent of Total Fares by City Type')




![png](output_12_1.png)



```python
#% of Total Rides by City Type
ride_group = joined_df.groupby('type').ride_id.count()
plt.pie(ride_group, 
        explode=(0, 0, 0.1), 
        colors = ('lightskyblue', 'gold', 'lightcoral'), 
        labels = ('Rural', 'Suburban', 'Urban'), 
        shadow=True, 
        startangle=90, 
        autopct='%1.1f%%')
plt.axis('equal')
plt.title('Percent of Total Rides by City Type')
```




    Text(0.5,1,'Percent of Total Rides by City Type')




![png](output_13_1.png)



```python
#% of Total Drivers by City Type
driver_group = joined_df.groupby('type').driver_count.sum()
plt.pie(driver_group, 
        explode=(0, 0, 0.1), 
        colors = ('lightskyblue', 'gold', 'lightcoral'), 
        labels = ('Rural', 'Suburban', 'Urban'), 
        shadow=True, 
        startangle=90, 
        autopct='%1.1f%%')
plt.axis('equal')
plt.title('Percent of Total Drivers by City Type')
```




    Text(0.5,1,'Percent of Total Drivers by City Type')




![png](output_14_1.png)



```python
joined_df.groupby('type').fare.mean()
```




    type
    Rural       34.623440
    Suburban    30.970128
    Urban       24.525772
    Name: fare, dtype: float64


