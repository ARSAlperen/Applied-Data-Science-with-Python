
# NumPy

Numpy is the fundamental package for numeric computing with Python. It provides powerful ways to create store and manipulate data, which makes it able to seamlessly and speedily integrate with a wide variety of databases and data formats. This is also the foundation that Pandas is built on which is a high performance data-centric package that we're going to learn more about in this course.


```python
import numpy as np
import math
```

## Array Creation

Array are displayed as a list or list of lists.


```python
x=np.array([6, 9, 12]) # Creating one dimensional array
print(x)

# Using array.ndim to find dimension size
print("There is/are {} dimension in this array".format(x.ndim))
```

    [ 6  9 12]
    There is/are 1 dimension in this array



```python
a=np.array([[1,2,3],[4,5,6],[9,8,6]]) 
# passing list of list to create multi-dimensional array
print(a)
```

    [[1 2 3]
     [4 5 6]
     [9 8 6]]


### Shape, Dimension, and Type


```python
a.shape # get the length of each dimension / returns a tuple
```




    (3, 3)




```python
a.dtype
```




    dtype('int64')



### Create Arrays with Filler Values (like '0')



```python
array_of_zeros=np.zeros((3,2))
array_of_ones=np.ones((2,3))
array_of_random_values=np.random.rand(2,3)*10

print(array_of_zeros)
print(array_of_ones)
print(array_of_random_values)
```

    [[0. 0.]
     [0. 0.]
     [0. 0.]]
    [[1. 1. 1.]
     [1. 1. 1.]]
    [[8.39332743 0.54308474 5.24431403]
     [5.02621355 8.88207678 7.63330546]]


### Create Array with arange() function


```python
array_sequence=np.arange(0,25,3.5) #between 0,25 and difference btwn each one is 3
print(array_sequence)
```

    [ 0.   3.5  7.  10.5 14.  17.5 21.  24.5]


### Create Array wih linspace() function for floats


```python
array_float_inrange=np.linspace(0,1,5) 
# between 0,1 and total number to be generated is 15
print(array_float_inrange)
```

    [0.   0.25 0.5  0.75 1.  ]


## Array Operations

### Aritmethic - Elementwise

Aritmethic operators (+,x,/,-) on array apply ***elementwise***



```python
a=np.array([8,9,5]);b=np.array([0,9,1])

print(a*b)
print(a-b)
print(a+b)
print(a/b)
```

    [ 0 81  5]
    [8 0 4]
    [ 8 18  6]
    [inf  1.  5.]



```python
# Conversion from inch to metre using np.array

inc=np.array([45,65,75])
metre=inc/39.37
print(metre)
```

    [1.14300229 1.6510033  1.90500381]


### Boolen Array


```python
metre>1.5
```




    array([False,  True,  True])




```python
metre%3<=3
```




    array([ True,  True,  True])



### Matrix Level Aritmethic Operations using "@"


```python
a=np.array([[8,9,5],[1,2,9],[8,7,6]])
b=np.array([[0,9,1],[7,3,6],[1,4,9]])

print(a*b) #elementwise

print(a@b) #matrix-level
```

    [[ 0 81  5]
     [ 7  6 54]
     [ 8 28 54]]
    [[ 68 119 107]
     [ 23  51  94]
     [ 55 117 104]]


### Aggregation Function in Arrays


```python
print(a.max())
print(a.min())
print(a.sum())
print(a.mean())
```

    9
    1
    55
    6.111111111111111


## Indexing, Slicing, and Iterating

### Indexing


```python
a=np.array([1,2,3])
a[2]
```




    3




```python
b=np.array([[1,2,3],[4,6,9]])
print(b[0,2])
print(b[1,1])
```

    3
    6



```python
print(b[[1,0,1],[0,1,1]])
```

    [4 2 6]


### Boolean Indexing


```python
print(b>=3)
print(b[b>=3])
```

    [[False False  True]
     [ True  True  True]]
    [3 4 6 9]


### Slicing (":")



```python
c=np.array([2,65,4,99,52,1,3])
c[2:]
```




    array([ 4, 99, 52,  1,  3])



for multi dimensional array slicing first argument is selecting rows,
and the second argument is for selecting columns


