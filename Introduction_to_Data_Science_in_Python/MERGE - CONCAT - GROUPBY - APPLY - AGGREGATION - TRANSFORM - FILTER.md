
# Merge Dataframes


```python
import pandas as pd

staff_df = pd.DataFrame([{'Name': 'Kelly', 'Role': 'Director of HR'},
                         {'Name': 'Sally', 'Role': 'Course liasion'},
                         {'Name': 'James', 'Role': 'Grader'}])


student_df = pd.DataFrame([{'Name': 'James', 'School': 'Business'},
                           {'Name': 'Mike', 'School': 'Law'},
                           {'Name': 'Sally', 'School': 'Engineering'}])

student_df
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
      <th>Name</th>
      <th>School</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>James</td>
      <td>Business</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Mike</td>
      <td>Law</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Sally</td>
      <td>Engineering</td>
    </tr>
  </tbody>
</table>
</div>



## UNION / FULL OUTER JOIN 


```python
pd.merge(staff_df,student_df,how="outer",on="Name")

pd.merge(staff_df,student_df,how="outer",left_on="Name",right_on="Name")

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
      <th>Name</th>
      <th>Role</th>
      <th>School</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Kelly</td>
      <td>Director of HR</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Sally</td>
      <td>Course liasion</td>
      <td>Engineering</td>
    </tr>
    <tr>
      <th>2</th>
      <td>James</td>
      <td>Grader</td>
      <td>Business</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Mike</td>
      <td>NaN</td>
      <td>Law</td>
    </tr>
  </tbody>
</table>
</div>



## INTERSECTION / INNER JOIN



```python
pd.merge(staff_df,student_df,how="inner",on="Name")

pd.merge(staff_df,student_df,how="inner",left_on="Name",right_on="Name")
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
      <th>Name</th>
      <th>Role</th>
      <th>School</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Sally</td>
      <td>Course liasion</td>
      <td>Engineering</td>
    </tr>
    <tr>
      <th>1</th>
      <td>James</td>
      <td>Grader</td>
      <td>Business</td>
    </tr>
  </tbody>
</table>
</div>



## LEFT JOIN


```python
pd.merge(staff_df,student_df,how="left",left_on="Name",right_on="Name")

pd.merge(staff_df,student_df,how="left",on="Name")
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
      <th>Name</th>
      <th>Role</th>
      <th>School</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Kelly</td>
      <td>Director of HR</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Sally</td>
      <td>Course liasion</td>
      <td>Engineering</td>
    </tr>
    <tr>
      <th>2</th>
      <td>James</td>
      <td>Grader</td>
      <td>Business</td>
    </tr>
  </tbody>
</table>
</div>



## RIGHT JOIN


```python
pd.merge(staff_df,student_df,how="right",left_on="Name",right_on="Name")

pd.merge(staff_df,student_df,how="right",on="Name")
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
      <th>Name</th>
      <th>Role</th>
      <th>School</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Sally</td>
      <td>Course liasion</td>
      <td>Engineering</td>
    </tr>
    <tr>
      <th>1</th>
      <td>James</td>
      <td>Grader</td>
      <td>Business</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Mike</td>
      <td>NaN</td>
      <td>Law</td>
    </tr>
  </tbody>
</table>
</div>



## More than one join columns


```python
staff_df = pd.DataFrame([{'Name': 'Kelly', 'Role': 'Director of HR', 
                          'Location': 'State Street'},
                         {'Name': 'Sally', 'Role': 'Course liasion', 
                          'Location': 'Washington Avenue'},
                         {'Name': 'James', 'Role': 'Grader', 
                          'Location': 'Washington Avenue'}])
student_df = pd.DataFrame([{'Name': 'James', 'School': 'Business', 
                            'Location': '1024 Billiard Avenue'},
                           {'Name': 'Mike', 'School': 'Law', 
                            'Location': 'Fraternity House #22'},
                           {'Name': 'Sally', 'School': 'Engineering', 
                            'Location': '512 Wilson Crescent'}])

