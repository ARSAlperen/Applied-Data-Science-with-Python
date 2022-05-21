
# Introduction to Pandas


```python
import pandas as pd
```

## Creating a DataFrame

### from Lists


```python
record1 = pd.Series({'Name': 'Alice',
                        'Class': 'Physics',
                        'Score': 85})
record2 = pd.Series({'Name': 'Jack',
                        'Class': 'Chemistry',
                        'Score': 82})
record3 = pd.Series({'Name': 'Helen',
                        'Class': 'Biology',
                        'Score': 90})


df=pd.DataFrame([record1,record2,record3],index=["school1","school2","school3"])
df
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
      <th>Class</th>
      <th>Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>school1</th>
      <td>Alice</td>
      <td>Physics</td>
      <td>85</td>
    </tr>
    <tr>
      <th>school2</th>
      <td>Jack</td>
      <td>Chemistry</td>
      <td>82</td>
    </tr>
    <tr>
      <th>school3</th>
      <td>Helen</td>
      <td>Biology</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>



### from Dictionaries


```python
students = [{'Name': 'Alice',
              'Class': 'Physics',
              'Score': 85},
            {'Name': 'Jack',
             'Class': 'Chemistry',
             'Score': 82},
            {'Name': 'Helen',
             'Class': 'Biology',
             'Score': 90}]
df=pd.DataFrame(students,index=["school1","school2","school1"])
df
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
      <th>Class</th>
      <th>Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>school1</th>
      <td>Alice</td>
      <td>Physics</td>
      <td>85</td>
    </tr>
    <tr>
      <th>school2</th>
      <td>Jack</td>
      <td>Chemistry</td>
      <td>82</td>
    </tr>
    <tr>
      <th>school1</th>
      <td>Helen</td>
      <td>Biology</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>



## loc and iloc attributes

### loc attribute usage

The loc property is used to access a group of rows and columns by label(s)



```python
df.loc["school2"]
```




    Name          Jack
    Class    Chemistry
    Score           82
    Name: school2, dtype: object




```python
type(df.loc["school2"])
```




    pandas.core.series.Series




```python
type(df.loc["school1"])
```




    pandas.core.frame.DataFrame




```python
df.loc["school1","Name"]
```




    school1    Alice
    school1    Helen
    Name: Name, dtype: object



Getting transpose of the dataframe to get rows as columns


```python
df.T.loc["Name"]
```




    school1    Alice
    school2     Jack
    school1    Helen
    Name: Name, dtype: object




```python
df["Name"]
```




    school1    Alice
    school2     Jack
    school1    Helen
    Name: Name, dtype: object




```python
df.loc["school1"]['Name']
```




    school1    Alice
    school1    Helen
    Name: Name, dtype: object




```python
df.loc[:,['Name','Score']] # get all rows and specified columns
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
      <th>Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>school1</th>
      <td>Alice</td>
      <td>85</td>
    </tr>
    <tr>
      <th>school2</th>
      <td>Jack</td>
      <td>82</td>
    </tr>
    <tr>
      <th>school1</th>
      <td>Helen</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>



## Dropping Rows and Columns


```python
df.drop("school1") #real df is not updated
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
      <th>Class</th>
      <th>Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>school2</th>
      <td>Jack</td>
      <td>Chemistry</td>
      <td>82</td>
    </tr>
  </tbody>
</table>
</div>




if inplace set to True, df will be updated 
--
if axis parameter set to 1, code will drop specified coloumn
--


```python
copy_df=df.copy()
copy_df.drop("Name",inplace=True,axis=1) #drop column
copy_df
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
      <th>Class</th>
      <th>Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>school1</th>
      <td>Physics</td>
      <td>85</td>
    </tr>
    <tr>
      <th>school2</th>
      <td>Chemistry</td>
      <td>82</td>
    </tr>
    <tr>
      <th>school1</th>
      <td>Biology</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>




```python
copy_df=df.copy()
copy_df.drop("school1",inplace=True) #drop rows
copy_df

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
      <th>Class</th>
      <th>Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>school2</th>
      <td>Jack</td>
      <td>Chemistry</td>
      <td>82</td>
    </tr>
  </tbody>
</table>
</div>



# Turn CSV files to Pandas DataFrame



```python
import pandas as pd
df=pd.read_csv('resources/week-2/datasets/Admission_Predict.csv')
```


```python
df.head(2)
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
      <th>Serial No.</th>
      <th>GRE Score</th>
      <th>TOEFL Score</th>
      <th>University Rating</th>
      <th>SOP</th>
      <th>LOR</th>
      <th>CGPA</th>
      <th>Research</th>
      <th>Chance of Admit</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>337</td>
      <td>118</td>
      <td>4</td>
      <td>4.5</td>
      <td>4.5</td>
      <td>9.65</td>
      <td>1</td>
      <td>0.92</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>324</td>
      <td>107</td>
      <td>4</td>
      <td>4.0</td>
      <td>4.5</td>
      <td>8.87</td>
      <td>1</td>
      <td>0.76</td>
    </tr>
  </tbody>
</table>
</div>



### Setting a Column as an index col


```python
df=pd.read_csv('resources/week-2/datasets/Admission_Predict.csv',index_col=0)
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
      <th>GRE Score</th>
      <th>TOEFL Score</th>
      <th>University Rating</th>
      <th>SOP</th>
      <th>LOR</th>
      <th>CGPA</th>
      <th>Research</th>
      <th>Chance of Admit</th>
    </tr>
    <tr>
      <th>Serial No.</th>
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
      <th>1</th>
      <td>337</td>
      <td>118</td>
      <td>4</td>
      <td>4.5</td>
      <td>4.5</td>
      <td>9.65</td>
      <td>1</td>
      <td>0.92</td>
    </tr>
    <tr>
      <th>2</th>
      <td>324</td>
      <td>107</td>
      <td>4</td>
      <td>4.0</td>
      <td>4.5</td>
      <td>8.87</td>
      <td>1</td>
      <td>0.76</td>
    </tr>
    <tr>
      <th>3</th>
      <td>316</td>
      <td>104</td>
      <td>3</td>
      <td>3.0</td>
      <td>3.5</td>
      <td>8.00</td>
      <td>1</td>
      <td>0.72</td>
    </tr>
    <tr>
      <th>4</th>
      <td>322</td>
      <td>110</td>
      <td>3</td>
      <td>3.5</td>
      <td>2.5</td>
      <td>8.67</td>
      <td>1</td>
      <td>0.80</td>
    </tr>
    <tr>
      <th>5</th>
      <td>314</td>
      <td>103</td>
      <td>2</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>8.21</td>
      <td>0</td>
      <td>0.65</td>
    </tr>
  </tbody>
