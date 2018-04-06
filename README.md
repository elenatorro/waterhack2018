
## Importamos librerias 


```python
import pandas as pd 
import matplotlib.pyplot as plt
%matplotlib inline
```

# Households


```python
general = pd.read_csv('/Users/servandotorres/Documents/data/households/general.csv')
economy =  pd.read_csv('/Users/servandotorres/Documents/data/households/economy.csv')
house_info = pd.read_csv('/Users/servandotorres/Documents/data/households/households_info.csv')
social_services_access = pd.read_csv('/Users/servandotorres/Documents/data/households/social_services_access.csv')
economy_1 = pd.read_csv('/Users/servandotorres/Documents/data/households/economy.csv', index_col='village')
```

## Empezamos el analisis 

## Dataset general 


```python
general.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>gender</th>
      <th>hh_head</th>
      <th>relation_hh_head</th>
      <th>gender_hh_head</th>
      <th>district</th>
      <th>ward</th>
      <th>village</th>
      <th>subvillage</th>
      <th>house_condition</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>V4-01</td>
      <td>Male</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Muheza</td>
      <td>Misalai</td>
      <td>Kazita</td>
      <td>Kwemuyu</td>
      <td>The house is not good</td>
    </tr>
    <tr>
      <th>1</th>
      <td>V4-02</td>
      <td>Female</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Muheza</td>
      <td>Misalai</td>
      <td>Kazita</td>
      <td>Kwemuyu</td>
      <td>The house is not good</td>
    </tr>
    <tr>
      <th>2</th>
      <td>V4-03</td>
      <td>Female</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Muheza</td>
      <td>Misalai</td>
      <td>Kazita</td>
      <td>Kwemuyu</td>
      <td>The house is normal</td>
    </tr>
    <tr>
      <th>3</th>
      <td>V4-04</td>
      <td>Female</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Muheza</td>
      <td>Misalai</td>
      <td>Kazita</td>
      <td>Kwemuyu</td>
      <td>The house is normal</td>
    </tr>
    <tr>
      <th>4</th>
      <td>V4-05</td>
      <td>Male</td>
      <td>Yes</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Muheza</td>
      <td>Misalai</td>
      <td>Kazita</td>
      <td>Kwemuyu</td>
      <td>Good house</td>
    </tr>
  </tbody>
</table>
</div>




```python
general.isnull().sum()
#esta un poco sucio
```




    id                    0
    gender                0
    hh_head               0
    relation_hh_head    226
    gender_hh_head      226
    district              0
    ward                  0
    village               0
    subvillage            0
    house_condition      46
    dtype: int64




```python
general.head()
general.shape
```




    (339, 10)




```python
# Estadistica descriptiva 
general.describe()

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>gender</th>
      <th>hh_head</th>
      <th>relation_hh_head</th>
      <th>gender_hh_head</th>
      <th>district</th>
      <th>ward</th>
      <th>village</th>
      <th>subvillage</th>
      <th>house_condition</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>339</td>
      <td>339</td>
      <td>339</td>
      <td>113</td>
      <td>113</td>
      <td>339</td>
      <td>339</td>
      <td>339</td>
      <td>339</td>
      <td>293</td>
    </tr>
    <tr>
      <th>unique</th>
      <td>339</td>
      <td>2</td>
      <td>2</td>
      <td>5</td>
      <td>2</td>
      <td>1</td>
      <td>2</td>
      <td>8</td>
      <td>39</td>
      <td>75</td>
    </tr>
    <tr>
      <th>top</th>
      <td>V3-09</td>
      <td>Male</td>
      <td>Yes</td>
      <td>husband / wife</td>
      <td>Male</td>
      <td>Muheza</td>
      <td>Misalai</td>
      <td>Misalai</td>
      <td>Mlalo</td>
      <td>Normal house</td>
    </tr>
    <tr>
      <th>freq</th>
      <td>1</td>
      <td>179</td>
      <td>226</td>
      <td>74</td>
      <td>100</td>
      <td>339</td>
      <td>224</td>
      <td>70</td>
      <td>20</td>
      <td>77</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Descricion categorica 