pd.merge(staff_df,student_df,how="outer",on=["Name","Location"])
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
      <th>Name</th>
      <th>Role</th>
      <th>Location</th>
      <th>School</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Kelly</td>
      <td>Director of HR</td>
      <td>State Street</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Sally</td>
      <td>Course liasion</td>
      <td>Washington Avenue</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>James</td>
      <td>Grader</td>
      <td>Washington Avenue</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>James</td>
      <td>NaN</td>
      <td>1024 Billiard Avenue</td>
      <td>Business</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Mike</td>
      <td>NaN</td>
      <td>Fraternity House #22</td>
      <td>Law</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Sally</td>
      <td>NaN</td>
      <td>512 Wilson Crescent</td>
      <td>Engineering</td>
    </tr>
  </tbody>
</table>
</div>



# CONCAT DATAFRAME


```python
%%capture
df_2011 = pd.read_csv("resources/week-3/datasets/college_scorecard/MERGED2011_12_PP.csv", error_bad_lines=False)
df_2012 = pd.read_csv("resources/week-3/datasets/college_scorecard/MERGED2012_13_PP.csv", error_bad_lines=False)
df_2013 = pd.read_csv("resources/week-3/datasets/college_scorecard/MERGED2013_14_PP.csv", error_bad_lines=False)
```


```python
frames = [df_2011, df_2012, df_2013]
pd.concat(frames).head()
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
      <th>UNITID</th>
      <th>OPEID</th>
      <th>OPEID6</th>
      <th>INSTNM</th>
      <th>CITY</th>
      <th>STABBR</th>
      <th>ZIP</th>
      <th>ACCREDAGENCY</th>
      <th>INSTURL</th>
      <th>NPCURL</th>
      <th>...</th>
      <th>OMAWDP8_NOTFIRSTTIME_POOLED_SUPP</th>
      <th>OMENRUP_NOTFIRSTTIME_POOLED_SUPP</th>
      <th>OMENRYP_FULLTIME_POOLED_SUPP</th>
      <th>OMENRAP_FULLTIME_POOLED_SUPP</th>
      <th>OMAWDP8_FULLTIME_POOLED_SUPP</th>
      <th>OMENRUP_FULLTIME_POOLED_SUPP</th>
      <th>OMENRYP_PARTTIME_POOLED_SUPP</th>
      <th>OMENRAP_PARTTIME_POOLED_SUPP</th>
      <th>OMAWDP8_PARTTIME_POOLED_SUPP</th>
      <th>OMENRUP_PARTTIME_POOLED_SUPP</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>100654.0</td>
      <td>100200.0</td>
      <td>1002</td>
      <td>Alabama A &amp; M University</td>
      <td>Normal</td>
      <td>AL</td>
      <td>35762</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>100663.0</td>
      <td>105200.0</td>
      <td>1052</td>
      <td>University of Alabama at Birmingham</td>
      <td>Birmingham</td>
      <td>AL</td>
      <td>35294-0110</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>100690.0</td>
      <td>2503400.0</td>
      <td>25034</td>
      <td>Amridge University</td>
      <td>Montgomery</td>
      <td>AL</td>
      <td>36117-3553</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>100706.0</td>
      <td>105500.0</td>
      <td>1055</td>
      <td>University of Alabama in Huntsville</td>
      <td>Huntsville</td>
      <td>AL</td>
      <td>35899</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>100724.0</td>
      <td>100500.0</td>
      <td>1005</td>
      <td>Alabama State University</td>
      <td>Montgomery</td>
      <td>AL</td>
      <td>36104-0271</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 1977 columns</p>
</div>




```python
pd.concat(frames, keys=['2011','2012','2013']).head()
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
      <th>UNITID</th>
      <th>OPEID</th>
      <th>OPEID6</th>
      <th>INSTNM</th>
      <th>CITY</th>
      <th>STABBR</th>
      <th>ZIP</th>
      <th>ACCREDAGENCY</th>
      <th>INSTURL</th>
      <th>NPCURL</th>
      <th>...</th>
      <th>OMAWDP8_NOTFIRSTTIME_POOLED_SUPP</th>
      <th>OMENRUP_NOTFIRSTTIME_POOLED_SUPP</th>
      <th>OMENRYP_FULLTIME_POOLED_SUPP</th>
      <th>OMENRAP_FULLTIME_POOLED_SUPP</th>
      <th>OMAWDP8_FULLTIME_POOLED_SUPP</th>
      <th>OMENRUP_FULLTIME_POOLED_SUPP</th>
      <th>OMENRYP_PARTTIME_POOLED_SUPP</th>
      <th>OMENRAP_PARTTIME_POOLED_SUPP</th>
      <th>OMAWDP8_PARTTIME_POOLED_SUPP</th>
      <th>OMENRUP_PARTTIME_POOLED_SUPP</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">2011</th>
      <th>0</th>
      <td>100654.0</td>
      <td>100200.0</td>
      <td>1002</td>
      <td>Alabama A &amp; M University</td>
      <td>Normal</td>
      <td>AL</td>
      <td>35762</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>100663.0</td>
      <td>105200.0</td>
      <td>1052</td>
      <td>University of Alabama at Birmingham</td>
      <td>Birmingham</td>
      <td>AL</td>
      <td>35294-0110</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>100690.0</td>
      <td>2503400.0</td>
      <td>25034</td>
      <td>Amridge University</td>
      <td>Montgomery</td>
      <td>AL</td>
      <td>36117-3553</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>100706.0</td>
      <td>105500.0</td>
      <td>1055</td>
      <td>University of Alabama in Huntsville</td>
      <td>Huntsville</td>
      <td>AL</td>
      <td>35899</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>100724.0</td>
      <td>100500.0</td>
      <td>1005</td>
      <td>Alabama State University</td>
      <td>Montgomery</td>
      <td>AL</td>
      <td>36104-0271</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 1977 columns</p>