</table>
</div>



### Rename Column Names


```python
new_df=df.rename(columns={'GRE Score':'GRE Score', 'TOEFL Score':'TOEFL Score',
                   'University Rating':'University Rating', 
                   'SOP': 'Statement of Purpose','LOR': 'Letter of Recommendation',
                   'CGPA':'CGPA', 'Research':'Research',
                   'Chance of Admit':'Chance of Admit'})
new_df.head()
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
      <th>GRE Score</th>
      <th>TOEFL Score</th>
      <th>University Rating</th>
      <th>Statement of Purpose</th>
      <th>LOR</th>
      <th>CGPA</th>
      <th>Research</th>
      <th>Chance of Admit</th>
    </tr>
    <tr>
      <th>Serial No.</th>
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
      <th>1</th>
      <td>337</td>
      <td>118</td>
      <td>4</td>
      <td>4.5</td>
      <td>4.5</td>
      <td>9.65</td>
      <td>1</td>
      <td>0.92</td>
    </tr>
    <tr>
      <th>2</th>
      <td>324</td>
      <td>107</td>
      <td>4</td>
      <td>4.0</td>
      <td>4.5</td>
      <td>8.87</td>
      <td>1</td>
      <td>0.76</td>
    </tr>
    <tr>
      <th>3</th>
      <td>316</td>
      <td>104</td>
      <td>3</td>
      <td>3.0</td>
      <td>3.5</td>
      <td>8.00</td>
      <td>1</td>
      <td>0.72</td>
    </tr>
    <tr>
      <th>4</th>
      <td>322</td>
      <td>110</td>
      <td>3</td>
      <td>3.5</td>
      <td>2.5</td>
      <td>8.67</td>
      <td>1</td>
      <td>0.80</td>
    </tr>
    <tr>
      <th>5</th>
      <td>314</td>
      <td>103</td>
      <td>2</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>8.21</td>
      <td>0</td>
      <td>0.65</td>
    </tr>
  </tbody>
</table>
</div>



### Deleting Spaces and Tabs in Columns


```python
# Python comes with a handy string function to strip white space called "strip()".
# When we pass this in to rename we pass the function as the mapper parameter, and then indicate whether the
# axis should be columns or index (row labels)

new_df=new_df.rename(mapper=str.strip, axis='columns')
new_df.head()
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
      <th>GRE Score</th>
      <th>TOEFL Score</th>
      <th>University Rating</th>
      <th>Statement of Purpose</th>
      <th>LOR</th>
      <th>CGPA</th>
      <th>Research</th>
      <th>Chance of Admit</th>
    </tr>
    <tr>
      <th>Serial No.</th>
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
      <th>1</th>
      <td>337</td>
      <td>118</td>
      <td>4</td>
      <td>4.5</td>
      <td>4.5</td>
      <td>9.65</td>
      <td>1</td>
      <td>0.92</td>
    </tr>
    <tr>
      <th>2</th>
      <td>324</td>
      <td>107</td>
      <td>4</td>
      <td>4.0</td>
      <td>4.5</td>
      <td>8.87</td>
      <td>1</td>
      <td>0.76</td>
    </tr>
    <tr>
      <th>3</th>
      <td>316</td>
      <td>104</td>
      <td>3</td>
      <td>3.0</td>
      <td>3.5</td>
      <td>8.00</td>
      <td>1</td>
      <td>0.72</td>
    </tr>
    <tr>
      <th>4</th>
      <td>322</td>
      <td>110</td>
      <td>3</td>
      <td>3.5</td>
      <td>2.5</td>
      <td>8.67</td>
      <td>1</td>
      <td>0.80</td>
    </tr>
    <tr>
      <th>5</th>
      <td>314</td>
      <td>103</td>
      <td>2</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>8.21</td>
      <td>0</td>
      <td>0.65</td>
    </tr>
  </tbody>
</table>
</div>



### Rename Columns with a List also using strip()



```python
cols = list(df.columns)
# Then a little list comprehenshion
cols = [x.lower().strip() for x in cols]
# Then we just overwrite what is already in the .columns attribute
df.columns=cols
# And take a look at our results
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
      <th>gre score</th>
      <th>toefl score</th>
      <th>university rating</th>
      <th>sop</th>
      <th>lor</th>
      <th>cgpa</th>
      <th>research</th>
      <th>chance of admit</th>
    </tr>
    <tr>
      <th>Serial No.</th>
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
      <th>1</th>
      <td>337</td>
      <td>118</td>
      <td>4</td>
      <td>4.5</td>
      <td>4.5</td>
      <td>9.65</td>
      <td>1</td>
      <td>0.92</td>
    </tr>
    <tr>
      <th>2</th>
      <td>324</td>
      <td>107</td>
      <td>4</td>
      <td>4.0</td>
      <td>4.5</td>
      <td>8.87</td>
      <td>1</td>
      <td>0.76</td>
    </tr>
    <tr>
      <th>3</th>
      <td>316</td>
      <td>104</td>
      <td>3</td>
      <td>3.0</td>
      <td>3.5</td>
      <td>8.00</td>
      <td>1</td>
      <td>0.72</td>
    </tr>
    <tr>
      <th>4</th>
      <td>322</td>
      <td>110</td>
      <td>3</td>
      <td>3.5</td>
      <td>2.5</td>
      <td>8.67</td>
      <td>1</td>
      <td>0.80</td>
    </tr>
    <tr>
      <th>5</th>
      <td>314</td>
      <td>103</td>
      <td>2</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>8.21</td>
      <td>0</td>
      <td>0.65</td>
    </tr>
  </tbody>
</table>
</div>



# Querying a DataFrame using Boolean Masking


```python
import pandas as pd
df = pd.read_csv('resources/week-1/datasets/Admission_Predict.csv', index_col=0)

