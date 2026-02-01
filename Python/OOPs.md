# OOPs

# 1.
> **Object = real world entity** 
> **Class = blueprint** 

| Real World      | Programming |
| --------------- | ----------- |
| Car ka design   | `class Car` |
| Red BMW car     | `object`    |
| Blue Audi car   | `object`    |
| White Swift car | `object`    |

**Model / name / color**
is **object'sdata (attributes)**

##  Programming Angle 

> **Class = structure + behavior**
> **Object = real usable thing in memory**

* **Object = data + methods (together)** 

# 2.

#  PHASE 1 – CLASS & OBJECT 

## Step 1️⃣: Class ( structure)

```python
class Student:
    pass
```

### Explain :

* `class` 
* `Student` 
* `pass` 

---

## Step 2️⃣: Object (REAL student)

```python
rahul = Student()
rohan = Student()
```

### Important truth:

* `Student()` → object creation
* `rahul` / `rohan` → only names (reference)

📌 **In RAM different students were made**
Even though same they belong to same class.

---

## Step 3️⃣: Object'sdata  (Attributes)

* name
* roll number
* marks

### (manual way):

```python
rahul.name = "Rahul"
rahul.roll = 1
rahul.marks = 85

rohan.name = "Rohan"
rohan.roll = 2
rohan.marks = 78
```

##  PROBLEM

Ab imagine:

* 100 students
* repetitive writings of code 

👉 **Use `__init__` **

---

# Step 4️⃣: `__init__` 

### Simple definition:

> `__init__` = function taht runs on birth of object

### Code:

```python
class Student:
    def __init__(self, name, roll, marks):
        self.name = name
        self.roll = roll
        self.marks = marks
```
when u write 

```python
rahul = Student("Rahul", 1, 85)
```

Python internally does:

```python
Student.__init__(rahul, "Rahul", 1, 85)
```

👉 `self` **refer object rahul**

---

## Step 5️⃣: Clean Object Creation

```python
rahul = Student("Rahul", 1, 85)
rohan = Student("Rohan", 2, 78)
monu  = Student("Monu", 3, 92)
```

# 3.

#  METHODS

## PHASE 1 – STEP 6️⃣: METHOD ?

##  Method Example 

```python
class Student:
    def __init__(self, name, roll, marks):
        self.name = name
        self.roll = roll
        self.marks = marks

    def show_details(self):
        print("Name:", self.name)
        print("Roll:", self.roll)
        print("Marks:", self.marks)

    def is_pass(self):
        if self.marks >= 40:
            return True
        else:
            return False
```

👉 **Methods = object's behaviors**


## ⚠️ MOST COMMON MISTAKE (don’t do this)

```python
def is_pass(marks):   # ❌ wrong
```

 **self compulsory**

---


###  Task:

**Student Result System**

Add a method:

```python
def grade(self):
    if self.marks >= 90:
        return "A"
    elif self.marks >= 75:
        return "B"
    elif self.marks >= 50:
        return "C"
    else:
        return "Fail"
```
Function requires procedural thinking while methods depends on data's behaviour 
---
 # 4.

##  Instance Variable vs Class Variable

## 1️⃣ Instance Variable (PERSONAL)

* Each object's **different**
* `self.variable`

Example:

* name
* roll
* marks

---

## 2️⃣ Class Variable (SHARED)

* For all objects- **same**
* Define under class

Example:

* school name
* bank name
* company name

---

## 🧪 Code

```python
class Student:
    school_name = "DPS"   # ✅ class variable (shared)

    def __init__(self, name, roll, marks):
        self.name = name      # instance variable
        self.roll = roll
        self.marks = marks
```

```python
rahul = Student("Rahul", 1, 85)
rohan = Student("Rohan", 2, 78)
```

In Memory :

* `rahul.name` → Rahul
* `rohan.name` → Rohan
* `rahul.school_name` → DPS
* `rohan.school_name` → DPS

---

## ⚠️ MOST COMMON MISTAKE (VERY DANGEROUS)

```python
self.school_name = "DPS"   # ❌ (duplicate data)
```

Make copy in each object

---

## 🏦 MINI PROJECT (STARTING NOW)

### Bank Account System

Think:

* Bank name → same for all accounts
* Account holder → different