```python
d=np.array([[2,65,4,99,52,1,3],[5,6,67,8,1,0,6]])
print(d[:1])
print(d[:2,1:3])
```

    [[ 2 65  4 99 52  1  3]]
    [[65  4]
     [ 6 67]]


## NumPy with Datasets

### Wine Dataset


```python
wines=np.genfromtxt("winequality-red.csv",delimiter=";",skip_header=1)
wines
```




    array([[ 7.4  ,  0.7  ,  0.   , ...,  0.56 ,  9.4  ,  5.   ],
           [ 7.8  ,  0.88 ,  0.   , ...,  0.68 ,  9.8  ,  5.   ],
           [ 7.8  ,  0.76 ,  0.04 , ...,  0.65 ,  9.8  ,  5.   ],
           ...,
           [ 6.3  ,  0.51 ,  0.13 , ...,  0.75 , 11.   ,  6.   ],
           [ 5.9  ,  0.645,  0.12 , ...,  0.71 , 10.2  ,  5.   ],
           [ 6.   ,  0.31 ,  0.47 , ...,  0.66 , 11.   ,  6.   ]])




```python
# All rows of column 1 
print(wines[:,0])
```

    [7.4 7.8 7.8 ... 6.3 5.9 6. ]



```python
#All rows of column 1 but in correct order as they sit in their own rows
print(wines[:,0:1])
```

    [[7.4]
     [7.8]
     [7.8]
     ...
     [6.3]
     [5.9]
     [6. ]]



```python
# columns 0 through 3 
wines[:,0:3] 
```




    array([[7.4  , 0.7  , 0.   ],
           [7.8  , 0.88 , 0.   ],
           [7.8  , 0.76 , 0.04 ],
           ...,
           [6.3  , 0.51 , 0.13 ],
           [5.9  , 0.645, 0.12 ],
           [6.   , 0.31 , 0.47 ]])




```python
# give the needed column as a list to slicing operation

wines[:,[1,3,5]]
```




    array([[ 0.7  ,  1.9  , 11.   ],
           [ 0.88 ,  2.6  , 25.   ],
           [ 0.76 ,  2.3  , 15.   ],
           ...,
           [ 0.51 ,  2.3  , 29.   ],
           [ 0.645,  2.   , 32.   ],
           [ 0.31 ,  3.6  , 18.   ]])




```python
#Average of last data column 
wines[:,-1].mean()
```




    5.6360225140712945



### Graduate Admission Dataset


```python
graduate_admission=np.genfromtxt("resources/week-1/datasets/Admission_Predict.csv",dtype=None,
                                 delimiter=",",skip_header=1,
                                 names=("Serial No.","GRE_Score","TOEFL Score","University Rating","SOP",
                                        "LOR" ,"CGPA","Research","Chance_of_Admit"))
```


```python
graduate_admission.shape #consist of 400 tuples
```




    (400,)




```python
# get first 5 values from CGPA column
graduate_admission["CGPA"][0:5]
```




    array([9.65, 8.87, 8.  , 8.67, 8.21])




```python
# transform GPA's range from (1,10) to (1,4)

graduate_admission["CGPA"]=graduate_admission["CGPA"]/10*4
graduate_admission["CGPA"][0:20]
```




    array([3.86 , 3.548, 3.2  , 3.468, 3.284, 3.736, 3.28 , 3.16 , 3.2  ,
           3.44 , 3.36 , 3.6  , 3.64 , 3.2  , 3.28 , 3.32 , 3.48 , 3.2  ,
           3.52 , 3.4  ])




```python
# How many students have had research experince by creating a boolean mask
len(graduate_admission[graduate_admission["Research"]==1])
```




    219




```python
print(graduate_admission[graduate_admission["Chance_of_Admit"]>0.8]["GRE_Score"].mean())
```

    328.7350427350427



```python
print(graduate_admission[graduate_admission["Chance_of_Admit"]<0.4]["GRE_Score"].mean())
```

    302.2857142857143



```python
print(graduate_admission[graduate_admission["Chance_of_Admit"]>0.8]["CGPA"].mean())
print(graduate_admission[graduate_admission["Chance_of_Admit"]<0.4]["CGPA"].mean())
```

    3.7106666666666666
    3.0222857142857142



```python

```