general.describe(include=[np.object, pd.Categorical]).T

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>count</th>
      <th>unique</th>
      <th>top</th>
      <th>freq</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>id</th>
      <td>339</td>
      <td>339</td>
      <td>V3-09</td>
      <td>1</td>
    </tr>
    <tr>
      <th>gender</th>
      <td>339</td>
      <td>2</td>
      <td>Male</td>
      <td>179</td>
    </tr>
    <tr>
      <th>hh_head</th>
      <td>339</td>
      <td>2</td>
      <td>Yes</td>
      <td>226</td>
    </tr>
    <tr>
      <th>relation_hh_head</th>
      <td>113</td>
      <td>5</td>
      <td>husband / wife</td>
      <td>74</td>
    </tr>
    <tr>
      <th>gender_hh_head</th>
      <td>113</td>
      <td>2</td>
      <td>Male</td>
      <td>100</td>
    </tr>
    <tr>
      <th>district</th>
      <td>339</td>
      <td>1</td>
      <td>Muheza</td>
      <td>339</td>
    </tr>
    <tr>
      <th>ward</th>
      <td>339</td>
      <td>2</td>
      <td>Misalai</td>
      <td>224</td>
    </tr>
    <tr>
      <th>village</th>
      <td>339</td>
      <td>8</td>
      <td>Misalai</td>
      <td>70</td>
    </tr>
    <tr>
      <th>subvillage</th>
      <td>339</td>
      <td>39</td>
      <td>Mlalo</td>
      <td>20</td>
    </tr>
    <tr>
      <th>house_condition</th>
      <td>293</td>
      <td>75</td>
      <td>Normal house</td>
      <td>77</td>
    </tr>
  </tbody>
</table>
</div>



## Economia 


```python
economy.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>village</th>
      <th>acres_own_land</th>
      <th>acres_rent_land</th>
      <th>acres_not_paying_land</th>
      <th>certificate</th>
      <th>acres_cultivate_land</th>
      <th>land_use</th>
      <th>decision_maker</th>
      <th>savings</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>V4-01</td>
      <td>Kazita</td>
      <td>7.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>No</td>
      <td>7.0</td>
      <td>Crop cultivation</td>
      <td>father</td>
      <td>Yes</td>
    </tr>
    <tr>
      <th>1</th>
      <td>V4-02</td>
      <td>Kazita</td>
      <td>0.5</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>No</td>
      <td>0.5</td>
      <td>Crop cultivation</td>
      <td>mother</td>
      <td>No</td>
    </tr>
    <tr>
      <th>2</th>
      <td>V4-03</td>
      <td>Kazita</td>
      <td>4.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>No</td>
      <td>1.0</td>
      <td>Crop cultivation</td>
      <td>mother</td>
      <td>Yes</td>
    </tr>
    <tr>
      <th>3</th>
      <td>V4-04</td>
      <td>Kazita</td>
      <td>1.5</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>Yes</td>
      <td>1.5</td>
      <td>Crop cultivation</td>
      <td>both</td>
      <td>Yes</td>
    </tr>
    <tr>
      <th>4</th>
      <td>V4-05</td>
      <td>Kazita</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>No</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>father</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>
</div>



## Vision global de el tomador de decisiones 


```python
sns.countplot(y='decision_maker', data=economy)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1131985c0>




![png](output_14_1.png)



```python
#Valores nulos 
economy.isnull().sum()
```




    id                       0
    village                  0
    acres_own_land           0
    acres_rent_land          2
    acres_not_paying_land    2
    certificate              1
    acres_cultivate_land     2
    land_use                 6
    decision_maker           0
    savings                  0
    dtype: int64



### Superficie en propiedad por pueblo 


```python

ax = sns.barplot(x='village', y='acres_own_land', data=economy)
ax.figure.set_size_inches(16, 4)
```