</div>



# METHOD CHAINNING 


```python
import pandas as pd
import numpy as np

# And lets look at some census data from the US
df = pd.read_csv('resources/week-3/datasets/census.csv')
(df.where(df['SUMLEV']==50)
    .dropna()
    .set_index(['STNAME','CTYNAME'])
    .rename(columns={'ESTIMATESBASE2010': 'Estimates Base 2010'})
    .head())

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
      <th>SUMLEV</th>
      <th>REGION</th>
      <th>DIVISION</th>
      <th>STATE</th>
      <th>COUNTY</th>
      <th>CENSUS2010POP</th>
      <th>Estimates Base 2010</th>
      <th>POPESTIMATE2010</th>
      <th>POPESTIMATE2011</th>
      <th>POPESTIMATE2012</th>
      <th>...</th>
      <th>RDOMESTICMIG2011</th>
      <th>RDOMESTICMIG2012</th>
      <th>RDOMESTICMIG2013</th>
      <th>RDOMESTICMIG2014</th>
      <th>RDOMESTICMIG2015</th>
      <th>RNETMIG2011</th>
      <th>RNETMIG2012</th>
      <th>RNETMIG2013</th>
      <th>RNETMIG2014</th>
      <th>RNETMIG2015</th>
    </tr>
    <tr>
      <th>STNAME</th>
      <th>CTYNAME</th>
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
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">Alabama</th>
      <th>Autauga County</th>
      <td>50.0</td>
      <td>3.0</td>
      <td>6.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>54571.0</td>
      <td>54571.0</td>
      <td>54660.0</td>
      <td>55253.0</td>
      <td>55175.0</td>
      <td>...</td>
      <td>7.242091</td>
      <td>-2.915927</td>
      <td>-3.012349</td>
      <td>2.265971</td>
      <td>-2.530799</td>
      <td>7.606016</td>
      <td>-2.626146</td>
      <td>-2.722002</td>
      <td>2.592270</td>
      <td>-2.187333</td>
    </tr>
    <tr>
      <th>Baldwin County</th>
      <td>50.0</td>
      <td>3.0</td>
      <td>6.0</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>182265.0</td>
      <td>182265.0</td>
      <td>183193.0</td>
      <td>186659.0</td>
      <td>190396.0</td>
      <td>...</td>
      <td>14.832960</td>
      <td>17.647293</td>
      <td>21.845705</td>
      <td>19.243287</td>
      <td>17.197872</td>
      <td>15.844176</td>
      <td>18.559627</td>
      <td>22.727626</td>
      <td>20.317142</td>
      <td>18.293499</td>
    </tr>
    <tr>
      <th>Barbour County</th>
      <td>50.0</td>
      <td>3.0</td>
      <td>6.0</td>
      <td>1.0</td>
      <td>5.0</td>
      <td>27457.0</td>
      <td>27457.0</td>
      <td>27341.0</td>
      <td>27226.0</td>
      <td>27159.0</td>
      <td>...</td>
      <td>-4.728132</td>
      <td>-2.500690</td>
      <td>-7.056824</td>
      <td>-3.904217</td>
      <td>-10.543299</td>
      <td>-4.874741</td>
      <td>-2.758113</td>
      <td>-7.167664</td>
      <td>-3.978583</td>
      <td>-10.543299</td>
    </tr>
    <tr>
      <th>Bibb County</th>
      <td>50.0</td>
      <td>3.0</td>
      <td>6.0</td>
      <td>1.0</td>
      <td>7.0</td>
      <td>22915.0</td>
      <td>22919.0</td>
      <td>22861.0</td>
      <td>22733.0</td>
      <td>22642.0</td>
      <td>...</td>
      <td>-5.527043</td>
      <td>-5.068871</td>
      <td>-6.201001</td>
      <td>-0.177537</td>
      <td>0.177258</td>
      <td>-5.088389</td>
      <td>-4.363636</td>
      <td>-5.403729</td>
      <td>0.754533</td>
      <td>1.107861</td>
    </tr>
    <tr>
      <th>Blount County</th>
      <td>50.0</td>
      <td>3.0</td>
      <td>6.0</td>
      <td>1.0</td>
      <td>9.0</td>
      <td>57322.0</td>
      <td>57322.0</td>
      <td>57373.0</td>
      <td>57711.0</td>
      <td>57776.0</td>
      <td>...</td>
      <td>1.807375</td>
      <td>-1.177622</td>
      <td>-1.748766</td>
      <td>-2.062535</td>
      <td>-1.369970</td>
      <td>1.859511</td>
      <td>-0.848580</td>
      <td>-1.402476</td>
      <td>-1.577232</td>
      <td>-0.884411</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 98 columns</p>
</div>



# APPLY FUNCTION


```python
def min_max(row):
    data = row[['POPESTIMATE2010',
                'POPESTIMATE2011',
                'POPESTIMATE2012',
                'POPESTIMATE2013',
                'POPESTIMATE2014',
                'POPESTIMATE2015']]
    return pd.Series({'min': np.min(data), 'max': np.max(data)})

