
we have four collections in python:
1. List
2. Tuples
3. Sets
4. Dictionaries

## List

#### introduction
Lists are used to store multiple items in a single variable.

```python
thislist = ["apple", "banana", "cherry"]  
print(thislist)
```

> List is :
> - **Ordered**
> - **Changeable**
> - **Allow Duplicates**

> To determine how many items a list has, use the `len()` function

A list can contain different data types:
```python
list1 = ["abc", 34, True, 40, "male"]
```


From Python's perspective, lists are defined as objects with the data type 'list':
```python
# <class 'list'>

mylist = ["apple", "banana", "cherry"]  
print(type(mylist)) # <class 'list'>
```

 Using the `list()` constructor to make a List:
 ```python
 thislist = list(("apple", "banana", "cherry")) # note the double round-brackets  
print(thislist)
```

> the `list()` constructor gets an iterator, like the above example:
>  `("apple", "banana", "cherry"`) is an iterator.


#### **negative indexes**
```python
thislist = ["apple", "banana", "cherry"]  
print(thislist[-2]) # banana
```

#### **range of indexes**
```python
thislist = ["apple", "banana", "cherry", "orange", "kiwi", "melon", "mango"]  
print(thislist[2:5]) 
```

> From index 2 to 5 (**5 not included**)

#### **Check if Item Exists**
To determine if a specified item is present in a list use the `in` keyword:
```python
thislist = ["apple", "banana", "cherry"]  
if "apple" in thislist:  
  print("Yes, 'apple' is in the fruits list")
```


#### Change a range of item values
```python
thislist = ["apple", "banana", "cherry"]  
thislist[1:2] = ["blackcurrant", "watermelon"]  
print(thislist)

# output: ['apple', 'blackcurrant', 'watermelon', 'cherry']
```

#### Insert Items
Insert `"watermelon"` as the third item :
```python
thislist = ["apple", "banana", "cherry"]  
thislist.insert(2, "watermelon")  
print(thislist)
```

#### Append Items
```python
thislist = ["apple", "banana", "cherry"]  
thislist.append("orange")  
print(thislist)
```

#### Add any iterable
The `extend()` method appends any iterable object.
```python
thislist = ["apple", "banana", "cherry"]  
thistuple = ("kiwi", "orange")  
thislist.extend(thistuple)  
print(thislist)
```

#### Remove specified Item
```python
thislist = ["apple", "banana", "cherry"]  
thislist.remove("banana")  
print(thislist)
```


#### Remove specified Index
`pop()`:
```python
thislist = ["apple", "banana", "cherry"]  
thislist.pop(1)  
print(thislist)
```

`del:`
```python
thislist = ["apple", "banana", "cherry"]  
del thislist[0]  
print(thislist)
```

The `del` keyword also delete the list completely.
```python
thislist = ["apple", "banana", "cherry"]  
del thislist
```


#### Clear the List
The `clear()` method empties the list
```python
thislist = ["apple", "banana", "cherry"]  
thislist.clear()  
print(thislist)
```

#### Loop
```python
thislist = ["apple", "banana", "cherry"]  
for x in thislist:  
  print(x)
```

**Loop through the index numbers**
```python
thislist = ["apple", "banana", "cherry"]  
for i in range(len(thislist)):  
  print(thislist[i])
```

**`range(x)` mean from 1 to x - 1**