![png](output_17_0.png)



```python
ax = sns.barplot(x='village', y='acres_own_land', hue='land_use', 
                 data=economy, palette='Greys')
ax.figure.set_size_inches(16,4)
```


![png](output_18_0.png)


# Propiedad


```python
ax = sns.barplot(x='village', y='acres_own_land', data=economy)
ax.figure.set_size_inches(16, 4)
```


![png](output_20_0.png)


# No paga


```python
ax = sns.barplot(x='village', y='acres_not_paying_land', data=economy)
ax.figure.set_size_inches(16, 4)
```


![png](output_22_0.png)


# Aquila


```python
ax = sns.barplot(x='village', y='acres_rent_land', data=economy)
ax.figure.set_size_inches(16, 4)
```


![png](output_24_0.png)



```python
house_info.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>village</th>
      <th>household_member</th>
      <th>gender</th>
      <th>age</th>
      <th>edu_level</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>V1-03</td>
      <td>Misalai</td>
      <td>1st member</td>
      <td>male</td>
      <td>80</td>
      <td>Primary</td>
    </tr>
    <tr>
      <th>1</th>
      <td>V4-01</td>
      <td>Kazita</td>
      <td>2nd member</td>
      <td>female</td>
      <td>42</td>
      <td>No formal education</td>
    </tr>
    <tr>
      <th>2</th>
      <td>V4-01</td>
      <td>Kazita</td>
      <td>3rd member</td>
      <td>female</td>
      <td>40</td>
      <td>No formal education</td>
    </tr>
    <tr>
      <th>3</th>
      <td>V4-01</td>
      <td>Kazita</td>
      <td>1st member</td>
      <td>male</td>
      <td>55</td>
      <td>Secundary</td>
    </tr>
    <tr>
      <th>4</th>
      <td>V4-01</td>
      <td>Kazita</td>
      <td>5th member</td>
      <td>female</td>
      <td>11</td>
      <td>Primary</td>
    </tr>
  </tbody>
</table>
</div>




```python
social_services_access.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>village</th>
      <th>primary_school</th>
      <th>service_quality</th>
      <th>secundary_school</th>
      <th>service_quality.1</th>
      <th>market_place</th>
      <th>service_quality.2</th>
      <th>dispensary</th>
      <th>service_quality.3</th>
      <th>...</th>
      <th>agriculture_storage</th>
      <th>service_quality.8</th>
      <th>agricultural_extension_service</th>
      <th>service_quality.9</th>
      <th>veterinary</th>
      <th>service_quality.10</th>
      <th>forest_service</th>
      <th>service_quality.11</th>
      <th>water_service</th>
      <th>service_quality.12</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>V4-01</td>
      <td>Kazita</td>
      <td>yes</td>
      <td>Bad</td>
      <td>no</td>
      <td>No</td>
      <td>no</td>
      <td>No</td>
      <td>no</td>
      <td>No</td>
      <td>...</td>
      <td>no</td>
      <td>No</td>
      <td>no</td>
      <td>No</td>
      <td>no</td>
      <td>No</td>
      <td>no</td>
      <td>No</td>
      <td>no</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1</th>
      <td>V4-02</td>
      <td>Kazita</td>
      <td>yes</td>
      <td>Good</td>
      <td>yes</td>
      <td>Good</td>
      <td>no</td>
      <td>No</td>
      <td>no</td>
      <td>No</td>
      <td>...</td>
      <td>no</td>
      <td>No</td>
      <td>no</td>
      <td>No</td>
      <td>yes</td>
      <td>Bad</td>
      <td>yes</td>
      <td>Bad</td>
      <td>no</td>
      <td>No</td>
    </tr>
    <tr>
      <th>2</th>
      <td>V4-03</td>
      <td>Kazita</td>
      <td>yes</td>
      <td>Good</td>
      <td>yes</td>
      <td>Good</td>
      <td>yes</td>
      <td>Good</td>
      <td>yes</td>
      <td>Good</td>
      <td>...</td>
      <td>no</td>
      <td>No</td>
      <td>no</td>
      <td>No</td>
      <td>no</td>
      <td>No</td>
      <td>yes</td>
      <td>Good</td>
      <td>yes</td>
      <td>Good</td>
    </tr>
    <tr>
      <th>3</th>
      <td>V4-04</td>
      <td>Kazita</td>
      <td>yes</td>
      <td>Good</td>
      <td>yes</td>
      <td>Good</td>
      <td>yes</td>
      <td>Good</td>
      <td>no</td>
      <td>No</td>
      <td>...</td>
      <td>no</td>
      <td>No</td>
      <td>no</td>
      <td>No</td>
      <td>yes</td>
      <td>Good</td>
      <td>yes</td>
      <td>Good</td>
      <td>yes</td>
      <td>Good</td>
    </tr>
    <tr>
      <th>4</th>
      <td>V4-05</td>
      <td>Kazita</td>
      <td>yes</td>
      <td>Good</td>
      <td>yes</td>
      <td>Good</td>
      <td>yes</td>
      <td>Good</td>
      <td>yes</td>
      <td>Good</td>
      <td>...</td>
      <td>no</td>
      <td>No</td>
      <td>no</td>
      <td>No</td>
      <td>no</td>
      <td>No</td>
      <td>no</td>
      <td>No</td>
      <td>yes</td>
      <td>Good</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 28 columns</p>