df.apply(min_max, axis='columns').head()
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
      <th>min</th>
      <th>max</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>4785161</td>
      <td>4858979</td>
    </tr>
    <tr>
      <th>1</th>
      <td>54660</td>
      <td>55347</td>
    </tr>
    <tr>
      <th>2</th>
      <td>183193</td>
      <td>203709</td>
    </tr>
    <tr>
      <th>3</th>
      <td>26489</td>
      <td>27341</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22512</td>
      <td>22861</td>
    </tr>
  </tbody>
</table>
</div>



# LAMBDA FUNCTION


```python
rows = ['POPESTIMATE2010', 'POPESTIMATE2011', 'POPESTIMATE2012', 'POPESTIMATE2013','POPESTIMATE2014', 
        'POPESTIMATE2015']

df.apply(lambda x: np.max(x[rows]), axis=1).head()
```




    0    4858979
    1      55347
    2     203709
    3      27341
    4      22861
    dtype: int64



# GROUP BY (TOO FAST)

might be used in X06 daily report

used to split the data into groups based on some criteria. pandas objects can be split on any of their axes. 


```python
import pandas as pd
import numpy as np
df = pd.read_csv('resources/week-3/datasets/census.csv')
```


```python
df=df[df["SUMLEV"]==50]
```


```python
# group is the filter 
# frame is that filters data 
for group,frame in df.groupby("STNAME"):
    minimum=np.min(frame["CENSUS2010POP"])
    maximum=np.max(frame["CENSUS2010POP"])
    abstract=maximum-minimum
    
    print(group + " abstract is "+ str(abstract))
```

    Alabama abstract is 649421
    Alaska abstract is 291164
    Arizona abstract is 3808680
    Arkansas abstract is 377380
    California abstract is 9817430
    Colorado abstract is 621564
    Connecticut abstract is 798401
    Delaware abstract is 376169
    District of Columbia abstract is 0
    Florida abstract is 2488070
    Georgia abstract is 918864
    Hawaii abstract is 953117
    Idaho abstract is 391383
    Illinois abstract is 5190355
    Indiana abstract is 897265
    Iowa abstract is 426611
    Kansas abstract is 542932
    Kentucky abstract is 738814
    Louisiana abstract is 434919
    Maine abstract is 264139
    Maryland abstract is 951580
    Massachusetts abstract is 1492913
    Michigan abstract is 1818428
    Minnesota abstract is 1148867
    Mississippi abstract is 243879
    Missouri abstract is 996783
    Montana abstract is 147478
    Nebraska abstract is 516650
    Nevada abstract is 1950486
    New Hampshire abstract is 367666
    New Jersey abstract is 839033
    New Mexico abstract is 661869
    New York abstract is 2499864
    North Carolina abstract is 915221
    North Dakota abstract is 149051
    Ohio abstract is 1266687
    Oklahoma abstract is 716158
    Oregon abstract is 733893
    Pennsylvania abstract is 1520921
    Rhode Island abstract is 576792
    South Carolina abstract is 440992
    South Dakota abstract is 168462
    Tennessee abstract is 922567
    Texas abstract is 4092377
    Utah abstract is 1028596
    Vermont abstract is 150239
    Virginia abstract is 1079405
    Washington abstract is 1928983
    West Virginia abstract is 187346
    Wisconsin abstract is 943503
    Wyoming abstract is 89254