df.columns = [x.lower().strip() for x in df.columns]

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
      <th>gre score</th>
      <th>toefl score</th>
      <th>university rating</th>
      <th>sop</th>
      <th>lor</th>
      <th>cgpa</th>
      <th>research</th>
      <th>chance of admit</th>
    </tr>
    <tr>
      <th>Serial No.</th>
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
      <th>1</th>
      <td>337</td>
      <td>118</td>
      <td>4</td>
      <td>4.5</td>
      <td>4.5</td>
      <td>9.65</td>
      <td>1</td>
      <td>0.92</td>
    </tr>
    <tr>
      <th>2</th>
      <td>324</td>
      <td>107</td>
      <td>4</td>
      <td>4.0</td>
      <td>4.5</td>
      <td>8.87</td>
      <td>1</td>
      <td>0.76</td>
    </tr>
    <tr>
      <th>3</th>
      <td>316</td>
      <td>104</td>
      <td>3</td>
      <td>3.0</td>
      <td>3.5</td>
      <td>8.00</td>
      <td>1</td>
      <td>0.72</td>
    </tr>
    <tr>
      <th>4</th>
      <td>322</td>
      <td>110</td>
      <td>3</td>
      <td>3.5</td>
      <td>2.5</td>
      <td>8.67</td>
      <td>1</td>
      <td>0.80</td>
    </tr>
    <tr>
      <th>5</th>
      <td>314</td>
      <td>103</td>
      <td>2</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>8.21</td>
      <td>0</td>
      <td>0.65</td>
    </tr>
  </tbody>
</table>
</div>




```python
df[df["gre score"]==314]
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
      <th>gre score</th>
      <th>toefl score</th>
      <th>university rating</th>
      <th>sop</th>
      <th>lor</th>
      <th>cgpa</th>
      <th>research</th>
      <th>chance of admit</th>
    </tr>
    <tr>
      <th>Serial No.</th>
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
      <th>5</th>
      <td>314</td>
      <td>103</td>
      <td>2</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>8.21</td>
      <td>0</td>
      <td>0.65</td>
    </tr>
    <tr>
      <th>16</th>
      <td>314</td>
      <td>105</td>
      <td>3</td>
      <td>3.5</td>
      <td>2.5</td>
      <td>8.30</td>
      <td>0</td>
      <td>0.54</td>
    </tr>
    <tr>
      <th>74</th>
      <td>314</td>
      <td>108</td>
      <td>4</td>
      <td>4.5</td>
      <td>4.0</td>
      <td>9.04</td>
      <td>1</td>
      <td>0.84</td>
    </tr>
    <tr>
      <th>75</th>
      <td>314</td>
      <td>106</td>
      <td>3</td>
      <td>3.0</td>
      <td>5.0</td>
      <td>8.90</td>
      <td>0</td>
      <td>0.74</td>
    </tr>
    <tr>
      <th>89</th>
      <td>314</td>
      <td>108</td>
      <td>3</td>
      <td>4.5</td>
      <td>3.5</td>
      <td>8.14</td>
      <td>0</td>
      <td>0.64</td>
    </tr>
    <tr>
      <th>103</th>
      <td>314</td>
      <td>106</td>
      <td>2</td>
      <td>4.0</td>
      <td>3.5</td>
      <td>8.25</td>
      <td>0</td>
      <td>0.62</td>
    </tr>
    <tr>
      <th>136</th>
      <td>314</td>
      <td>109</td>
      <td>4</td>
      <td>3.5</td>
      <td>4.0</td>
      <td>8.77</td>
      <td>1</td>
      <td>0.82</td>
    </tr>
    <tr>
      <th>184</th>
      <td>314</td>
      <td>110</td>
      <td>3</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>8.80</td>
      <td>0</td>
      <td>0.75</td>
    </tr>
    <tr>
      <th>245</th>
      <td>314</td>
      <td>107</td>
      <td>2</td>
      <td>2.5</td>
      <td>4.0</td>
      <td>8.56</td>
      <td>0</td>
      <td>0.63</td>
    </tr>
    <tr>
      <th>268</th>
      <td>314</td>
      <td>107</td>
      <td>3</td>
      <td>3.0</td>
      <td>3.5</td>
      <td>8.17</td>
      <td>1</td>
      <td>0.73</td>
    </tr>
    <tr>
      <th>289</th>
      <td>314</td>
      <td>104</td>
      <td>4</td>
      <td>5.0</td>
      <td>5.0</td>
      <td>9.02</td>
      <td>0</td>
      <td>0.82</td>
    </tr>
    <tr>
      <th>323</th>
      <td>314</td>
      <td>107</td>
      <td>2</td>
      <td>2.5</td>
      <td>4.0</td>
      <td>8.27</td>
      <td>0</td>
      <td>0.72</td>
    </tr>
    <tr>
      <th>359</th>
      <td>314</td>
      <td>105</td>
      <td>2</td>
      <td>2.5</td>
      <td>2.0</td>
      <td>7.64</td>
      <td>0</td>
      <td>0.70</td>
    </tr>
    <tr>
      <th>391</th>
      <td>314</td>
      <td>102</td>
      <td>2</td>
      <td>2.0</td>
      <td>2.5</td>
      <td>8.24</td>
      <td>0</td>
      <td>0.64</td>
    </tr>
  </tbody>
</table>
</div>




```python

df[["gre score","toefl score"]].head()
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
      <th>gre score</th>
      <th>toefl score</th>
    </tr>
    <tr>
      <th>Serial No.</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>337</td>
      <td>118</td>
    </tr>
    <tr>
      <th>2</th>
      <td>324</td>
      <td>107</td>
    </tr>
    <tr>
      <th>3</th>
      <td>316</td>
      <td>104</td>
    </tr>
    <tr>
      <th>4</th>
      <td>322</td>
      <td>110</td>
    </tr>
    <tr>
      <th>5</th>
      <td>314</td>
      <td>103</td>
    </tr>
  </tbody>
</table>
</div>




```python
df[(df['chance of admit'] > 0.7) & (df['chance of admit'] < 0.9)].head()
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
      <th>gre score</th>
      <th>toefl score</th>
      <th>university rating</th>
      <th>sop</th>
      <th>lor</th>
      <th>cgpa</th>
      <th>research</th>
      <th>chance of admit</th>
    </tr>
    <tr>
      <th>Serial No.</th>
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
      <th>2</th>
      <td>324</td>
      <td>107</td>
      <td>4</td>
      <td>4.0</td>
      <td>4.5</td>
      <td>8.87</td>
      <td>1</td>
      <td>0.76</td>
    </tr>
    <tr>
      <th>3</th>
      <td>316</td>
      <td>104</td>
      <td>3</td>
      <td>3.0</td>
      <td>3.5</td>
      <td>8.00</td>
      <td>1</td>
      <td>0.72</td>
    </tr>
    <tr>
      <th>4</th>
      <td>322</td>
      <td>110</td>
      <td>3</td>
      <td>3.5</td>
      <td>2.5</td>
      <td>8.67</td>
      <td>1</td>
      <td>0.80</td>
    </tr>
    <tr>
      <th>7</th>
      <td>321</td>
      <td>109</td>
      <td>3</td>
      <td>3.0</td>
      <td>4.0</td>
      <td>8.20</td>
      <td>1</td>
      <td>0.75</td>
    </tr>
    <tr>
      <th>12</th>
      <td>327</td>
      <td>111</td>
      <td>4</td>
      <td>4.0</td>
      <td>4.5</td>
      <td>9.00</td>
      <td>1</td>
      <td>0.84</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['chance of admit'].gt(0.7) & df['chance of admit'].lt(0.9)
```




    Serial No.
    1      False
    2       True
    3       True
    4       True
    5      False
           ...  
    396     True
    397     True
    398    False
    399    False
    400    False
    Name: chance of admit, Length: 400, dtype: bool




