# ECE-2112-PA-2
**Submitted by: Niamh Reese B. Pamilar | 2ECE-C**

**Date Submitted: August 30, 2026**


This repository contains Programming Assignment 2 for the course **ECE 2112: Advanced Computer Programming and Algorithms**. The assignment, titled **Experiment 2: Numerical Python (NumPy)**, consists of three Python problems that apply NumPy arrays, array reshaping, vectorized numerical operations, array statistics, Boolean filtering, and saving NumPy arrays as `.npy` files.



**Objectives:**

By the end of this activity, students should be able to:
1. create and reshape NumPy arrays using appropriate NumPy functions;
2. perform vectorized numerical operations on an ndarray;
3. compute array statistics and use Boolean conditions to select elements; and
4. save computed NumPy arrays as .npy files.



## A. Reproducible Normalization Problem
Create a reproducible random 5×5 integer `ndarray` named `X`. The random number generator is initialized using the required seed, and the array contains random integers from 10 to 100.

The following NumPy functions and methods were used in this problem:
- `np.random.seed(2112)` - sets the seed of NumPy's random number generator. Using a fixed seed makes the generated random numbers reproducible, meaning the same values will be generated every time the code is executed.
- `np.random.randint(10, 101, size=(5, 5))` - generated random integers from 10 up to, but not including, 101. The `size=(5, 5)` argument creates an array with 5 rows and 5 columns.
- `np.mean(X)` - calculates the arithmetic mean of all the elements in the array.
- `np.std(X)` - calculates the standard deviation of the elements in the array. The default NumPy behavior was used as required in the instructions.
- `(X - X_mean) / X_std)` - performs the normalization calculation using the given formula `Z = (X - x̄) / σ`. NumPy performs the subtraction and division on every element of the array without requiring a loop.

The random seed and array were created using:
```python
np.random.seed(2112)
X = np.random.randint(10, 101, size=(5, 5))
```

The generated array was:
```text
[[48 11 15 67 21]
 [11 41 13 66 24]
 [71 79 53 67 70]
 [77 35 91 19 96]
 [35 54 37 41 17]]
```

The mean and standard deviation were then calculated:
```python
X_mean = np.mean(X)
X_std = np.std(X)
```

The calculated values were:
```text
Mean = 46.36
Standard deviation = 25.864075471588002
```

The normalized array was calculated using:
```python
X_normalized = (X - X_mean) / X_std
```

The expression `X -  X_mean` subtracts the mean from every element of `X`. The result if then divided by `X_std`, which produces the normalized values.

The resulting normalized array was:
```python
[[ 0.06340841 -1.36714726 -1.2124926 0.79801809 -0.98051059] 
[-1.36714726 -0.20723725 -1.28981993 0.75935442 -0.86451959] 
[ 0.95267275 1.26198209 0.25672675 0.79801809 0.91400909] 
[1.18465476 -0.43921926 1.72594609 -1.05783793 1.91926443] 
[-0.43921926 0.29539042 -0.36189192 -0.20723725 -1.13516526]]
```

The normalized array was checked using:
```python
X_normalized_mean = np.mean(X_normalized)
X_normalized_std = np.std(X_normalized)

print("Normalized Mean (must be 0):", X_normalized_mean)
print("Normalized Std Dev (must be 1):", X_normalized_std)
```

Output:
```python
Normalized Mean (must be 0): 0.0 
Normalized Std Dev (must be 1): 0.9999999999999999
```

The normalized array produced a mean of `0.0`, which satisfies the required value of 0. The normalized standard deviation of approximately `0.9999999999999999`, which is effectively 1. The very small difference from exactly 1 is caused by floating-point representation when numerical calculations are performed by a computer.

The normalized array was saved using:
`np.save("X_normalized.npy", X_normalized)`.
`np.save()` saves a NumPy array into a `.npy` file. In this case, the normalized array is stored in the file `X_normalized.npy`.


## B. Cubes Divisible by 4 Problem
Create an array containing the first 100 positive integers, reshape it into a 10 × 10 `ndarray`, cube every element, and select only the cubed values that are divisible by 4.

The following NumPy functions and methods were used in this problem:
- `np.arange(1, 101)` - creates a sequence of integers beginning at 1 and ending before 101. Therefore, the resulting array contains the numbers 1 through 100.
- `.resize(10, 10)` - changes the shape of the array into 10 rows and 10 columns.
- `np.power(C, 3)` - raises every element of C to the third power. For example, 2 becomes 8 because 2³ = 8.
- `%` - the modulo operator returns the remainder after division. For examples, `8 % 4` returns 0 because 8 is exactly divisible by 4.
- `==` - checks whether two values are equal. In `C % 4 == 0`, it checks whether the remainder is equal to 0.
- `C[C % 4 == 0]` - uses Boolean filtering to select only the elements of C that satisfy the condition.

