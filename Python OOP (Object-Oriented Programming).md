চলুন আমরা Python OOP (Object-Oriented Programming)-এর একটি **পূর্ণাঙ্গ শেখার সফর (learning tour)** শুরু করি — বাংলায় ধাপে ধাপে, উদাহরণসহ এবং বাস্তব জীবনের উদাহরণ দিয়ে।

---

# 🧠 Python OOP Full Learning Tour (বাংলায়)

---

## 🔰 Step 1: OOP কী এবং কেন?

### 📌 সংজ্ঞা:

**Object-Oriented Programming (OOP)** হলো এমন একটি পদ্ধতি যেখানে বাস্তব জীবনের জিনিসগুলোকে অবজেক্ট হিসেবে চিন্তা করে প্রোগ্রাম লেখা হয়।

### ✅ কেন ব্যবহার করবো?

* বড় প্রজেক্টে কোড অর্গানাইজড রাখতে
* পুনঃব্যবহারযোগ্যতা (Reusability)
* maintain করা সহজ
* বাস্তব জগতের মডেল করা যায়

### 🎯 বাস্তব উদাহরণ:

“গাড়ি” = একটি ক্লাস → `Car`
"Toyota Prius, Red, 2020" = একটি অবজেক্ট → `my_car`

---

## 🧱 Step 2: Class এবং Object

```python
class Car:
    def __init__(self, brand, year):
        self.brand = brand
        self.year = year

    def show_info(self):
        print(f"{self.brand} - {self.year}")

# অবজেক্ট তৈরি
my_car = Car("Toyota", 2020)
my_car.show_info()
```

🧾 **বোঝার বিষয়:**

* `class` = নীল নকশা (blueprint)
* `__init__` = constructor (অবজেক্ট তৈরি হলে চলে)
* `self` = বর্তমান অবজেক্ট বোঝায়

---

## 🧱 Step 3: Attribute এবং Method

* **Attribute** = data (e.g. name, age)
* **Method** = action/function (e.g. run, stop)

```python
class Person:
    def __init__(self, name):
        self.name = name

    def greet(self):
        print("Hello", self.name)
```

---

## 🔄 Step 4: Encapsulation (ডেটা লুকানো)

```python
class BankAccount:
    def __init__(self):
        self.__balance = 0  # private attribute

    def deposit(self, amount):
        self.__balance += amount

    def show_balance(self):
        print("Balance:", self.__balance)
```

🔐 **\_\_ (double underscore)** দিয়ে ডেটা private রাখা যায়।

---

## 🧬 Step 5: Inheritance (উত্তরাধিকার)

```python
class Animal:
    def speak(self):
        print("Animal sound")

class Dog(Animal):
    def speak(self):
        print("Woof!")

d = Dog()
d.speak()
```

📌 **কেন দরকার?**
প্যারেন্ট ক্লাস থেকে চাইল্ড ক্লাস ফিচার নেয় = কোড রিপিট কম হয়।

---

## 🧪 Step 6: Polymorphism (একাধিক রূপ)

```python
class Bird:
    def sound(self):
        print("Tweet")

class Cat:
    def sound(self):
        print("Meow")

def make_sound(animal):
    animal.sound()

make_sound(Bird())
make_sound(Cat())
```

📌 **একই ফাংশন নাম, কিন্তু আলাদা আচরণ।**

---

## 🧰 Step 7: Abstraction (প্রয়োজনীয় জিনিস দেখা, বাকিটা লুকানো)

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

class Circle(Shape):
    def area(self):
        return 3.14 * 5 * 5
```

📌 `abstractmethod` ব্যবহার করলে Child Class বাধ্য হবে override করতে।

---

## 📦 Step 8: Class Variable vs Instance Variable

```python
class Student:
    college = "RUET"  # class variable

    def __init__(self, name):
        self.name = name  # instance variable
```

---

## 💥 Step 9: Special Methods (`__str__`, `__len__`, `__add__`)

```python
class Book:
    def __init__(self, title):
        self.title = title

    def __str__(self):
        return f"Book: {self.title}"

b = Book("Python")
print(b)  # ➡️ Book: Python
```

---

## 🔁 Step 10: Composition (এক ক্লাসে আরেক ক্লাস ব্যবহার)

```python
class Engine:
    def start(self):
        print("Engine started")

class Car:
    def __init__(self):
        self.engine = Engine()

    def start(self):
        self.engine.start()
```

---

## 🎓 Final Step: Practice Ideas

1. **Library System** ➝ Book, User, Borrow logic
2. **Bank System** ➝ Account, Transaction
3. **E-commerce** ➝ Product, Cart, Order
4. **University** ➝ Student, Course, Instructor