```python
df['chance of admit'].gt(0.7).lt(0.9)
#gt greater than
#lt lower than
```




    Serial No.
    1      False
    2      False
    3      False
    4      False
    5       True
           ...  
    396    False
    397    False
    398    False
    399     True
    400    False
    Name: chance of admit, Length: 400, dtype: bool



# Indexing DataFrame 

## Set a Column as index column at the beginning


```python
import pandas as pd
df = pd.read_csv("resources/week-1/datasets/Admission_Predict.csv", index_col=0)
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
      <th>GRE Score</th>
      <th>TOEFL Score</th>
      <th>University Rating</th>
      <th>SOP</th>
      <th>LOR</th>
      <th>CGPA</th>
      <th>Research</th>
      <th>Chance of Admit</th>
    </tr>
    <tr>
      <th>Serial No.</th>
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
      <th>1</th>
      <td>337</td>
      <td>118</td>
      <td>4</td>
      <td>4.5</td>
      <td>4.5</td>
      <td>9.65</td>
      <td>1</td>
      <td>0.92</td>
    </tr>
    <tr>
      <th>2</th>
      <td>324</td>
      <td>107</td>
      <td>4</td>
      <td>4.0</td>
      <td>4.5</td>
      <td>8.87</td>
      <td>1</td>
      <td>0.76</td>
    </tr>
    <tr>
      <th>3</th>
      <td>316</td>
      <td>104</td>
      <td>3</td>
      <td>3.0</td>
      <td>3.5</td>
      <td>8.00</td>
      <td>1</td>
      <td>0.72</td>
    </tr>
    <tr>
      <th>4</th>
      <td>322</td>
      <td>110</td>
      <td>3</td>
      <td>3.5</td>
      <td>2.5</td>
      <td>8.67</td>
      <td>1</td>
      <td>0.80</td>
    </tr>
    <tr>
      <th>5</th>
      <td>314</td>
      <td>103</td>
      <td>2</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>8.21</td>
      <td>0</td>
      <td>0.65</td>
    </tr>
  </tbody>
</table>
</div>



## Index Column to a normal column with df.index


```python
df["Serial No"]=df.index
```


```python
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
      <th>GRE Score</th>
      <th>TOEFL Score</th>
      <th>University Rating</th>
      <th>SOP</th>
      <th>LOR</th>
      <th>CGPA</th>
      <th>Research</th>
      <th>Chance of Admit</th>
      <th>Serial No</th>
    </tr>
    <tr>
      <th>Serial No.</th>
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
      <th>1</th>
      <td>337</td>
      <td>118</td>
      <td>4</td>
      <td>4.5</td>
      <td>4.5</td>
      <td>9.65</td>
      <td>1</td>
      <td>0.92</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>324</td>
      <td>107</td>
      <td>4</td>
      <td>4.0</td>
      <td>4.5</td>
      <td>8.87</td>
      <td>1</td>
      <td>0.76</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>316</td>
      <td>104</td>
      <td>3</td>
      <td>3.0</td>
      <td>3.5</td>
      <td>8.00</td>
      <td>1</td>
      <td>0.72</td>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>322</td>
      <td>110</td>
      <td>3</td>
      <td>3.5</td>
      <td>2.5</td>
      <td>8.67</td>
      <td>1</td>
      <td>0.80</td>
      <td>4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>314</td>
      <td>103</td>
      <td>2</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>8.21</td>
      <td>0</td>
      <td>0.65</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
df = df.reset_index()
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
      <th>Serial No.</th>
      <th>GRE Score</th>
      <th>TOEFL Score</th>
      <th>University Rating</th>
      <th>SOP</th>
      <th>LOR</th>
      <th>CGPA</th>
      <th>Research</th>
      <th>Chance of Admit</th>
      <th>Serial No</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>337</td>
      <td>118</td>
      <td>4</td>
      <td>4.5</td>
      <td>4.5</td>
      <td>9.65</td>
      <td>1</td>
      <td>0.92</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>324</td>
      <td>107</td>
      <td>4</td>
      <td>4.0</td>
      <td>4.5</td>
      <td>8.87</td>
      <td>1</td>
      <td>0.76</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>316</td>
      <td>104</td>
      <td>3</td>
      <td>3.0</td>
      <td>3.5</td>
      <td>8.00</td>
      <td>1</td>
      <td>0.72</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>322</td>
      <td>110</td>
      <td>3</td>
      <td>3.5</td>
      <td>2.5</td>
      <td>8.67</td>
      <td>1</td>
      <td>0.80</td>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>314</td>
      <td>103</td>
      <td>2</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>8.21</td>
      <td>0</td>
      <td>0.65</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>



## Unique Values in a Column 


```python
df=pd.read_csv('resources/week-2/datasets/census.csv')
```


