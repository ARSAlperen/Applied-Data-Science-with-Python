
# Pivot Table


```python
import pandas as pd
import numpy as np
```


```python
df = pd.read_csv('resources/week-3/datasets/cwurData.csv')
df.head()

def create_ranking_cate(rank):
    if rank<=100:
        return "First Tier"
    elif rank<=200:
        return "Second Tier"
    elif rank<=300:
        return "Third Tier"
    else:
        return "Other Tier"
    

df["Ranking"]=df["world_rank"].apply(lambda x:create_ranking_cate(x))
df.head()

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
      <th>world_rank</th>
      <th>institution</th>
      <th>country</th>
      <th>national_rank</th>
      <th>quality_of_education</th>
      <th>alumni_employment</th>
      <th>quality_of_faculty</th>
      <th>publications</th>
      <th>influence</th>
      <th>citations</th>
      <th>broad_impact</th>
      <th>patents</th>
      <th>score</th>
      <th>year</th>
      <th>Ranking</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Harvard University</td>
      <td>USA</td>
      <td>1</td>
      <td>7</td>
      <td>9</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>NaN</td>
      <td>5</td>
      <td>100.00</td>
      <td>2012</td>
      <td>First Tier</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Massachusetts Institute of Technology</td>
      <td>USA</td>
      <td>2</td>
      <td>9</td>
      <td>17</td>
      <td>3</td>
      <td>12</td>
      <td>4</td>
      <td>4</td>
      <td>NaN</td>
      <td>1</td>
      <td>91.67</td>
      <td>2012</td>
      <td>First Tier</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Stanford University</td>
      <td>USA</td>
      <td>3</td>
      <td>17</td>
      <td>11</td>
      <td>5</td>
      <td>4</td>
      <td>2</td>
      <td>2</td>
      <td>NaN</td>
      <td>15</td>
      <td>89.50</td>
      <td>2012</td>
      <td>First Tier</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>University of Cambridge</td>
      <td>United Kingdom</td>
      <td>1</td>
      <td>10</td>
      <td>24</td>
      <td>4</td>
      <td>16</td>
      <td>16</td>
      <td>11</td>
      <td>NaN</td>
      <td>50</td>
      <td>86.17</td>
      <td>2012</td>
      <td>First Tier</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>California Institute of Technology</td>
      <td>USA</td>
      <td>4</td>
      <td>2</td>
      <td>29</td>
      <td>7</td>
      <td>37</td>
      <td>22</td>
      <td>22</td>
      <td>NaN</td>
      <td>18</td>
      <td>85.21</td>
      <td>2012</td>
      <td>First Tier</td>
    </tr>
  </tbody>
</table>
</div>




```python
pivot_table=df.pivot_table(values='score', index=['country',"year"], columns='Ranking', aggfunc=[np.mean,np.max],
              margins=True)
pivot_table.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th></th>
      <th colspan="5" halign="left">mean</th>
      <th colspan="5" halign="left">amax</th>
    </tr>
    <tr>
      <th></th>
      <th>Ranking</th>
      <th>First Tier</th>
      <th>Other Tier</th>
      <th>Second Tier</th>
      <th>Third Tier</th>
      <th>All</th>
      <th>First Tier</th>
      <th>Other Tier</th>
      <th>Second Tier</th>
      <th>Third Tier</th>
      <th>All</th>
    </tr>
    <tr>
      <th>country</th>
      <th>year</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">Argentina</th>
      <th>2014</th>
      <td>NaN</td>
      <td>44.732500</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>44.732500</td>
      <td>NaN</td>
      <td>45.66</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>45.66</td>
    </tr>
    <tr>
      <th>2015</th>
      <td>NaN</td>
      <td>44.593333</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>44.593333</td>
      <td>NaN</td>
      <td>45.37</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>45.37</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">Australia</th>
      <th>2012</th>
      <td>44.155</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>44.155000</td>
      <td>44.18</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>44.18</td>
    </tr>
    <tr>
      <th>2013</th>
      <td>44.635</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>44.635000</td>
      <td>44.77</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>44.77</td>
    </tr>
    <tr>
      <th>2014</th>
      <td>51.505</td>
      <td>44.778000</td>
      <td>49.3325</td>
      <td>47.47</td>
      <td>46.050741</td>
      <td>51.58</td>
      <td>45.97</td>
      <td>50.37</td>
      <td>47.47</td>
      <td>51.58</td>
    </tr>
  </tbody>
</table>
</div>




```python
pivot_table.stack().head()
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
      <th></th>
      <th></th>
      <th>mean</th>
      <th>amax</th>
    </tr>
    <tr>
      <th>country</th>
      <th>year</th>
      <th>Ranking</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="4" valign="top">Argentina</th>
      <th rowspan="2" valign="top">2014</th>
      <th>Other Tier</th>
      <td>44.732500</td>
      <td>45.66</td>
    </tr>
    <tr>
      <th>All</th>
      <td>44.732500</td>
      <td>45.66</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">2015</th>
      <th>Other Tier</th>
      <td>44.593333</td>
      <td>45.37</td>
    </tr>
    <tr>
      <th>All</th>
      <td>44.593333</td>
      <td>45.37</td>
    </tr>
    <tr>
      <th>Australia</th>
      <th>2012</th>
      <th>First Tier</th>
      <td>44.155000</td>
      <td>44.18</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
