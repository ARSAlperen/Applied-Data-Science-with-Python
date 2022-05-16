
# Python Functions


```python
x=1;y=2;x+y
```




    3




```python
def add_values(x,y,z=None):
    if z==None:
        return x+y
    else:
        return x+y+z

var=add_values(1,3,5)
var
```




    9



# Python Types and Sequences

## Tuples and Lists


```python
example_tuple=(1,'a',2,'b') #not mutable
```


```python
example_list=[1,'a',2,'b'] #mutable
```


```python
[1,2]+[3,4] #append list
```




    [1, 2, 3, 4]




```python
[1,2]*3 #create a list that have 3 times given list
```




    [1, 2, 1, 2, 1, 2]




```python
1 in [1,2,3] #check 1 is in list
```




    True



## String Operations

### Slicing


```python
example_string="Türkiye"
print(example_string[0:4])
```

    Türk


### Concat / Split


```python
Name="Alperen"
Surname="Arslan"
Full_name=Name+" "+Surname
print(Full_name)

"Alp" in Full_name
```

    Alperen Arslan





    True




```python
split_name=Full_name.split()
print(split_name)
```

    ['Alperen', 'Arslan']


## Dictionaries


```python
my_cats={"ra":"black","luna":"white"}
print(my_cats["ra"])
```

    black



```python
for cat_names in my_cats:
    print(my_cats[cat_names])
```

    black
    white



```python
for cat_names,cat_color in my_cats.items():
    print("{} is {}".format(cat_names,cat_color))
```

    ra is black
    luna is white


## Unpacking in Python


```python
name=('Zeynep','Sahin','Arslan')
fname,mname,lastname=name #with assignment
print(fname)
print(mname)
print(lastname)
```

    Zeynep
    Sahin
    Arslan


# Reading and Writing CSV Files 


```python
import csv

%precision 2
```




    '%.2f'




```python
with open('mpg.csv') as csvfile:
    mpg=list(csv.DictReader(csvfile))
```


    ---------------------------------------------------------------------------

    FileNotFoundError                         Traceback (most recent call last)

    <ipython-input-43-54100bdb20ae> in <module>
    ----> 1 with open('mpg.csv') as csvfile:
          2     mpg=list(csv.DictReader(csvfile))


    FileNotFoundError: [Errno 2] No such file or directory: 'mpg.csv'


# Python Dates and Times


```python
import datetime as dt
import time as tm
```


```python
tm.time()
```




    1652733794.71




```python
datenow=dt.datetime.fromtimestamp(tm.time())
datenow
```




    datetime.datetime(2022, 5, 16, 20, 43, 19, 950003)




```python
datenow.year,datenow.month,datenow.day
```




    (2022, 5, 16)




```python
today=dt.date.today()
delta=dt.timedelta(days=1)
today-delta
```




    datetime.date(2022, 5, 15)



# map() 

map(fun, iter,...)

***fun*** : It is a function to which map passes each element of given iterable. \
***iter*** : It is a iterable which is to be mapped.


```python
store1=[10,1,6,9]
store2=[8,5,6,1]
cheapest=map(min,store1,store2)
list(cheapest)
```




    [8, 1, 6, 1]




```python
people = ['Dr. Christopher Brooks', 'Dr. Kevyn Collins-Thompson', 'Dr. VG Vinod Vydiswaran', 'Dr. Daniel Romero']

def split_title_and_name(person):
    title = person.split()[0]
    lastname = person.split()[-1]
    return '{} {}'.format(title, lastname)

list(map(split_title_and_name, people))

```




    ['Dr. Brooks', 'Dr. Collins-Thompson', 'Dr. Vydiswaran', 'Dr. Romero']



# lambda() and list comprehensions

Python Lambda Functions are ***__anonymous function__*** means that the function is without a name. \
Only one expression but can be many arguments in it.

***Syntax:***
lambda arguments,...: expression


```python
def cube(y):
    return y*y*y
 
lambda_cube = lambda y: y*y*y
 
# using the normally
# defined function
print(cube(5))
 
# using the lambda function
print(lambda_cube(5))
```

    125
    125



```python
people = ['Dr. Christopher Brooks', 'Dr. Kevyn Collins-Thompson', 'Dr. VG Vinod Vydiswaran', 'Dr. Daniel Romero']

def split_title_and_name(person):
    return person.split()[0] + ' ' + person.split()[-1]

#option 1
for person in people:
    print(split_title_and_name(person) == (lambda x: x.split()[0] + ' ' + x.split()[-1])(person))

#option 2
list(map(split_title_and_name, people)) == list(map(lambda person: person.split()[0] + ' ' + person.split()[-1], people))
```

    True
    True
    True
    True





    True



# list Comprehensions


```python
my_list=[number for number in range(0,12) if number %2==0]
my_list
```




    [0, 2, 4, 6, 8, 10]




```python
def times_tables():
    lst = []
    for i in range(10):
        for j in range (10):
            lst.append(i*j)
    return lst

times_tables() == [j*i for i in range(10) for j in range(10)]

```




    True




```python
lowercase = 'abcdefghijklmnopqrstuvwxyz'
digits = '0123456789'

correct_answer = [a+b+c+d for a in lowercase for b in lowercase for c in digits for d in digits]

correct_answer[:50] # Display first 50 ids

```




    ['aa00',
     'aa01',
     'aa02',
     'aa03',
     'aa04',
     'aa05',
     'aa06',
     'aa07',
     'aa08',
     'aa09',
     'aa10',
     'aa11',
     'aa12',
     'aa13',
     'aa14',
     'aa15',
     'aa16',
     'aa17',
     'aa18',
     'aa19',
     'aa20',
     'aa21',
     'aa22',
     'aa23',
     'aa24',
     'aa25',
     'aa26',
     'aa27',
     'aa28',
     'aa29',
     'aa30',
     'aa31',
     'aa32',
     'aa33',
     'aa34',
     'aa35',
     'aa36',
     'aa37',
     'aa38',
     'aa39',
     'aa40',
     'aa41',
     'aa42',
     'aa43',
     'aa44',
     'aa45',
     'aa46',
     'aa47',
     'aa48',
     'aa49']




```python

```