```python
df.tail()
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
      <th>SUMLEV</th>
      <th>REGION</th>
      <th>DIVISION</th>
      <th>STATE</th>
      <th>COUNTY</th>
      <th>STNAME</th>
      <th>CTYNAME</th>
      <th>CENSUS2010POP</th>
      <th>ESTIMATESBASE2010</th>
      <th>POPESTIMATE2010</th>
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
  </thead>
  <tbody>
    <tr>
      <th>3188</th>
      <td>50</td>
      <td>4</td>
      <td>8</td>
      <td>56</td>
      <td>37</td>
      <td>Wyoming</td>
      <td>Sweetwater County</td>
      <td>43806</td>
      <td>43806</td>
      <td>43593</td>
      <td>...</td>
      <td>1.072643</td>
      <td>16.243199</td>
      <td>-5.339774</td>
      <td>-14.252889</td>
      <td>-14.248864</td>
      <td>1.255221</td>
      <td>16.243199</td>
      <td>-5.295460</td>
      <td>-14.075283</td>
      <td>-14.070195</td>
    </tr>
    <tr>
      <th>3189</th>
      <td>50</td>
      <td>4</td>
      <td>8</td>
      <td>56</td>
      <td>39</td>
      <td>Wyoming</td>
      <td>Teton County</td>
      <td>21294</td>
      <td>21294</td>
      <td>21297</td>
      <td>...</td>
      <td>-1.589565</td>
      <td>0.972695</td>
      <td>19.525929</td>
      <td>14.143021</td>
      <td>-0.564849</td>
      <td>0.654527</td>
      <td>2.408578</td>
      <td>21.160658</td>
      <td>16.308671</td>
      <td>1.520747</td>
    </tr>
    <tr>
      <th>3190</th>
      <td>50</td>
      <td>4</td>
      <td>8</td>
      <td>56</td>
      <td>41</td>
      <td>Wyoming</td>
      <td>Uinta County</td>
      <td>21118</td>
      <td>21118</td>
      <td>21102</td>
      <td>...</td>
      <td>-17.755986</td>
      <td>-4.916350</td>
      <td>-6.902954</td>
      <td>-14.215862</td>
      <td>-12.127022</td>
      <td>-18.136812</td>
      <td>-5.536861</td>
      <td>-7.521840</td>
      <td>-14.740608</td>
      <td>-12.606351</td>
    </tr>
    <tr>
      <th>3191</th>
      <td>50</td>
      <td>4</td>
      <td>8</td>
      <td>56</td>
      <td>43</td>
      <td>Wyoming</td>
      <td>Washakie County</td>
      <td>8533</td>
      <td>8533</td>
      <td>8545</td>
      <td>...</td>
      <td>-11.637475</td>
      <td>-0.827815</td>
      <td>-2.013502</td>
      <td>-17.781491</td>
      <td>1.682288</td>
      <td>-11.990126</td>
      <td>-1.182592</td>
      <td>-2.250385</td>
      <td>-18.020168</td>
      <td>1.441961</td>
    </tr>
    <tr>
      <th>3192</th>
      <td>50</td>
      <td>4</td>
      <td>8</td>
      <td>56</td>
      <td>45</td>
      <td>Wyoming</td>
      <td>Weston County</td>
      <td>7208</td>
      <td>7208</td>
      <td>7181</td>
      <td>...</td>
      <td>-11.752361</td>
      <td>-8.040059</td>
      <td>12.372583</td>
      <td>1.533635</td>
      <td>6.935294</td>
      <td>-12.032179</td>
      <td>-8.040059</td>
      <td>12.372583</td>
      <td>1.533635</td>
      <td>6.935294</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 100 columns</p>
</div>




```python
df["SUMLEV"].unique() # only two values in 3193 rows is unique
```




    array([40, 50])



## Keep the selected Columns


```python
columns_to_keep = ['STNAME','CTYNAME','BIRTHS2010','BIRTHS2011','BIRTHS2012','BIRTHS2013',
                   'BIRTHS2014','BIRTHS2015','POPESTIMATE2010','POPESTIMATE2011',
                   'POPESTIMATE2012','POPESTIMATE2013','POPESTIMATE2014','POPESTIMATE2015']
df = df[columns_to_keep]
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
      <th>STNAME</th>
      <th>CTYNAME</th>
      <th>BIRTHS2010</th>
      <th>BIRTHS2011</th>
      <th>BIRTHS2012</th>
      <th>BIRTHS2013</th>
      <th>BIRTHS2014</th>
      <th>BIRTHS2015</th>
      <th>POPESTIMATE2010</th>
      <th>POPESTIMATE2011</th>
      <th>POPESTIMATE2012</th>
      <th>POPESTIMATE2013</th>
      <th>POPESTIMATE2014</th>
      <th>POPESTIMATE2015</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alabama</td>
      <td>Alabama</td>
      <td>14226</td>
      <td>59689</td>
      <td>59062</td>
      <td>57938</td>
      <td>58334</td>
      <td>58305</td>
      <td>4785161</td>
      <td>4801108</td>
      <td>4816089</td>
      <td>4830533</td>
      <td>4846411</td>
      <td>4858979</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alabama</td>
      <td>Autauga County</td>
      <td>151</td>
      <td>636</td>
      <td>615</td>
      <td>574</td>
      <td>623</td>
      <td>600</td>
      <td>54660</td>
      <td>55253</td>
      <td>55175</td>
      <td>55038</td>
      <td>55290</td>
      <td>55347</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Alabama</td>
      <td>Baldwin County</td>
      <td>517</td>
      <td>2187</td>
      <td>2092</td>
      <td>2160</td>
      <td>2186</td>
      <td>2240</td>
      <td>183193</td>
      <td>186659</td>
      <td>190396</td>
      <td>195126</td>
      <td>199713</td>
      <td>203709</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Alabama</td>
      <td>Barbour County</td>
      <td>70</td>
      <td>335</td>
      <td>300</td>
      <td>283</td>
      <td>260</td>
      <td>269</td>
      <td>27341</td>
      <td>27226</td>
      <td>27159</td>
      <td>26973</td>
      <td>26815</td>
      <td>26489</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Alabama</td>
      <td>Bibb County</td>
      <td>44</td>
      <td>266</td>
      <td>245</td>
      <td>259</td>
      <td>247</td>
      <td>253</td>
      <td>22861</td>
      <td>22733</td>
      <td>22642</td>
      <td>22512</td>
      <td>22549</td>
      <td>22583</td>
    </tr>
  </tbody>
</table>
</div>



## Multiple Index Columns


