# 1.File Handling 

##  File open 

```python
f = open("notes.txt", "r")
```

Here:

* `"notes.txt"` → file name
* `"r"` → mode (read)

### Modes :

| Mode | Meaning                     |
| ---- | --------------------------- |
| `r`  | Read (file must exist)    |
| `w`  | Write (old file erase ❗) |
| `a`  | Append (safe add)           |
| `r+` | Read + write                |

---

## 📖 File read 

### 1️⃣ read() — all at a time

```python
f = open("notes.txt", "r")
data = f.read()
print(data)
f.close()
```

### Important:

* `read()` whole file in string

---

### 2️⃣ readline() — 1 line

```python
print(f.readline())
```

---

### 3️⃣ readlines() — list of lines

```python
lines = f.readlines()
print(lines)
```

Output:

```python
["hello\n", "world\n"]
```

---

## ✍️ File write 

### Write mode (`w`)

```python
f = open("notes.txt", "w")
f.write("Hello Soni\n")
f.write("Learning Python\n")
f.close()
```

🧨 Warning:

* If there was a file , it will delete it:)

---

### Append mode (`a`) — SAFE MODE ✅

```python
f = open("notes.txt", "a")
f.write("New line added\n")
f.close()
```

---

##  VERY IMPORTANT: `with` keyword


```python
with open("notes.txt", "r") as f:
    data = f.read()
    print(data)
```
##  JSON 

```json
[
  {"id": 1, "name": "Aman", "age": 21},
  {"id": 2, "name": "Riya", "age": 20}
]
```

👉 Easy to read
👉 Easy to write
👉 Industry standard

---

##  JSON handling in Python

Python me built-in module:

```python
import json
```

---

## ✍️ Writing dict/list to JSON file

```python
import json

students = [
    {"id": 1, "name": "Aman", "age": 21},
    {"id": 2, "name": "Riya", "age": 20}
]

with open("students.json", "w") as f:
    json.dump(students, f, indent=4)
```

💡 `indent=4` = readable format

---

## 📖 Reading JSON file

```python
import json

with open("students.json", "r") as f:
    data = json.load(f)

print(data)
print(type(data))  # list
```

---

## 🔁 Update JSON data

File never update directly , here is the flow👇

```text
Read → Modify → Write back
```

---

#  Student Record Manager (CLI)

###  File: `student_manager.py`

---

### Step 1️⃣: Load data safely

```python
import json

def load_students():
    try:
        with open("students.json", "r") as f:
            return json.load(f)
    except FileNotFoundError:
        return []
```

### Step 2️⃣: Save data

```python
def save_students(students):
    with open("students.json", "w") as f:
        json.dump(students, f, indent=4)
```

---

### Step 3️⃣: Add student

```python
def add_student():
    students = load_students()

    sid = int(input("Enter ID: "))
    name = input("Enter name: ")
    age = int(input("Enter age: "))

    student = {
        "id": sid,
        "name": name,
        "age": age
    }

    students.append(student)
    save_students(students)

    print("Student added successfully ✅")
```

---

### Step 4️⃣: View students

```python
def view_students():
    students = load_students()

    if not students:
        print("No records found")
        return

    for s in students:
        print(f"{s['id']} | {s['name']} | {s['age']}")
```

---

### Step 5️⃣: Menu loop

```python
while True:
    print("\n1. Add Student")
    print("2. View Students")
    print("3. Exit")

    choice = input("Choose: ")

    if choice == "1":
        add_student()
    elif choice == "2":
        view_students()
    elif choice == "3":
        break
    else:
        print("Invalid choice ❌")
```

# 2. Exception Handling

Exception = **runtime problem**

##  Common Exceptions 

| Situation             | Exception           |
| --------------------- | ------------------- |
| File missing          | `FileNotFoundError` |
| `"abc"` ko int banaya | `ValueError`        |
| 5 / 0                 | `ZeroDivisionError` |
| Dict key nahi         | `KeyError`          |

---

## ❌ Without Exception Handling (BAD)

```python
x = int(input("Enter number: "))
print(10 / x)
```

Input: `abc`
➡️ Program CRASH 💥

---

## ✅ With Exception Handling (PRO WAY)

```python
try:
    x = int(input("Enter number: "))
    print(10 / x)

except ValueError:
    print("Please enter a number")

except ZeroDivisionError:
    print("Cannot divide by zero")
```

## 🧠 try–except 

```text
try block run
↳ error?
   ↳ yes → except
   ↳ no  → skip except
```

---

##  else & finally

