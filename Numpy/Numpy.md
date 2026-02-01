## 🔹 STEP 1: Problem with Python Lists

```python
a = [1, 2, 3, 4]
b = [10, 20, 30, 40]

# element-wise addition
result = []
for i in range(len(a)):
    result.append(a[i] + b[i])

print(result)
```

### ❌ Problems with Python Lists

1. Loop manually likhna padta hai
2. Code lengthy ho jata hai
3. Large data pe slow hota hai
4. Memory efficient nahi hota

---

## 🔹 STEP 2: NumPy Solution

```python
import numpy as np

a = np.array([1, 2, 3, 4])
b = np.array([10, 20, 30, 40])

print(a + b)
```

### ✅ Output

```
[11 22 33 44]
```

<img width="758" height="309" alt="image" src="https://github.com/user-attachments/assets/b4f0f40b-940f-4799-ad4d-02650dd9ca47" />

✔ No loops
✔ Short & readable code
✔ Faster & memory efficient

---

## 🔹 STEP 3: What is ndarray?

```python
type(a)
```

### Output

```
<class 'numpy.ndarray'>
```

👉 **ndarray** = NumPy ka main object
👉 Matlab **n-dimensional array**

---

## 🔹 STEP 4: Creating NumPy Arrays

```python
import numpy as np

arr = np.array([1, 2, 3, 4])

arr = np.array([1, 2.5, 3])
print(arr)
print(arr.dtype)
```

### Output

```
[1.  2.5 3. ]
float64
```

📌 NumPy automatically type convert kar deta hai (int → float)

---

## 🔹 Array Properties: shape, ndim, indexing

```python
import numpy as np

arr1 = np.array([10, 20, 30, 40])

print(arr1)
print(arr1.ndim)
print(arr1.shape)
```

### Output

```
[10 20 30 40]
1
(4,)
```

---

## 🔹 STEP 5: 2D Arrays

```python
marks = np.array([
    [80, 85, 90],
    [70, 75, 88],
    [92, 89, 95]
])

print(marks.ndim)
print(marks.shape)
```

### Output

```
2
(3, 3)
```

---

## 🔹 Array Slicing

```python
marks[0:2, 1:3]
```

✔ Rows: 0 & 1
✔ Columns: 1 & 2

### Negative Indexing

```python
marks[-1]       # last student
marks[:, -1]   # last subject
```

```python
print(marks.shape)
```

---

## 🔹 Array Creation Functions

### zeros() & ones()

```python
z = np.zeros((3, 4))
o = np.ones((2, 3))

print(z)
print(o)
```

---

### arange() – Better than range()

```python
arr = np.arange(1, 10)
print(arr)
```

Output:

```
[1 2 3 4 5 6 7 8 9]
```

With step:

```python
np.arange(0, 20, 2)
```

---

### linspace()

```python
np.linspace(1, 10, 5)
```

Output:

```
[ 1.    3.25  5.5   7.75 10.  ]
```

---

### reshape()

```python
arr = np.arange(1, 7)
print(arr.reshape(2, 3))
```

Output:

```
[[1 2 3]
 [4 5 6]]
```

---

### flatten()

```python
arr2d = np.array([[1, 2, 3], [4, 5, 6]])
print(arr2d.flatten())
```

Output:

```
[1 2 3 4 5 6]
```

---

## 🔹 AXIS Concept

```python
marks.mean(axis=0)   # column-wise average
marks.mean(axis=1)   # row-wise average
```

---

## 🔹 Broadcasting

### ❌ Problem (Python List)

```python
salary = [30000, 40000, 50000]
bonus = 5000

new_salary = []
for s in salary:
    new_salary.append(s + bonus)

print(new_salary)
```

Issues: loop, boring, slow for big data.

---

### ✅ NumPy Way

```python
salary = np.array([30000, 40000, 50000])
bonus = 5000

print(salary + bonus)
```

Output:

```
[35000 45000 55000]
```

---

### Scalar Broadcasting

```python
arr = np.array([1, 2, 3, 4])

print(arr * 10)
print(arr + 5)
print(arr - 2)
```

---

### Broadcasting with 2D Arrays

```python
marks = np.array([
    [80, 85, 90],
    [70, 75, 88],
    [92, 89, 95]
])

bonus = 5
print(marks + bonus)
```

---

## 🔹 Boolean Masking & Filtering

### Boolean Array

```python
arr = np.array([10, 20, 30, 40])
print(arr > 25)
```

Output:

```
[False False  True  True]
```

---

### Filtering using Boolean Mask

```python
arr[arr > 25]
```

Output:

```
[30 40]
```

---

### Multiple Conditions

```python
salary[(salary > 20000) & (salary < 50000)]
```

---

### Boolean Mask on 2D Array

```python
marks = np.array([
    [80, 35, 90],
    [45, 60, 30],
    [92, 88, 95]
])

marks[marks > 40]
```

Output:

```
[80 90 45 60 92 88 95]
```

---

## 🔹 File Handling with NumPy (loadtxt & savetxt)

### marks.csv

```
80,85,90
70,75,88
92,89,95
```

---

### Reading File using loadtxt()

```python
data = np.loadtxt("marks.csv", delimiter=",")
print(data)
print(data.shape)
```

Output:

```
[[80. 85. 90.]
 [70. 75. 88.]
 [92. 89. 95.]]
```

📌 Default dtype = float

---

### Load with Specific dtype

```python
data = np.loadtxt("marks.csv", delimiter=",", dtype=int)
```

---

### File with Header

```python
data = np.loadtxt(
    "marks.csv",
    delimiter=",",
    skiprows=1
)
```

---

### Writing File using savetxt()

```python
np.savetxt(
    "output.csv",
    data,
    delimiter=",",
    fmt="%d"
)
```

Format options:

* `%d` → integer
* `%.2f` → float (2 decimals)

---

## 🔹 Mini Project: Student Result System

### marks.csv

```
78,85,90
35,40,45
88,92,95
60,70,65
```

### Code

```python
import numpy as np

# 1. Load data
marks = np.loadtxt("marks.csv", delimiter=",", dtype=int)

# 2. Student-wise average
student_avg = marks.mean(axis=1)

# 3. Pass / Fail
result = np.where(student_avg >= 50, "Pass", "Fail")

# 4. Combine data
final_data = np.column_stack((student_avg, result))

print(final_data)
```

---

### Save Result to File

```python
np.savetxt(
    "result.csv",
    final_data,
    delimiter=",",
    fmt="%s",
    header="Average,Result",
    comments=""
)
```