## Using GROUPBY with Function

__In order to do this you need to set the index of the data frame to be the column that you want to group by first.__


```python
def groupby_function(cols):
    if len(cols)<15:
        return 0
    elif len(cols)<20:
        return 1
    else:
        return 2

df=df.set_index("CTYNAME")

for group,frame in df.groupby(groupby_function):
    print("County of "+str(group) + " has " + str(len(frame)) + " record.")
```

    County of 0 has 2020 record.
    County of 1 has 1063 record.
    County of 2 has 59 record.


## GROUP BY FUNCTION WITH MULTIPLE COLUMNS



```python
df=pd.read_csv("resources/week-3/datasets/listings.csv")
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
      <th>id</th>
      <th>listing_url</th>
      <th>scrape_id</th>
      <th>last_scraped</th>
      <th>name</th>
      <th>summary</th>
      <th>space</th>
      <th>description</th>
      <th>experiences_offered</th>
      <th>neighborhood_overview</th>
      <th>...</th>
      <th>review_scores_value</th>
      <th>requires_license</th>
      <th>license</th>
      <th>jurisdiction_names</th>
      <th>instant_bookable</th>
      <th>cancellation_policy</th>
      <th>require_guest_profile_picture</th>
      <th>require_guest_phone_verification</th>
      <th>calculated_host_listings_count</th>
      <th>reviews_per_month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>12147973</td>
      <td>https://www.airbnb.com/rooms/12147973</td>
      <td>20160906204935</td>
      <td>2016-09-07</td>
      <td>Sunny Bungalow in the City</td>
      <td>Cozy, sunny, family home.  Master bedroom high...</td>
      <td>The house has an open and cozy feel at the sam...</td>
      <td>Cozy, sunny, family home.  Master bedroom high...</td>
      <td>none</td>
      <td>Roslindale is quiet, convenient and friendly. ...</td>
      <td>...</td>
      <td>NaN</td>
      <td>f</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>f</td>
      <td>moderate</td>
      <td>f</td>
      <td>f</td>
      <td>1</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3075044</td>
      <td>https://www.airbnb.com/rooms/3075044</td>
      <td>20160906204935</td>
      <td>2016-09-07</td>
      <td>Charming room in pet friendly apt</td>
      <td>Charming and quiet room in a second floor 1910...</td>
      <td>Small but cozy and quite room with a full size...</td>
      <td>Charming and quiet room in a second floor 1910...</td>
      <td>none</td>
      <td>The room is in Roslindale, a diverse and prima...</td>
      <td>...</td>
      <td>9.0</td>
      <td>f</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>t</td>
      <td>moderate</td>
      <td>f</td>
      <td>f</td>
      <td>1</td>
      <td>1.30</td>
    </tr>
    <tr>
      <th>2</th>
      <td>6976</td>
      <td>https://www.airbnb.com/rooms/6976</td>
      <td>20160906204935</td>
      <td>2016-09-07</td>
      <td>Mexican Folk Art Haven in Boston</td>
      <td>Come stay with a friendly, middle-aged guy in ...</td>
      <td>Come stay with a friendly, middle-aged guy in ...</td>
      <td>Come stay with a friendly, middle-aged guy in ...</td>
      <td>none</td>
      <td>The LOCATION: Roslindale is a safe and diverse...</td>
      <td>...</td>
      <td>10.0</td>
      <td>f</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>f</td>
      <td>moderate</td>
      <td>t</td>
      <td>f</td>
      <td>1</td>
      <td>0.47</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1436513</td>
      <td>https://www.airbnb.com/rooms/1436513</td>
      <td>20160906204935</td>
      <td>2016-09-07</td>
      <td>Spacious Sunny Bedroom Suite in Historic Home</td>
      <td>Come experience the comforts of home away from...</td>
      <td>Most places you find in Boston are small howev...</td>
      <td>Come experience the comforts of home away from...</td>
      <td>none</td>
      <td>Roslindale is a lovely little neighborhood loc...</td>
      <td>...</td>
      <td>10.0</td>
      <td>f</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>f</td>
      <td>moderate</td>
      <td>f</td>
      <td>f</td>
      <td>1</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7651065</td>
      <td>https://www.airbnb.com/rooms/7651065</td>
      <td>20160906204935</td>
      <td>2016-09-07</td>
      <td>Come Home to Boston</td>
      <td>My comfy, clean and relaxing home is one block...</td>
      <td>Clean, attractive, private room, one block fro...</td>
      <td>My comfy, clean and relaxing home is one block...</td>
      <td>none</td>
      <td>I love the proximity to downtown, the neighbor...</td>
      <td>...</td>
      <td>10.0</td>
      <td>f</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>f</td>
      <td>flexible</td>
      <td>f</td>
      <td>f</td>
      <td>1</td>
      <td>2.25</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 95 columns</p>
</div>




```python
df=df.set_index((["cancellation_policy","review_scores_value"])) 
#IMPORTANT PART
```


```python
def define_groups(item):
    if item[1]==10:
        return (item[0],"10")
    else:
        return (item[0],"no ten")
    