```python
class BankAccount:
    bank_name = "State Bank"

    def __init__(self, name, balance):
        self.name = name
        self.balance = balance
```

# 5.

Methods type :

#  PHASE 3 – METHODS 

## 1️⃣ Instance Method 

```python
def deposit(self, amount):
    self.balance += amount
```

* `self` 
* Change object data
* Call: `acc.deposit(500)`

---

## 2️⃣ Class Method

### Syntax:

```python
@classmethod
def change_bank_name(cls, new_name):
    cls.bank_name = new_name
```

### Full Example:

```python
class BankAccount:
    bank_name = "State Bank"

    def __init__(self, name, balance):
        self.name = name
        self.balance = balance

    @classmethod
    def change_bank_name(cls, new_name):
        cls.bank_name = new_name
```

---

##  Important clarity:

* `cls` → **refer to class**
* `cls.bank_name` → change class variable

### Call:

```python
BankAccount.change_bank_name("HDFC")
```

---

## ⚠️ VERY COMMON MISTAKE

```python
def change_bank_name(self, name):   # ❌ wrong
    self.bank_name = name
```

* This will become the instance method
* This will change only 1 bank's name

---

## 3️⃣ Static Method 

```python
@staticmethod
def is_valid_amount(amount):
    return amount > 0
```

Call:

```python
BankAccount.is_valid_amount(500)
```

---

##  Comparison Table

| Method Type | Uses          | Parameter |
| ----------- | ------------- | --------- |
| Instance    | Object data   | `self`    |
| Classmethod | Class data    | `cls`     |
| Static      | Utility logic | none      |

---

# 6.Encapsulation

```python
acc.balance = 1000000   # ❌ dangerous
```

* No validation
* No rules
* No control

---

##  Solution: Stop data from direct access

3 levels

---

## 1️⃣ Public (default)

```python
self.name
```

* Access to everyone
* Risky for sensitive data

---

## 2️⃣ Protected ( _single underscore )

```python
self._balance
```

 Meaning:

> “Don't use from outside”
> (Developer discipline)

---

## 3️⃣ Private ( __double underscore )

```python
self.__balance
```

* Python name-mangling 
* No direct access from outside

---

##  Code (slow + clear)

```python
class Wallet:
    def __init__(self, owner, balance):
        self.owner = owner
        self.__balance = balance   # 🔒 private

    def show_balance(self):
        return self.__balance

    def add_money(self, amount):
        if amount > 0:
            self.__balance += amount
        else:
            print("Invalid amount")
```

---

## Python change internally:

```python
self.__balance  →  _Wallet__balance
```

that's why:)

```python
wallet.__balance   # ❌ error
```

---

##  Getter & Setter (controlled access)

```python
def get_balance(self):
    return self.__balance

def set_balance(self, amount):
    if amount >= 0:
        self.__balance = amount
```

---

 #7. Inheritance

* **User = parent class** → common features (name, email, login)
* **Admin = child class** → extra powers (view all users, modify data)
* **Customer = child class** → limited powers (own profile, purchase)
* Shared behavior → parent class me define
* Extra behavior → child class me define

---

## 🔥 Python Code Example 

```python
class User:
    def __init__(self, name, email):
        self.name = name
        self.email = email

    def login(self):
        print(f"{self.name} logged in")

class Admin(User):   # Parent = User
    def view_all_users(self):
        print(f"{self.name} can view all users")

class Customer(User):
    def purchase(self, item):
        print(f"{self.name} purchased {item}")
```

---

## Objects

```python
admin1 = Admin("Ritika", "ritika@dev.com")
customer1 = Customer("Rahul", "rahul@gmail.com")

admin1.login()         # inherited method from User
admin1.view_all_users() # Admin method

customer1.login()       # inherited
customer1.purchase("Laptop") # Customer method
```

---

##  Key Points 

1. **`super()` ka use** → parent ka init/behavior call karne ke liye
2. **Method Overriding** → child method same name use karke parent ka behavior change kar sakta hai
3. **Inheritance hierarchy** → multiple level possible (multi-level inheritance)
4. **Code reuse** → common code parent me, extra code child me

---

# 8. Polymorphism and Abstraction

#  Phase 6 – POLYMORPHISM & ABSTRACTION

