
# Pandas Series


```python
import pandas as pd
```

## How to create a Serie?

The series is one of the core data structures in pandas. You think of it a cross between a list and a dictionary. 

### Creating Series with Lists


```python
names=["Ra","Luna","Zeynep"]
pd.Series(names)
```




    0        Ra
    1      Luna
    2    Zeynep
    dtype: object




```python
numbers=[1,2,3]
pd.Series(numbers)
```




    0    1
    1    2
    2    3
    dtype: int64




```python
#Missing data on string list
names=["Ra",None,"Zeynep"]
pd.Series(names)
```




    0        Ra
    1      None
    2    Zeynep
    dtype: object




```python
# Missing data on number list
numbers=[1,None,3]
pd.Series(numbers)
```




    0    1.0
    1    NaN
    2    3.0
    dtype: float64



__NaN != None__
--


```python
import numpy as np
np.nan==None
```




    False




```python
np.isnan(np.nan)
```




    True



### Creating Series with Dictionaries

Series indexes are automatically assigned to the __keys of the dictionary__.


```python
students_scores={"Alice":"Physics",
                "Jack":"Chemistry",
                "Molly":"English"}

s=pd.Series(students_scores)
s
```




    Alice      Physics
    Jack     Chemistry
    Molly      English
    dtype: object




```python
students_scores.keys()
```




    dict_keys(['Alice', 'Jack', 'Molly'])




```python
s.index
```




    Index(['Alice', 'Jack', 'Molly'], dtype='object')



### Creating Series with Tuples


```python
students=[("Alica","Brown"),("Jackie","Black"),("Molly","Green")]
```


```python
pd.Series(students)
```




    0     (Alica, Brown)
    1    (Jackie, Black)
    2     (Molly, Green)
    dtype: object



### Pandas Series on Missing Values


```python
students_scores = {'Alice': 'Physics',
                   'Jack': 'Chemistry',
                   'Molly': 'English'}
# When I create the series object though I'll only ask for an index with three students, and
# I'll exclude Jack
s = pd.Series(students_scores, index=['Alice', 'Molly', 'Sam'])
s
```




    Alice    Physics
    Molly    English
    Sam          NaN
    dtype: object



## Querying a Series


```python
import pandas as pd 
```


```python
students_classes = {'Alice': 'Physics',
                   'Jack': 'Chemistry',
                   'Molly': 'English',
                   'Sam': 'History'}
s = pd.Series(students_classes)
s
```




    Alice      Physics
    Jack     Chemistry
    Molly      English
    Sam        History
    dtype: object



__.iloc[ ] attribute__
--

__To query by numeric location, starting at zero, use the iloc attribute.__


```python
s.iloc[3]
```




    'History'




```python
s[3]
```




    'History'



__.loc[ ] attribute__
--

__To query by the index label, you can use the loc attribute.__


```python
s.loc["Molly"]
```




    'English'




```python
s["Molly"]
```




    'English'



__what if indexes are a list of integers?__
--
must use  iloc or loc attributes otherwise python code will not run.


```python
class_code = {99: 'Physics',
              100: 'Chemistry',
              101: 'English',
              102: 'History'}
s = pd.Series(class_code)
```


```python
s[99]
```




    'Physics'




```python
s.loc[99]
```




    'Physics'




```python
s.iloc[0]
```




    'Physics'



## Using numpy functions to speed up loop operations


```python
numbers=pd.Series(np.random.randint(0,1000,10000))
numbers.head()
```




    0    359
    1    671
    2     59
    3    879
    4    535
    dtype: int64




```python
%%timeit -n 100
total=0
for number in numbers:
    total+=number
total/len(numbers)
```

    1.1 ms ± 4.94 µs per loop (mean ± std. dev. of 7 runs, 100 loops each)



```python
%%timeit -n 100
total=np.sum(numbers)
total/len(numbers)
```

    67.7 µs ± 3.58 µs per loop (mean ± std. dev. of 7 runs, 100 loops each)


#### Do arithmetic operations without loops



```python
numbers.head()
```




    0    365
    1    677
    2     65
    3    885
    4    541
    dtype: int64




```python
numbers+=2
numbers.head()
```




    0    367
    1    679
    2     67
    3    887
    4    543
    dtype: int64



## Creating a new element in the existing series


```python
s=pd.Series([1,2,3])
s
```




    0    1
    1    2
    2    3
    dtype: int64




```python
s["Alp"]=6
s
```




    0      1
    1      2
    2      3
    Alp    6
    dtype: int64




```python
s.loc["Eren"]=78
s
```




    0        1
    1        2
    2        3
    Alp      6
    Eren    78
    dtype: int64



## How to Merge Series with append


```python
jobs=pd.Series({"Iso":"ABS",
               "Akut":"BWC",
               "Moll":"HCK",
               "Tess":"GRB"})
jobs
```




    Iso     ABS
    Akut    BWC
    Moll    HCK
    Tess    GRB
    dtype: object




```python
my_jobs=pd.Series(["B19","JBW","NSM"],index=["Alperen","Alperen","Alperen"])

my_jobs
```




    Alperen    B19
    Alperen    JBW
    Alperen    NSM
    dtype: object




```python
all_jobs=jobs.append(my_jobs)
all_jobs
```




    Iso        ABS
    Akut       BWC
    Moll       HCK
    Tess       GRB
    Alperen    B19
    Alperen    JBW
    Alperen    NSM
    dtype: object




```python
all_jobs["Alperen"]
```




    Alperen    B19
    Alperen    JBW
    Alperen    NSM
    dtype: object




```python
all_jobs.loc["Alperen"]
```




    Alperen    B19
    Alperen    JBW
    Alperen    NSM
    dtype: object




```python

```