```python
try:
    x = int(input("Enter number: "))
    print(10 / x)

except Exception as e:
    print("Error:", e)

else:
    print("Calculation successful")

finally:
    print("Program ended")
```
-

##  Catching ALL exceptions (careful!)

```python
except Exception as e:
    print(e)
```

##  Custom Exception

```python
class AgeError(Exception):
    pass

age = int(input("Enter age: "))

if age < 18:
    raise AgeError("Age must be 18+")
```

---

##  PROJECT


### Code:

```python
def log_error(msg):
    with open("error.log", "a") as f:
        f.write(msg + "\n")

while True:
    try:
        a = int(input("Enter first number: "))
        b = int(input("Enter second number: "))

        print("Result:", a / b)
        break

    except ValueError:
        print("Enter only numbers")
        log_error("ValueError occurred")

    except ZeroDivisionError:
        print("Division by zero not allowed")
        log_error("ZeroDivisionError occurred")

    except Exception as e:
        print("Unknown error:", e)
        log_error(str(e))
```

# 3. Regex 
> Regex = **Tool for finding pattern in text**

```python
import re
```

---

## 1st function: `re.search()`

```python
import re

text = "I am learning python"
result = re.search("python", text)

print(result)
```


---

## ❓ Match vs Search (important)

| Function    | Meaning        |
| ----------- | -------------- |
| `match()`   | Check from start|
| `search()`  | wherever        |
| `findall()` | All matches     |

---

## 🔤 Character basics (foundation)

### 1️⃣ Normal text

```python
re.search("cat", "black cat")
```

---

### 2️⃣ Dot `.` (ANY one character)

```python
re.search("c.t", "cat")
re.search("c.t", "cut")
```

---

### 3️⃣ Star `*` (0 or more)

```python
re.search("ab*", "a")
re.search("ab*", "abbbb")
```

---

### 4️⃣ Plus `+` (1 or more)

```python
re.search("ab+", "a")      # ❌
re.search("ab+", "abbb")   # ✅
```

---

### 5️⃣ Question `?` (0 or 1)

```python
re.search("colou?r", "color")
re.search("colou?r", "colour")
```

---

##  Character sets `[]`

```python
re.search("[abc]", "dog")   # ❌
re.search("[abc]", "cat")   # ✅
```

Ranges:

```python
[0-9]   # digits
[a-z]   # lowercase
[A-Z]   # uppercase
```

---

##  Anchors (position matters)

| Symbol | Meaning |
| ------ | ------- |
| `^`    | start   |
| `$`    | end     |

```python
re.search("^hello", "hello world")
re.search("world$", "hello world")
```

---

## 🧠 Real Example: Phone number

```python
pattern = "^[0-9]{10}$"
```

Means:

* start
* exactly 10 digits
* end

---

## 🔁 `findall()` — MOST USED

```python
text = "Emails: a@gmail.com, b@yahoo.com"
emails = re.findall("[a-z]+@[a-z]+\\.com", text)
print(emails)
```

Output:

```python
['a@gmail.com', 'b@yahoo.com']
```

---

##  MINI PROJECT 

#  User Input Validator

---

### Features:

* Email check
* Phone number check
* Password rules

---

### Code:

```python
import re

def valid_email(email):
    return re.search("^[a-z0-9]+@[a-z]+\\.com$", email)

def valid_phone(phone):
    return re.search("^[0-9]{10}$", phone)

def valid_password(pwd):
    return re.search("^(?=.*[A-Z])(?=.*[0-9]).{8,}$", pwd)

email = input("Enter email: ")
phone = input("Enter phone: ")
password = input("Enter password: ")

if not valid_email(email):
    print("Invalid email")

elif not valid_phone(phone):
    print("Invalid phone")

elif not valid_password(password):
    print("Weak password")

else:
    print("All inputs valid ✅")
`
```

# 4. Functional Handling

##  Core tools 

1️⃣ `lambda`
2️⃣ `map()`
3️⃣ `filter()`
4️⃣ `reduce()`

---

# 🧩 1️⃣ Lambda (anonymous function)

Normal function:

```python
def add(a, b):
    return a + b
```

Lambda:

```python
add = lambda a, b: a + b
```

Rules:

* Single line
* No name (mostly)
* Short logic only

---

# 🗺️ 2️⃣ map() — transform data

Structure:

```python
map(function, iterable)
```

Example:

```python
nums = [1, 2, 3]
result = list(map(lambda x: x + 10, nums))
print(result)
```

---

# 🚿 3️⃣ filter() — clean data

Structure:

```python
filter(condition, iterable)
```

Example:

```python
nums = [1, 2, 3, 4, 5]
evens = list(filter(lambda x: x % 2 == 0, nums))
print(evens)
```

---

# 🧮 4️⃣ reduce() — combine data

```python
from functools import reduce

