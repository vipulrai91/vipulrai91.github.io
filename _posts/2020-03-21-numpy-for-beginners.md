---
layout: post
tags: [python ,numpy] 
comments: true
---

# This tutorial is practice assignment from the course <http://cs231n.github.io/>

# To find the version of Python

```python
import sys
print(sys.version)
```

```console
3.6.8 |Anaconda, Inc.| (default, Dec 30 2018, 01:22:34)
[GCC 7.3.0]
```

## Slicing in Python

```python
num = [22,44,66,11,45,56]
print(num)
```

```console
[22, 44, 66, 11, 45, 56]
```

```python
print(num[:3])
```

```console
[22, 44, 66]
```

```python
print(num[1:3])
```

```console
[44, 66]
```

```python
print(num[2:])
```

```console
[66, 11, 45, 56]
```

## List comprehension to print square of numbers

### First we create a list of numbers from 1-9 using range and then get the square as list , Note : list comprehension is applied on list and returns a list

```python
[ x*x for x in list(range(1,10))]
```

```console
[1, 4, 9, 16, 25, 36, 49, 64, 81]
```

## Conditional list comprehension , returning only the even sqaures

```python
[ x*x for x in list(range(1,10)) if x%2==0]
```

```console
[4, 16, 36, 64]
```

## Numpy

```python
import numpy as np
```

### Arrays

#### A numpy array is grid of values all of same type

#### Is indexed by a tuple of nonnegative integers

#### RANK : The number of dimension is the rank of array

#### SHAPE : The shape of array is a tuple of integers giving the size of each dimension

```python
# Creating a rank 1 array
array1 = np.array([1,2,3,4,5,6])
```

```python
print(type(array1)) ; print(array1.shape) ; print(array1[1])
```

```console
<class 'numpy.ndarray'>
(6,)
2
```

```python
# Creating a rank 2 array
array2 = np.array([[1,2,3] , [6,7,8]])
```

```python
print(type(array2)) ; print(array2.shape) , print(array2[0])
```

```console
<class 'numpy.ndarray'>
(2, 3)
[1 2 3]
```

### Other ways to create np arrays

#### Create an array of all zeros

```python
np.zeros((3,3))
```

```console
array([[0., 0., 0.],
       [0., 0., 0.],
       [0., 0., 0.]])
```

#### Create an array of all ones

```python
np.ones((2,2))
```

```console
array([[1., 1.],
       [1., 1.]])
```

#### Create constant array

```python
np.full((3,3),2)
```

```console
array([[2, 2, 2],
       [2, 2, 2],
       [2, 2, 2]])
```

#### Create identity matrix

```python
np.eye(3)
```

```console
array([[1., 0., 0.],
       [0., 1., 0.],
       [0., 0., 1.]])
```

#### Create an array with Random values

```python
rand_np = np.random.random((6,4))
print(rand_np)
```

```console
[[0.05080747 0.42425544 0.57862652 0.32096002]
 [0.07626656 0.2110246  0.05251395 0.75752798]
 [0.63088127 0.67261688 0.92382051 0.34417774]
 [0.21743804 0.15609258 0.07513012 0.78520746]
 [0.23994478 0.32181935 0.3711074  0.67729622]
 [0.68537627 0.49100271 0.81613017 0.89442773]]
```

### Array Mathematics

```python
x = np.array([[1,2],[3,4]] ,dtype = np.float64)
x
```

```console
array([[1., 2.],
       [3., 4.]])
```

```python
y = np.array([[5,6],[7,8]] , dtype = np.float64)
```

```python
x + y
```

```console
array([[ 6.,  8.],
       [10., 12.]])
```

```python
v = np.array([9,10]) ;  v
```

```console
array([ 9, 10])
```

```python
w = np.array([11, 12]) ; w
```

```console
array([11, 12])
```

```python
np.add(x,y)
```

```console
array([[ 6.,  8.],
       [10., 12.]])
```

```python
# Matrix / Vector product , produce rank 1 array
print(x.dot(v))
# or
print(np.dot(x,v))
```

```console
[29\. 67.]
[29\. 67.]
```

```python
#Matrix/matix product
print(x.dot(y))
# or
print(np.dot(x,y))
```

```console
[[19\. 22.]
 [43\. 50.]]
[[19\. 22.]
 [43\. 50.]]
```

### Broadcasting

#### _If the dimensions of two arrays are dissimilar, element-to-element operations are not possible. However, operations on arrays of non-similar shapes is still possible in NumPy, because of the broadcasting capability. The smaller array is broadcast to the size of the larger array so that they have compatible shapes._

```python
a = np.array([[1,2] , [5,6], [3,5]])
b = np.array([30,40])
```

```python
print(a.shape) ; print(b.shape)
```

```console
(3, 2)
(2,)
```

```python
np.dot(a,b)
```

```console
array([110, 390, 290])
```

## Matplotlib

```python
import numpy as np
import matplotlib.pyplot as plt

# Compute the x and y coordinates for points on a sine curve
x = np.arange(0, 4 * np.pi, 0.1)
y = np.sin(x)

# Plot the points using matplotlib
plt.plot(x, y)
plt.show()
```

![sine](/assets/img/numpy/output_48_0.png "sine")

```python
import numpy as np
import matplotlib.pyplot as plt

# Compute the x and y coordinates for points on sine and cosine curves
x = np.arange(0, 3 * np.pi, 0.1)
y_sin = np.sin(x)
y_cos = np.cos(x)

# Plot the points using matplotlib
plt.plot(x, y_sin)
plt.plot(x, y_cos)
plt.xlabel('x axis label')
plt.ylabel('y axis label')
plt.title('Sine and Cosine')
plt.legend(['Sine', 'Cosine'])
plt.show()
```

![cosine](/assets/img/numpy/output_49_0.png "sine and cosine")
