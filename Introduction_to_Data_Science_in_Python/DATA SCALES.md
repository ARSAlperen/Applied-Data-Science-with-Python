
# DATA SCALES
![image.png](attachment:image.png)

there's at least four
different scales

## Nominal Scales (Classification)
- __Variables are just named or labeled with no specific order.__
- Categories of data, but categories have no order with respect to one another
- Gender, Political Choose, Place of living

![image.png](attachment:image.png)

## Ordinal Scale (Sıralamalı)
- __Variables are named and in specific order.__
- The order of the units is important, but __not equally spaced.__
- Like letter grades such as A+, A are a good example.
- frequency, satisfaction, happiness, a degree of pain, etc

![image.png](attachment:image.png)

## Interval Scale (Aralıklı)
- Units are equally spaced.
- But there is no true zero point so mathematical operations of */ are not valid.
- Temperatureas measured in Celsius or Fahrenheit
- Direction on a compass
- __Zero value is actually a meaningful value__
![image.png](attachment:image.png)

## Ratio Scale (Oranlı)
- Units are equally spaced
- Mathematical operations of +-/* are all valid.
- like height and weight
- Because of the existence of true zero value, __the ratio scale doesn’t have negative values.__

![image.png](attachment:image.png)


![image.png](attachment:image.png)

# DATA SCALES IN PYTHON



```python
import pandas as pd

df=pd.DataFrame(['A+', 'A', 'A-', 'B+', 'B', 'B-', 'C+', 'C', 'C-', 'D+', 'D'],
                index=['excellent', 'excellent', 'excellent', 'good', 'good', 'good', 
                       'ok', 'ok', 'ok', 'poor', 'poor'],
               columns=["Grades"])

print(df)
df.dtypes
```

              Grades
    excellent     A+
    excellent      A
    excellent     A-
    good          B+
    good           B
    good          B-
    ok            C+
    ok             C
    ok            C-
    poor          D+
    poor           D





    Grades    object
    dtype: object



## Nominal - Categorical


```python
df["Grades"].astype("category")
```




    excellent    A+
    excellent     A
    excellent    A-
    good         B+
    good          B
    good         B-
    ok           C+
    ok            C
    ok           C-
    poor         D+
    poor          D
    Name: Grades, dtype: category
    Categories (11, object): [A, A+, A-, B, ..., C+, C-, D, D+]



## Ordinal - Categorical and in Order


```python
my_categories=pd.CategoricalDtype(categories=['D', 'D+', 'C-', 'C', 'C+', 'B-', 'B', 'B+', 'A-', 'A', 'A+'], 
                           ordered=True)
grades=df["Grades"].astype(my_categories)
grades.head()
```




    excellent    A+
    excellent     A
    excellent    A-
    good         B+
    good          B
    Name: Grades, dtype: category
    Categories (11, object): [D < D+ < C- < C ... B+ < A- < A < A+]




```python
grades[grades>"C"]
```




    excellent    A+
    excellent     A
    excellent    A-
    good         B+
    good          B
    good         B-
    ok           C+
    Name: Grades, dtype: category
    Categories (11, object): [D < D+ < C- < C ... B+ < A- < A < A+]



## Create Categorical Intervals from Inverval or Ratio Scaled Data

Espacially important for creating histograms and classification machine learning algorithms


```python
import numpy as np

df=pd.read_csv("resources/week-3/datasets/census.csv")

df=df[df['SUMLEV']==50]

df=df.set_index('STNAME').groupby(level=0)['CENSUS2010POP'].agg(np.average)
df.head()
```




    STNAME
    Alabama        71339.343284
    Alaska         24490.724138
    Arizona       426134.466667
    Arkansas       38878.906667
    California    642309.586207
    Name: CENSUS2010POP, dtype: float64



### Create bins with cut function

Pandas cut() function is used to separate the array elements into different __bins__ . The cut function is mainly used to perform statistical analysis on scalar data.  


```python
pd.cut(df,10).head()
```




    STNAME
    Alabama         (11706.087, 75333.413]
    Alaska          (11706.087, 75333.413]
    Arizona       (390320.176, 453317.529]
    Arkansas        (11706.087, 75333.413]
    California    (579312.234, 642309.586]
    Name: CENSUS2010POP, dtype: category
    Categories (10, interval[float64]): [(11706.087, 75333.413] < (75333.413, 138330.766] < (138330.766, 201328.118] < (201328.118, 264325.471] ... (390320.176, 453317.529] < (453317.529, 516314.881] < (516314.881, 579312.234] < (579312.234, 642309.586]]




```python
df= pd.DataFrame({'number': np.random.randint(1, 100, 10)})
df['bins'] = pd.cut(x=df['number'], bins=[1, 20, 40, 60,
                                          80, 100])
print(df)
 
# We can check the frequency of each bin
print(df['bins'].unique())
```

       number       bins
    0       8    (1, 20]
    1      80   (60, 80]
    2      35   (20, 40]
    3      95  (80, 100]
    4      90  (80, 100]
    5      13    (1, 20]
    6      15    (1, 20]
    7      12    (1, 20]
    8      49   (40, 60]
    9      54   (40, 60]
    [(1, 20], (60, 80], (20, 40], (80, 100], (40, 60]]
    Categories (5, interval[int64]): [(1, 20] < (20, 40] < (40, 60] < (60, 80] < (80, 100]]



```python

```