```python
df=df.set_index(["STNAME","CTYNAME"])
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
      <th></th>
      <th>BIRTHS2010</th>
      <th>BIRTHS2011</th>
      <th>BIRTHS2012</th>
      <th>BIRTHS2013</th>
      <th>BIRTHS2014</th>
      <th>BIRTHS2015</th>
      <th>POPESTIMATE2010</th>
      <th>POPESTIMATE2011</th>
      <th>POPESTIMATE2012</th>
      <th>POPESTIMATE2013</th>
      <th>POPESTIMATE2014</th>
      <th>POPESTIMATE2015</th>
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">Alabama</th>
      <th>Alabama</th>
      <td>14226</td>
      <td>59689</td>
      <td>59062</td>
      <td>57938</td>
      <td>58334</td>
      <td>58305</td>
      <td>4785161</td>
      <td>4801108</td>
      <td>4816089</td>
      <td>4830533</td>
      <td>4846411</td>
      <td>4858979</td>
    </tr>
    <tr>
      <th>Autauga County</th>
      <td>151</td>
      <td>636</td>
      <td>615</td>
      <td>574</td>
      <td>623</td>
      <td>600</td>
      <td>54660</td>
      <td>55253</td>
      <td>55175</td>
      <td>55038</td>
      <td>55290</td>
      <td>55347</td>
    </tr>
    <tr>
      <th>Baldwin County</th>
      <td>517</td>
      <td>2187</td>
      <td>2092</td>
      <td>2160</td>
      <td>2186</td>
      <td>2240</td>
      <td>183193</td>
      <td>186659</td>
      <td>190396</td>
      <td>195126</td>
      <td>199713</td>
      <td>203709</td>
    </tr>
    <tr>
      <th>Barbour County</th>
      <td>70</td>
      <td>335</td>
      <td>300</td>
      <td>283</td>
      <td>260</td>
      <td>269</td>
      <td>27341</td>
      <td>27226</td>
      <td>27159</td>
      <td>26973</td>
      <td>26815</td>
      <td>26489</td>
    </tr>
    <tr>
      <th>Bibb County</th>
      <td>44</td>
      <td>266</td>
      <td>245</td>
      <td>259</td>
      <td>247</td>
      <td>253</td>
      <td>22861</td>
      <td>22733</td>
      <td>22642</td>
      <td>22512</td>
      <td>22549</td>
      <td>22583</td>
    </tr>
  </tbody>
</table>
</div>



### Querying multi index dataframe wih loc attribute


```python
df.loc["Alabama","Autauga County"]
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
      <th>BIRTHS2010</th>
      <th>BIRTHS2011</th>
      <th>BIRTHS2012</th>
      <th>BIRTHS2013</th>
      <th>BIRTHS2014</th>
      <th>BIRTHS2015</th>
      <th>POPESTIMATE2010</th>
      <th>POPESTIMATE2011</th>
      <th>POPESTIMATE2012</th>
      <th>POPESTIMATE2013</th>
      <th>POPESTIMATE2014</th>
      <th>POPESTIMATE2015</th>
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alabama</th>
      <th>Autauga County</th>
      <td>151</td>
      <td>636</td>
      <td>615</td>
      <td>574</td>
      <td>623</td>
      <td>600</td>
      <td>54660</td>
      <td>55253</td>
      <td>55175</td>
      <td>55038</td>
      <td>55290</td>
      <td>55347</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.loc[ [("Alabama","Autauga County"),("Alabama","Bibb County")] ]
# pasting a tuple inside
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
      <th>BIRTHS2010</th>
      <th>BIRTHS2011</th>
      <th>BIRTHS2012</th>
      <th>BIRTHS2013</th>
      <th>BIRTHS2014</th>
      <th>BIRTHS2015</th>
      <th>POPESTIMATE2010</th>
      <th>POPESTIMATE2011</th>
      <th>POPESTIMATE2012</th>
      <th>POPESTIMATE2013</th>
      <th>POPESTIMATE2014</th>
      <th>POPESTIMATE2015</th>
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">Alabama</th>
      <th>Autauga County</th>
      <td>151</td>
      <td>636</td>
      <td>615</td>
      <td>574</td>
      <td>623</td>
      <td>600</td>
      <td>54660</td>
      <td>55253</td>
      <td>55175</td>
      <td>55038</td>
      <td>55290</td>
      <td>55347</td>
    </tr>
    <tr>
      <th>Bibb County</th>
      <td>44</td>
      <td>266</td>
      <td>245</td>
      <td>259</td>
      <td>247</td>
      <td>253</td>
      <td>22861</td>
      <td>22733</td>
      <td>22642</td>
      <td>22512</td>
      <td>22549</td>
      <td>22583</td>
    </tr>
  </tbody>
</table>
</div>



# Missing Data

if you are running a survey and a respondant didn't answer a question the missing value is actually an omission. This kind of missing data is called __Missing at Random__ if there are other variables that might be used to predict the variable which is missing. In my work when I delivery surveys I often find that missing data, say the interest in being involved in a follow up study, often has some correlation with another data field, like gender or ethnicity. If there is no relationship to other variables, then we call this data __Missing Completely at Random (MCAR).__


```python
df = pd.read_csv('resources/week-2/datasets/class_grades.csv')
df.head(10)

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
      <th>Prefix</th>
      <th>Assignment</th>
      <th>Tutorial</th>
      <th>Midterm</th>
      <th>TakeHome</th>
      <th>Final</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5</td>
      <td>57.14</td>
      <td>34.09</td>
      <td>64.38</td>
      <td>51.48</td>
      <td>52.50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8</td>
      <td>95.05</td>
      <td>105.49</td>
      <td>67.50</td>
      <td>99.07</td>
      <td>68.33</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>83.70</td>
      <td>83.17</td>
      <td>NaN</td>
      <td>63.15</td>
      <td>48.89</td>
    </tr>
    <tr>
      <th>3</th>
      <td>7</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>49.38</td>
      <td>105.93</td>
      <td>80.56</td>
    </tr>
    <tr>
      <th>4</th>
      <td>8</td>
      <td>91.32</td>
      <td>93.64</td>
      <td>95.00</td>
      <td>107.41</td>
      <td>73.89</td>
    </tr>
    <tr>
      <th>5</th>
      <td>7</td>
      <td>95.00</td>
      <td>92.58</td>
      <td>93.12</td>
      <td>97.78</td>
      <td>68.06</td>
    </tr>
    <tr>
      <th>6</th>
      <td>8</td>
      <td>95.05</td>
      <td>102.99</td>
      <td>56.25</td>
      <td>99.07</td>
      <td>50.00</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7</td>
      <td>72.85</td>
      <td>86.85</td>
      <td>60.00</td>
      <td>NaN</td>
      <td>56.11</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8</td>
      <td>84.26</td>
      <td>93.10</td>
      <td>47.50</td>
      <td>18.52</td>
      <td>50.83</td>
    </tr>
    <tr>
      <th>9</th>
      <td>7</td>
      <td>90.10</td>
      <td>97.55</td>
      <td>51.25</td>
      <td>88.89</td>
      <td>63.61</td>
    </tr>
  </tbody>
</table>
</div>



### isnull() boolen mask 


```python
df.isnull().head(2)
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
      <th>Prefix</th>
      <th>Assignment</th>
      <th>Tutorial</th>
      <th>Midterm</th>
      <th>TakeHome</th>
      <th>Final</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>



### .dropna()


