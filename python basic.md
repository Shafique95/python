
## ✅ Python Basic Cheat Sheet 

````md
# 🐍 Python Basic Cheat Sheet (বাংলা ব্যাখ্যা সহ)

---

## ✨ ভ্যারিয়েবল (Variable)

```python
name = "Shafiqul"
age = 25
pi = 3.1416
is_active = True
````

🔹 ভ্যারিয়েবল = তথ্য সংরক্ষণ করার জায়গা।

---

## 🔢 ডেটা টাইপ

```python
# স্ট্রিং
text = "Hello"

# পূর্ণসংখ্যা (Integer)
count = 10

# দশমিক সংখ্যা (Float)
price = 99.99

# লজিক্যাল মান (Boolean)
is_valid = True
```

---

## 🧰 ডেটা স্ট্রাকচার

### ✅ List (তালিকা)

```python
fruits = ["apple", "banana", "mango"]
print(fruits[1])  # banana
```

### ✅ Tuple (অপরিবর্তনযোগ্য তালিকা)

```python
colors = ("red", "green", "blue")
```

### ✅ Dictionary (কী-ভ্যালু জোড়া)

```python
person = {"name": "Shafiq", "age": 24}
print(person["name"])
```

### ✅ Set (ইউনিক ভ্যালু)

```python
unique_numbers = {1, 2, 3, 3}
```

---

## 🔁 লুপ

### ✅ for loop

```python
for fruit in fruits:
    print(fruit)
```

### ✅ while loop

```python
i = 0
while i < 5:
    print(i)
    i += 1
```

---

## 🔀 কন্ডিশন (if, elif, else)

```python
age = 18

if age >= 18:
    print("Adult")
elif age >= 13:
    print("Teenager")
else:
    print("Child")
```

---

## 🧩 ফাংশন

```python
def greet(name):
    return f"Hello, {name}"

print(greet("Shafiqul"))
```

---

## 🧱 ক্লাস ও অবজেক্ট

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def greet(self):
        return f"Hi, I'm {self.name}"

p1 = Person("Shafiq", 30)
print(p1.greet())
```

---

## ⚙️ Exception Handling

```python
try:
    x = 10 / 0
except ZeroDivisionError:
    print("ভাগ করার সময় শূন্য হতে পারে না")
finally:
    print("শেষ হয়েছে")
```

---

## 🔄 List Comprehension

```python
squares = [x*x for x in range(1, 6)]
```

---

## 📦 Import ও Module

```python
import math
print(math.sqrt(16))
```

---

## 🕐 Date & Time

```python
from datetime import datetime
now = datetime.now()
print(now.strftime("%Y-%m-%d %H:%M:%S"))
```

---

## 📄 File Handling

```python
with open("file.txt", "r") as f:
    content = f.read()
```

---

## 🧪 পাইথনে কোড রান করার কমান্ড

```bash
python filename.py
```

---

## 🔍 Input ও Output

```python
name = input("তোমার নাম লিখো: ")
print("স্বাগতম", name)
```

---

## 🚀 কিছু গুরুত্বপূর্ণ বিল্ট-ইন ফাংশন

| ফাংশন              | কাজ            |
| ------------------ | -------------- |
| `len()`            | দৈর্ঘ্য        |
| `type()`           | টাইপ দেখায়     |
| `range()`          | রেঞ্জ তৈরি করে |
| `int()`, `float()` | টাইপ কনভার্ট   |
| `str()`            | স্ট্রিং বানায়  |
| `input()`          | ইনপুট নেয়      |

---

## 🧠 পরামর্শ

✅ কোড অনেক লিখুন
✅ `print()` ব্যবহার করে বুঝে নিন
✅ ভুল হতে দিন, সেখান থেকেই শেখা হয়!

---