</div>



# Water access



```python
drinking_water_distance = pd.read_csv('/Users/servandotorres/Documents/data/water-access/drinking_water_distance.csv')
water_collection = pd.read_csv('/Users/servandotorres/Documents/data/water-access/water_collection.csv')
water_collection = pd.read_csv('/Users/servandotorres/Documents/data/water-access/water_collection.csv')
water_payment = pd.read_csv('/Users/servandotorres/Documents/data/water-access/water_payment.csv')
water_quality = pd.read_csv('/Users/servandotorres/Documents/data/water-access/water_quality.csv')
water_sanitation = pd.read_csv('/Users/servandotorres/Documents/data/water-access/water_sanitation.csv')



```


```python
drinking_water_distance['village']

import numpy as np
np.unique(drinking_water_distance['village'])
```




    array(['8 =Kwelumbizi', 'Kazita', 'Kizerui', 'Kwemsoso', 'Mgambo',
           'Misalai', 'Shambangeda', 'Zirai'], dtype=object)




```python
drinking_water_distance.head()

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>village</th>
      <th>rainy_season</th>
      <th>dry_season</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>V4-01</td>
      <td>Kazita</td>
      <td>1- 2 hours</td>
      <td>1- 2 hours</td>
    </tr>
    <tr>
      <th>1</th>
      <td>V4-02</td>
      <td>Kazita</td>
      <td>5 - 10 min</td>
      <td>5 - 10 min</td>
    </tr>
    <tr>
      <th>2</th>
      <td>V4-03</td>
      <td>Kazita</td>
      <td>5 - 10 min</td>
      <td>5 - 10 min</td>
    </tr>
    <tr>
      <th>3</th>
      <td>V4-04</td>
      <td>Kazita</td>
      <td>1- 2 hours</td>
      <td>1- 2 hours</td>
    </tr>
    <tr>
      <th>4</th>
      <td>V4-05</td>
      <td>Kazita</td>
      <td>&lt; 5 min</td>
      <td>&lt; 5 min</td>
    </tr>
  </tbody>
</table>
</div>




```python
water_collection.head()
#water_collection.describe(include=[np.object, pd.Categorical]).T
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>village</th>
      <th>collector</th>
      <th>no_buckets</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>V4-01</td>
      <td>Kazita</td>
      <td>Adult women</td>
      <td>6 - 7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>V4-02</td>
      <td>Kazita</td>
      <td>Adult women</td>
      <td>1 - 2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>V4-03</td>
      <td>Kazita</td>
      <td>Adult women</td>
      <td>2 - 3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>V4-04</td>
      <td>Kazita</td>
      <td>Adult women</td>
      <td>5 - 6</td>
    </tr>
    <tr>
      <th>4</th>
      <td>V4-05</td>
      <td>Kazita</td>
      <td>Adult men</td>
      <td>1 - 2</td>
    </tr>
  </tbody>