## 1️⃣ Polymorphism

> Same action, different behavior depending on object type

### Example in project:

```python
class User:
    def show_profile(self):
        print(f"User: {self.name} ({self.email})")

class Admin(User):
    def show_profile(self):
        print(f"Admin: {self.name} ({self.email}), manages {len(self.products_managed)} products")

class Customer(User):
    def show_profile(self):
        print(f"Customer: {self.name} ({self.email}), balance private")
```

Test:

```python
users = [admin, c1, c2]
for u in users:
    u.show_profile()  # same method, different behavior
```

## 2️⃣ Abstraction

> Hide implementation details, show only necessary actions

### Example in project:

* Customer **does not know how purchase() calculates balance** internally
* Admin **does not see Customer's cart**
* Only exposed methods:

```python
c1.add_to_cart(p1)
c1.purchase()
```

* We are just calling method, internal logic hidden
* That's what abstraction  🔒

---

### Updated Example with class + static methods

```python
class Product:
    total_products = 0   # class variable

    def __init__(self, name, price, stock):
        self.name = name
        self.price = price
        self.stock = stock
        Product.total_products += 1

    @staticmethod
    def is_valid_price(price):
        return price > 0
```

* `total_products` → class variable
* `is_valid_price` → static method for logic check

---

#9. Mini project:

Let’s start **E‑Commerce Mini-Project** - OOPS-based. 💪

topics:

* **Inheritance** (User → Admin & Customer)
* **Encapsulation** (private data like balance, orders)
* **Methods** (instance, class, static)
* **Polymorphism & Overriding** (optional for advanced practice)

---

#  Step 0 – Plan (Before coding)

**Classes we need:**

1. **User (Parent)**

   * Attributes: `name`, `email`
   * Methods: `login()`, `logout()`

2. **Admin (Child of User)**

   * Extra Methods:

     * `view_all_customers()`
     * `add_product()`

3. **Customer (Child of User)**

   * Extra Attributes: `__cart` (private), `__balance` (private)
   * Methods:

     * `add_to_cart(product)`
     * `purchase()`
     * `view_cart()`

4. **Product** (Separate class)

   * Attributes: `name`, `price`, `stock`
   * Methods: maybe `update_stock()`

---

#  Step 1 – Base Classes

```python
# Base User class
class User:
    def __init__(self, name, email):
        self.name = name
        self.email = email

    def login(self):
        print(f"{self.name} logged in.")

    def logout(self):
        print(f"{self.name} logged out.")
```

---

#  Step 2 – Admin Class

```python
class Admin(User):  # Inheritance
    def __init__(self, name, email):
        super().__init__(name, email)  # call parent init
        self.products_managed = []

    def add_product(self, product):
        self.products_managed.append(product)
        print(f"{self.name} added product {product.name}.")

    def view_all_customers(self, customers):
        print(f"{self.name} is viewing all customers:")
        for customer in customers:
            print(f"- {customer.name} ({customer.email})")
```

---

#  Step 3 – Customer Class

```python
class Customer(User):
    def __init__(self, name, email, balance):
        super().__init__(name, email)
        self.__balance = balance  # private
        self.__cart = []          # private

    def add_to_cart(self, product):
        self.__cart.append(product)
        print(f"{self.name} added {product.name} to cart.")

    def view_cart(self):
        print(f"{self.name}'s cart:")
        for p in self.__cart:
            print(f"- {p.name} : ${p.price}")

    def purchase(self):
        total = sum([p.price for p in self.__cart])
        if total > self.__balance:
            print(f"Not enough balance! Total: ${total}, Balance: ${self.__balance}")
        else:
            self.__balance -= total
            print(f"{self.name} purchased items for ${total}. Remaining balance: ${self.__balance}")
            self.__cart = []
```

---

#  Step 4 – Product Class

```python
class Product:
    def __init__(self, name, price, stock):
        self.name = name
        self.price = price
        self.stock = stock
```

---

#  Step 5 – Test Everything