for group,frame in df.groupby(by=define_groups):
    print(str(group) + " has "+ str(len(frame)) + " value")
```

    ('flexible', '10') has 332 value
    ('flexible', 'no ten') has 667 value
    ('moderate', '10') has 379 value
    ('moderate', 'no ten') has 540 value
    ('strict', '10') has 459 value
    ('strict', 'no ten') has 1123 value
    ('super_strict_30', '10') has 7 value
    ('super_strict_30', 'no ten') has 78 value


# GROUP BY AND AGGREGATION


```python
df=pd.read_csv("resources/week-1/datasets/winequality-red.csv",delimiter=";")
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
      <th>fixed acidity</th>
      <th>volatile acidity</th>
      <th>citric acid</th>
      <th>residual sugar</th>
      <th>chlorides</th>
      <th>free sulfur dioxide</th>
      <th>total sulfur dioxide</th>
      <th>density</th>
      <th>pH</th>
      <th>sulphates</th>
      <th>alcohol</th>
      <th>quality</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7.4</td>
      <td>0.70</td>
      <td>0.00</td>
      <td>1.9</td>
      <td>0.076</td>
      <td>11.0</td>
      <td>34.0</td>
      <td>0.9978</td>
      <td>3.51</td>
      <td>0.56</td>
      <td>9.4</td>
      <td>5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>7.8</td>
      <td>0.88</td>
      <td>0.00</td>
      <td>2.6</td>
      <td>0.098</td>
      <td>25.0</td>
      <td>67.0</td>
      <td>0.9968</td>
      <td>3.20</td>
      <td>0.68</td>
      <td>9.8</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7.8</td>
      <td>0.76</td>
      <td>0.04</td>
      <td>2.3</td>
      <td>0.092</td>
      <td>15.0</td>
      <td>54.0</td>
      <td>0.9970</td>
      <td>3.26</td>
      <td>0.65</td>
      <td>9.8</td>
      <td>5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>11.2</td>
      <td>0.28</td>
      <td>0.56</td>
      <td>1.9</td>
      <td>0.075</td>
      <td>17.0</td>
      <td>60.0</td>
      <td>0.9980</td>
      <td>3.16</td>
      <td>0.58</td>
      <td>9.8</td>
      <td>6</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7.4</td>
      <td>0.70</td>
      <td>0.00</td>
      <td>1.9</td>
      <td>0.076</td>
      <td>11.0</td>
      <td>34.0</td>
      <td>0.9978</td>
      <td>3.51</td>
      <td>0.56</td>
      <td>9.4</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby("quality").agg({"chlorides":(np.min,np.max,np.mean),
                          "residual sugar":np.nanmean})
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
      <th colspan="3" halign="left">chlorides</th>
      <th>residual sugar</th>
    </tr>
    <tr>
      <th></th>
      <th>amin</th>
      <th>amax</th>
      <th>mean</th>
      <th>nanmean</th>
    </tr>
    <tr>
      <th>quality</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>0.061</td>
      <td>0.267</td>
      <td>0.122500</td>
      <td>2.635000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.045</td>
      <td>0.610</td>
      <td>0.090679</td>
      <td>2.694340</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.039</td>
      <td>0.611</td>
      <td>0.092736</td>
      <td>2.528855</td>
    </tr>
    <tr>
      <th>6</th>
      <td>0.034</td>
      <td>0.415</td>
      <td>0.084956</td>
      <td>2.477194</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0.012</td>
      <td>0.358</td>
      <td>0.076588</td>
      <td>2.720603</td>
    </tr>
    <tr>
      <th>8</th>
      <td>0.044</td>
      <td>0.086</td>
      <td>0.068444</td>
      <td>2.577778</td>
    </tr>
  </tbody>