```python
dropped=df.dropna().head()
dropped.reset_index()
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
      <th>index</th>
      <th>Prefix</th>
      <th>Assignment</th>
      <th>Tutorial</th>
      <th>Midterm</th>
      <th>TakeHome</th>
      <th>Final</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>5</td>
      <td>57.14</td>
      <td>34.09</td>
      <td>64.38</td>
      <td>51.48</td>
      <td>52.50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>8</td>
      <td>95.05</td>
      <td>105.49</td>
      <td>67.50</td>
      <td>99.07</td>
      <td>68.33</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4</td>
      <td>8</td>
      <td>91.32</td>
      <td>93.64</td>
      <td>95.00</td>
      <td>107.41</td>
      <td>73.89</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5</td>
      <td>7</td>
      <td>95.00</td>
      <td>92.58</td>
      <td>93.12</td>
      <td>97.78</td>
      <td>68.06</td>
    </tr>
    <tr>
      <th>4</th>
      <td>6</td>
      <td>8</td>
      <td>95.05</td>
      <td>102.99</td>
      <td>56.25</td>
      <td>99.07</td>
      <td>50.00</td>
    </tr>
  </tbody>
</table>
</div>



### .fillna(parameter,inplace=True)

__Does not return a copy of the dataframe, but instead modifies the dataframe you have.instead modifies the dataframe you have.__


```python
df.fillna(666, inplace=True)
df.head(10)

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
      <th>Prefix</th>
      <th>Assignment</th>
      <th>Tutorial</th>
      <th>Midterm</th>
      <th>TakeHome</th>
      <th>Final</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5</td>
      <td>57.14</td>
      <td>34.09</td>
      <td>64.38</td>
      <td>51.48</td>
      <td>52.50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8</td>
      <td>95.05</td>
      <td>105.49</td>
      <td>67.50</td>
      <td>99.07</td>
      <td>68.33</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>83.70</td>
      <td>83.17</td>
      <td>666.00</td>
      <td>63.15</td>
      <td>48.89</td>
    </tr>
    <tr>
      <th>3</th>
      <td>7</td>
      <td>666.00</td>
      <td>666.00</td>
      <td>49.38</td>
      <td>105.93</td>
      <td>80.56</td>
    </tr>
    <tr>
      <th>4</th>
      <td>8</td>
      <td>91.32</td>
      <td>93.64</td>
      <td>95.00</td>
      <td>107.41</td>
      <td>73.89</td>
    </tr>
    <tr>
      <th>5</th>
      <td>7</td>
      <td>95.00</td>
      <td>92.58</td>
      <td>93.12</td>
      <td>97.78</td>
      <td>68.06</td>
    </tr>
    <tr>
      <th>6</th>
      <td>8</td>
      <td>95.05</td>
      <td>102.99</td>
      <td>56.25</td>
      <td>99.07</td>
      <td>50.00</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7</td>
      <td>72.85</td>
      <td>86.85</td>
      <td>60.00</td>
      <td>666.00</td>
      <td>56.11</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8</td>
      <td>84.26</td>
      <td>93.10</td>
      <td>47.50</td>
      <td>18.52</td>
      <td>50.83</td>
    </tr>
    <tr>
      <th>9</th>
      <td>7</td>
      <td>90.10</td>
      <td>97.55</td>
      <td>51.25</td>
      <td>88.89</td>
      <td>63.61</td>
    </tr>
  </tbody>
</table>
</div>



## ffill method and bfill method
- dataframe.ffill() function is used to fill the missing value in the dataframe. ‘ffill’ stands for ‘forward fill’ and will propagate last valid observation forward.

- dataframe.bfill() is used to backward fill the missing values in the dataset. It will backward fill the NaN values that are present in the pandas dataframe.


```python
df = pd.read_csv("resources/week-2/datasets/log.csv")
df.head(10)
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
      <th>time</th>
      <th>user</th>
      <th>video</th>
      <th>playback position</th>
      <th>paused</th>
      <th>volume</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1469974424</td>
      <td>cheryl</td>
      <td>intro.html</td>
      <td>5</td>
      <td>False</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1469974454</td>
      <td>cheryl</td>
      <td>intro.html</td>
      <td>6</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1469974544</td>
      <td>cheryl</td>
      <td>intro.html</td>
      <td>9</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1469974574</td>
      <td>cheryl</td>
      <td>intro.html</td>
      <td>10</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1469977514</td>
      <td>bob</td>
      <td>intro.html</td>
      <td>1</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1469977544</td>
      <td>bob</td>
      <td>intro.html</td>
      <td>1</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1469977574</td>
      <td>bob</td>
      <td>intro.html</td>
      <td>1</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1469977604</td>
      <td>bob</td>
      <td>intro.html</td>
      <td>1</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1469974604</td>
      <td>cheryl</td>
      <td>intro.html</td>
      <td>11</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1469974694</td>
      <td>cheryl</td>
      <td>intro.html</td>
      <td>14</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
df = df.set_index(['time', 'user'])
df = df.fillna(method='ffill')
df.head(20)
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
      <th>video</th>
      <th>playback position</th>
      <th>paused</th>
      <th>volume</th>
    </tr>
    <tr>
      <th>time</th>
      <th>user</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1469974424</th>
      <th>cheryl</th>
      <td>intro.html</td>
      <td>5</td>
      <td>False</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>1469974454</th>
      <th>cheryl</th>
      <td>intro.html</td>
      <td>6</td>
      <td>False</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>1469974544</th>
      <th>cheryl</th>
      <td>intro.html</td>
      <td>9</td>
      <td>False</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>1469974574</th>
      <th>cheryl</th>
      <td>intro.html</td>
      <td>10</td>
      <td>False</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>1469977514</th>
      <th>bob</th>
      <td>intro.html</td>
      <td>1</td>
      <td>False</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>1469977544</th>
      <th>bob</th>
      <td>intro.html</td>
      <td>1</td>
      <td>False</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>1469977574</th>
      <th>bob</th>
      <td>intro.html</td>
      <td>1</td>
      <td>False</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>1469977604</th>
      <th>bob</th>
      <td>intro.html</td>
      <td>1</td>
      <td>False</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>1469974604</th>
      <th>cheryl</th>
      <td>intro.html</td>
      <td>11</td>
      <td>False</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>1469974694</th>
      <th>cheryl</th>
      <td>intro.html</td>
      <td>14</td>
      <td>False</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>1469974724</th>
      <th>cheryl</th>
      <td>intro.html</td>
      <td>15</td>
      <td>False</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>1469974454</th>
      <th>sue</th>
      <td>advanced.html</td>
      <td>24</td>
      <td>False</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>1469974524</th>
      <th>sue</th>
      <td>advanced.html</td>
      <td>25</td>
      <td>False</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>1469974424</th>
      <th>sue</th>
      <td>advanced.html</td>
      <td>23</td>
      <td>False</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>1469974554</th>
      <th>sue</th>
      <td>advanced.html</td>
      <td>26</td>
      <td>False</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>1469974624</th>
      <th>sue</th>
      <td>advanced.html</td>
      <td>27</td>
      <td>False</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>1469974654</th>
      <th>sue</th>
      <td>advanced.html</td>
      <td>28</td>
      <td>False</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>1469974724</th>
      <th>sue</th>
      <td>advanced.html</td>
      <td>29</td>
      <td>False</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>1469974484</th>
      <th>cheryl</th>
      <td>intro.html</td>
      <td>7</td>
      <td>False</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>1469974514</th>
      <th>cheryl</th>
      <td>intro.html</td>
      <td>8</td>
      <td>False</td>
      <td>5.0</td>
    </tr>
  </tbody>
</table>
</div>



## replace("replaced","replacement")


```python
df = pd.DataFrame({'A': [1, 1, 2, 3, 4],
                   'B': [3, 6, 3, 8, 9],
                   'C': ['a', 'b', 'c', 'd', 'e']})