```python
# Products
p1 = Product("Laptop", 1200, 5)
p2 = Product("Mouse", 25, 50)

# Admin
admin = Admin("Ritika", "admin@shop.com")
admin.add_product(p1)
admin.add_product(p2)

# Customers
c1 = Customer("Rahul", "rahul@gmail.com", 1500)
c2 = Customer("Monu", "monu@gmail.com", 100)

customers = [c1, c2]
admin.view_all_customers(customers)

# Shopping
c1.add_to_cart(p1)
c1.add_to_cart(p2)
c1.view_cart()
c1.purchase()
```

---

# 10 : Multi - file 

```
ecommerce_project/
│
├── product.py      # Product class
├── user.py         # User, Admin, Customer classes
└── main.py         # Run / testing code
```

* Run terminal me **main.py**:

```bash
python main.py
```

# **Step 1 – product.py**

```python
# product.py
class Product:
    total_products = 0

    def __init__(self, name, price, stock):
        if not self.is_valid_price(price):
            raise ValueError("Price must be positive")
        self.name = name
        self.price = price
        self.stock = stock
        Product.total_products += 1

    @staticmethod
    def is_valid_price(price):
        return price > 0

    def update_stock(self, quantity):
        self.stock += quantity
```

✅ **Class variable, static & instance methods covered**

---

# **Step 2 – user.py**

```python
# user.py
from product import Product  # import Product class

class User:
    def __init__(self, name, email):
        self.name = name
        self.email = email

    def login(self):
        print(f"{self.name} logged in")

    def logout(self):
        print(f"{self.name} logged out")

    def show_profile(self):
        print(f"User: {self.name} ({self.email})")


class Admin(User):
    def __init__(self, name, email):
        super().__init__(name, email)
        self.products_managed = []

    def add_product(self, product):
        self.products_managed.append(product)
        print(f"{self.name} added product: {product.name}")

    def view_all_customers(self, customers):
        print(f"{self.name} is viewing all customers:")
        for customer in customers:
            print(f"- {customer.name} ({customer.email})")

    def show_profile(self):
        print(f"Admin: {self.name} ({self.email}) | Products managed: {len(self.products_managed)}")


class Customer(User):
    def __init__(self, name, email, balance):
        super().__init__(name, email)
        self.__balance = balance
        self.__cart = []

    def add_to_cart(self, product):
        if product.stock <= 0:
            print(f"{product.name} is out of stock!")
            return
        self.__cart.append(product)
        print(f"{self.name} added {product.name} to cart")

    def view_cart(self):
        print(f"{self.name}'s cart:")
        for p in self.__cart:
            print(f"- {p.name} : ${p.price}")

    def purchase(self):
        total = sum([p.price for p in self.__cart])
        if total > self.__balance:
            print(f"Not enough balance! Total: ${total}, Balance: ${self.__balance}")
        else:
            self.__balance -= total
            print(f"{self.name} purchased items for ${total}. Remaining balance: ${self.__balance}")
            self.__cart = []

    def get_balance(self):
        return self.__balance

    def show_profile(self):
        print(f"Customer: {self.name} ({self.email}) | Balance: ${self.__balance}")
```

✅ Covers: **Inheritance, encapsulation, polymorphism, abstraction**

---

# **Step 3 – main.py**

```python
# main.py
from product import Product
from user import Admin, Customer

# Products
p1 = Product("Laptop", 1200, 5)
p2 = Product("Mouse", 25, 50)

# Admin
admin = Admin("Ritika", "admin@shop.com")
admin.add_product(p1)
admin.add_product(p2)

# Customers
c1 = Customer("Rahul", "rahul@gmail.com", 1500)
c2 = Customer("Monu", "monu@gmail.com", 100)
customers = [c1, c2]

admin.view_all_customers(customers)

# Shopping
c1.add_to_cart(p1)
c1.add_to_cart(p2)
c1.view_cart()
c1.purchase()
c1.show_profile()  # polymorphism

c2.add_to_cart(p2)
c2.purchase()
c2.show_profile()  # polymorphism

# Admin profile
admin.show_profile()

# Check total products
print(f"Total products in system: {Product.total_products}")
```

---

# **Step 4 – How to Run (Python)**

1. Open terminal
2. Navigate to project folder (`ecommerce_project`)
3. Run:

```bash
python main.py
```

* Output will show:

  * Admin adding products
  * Customers adding to cart, purchasing
  * Profiles (polymorphism)
  * Total products (class variable)

---