</table>
</div>



# GROUP BY AND TRANSFORM

__it broadcasts the function you supply over the grouped dataframe, returning a new dataframe.__


```python
transformed=df[["residual sugar","quality"]].groupby("quality").transform(np.max)
transformed.rename({"residual sugar":"meansugar"},axis='columns', inplace=True)

df.merge(transformed,how="inner",left_index=True,right_index=True).head()
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
      <th>fixed acidity</th>
      <th>volatile acidity</th>
      <th>citric acid</th>
      <th>residual sugar</th>
      <th>chlorides</th>
      <th>free sulfur dioxide</th>
      <th>total sulfur dioxide</th>
      <th>density</th>
      <th>pH</th>
      <th>sulphates</th>
      <th>alcohol</th>
      <th>quality</th>
      <th>meansugar</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7.4</td>
      <td>0.70</td>
      <td>0.00</td>
      <td>1.9</td>
      <td>0.076</td>
      <td>11.0</td>
      <td>34.0</td>
      <td>0.9978</td>
      <td>3.51</td>
      <td>0.56</td>
      <td>9.4</td>
      <td>5</td>
      <td>15.5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>7.8</td>
      <td>0.88</td>
      <td>0.00</td>
      <td>2.6</td>
      <td>0.098</td>
      <td>25.0</td>
      <td>67.0</td>
      <td>0.9968</td>
      <td>3.20</td>
      <td>0.68</td>
      <td>9.8</td>
      <td>5</td>
      <td>15.5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7.8</td>
      <td>0.76</td>
      <td>0.04</td>
      <td>2.3</td>
      <td>0.092</td>
      <td>15.0</td>
      <td>54.0</td>
      <td>0.9970</td>
      <td>3.26</td>
      <td>0.65</td>
      <td>9.8</td>
      <td>5</td>
      <td>15.5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>11.2</td>
      <td>0.28</td>
      <td>0.56</td>
      <td>1.9</td>
      <td>0.075</td>
      <td>17.0</td>
      <td>60.0</td>
      <td>0.9980</td>
      <td>3.16</td>
      <td>0.58</td>
      <td>9.8</td>
      <td>6</td>
      <td>15.4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7.4</td>
      <td>0.70</td>
      <td>0.00</td>
      <td>1.9</td>
      <td>0.076</td>
      <td>11.0</td>
      <td>34.0</td>
      <td>0.9978</td>
      <td>3.51</td>
      <td>0.56</td>
      <td>9.4</td>
      <td>5</td>
      <td>15.5</td>
    </tr>
  </tbody>
</table>
</div>



# GROUP BY AND FILTER

__The filter() function takes in a function which it applies to each group dataframe and returns either a True or a False__


```python
df.groupby("quality").filter(lambda x: np.nanmean(x["residual sugar"])>2.720
                        ).head()
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
      <th>fixed acidity</th>
      <th>volatile acidity</th>
      <th>citric acid</th>
      <th>residual sugar</th>
      <th>chlorides</th>
      <th>free sulfur dioxide</th>
      <th>total sulfur dioxide</th>
      <th>density</th>
      <th>pH</th>
      <th>sulphates</th>
      <th>alcohol</th>
      <th>quality</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>7</th>
      <td>7.3</td>
      <td>0.65</td>
      <td>0.00</td>
      <td>1.2</td>
      <td>0.065</td>
      <td>15.0</td>
      <td>21.0</td>
      <td>0.9946</td>
      <td>3.39</td>
      <td>0.47</td>
      <td>10.0</td>
      <td>7</td>
    </tr>
    <tr>
      <th>8</th>
      <td>7.8</td>
      <td>0.58</td>
      <td>0.02</td>
      <td>2.0</td>
      <td>0.073</td>
      <td>9.0</td>
      <td>18.0</td>
      <td>0.9968</td>
      <td>3.36</td>
      <td>0.57</td>
      <td>9.5</td>
      <td>7</td>
    </tr>
    <tr>
      <th>16</th>
      <td>8.5</td>
      <td>0.28</td>
      <td>0.56</td>
      <td>1.8</td>
      <td>0.092</td>
      <td>35.0</td>
      <td>103.0</td>
      <td>0.9969</td>
      <td>3.30</td>
      <td>0.75</td>
      <td>10.5</td>
      <td>7</td>
    </tr>
    <tr>
      <th>37</th>
      <td>8.1</td>
      <td>0.38</td>
      <td>0.28</td>
      <td>2.1</td>
      <td>0.066</td>
      <td>13.0</td>
      <td>30.0</td>
      <td>0.9968</td>
      <td>3.23</td>
      <td>0.73</td>
      <td>9.7</td>
      <td>7</td>
    </tr>
    <tr>
      <th>62</th>
      <td>7.5</td>
      <td>0.52</td>
      <td>0.16</td>
      <td>1.9</td>
      <td>0.085</td>
      <td>12.0</td>
      <td>35.0</td>
      <td>0.9968</td>
      <td>3.38</td>
      <td>0.62</td>
      <td>9.5</td>
      <td>7</td>
    </tr>
  </tbody>
</table>
</div>




```python
import pandas as pd
(pd.Timestamp('11/29/2019') + pd.offsets.MonthEnd()).weekday()
```




    5




```python
import pandas as pd
pd.Period('01/12/2019', 'M') + 5
```




    Period('2019-06', 'M')




```python

```
