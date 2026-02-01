#include ndarray , & creation

STEP 1: Problem with Python Lists

a = [1, 2, 3, 4]
b = [10, 20, 30, 40]

# element-wise addition chahiye
result = []
for i in range(len(a)):
    result.append(a[i] + b[i])

print(result)


Problems were : 
1. Loop writing , 2. code lengthy , 3. Slow on large data  , 4. more memory


STEP 2: NumPy Solution

import numpy as np

a = np.array([1, 2, 3, 4])
b = np.array([10, 20, 30, 40])

print(a + b)

output:

[11 22 33 44]

<img width="758" height="309" alt="image" src="https://github.com/user-attachments/assets/b4f0f40b-940f-4799-ad4d-02650dd9ca47" />

STEP 3: What is ndarray?

type(a)

output: <class 'numpy.ndarray'>

NumPy ka main object = ndarray (n-dimensional array)

STEP 4: Creating NumPy Arrays

arr = np.array([1, 2, 3, 4])

arr = np.array([1, 2.5, 3])
print(arr)
print(arr.dtype)

output:

[1.  2.5 3. ]
float64


# Include shape , ndim , indexing 

import numpy as np

arr1 = np.array([10, 20, 30, 40])


print(arr1)
print(arr1.ndim)
print(arr1.shape)

output:

[10 20 30 40]
1
(4,)


STEP 2: 2D Array

marks = np.array([
    [80, 85, 90],
    [70, 75, 88],
    [92, 89, 95]
])

print(marks.ndim)
print(marks.shape)

output:

2
(3, 3)

## slicing

marks[0:2, 1:3]

include rows 0 & 1 and column 1 & 2

Negative indexing : 

marks[-1]        # last student
marks[:, -1]    # last subject

also , print(array.shape)



# include zeros • ones • arange • linspace • reshape • flatten • axis

STEP 1: zeros() & ones()

import numpy as np

z = np.zeros((3, 4))
o = np.ones((2, 3))

print(z)
print(o)


STEP 2: arange() (like range but better)

arr = np.arange(1, 10)
print(arr)

[1 2 3 4 5 6 7 8 9]

with steps: np.arange(0, 20, 2)


STEP 3: linspace()

np.linspace(1, 10, 5)

output:

[ 1.    3.25  5.5   7.75 10.  ]


STEP 4: reshape()

arr = np.arange(1, 7)
print(arr.reshape(2, 3))

output: 

[[1 2 3]
 [4 5 6]]


STEP 5: flatten()

arr2d = np.array([[1,2,3],[4,5,6]])
print(arr2d.flatten())

output:

[1 2 3 4 5 6]


STEP 6: AXIS

marks = np.array([
    [80, 85, 90],
    [70, 75, 88],
    [92, 89, 95]
])

marks.mean(axis=0) , means har column ka average

marks.mean(axis=1)


# Broadcasting 

STEP 1:Problem 

salary = [30000, 40000, 50000]
bonus = 5000

new_salary = []
for s in salary:
    new_salary.append(s + bonus)

print(new_salary)


again same issue of loop , boring , slow for big data

STEP 2: NumPy Way 

import numpy as np

salary = np.array([30000, 40000, 50000])
bonus = 5000

print(salary + bonus)


output:

[35000 45000 55000]


STEP 3: Scalar Broadcasting

arr = np.array([1, 2, 3, 4])

print(arr * 10)
print(arr + 5)
print(arr - 2)


STEP 5: Broadcasting with 2D Arrays

marks = np.array([
    [80, 85, 90],
    [70, 75, 88],
    [92, 89, 95]
])

bonus = 5
print(marks + bonus)


# include Boolean Masking & Filtering

STEP 1: Boolean Array

import numpy as np

arr = np.array([10, 20, 30, 40])

print(arr > 25)

output:

[False False  True  True]


STEP 2: Filtering using Boolean Mask

arr[arr > 25]

[30 40]


STEP 4: Multiple Conditions

salary[(salary > 20000) & (salary < 50000)]


STEP 6: Boolean Mask on 2D Array


marks = np.array([
    [80, 35, 90],
    [45, 60, 30],
    [92, 88, 95]
])

All passing marks (>40):

marks[marks > 40]


[80 90 45 60 92 88 95]



#include loadtxt • savetxt • mini project

marks.csv

80,85,90
70,75,88
92,89,95

STEP 2: np.loadtxt() — File READ

import numpy as np

data = np.loadtxt("marks.csv", delimiter=",")
print(data)
print(data.shape)

output:


[[80. 85. 90.]
 [70. 75. 88.]
 [92. 89. 95.]]


Now default dtype will be float , and delimiter is important


STEP 3: Specific dtype ke saath load karna


data = np.loadtxt("marks.csv", delimiter=",", dtype=int)


STEP 4: Agar file me header ho

eg:

Maths,Science,English
80,85,90
70,75,88

data = np.loadtxt(
    "marks.csv",
    delimiter=",",
    skiprows=1
)


STEP 5: np.savetxt() — File WRITE karna


np.savetxt(
    "output.csv",
    data,
    delimiter=",",
    fmt="%d"
)


%d → integer

%.2f → float (2 decimals)


Step 6:

avg = data.mean(axis=1)
print("Student averages:", avg)

subject_avg = data.mean(axis=0)
print("Subject averages:", subject_avg)


Suppose:

marks.csv

78,85,90
35,40,45
88,92,95
60,70,65


import numpy as np

# 1. Load data
marks = np.loadtxt("marks.csv", delimiter=",", dtype=int)

# 2. Student-wise average
student_avg = marks.mean(axis=1)

# 3. Pass / Fail (avg >= 50)
result = np.where(student_avg >= 50, "Pass", "Fail")

# 4. Combine data
final_data = np.column_stack((student_avg, result))

print(final_data)


save result to file

np.savetxt(
    "result.csv",
    final_data,
    delimiter=",",
    fmt="%s",
    header="Average,Result",
    comments=""
)