nums = [1, 2, 3, 4]
total = reduce(lambda a, b: a + b, nums)
print(total)
```

Think:

```text
((1 + 2) + 3) + 4
```

---

##  When to use what?

| Task             | Tool   |
| ---------------- | ------ |
| Change each item | map    |
| Remove items     | filter |
| Combine all      | reduce |

---

```python
prices = [100, 200, 300]

# Add 18% GST
final = list(map(lambda p: p * 1.18, prices))

# Only prices > 200
high = list(filter(lambda p: p > 200, final))

# Total bill
from functools import reduce
total = reduce(lambda a, b: a + b, high)
```

---


#  Student Marks Analyzer

---

### Data file (`marks.txt`):

```text
Aman 78
Riya 88
Neha 92
Raj 35
```

---

### Code:

```python
with open("marks.txt") as f:
    lines = f.readlines()

students = list(map(lambda l: (l.split()[0], int(l.split()[1])), lines))

passed = list(filter(lambda s: s[1] >= 40, students))

from functools import reduce
total = reduce(lambda a, b: a + b[1], passed, 0)

print("Passed students:", passed)
print("Total marks:", total)
```

# 5. Flask

```
Browser  → Request  → Server (Flask) → Response → Browser
```

Flask = **Tool for server formation**

---

### 1️⃣ Install Flask

```bash
pip install flask
```

---

### 2️⃣ Minimal Flask App

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    return "Hello Flask"

app.run(debug=True)
```

---

##  Line-by-line samjho

```python
from flask import Flask
```

➡️ Flask class import 

---

```python
app = Flask(__name__)
```

➡️ Server create 
➡️ `__name__` tells Flask **this is main app**

---

```python
@app.route("/")
```

➡️ URL's address
➡️ `/` = homepage

---

```python
def home():
    return "Hello Flask"
```

➡️ Function = response
➡️ Browser gets the string

---

```python
app.run(debug=True)
```

➡️ Server start
➡️ Debug = auto reload + error screen

---

## 🌐 What happens in browser?

User types:

```
http://127.0.0.1:5000/
```

Behind scenes:

```
Browser → GET / → Flask → home() → "Hello Flask"
```

---

#  Part 2: Routes deeply

### Multiple routes

```python
@app.route("/about")
def about():
    return "About Page"
```

URLs:

* `/` → home
* `/about` → about page

---

## 🔁 Dynamic routes (POWERFUL)

```python
@app.route("/user/<name>")
def user(name):
    return f"Hello {name}"
```

Browser:

```
/user/soni
/user/rahul
```


##  Type safety in route

```python
@app.route("/post/<int:id>")
def post(id):
    return f"Post number {id}"
```

❌ `/post/abc`
✅ `/post/10`

---

# 📩 Part 3: HTTP Methods (GET vs POST)

### Default = GET

```python
@app.route("/login")
def login():
    return "Login Page"
```

---

### GET + POST

```python
from flask import request

@app.route("/login", methods=["GET", "POST"])
def login():
    if request.method == "POST":
        return "Form Submitted"
    return "Login Page"
```

---

##  request ?

```python
request.form     # form data
request.args     # query params
request.method   # GET / POST
```
 
#  HTML Templates (Frontend connect)

---

### Folder structure (RULE)

```
project/
 ├── app.py
 └── templates/
     └── index.html
```

---

### HTML file (`templates/index.html`)

```html
<h1>Hello {{ name }}</h1>
```

---

### Flask render

```python
from flask import render_template

@app.route("/")
def home():
    return render_template("index.html", name="Soni")
```

➡️ Python → HTML sending data

---

##  Jinja2 (Template Engine)

`{{ }}` → data
`{% %}` → logic

Example:

```html
{% for s in students %}
  <p>{{ s }}</p>
{% endfor %}
```

---

# Forms 

### HTML form

```html
<form method="POST">
  <input name="username">
  <button>Submit</button>
</form>
```

---

### Flask handling

```python
@app.route("/form", methods=["GET", "POST"])
def form():
    if request.method == "POST":
        name = request.form["username"]
        return f"Hello {name}"
    return render_template("form.html")
```

---

## FLOW 

```
User fills form
→ POST request
→ Flask receives data
→ process
→ response
```