</table>
</div>




```python
water_payment.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>village</th>
      <th>rainy_season</th>
      <th>dry_season</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>V4-01</td>
      <td>Kazita</td>
      <td>No</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1</th>
      <td>V4-02</td>
      <td>Kazita</td>
      <td>No</td>
      <td>No</td>
    </tr>
    <tr>
      <th>2</th>
      <td>V4-03</td>
      <td>Kazita</td>
      <td>No</td>
      <td>No</td>
    </tr>
    <tr>
      <th>3</th>
      <td>V4-04</td>
      <td>Kazita</td>
      <td>No</td>
      <td>No</td>
    </tr>
    <tr>
      <th>4</th>
      <td>V4-05</td>
      <td>Kazita</td>
      <td>No</td>
      <td>No</td>
    </tr>
  </tbody>
</table>
</div>




```python
sns.countplot(y='dry_season', data=water_payment)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x11346a400>




![png](output_33_1.png)



```python
sns.countplot(y='rainy_season', data=water_payment)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1135ee710>




![png](output_34_1.png)



```python
water_quality.describe(include=[np.object, pd.Categorical]).T
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>count</th>
      <th>unique</th>
      <th>top</th>
      <th>freq</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>id</th>
      <td>339</td>
      <td>339</td>
      <td>V3-09</td>
      <td>1</td>
    </tr>
    <tr>
      <th>village</th>
      <td>339</td>
      <td>8</td>
      <td>Misalai</td>
      <td>70</td>
    </tr>
    <tr>
      <th>dry_season</th>
      <td>339</td>
      <td>5</td>
      <td>Clean</td>
      <td>152</td>
    </tr>
    <tr>
      <th>rainy_season</th>
      <td>339</td>
      <td>5</td>
      <td>Clean</td>
      <td>127</td>
    </tr>
  </tbody>
</table>
</div>



## Water Sanitation