The first positive integers were created and reshaped using:
```python
C = np.arange(1, 101)
C.resize(10, 10)
```

The `.resize(10, 10)` method changes the array from a one-dimensional array containing 100 elements into a two-dimensional array containing 10 rows and 10 columns.

Each element is then cubed using NumPy's `power()` function:
```python
C = np.power(C, 3)
```
This produces cubes from `1³` through `100³`. The array therefore begins with `1` and ends with `1,000,000`.

A Boolean condition is used to select only the cubed values divisible by 4:
```python
div_by_4 = C[C % 4 == 0]
```
The expression `C % 4` calculates the remainder when every element of `C` is divided by 4. The condition `== 0` identifies the values with no remainder. `C[C % 4 == 0]` is called Boolean filtering. It allows NumPy to select only the elements where the condition is `True`.

The required checks were performed using:
```python
print("Shape of C:", C.shape)
print("Number of selected elements:", len(div_by_4))
print("First selected:", div_by_4[0])
print("Last selected:", div_by_4[-1])
```

Output:
```python
Shape of C: (10, 10) 
Number of selected elements: 50 
First selected: 8 
Last selected: 1000000
```

The shape (10, 10) confirms that C contains 10 rows and 10 columns. There are 50 selected elements, and the first and last selected values are 8 and 1,000,000, respectively.

The selected values were saved using:
`np.save("div_by_4.npy", div_by_4)`.
This saves the resulting NumPy array into the file `div_by_4.npy`.


## C. Above-Mean Squares Problem
Create an array containing the first 36 positive integers, reshape it into a 6 × 6 `ndarray`, square every element, calculate the mean, and select only the values that are strictly greater than the mean.

The following NumPy functions and methods were used in this problem:
- `np.arange(1, 37)` - creates a sequence of integers beginning at 1 and ending before 37. This produces the numbers 1 through 36.
- `.resize(6, 6)` - changes the shape of the array into 6 rows and 6 columns.
- `np.square(S)` - calculates the square of every element in the array.
- `np.mean(S)` - calculates the arithmetic mean of all the squared values.
- `>` - the greater-than operator checks whether each value is strictly greater than the mean.
- `S[S > S_mean]` - uses Boolean filtering to select only the elements that are greater than the calculated mean.

The first 36 positive integers were created and reshaped using:
```python
S = np.arange(1, 37)
S.resize(6, 6)
```

The resulting array contains:
```python
[[ 1 2 3 4 5 6]
[ 7 8 9 10 11 12]
[13 14 15 16 17 18]
[19 20 21 22 23 24]
[25 26 27 28 29 30]
[31 32 33 34 35 36]]
```

The values were then squared using:
```python
S = np.square(S)
```

After squaring, the array becomes:
```python
[[   1    4    9   16   25   36]
 [  49   64   81  100  121  144]
 [ 169  196  225  256  289  324]
 [ 361  400  441  484  529  576]
 [ 625  676  729  784  841  900]
 [ 961 1024 1089 1156 1225 1296]]
```

The mean of the squared values was calculated using:
```python
S_mean = np.mean(S)
```

The calculated mean was:
`450.1666666666667`

The values strictly greater than the mean were selected using:
```python
above_mean = S[S > S_mean]
```

The `>` operator compares every element in `S` with `S_mean`. A value is selected only if it is greater than the mean.

The resulting array is:
```python
[ 484  529  576  625  676  729  784  841  900  961 1024 1089 1156 1225 1296]
```

The required checks were performed using:
```python
print("Number of selected elements:", len(above_mean))
print("First selected:", above_mean[0])
print("Last selected:", above_mean[-1])
```

Output:
```python
Number of selected elements: 15
First selected: 484
Last selected: 1296
```

There are 15 values strictly greater than the mean. The first selected value is `484`, while the last selected value is `1296`.

The selected values were saved using:
`np.save("above_mean.npy", above_mean)`.
This saves the resulting NumPy array into the file `above_mean.npy`.


## Jupyter Notebook

To view the complete Python program for Programming Assignment 2, open [ECE2112 - PA2](https://github.com/niamhreesepamilar/ECE-2112-PA-2/blob/main/ECE2112%20-%20PA2.ipynb). Open the file in Jupyter Notebook and select **Run All** to execute every cell.

The notebook contains the complete solutions for Problems A, B, and C, including the required calculations, Boolean filtering, checks, and saving of the resulting NumPy arrays.

The following `.npy` files are also included in the repository:
- `X_normalized.npy` - contains the normalized array from Problem A.
- `div_by_4.npy` - contains the cubed values divisible by 4 from Problem B.
- `above_mean.npy` - contains the squared values greater than the mean from Problem C.

Thank you for reading!