df

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
      <th>A</th>
      <th>B</th>
      <th>C</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>3</td>
      <td>a</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>6</td>
      <td>b</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>3</td>
      <td>c</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>8</td>
      <td>d</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>9</td>
      <td>e</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.replace(1, 100)
df.replace([1, 3], [100, 300])
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>100</td>
      <td>300</td>
      <td>a</td>
    </tr>
    <tr>
      <th>1</th>
      <td>100</td>
      <td>6</td>
      <td>b</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>300</td>
      <td>c</td>
    </tr>
    <tr>
      <th>3</th>
      <td>300</td>
      <td>8</td>
      <td>d</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>9</td>
      <td>e</td>
    </tr>
  </tbody>
</table>
</div>



# apply function for cleaning and wrangling data

__The apply() function on a dataframe will take some arbitrary function you have written and apply it to either a Series (a single column) or DataFrame across all rows or columns__


```python
df=pd.read_csv("resources/week-2/datasets/presidents.csv")
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
      <th>#</th>
      <th>President</th>
      <th>Born</th>
      <th>Age atstart of presidency</th>
      <th>Age atend of presidency</th>
      <th>Post-presidencytimespan</th>
      <th>Died</th>
      <th>Age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>George Washington</td>
      <td>Feb 22, 1732[a]</td>
      <td>57 years, 67 daysApr 30, 1789</td>
      <td>65 years, 10 daysMar 4, 1797</td>
      <td>2 years, 285 days</td>
      <td>Dec 14, 1799</td>
      <td>67 years, 295 days</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>John Adams</td>
      <td>Oct 30, 1735[a]</td>
      <td>61 years, 125 daysMar 4, 1797</td>
      <td>65 years, 125 daysMar 4, 1801</td>
      <td>25 years, 122 days</td>
      <td>Jul 4, 1826</td>
      <td>90 years, 247 days</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Thomas Jefferson</td>
      <td>Apr 13, 1743[a]</td>
      <td>57 years, 325 daysMar 4, 1801</td>
      <td>65 years, 325 daysMar 4, 1809</td>
      <td>17 years, 122 days</td>
      <td>Jul 4, 1826</td>
      <td>83 years, 82 days</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>James Madison</td>
      <td>Mar 16, 1751[a]</td>
      <td>57 years, 353 daysMar 4, 1809</td>
      <td>65 years, 353 daysMar 4, 1817</td>
      <td>19 years, 116 days</td>
      <td>Jun 28, 1836</td>
      <td>85 years, 104 days</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>James Monroe</td>
      <td>Apr 28, 1758</td>
      <td>58 years, 310 daysMar 4, 1817</td>
      <td>66 years, 310 daysMar 4, 1825</td>
      <td>6 years, 122 days</td>
      <td>Jul 4, 1831</td>
      <td>73 years, 67 days</td>
    </tr>
  </tbody>
</table>
</div>




```python
def splitname(row):
    row['First']=row['President'].split(" ")[0]
    # Let's do the same with the last word in the string
    row['Last']=row['President'].split(" ")[-1]
    # Now we just return the row and the pandas .apply() will take of merging them back into a DataFrame
    return row
df=df.apply(splitname, axis='columns')
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
      <th>#</th>
      <th>President</th>
      <th>Born</th>
      <th>Age atstart of presidency</th>
      <th>Age atend of presidency</th>
      <th>Post-presidencytimespan</th>
      <th>Died</th>
      <th>Age</th>
      <th>First</th>
      <th>Last</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>George Washington</td>
      <td>Feb 22, 1732[a]</td>
      <td>57 years, 67 daysApr 30, 1789</td>
      <td>65 years, 10 daysMar 4, 1797</td>
      <td>2 years, 285 days</td>
      <td>Dec 14, 1799</td>
      <td>67 years, 295 days</td>
      <td>George</td>
      <td>Washington</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>John Adams</td>
      <td>Oct 30, 1735[a]</td>
      <td>61 years, 125 daysMar 4, 1797</td>
      <td>65 years, 125 daysMar 4, 1801</td>
      <td>25 years, 122 days</td>
      <td>Jul 4, 1826</td>
      <td>90 years, 247 days</td>
      <td>John</td>
      <td>Adams</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Thomas Jefferson</td>
      <td>Apr 13, 1743[a]</td>
      <td>57 years, 325 daysMar 4, 1801</td>
      <td>65 years, 325 daysMar 4, 1809</td>
      <td>17 years, 122 days</td>
      <td>Jul 4, 1826</td>
      <td>83 years, 82 days</td>
      <td>Thomas</td>
      <td>Jefferson</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>James Madison</td>
      <td>Mar 16, 1751[a]</td>
      <td>57 years, 353 daysMar 4, 1809</td>
      <td>65 years, 353 daysMar 4, 1817</td>
      <td>19 years, 116 days</td>
      <td>Jun 28, 1836</td>
      <td>85 years, 104 days</td>
      <td>James</td>
      <td>Madison</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>James Monroe</td>
      <td>Apr 28, 1758</td>
      <td>58 years, 310 daysMar 4, 1817</td>
      <td>66 years, 310 daysMar 4, 1825</td>
      <td>6 years, 122 days</td>
      <td>Jul 4, 1831</td>
      <td>73 years, 67 days</td>
      <td>James</td>
      <td>Monroe</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