```python
water_sanitation.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>village</th>
      <th>floor_material</th>
      <th>wall_material</th>
      <th>roof_material</th>
      <th>toilet_type</th>
      <th>toilet_satisfaction</th>
      <th>water_in_toilet</th>
      <th>rubbish_pit</th>
      <th>utensils_rack</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>V4-01</td>
      <td>Kazita</td>
      <td>earth</td>
      <td>mud bricks</td>
      <td>galvanised metal sheets / iron sheets</td>
      <td>flush toilet with flushing system</td>
      <td>fairly satisfied</td>
      <td>Water bucket in the toilet</td>
      <td>Yes</td>
      <td>Yes</td>
    </tr>
    <tr>
      <th>1</th>
      <td>V4-02</td>
      <td>Kazita</td>
      <td>earth</td>
      <td>mud bricks</td>
      <td>galvanised metal sheets / iron sheets</td>
      <td>simple pit latrine unimproved</td>
      <td>unsatisifed</td>
      <td>Water bucket in the toilet</td>
      <td>Yes</td>
      <td>Yes</td>
    </tr>
    <tr>
      <th>2</th>
      <td>V4-03</td>
      <td>Kazita</td>
      <td>earth</td>
      <td>mud and poles or stones</td>
      <td>galvanised metal sheets / iron sheets</td>
      <td>flush toilet</td>
      <td>very satisfied</td>
      <td>Water bucket in the toilet</td>
      <td>Yes</td>
      <td>Yes</td>
    </tr>
    <tr>
      <th>3</th>
      <td>V4-04</td>
      <td>Kazita</td>
      <td>earth</td>
      <td>mud and poles or stones</td>
      <td>galvanised metal sheets / iron sheets</td>
      <td>flush toilet with flushing system</td>
      <td>fairly satisfied</td>
      <td>No water in the toilet</td>
      <td>No</td>
      <td>Yes</td>
    </tr>
    <tr>
      <th>4</th>
      <td>V4-05</td>
      <td>Kazita</td>
      <td>earth</td>
      <td>baked or burnt bricks</td>
      <td>galvanised metal sheets / iron sheets</td>
      <td>flush toilet with flushing system</td>
      <td>fairly satisfied</td>
      <td>Water bucket in the toilet</td>
      <td>Yes</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>
</div>




```python
water_sanitation.describe(include=[np.object, pd.Categorical]).T
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>count</th>
      <th>unique</th>
      <th>top</th>
      <th>freq</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>id</th>
      <td>339</td>
      <td>339</td>
      <td>V3-09</td>
      <td>1</td>
    </tr>
    <tr>
      <th>village</th>
      <td>339</td>
      <td>8</td>
      <td>Misalai</td>
      <td>70</td>
    </tr>
    <tr>
      <th>floor_material</th>
      <td>339</td>
      <td>4</td>
      <td>earth</td>
      <td>261</td>
    </tr>
    <tr>
      <th>wall_material</th>
      <td>339</td>
      <td>6</td>
      <td>mud and poles or stones</td>
      <td>180</td>
    </tr>
    <tr>
      <th>roof_material</th>
      <td>339</td>
      <td>5</td>
      <td>galvanised metal sheets / iron sheets</td>
      <td>291</td>
    </tr>
    <tr>
      <th>toilet_type</th>
      <td>339</td>
      <td>6</td>
      <td>simple pit latrine unimproved</td>
      <td>189</td>
    </tr>
    <tr>
      <th>toilet_satisfaction</th>
      <td>339</td>
      <td>4</td>
      <td>fairly satisfied</td>
      <td>157</td>
    </tr>
    <tr>
      <th>water_in_toilet</th>
      <td>337</td>
      <td>4</td>
      <td>Water bucket in the toilet</td>
      <td>311</td>
    </tr>
    <tr>
      <th>rubbish_pit</th>
      <td>339</td>
      <td>2</td>
      <td>Yes</td>
      <td>211</td>
    </tr>
    <tr>
      <th>utensils_rack</th>
      <td>339</td>
      <td>2</td>
      <td>Yes</td>
      <td>202</td>
    </tr>
  </tbody>
</table>
</div>




```python

np.unique(water_quality['dry_season'])
water_quality.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>village</th>
      <th>dry_season</th>
      <th>rainy_season</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>V4-01</td>
      <td>Kazita</td>
      <td>Quite clean</td>
      <td>Quite clean</td>
    </tr>
    <tr>
      <th>1</th>
      <td>V4-02</td>
      <td>Kazita</td>
      <td>Quite clean</td>
      <td>Clean</td>
    </tr>
    <tr>
      <th>2</th>
      <td>V4-03</td>
      <td>Kazita</td>
      <td>Clean</td>
      <td>Clean</td>
    </tr>
    <tr>
      <th>3</th>
      <td>V4-04</td>
      <td>Kazita</td>
      <td>Clean</td>
      <td>Clean</td>
    </tr>
    <tr>
      <th>4</th>
      <td>V4-05</td>
      <td>Kazita</td>
      <td>Quite clean</td>
      <td>Quite clean</td>
    </tr>
  </tbody>
</table>
</div>




```python
ax = sns.countplot(y='dry_season', data=water_quality)
ax
```




    <matplotlib.axes._subplots.AxesSubplot at 0x11125cf98>



## Calidad del agua por estacion 

### Sequía 


```python
sns.countplot(y='dry_season', data=water_quality)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a1acab860>




![png](output_43_1.png)


### Lluvia 


```python
sns.countplot(y='rainy_season', data=water_quality)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x113643d30>




![png](output_45_1.png)

