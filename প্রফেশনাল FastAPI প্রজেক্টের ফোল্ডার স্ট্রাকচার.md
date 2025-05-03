**একটি প্রফেশনাল FastAPI প্রজেক্টের ফোল্ডার স্ট্রাকচার** দেখাবো — যেটি production-grade অ্যাপের জন্যও কাজ করে। প্রতিটি ফোল্ডারের কাজ, কেন দরকার, কখন ব্যবহার করবেন, কী রাখবেন—সেটাও বাংলায় ব্যাখ্যা করলাম।

---

# 🗂️ Best Folder Structure for FastAPI Project

```
fastapi_project/
│
├── app/
│   ├── main.py                🔹 এপ এন্ট্রি পয়েন্ট
│   ├── core/                  🔹 config, settings, security
│   ├── models/                🔹 SQLAlchemy ORM টেবিল
│   ├── schemas/               🔹 Pydantic models (in/out)
│   ├── crud/                  🔹 DB query ফাংশন (CRUD logic)
│   ├── api/                   🔹 রাউটস (Routes)
│   │   ├── v1/                🔹 ভার্সন ম্যানেজমেন্ট
│   │   │   ├── user.py        🔹 একেক resource-এর route
│   ├── db/                    🔹 ডেটাবেজ সেশনের সেটআপ
│   ├── services/              🔹 বিজনেস লজিক
│   ├── dependencies/          🔹 reusable Depends() ফাংশন
│   └── utils/                 🔹 হেল্পার ফাংশন, JWT, ইত্যাদি
│
├── tests/                     🔹 Pytest টেস্ট ফাইল
├── .env                       🔹 গোপন config (DB_URL, SECRET)
├── requirements.txt           🔹 লাইব্রেরি
└── README.md                  🔹 প্রজেক্ট ব্যাখ্যা
```

---

## 🔍 Folder by Folder ব্যাখ্যা

---

### 📁 `main.py`

* 📌 FastAPI অ্যাপ রান করার এন্ট্রি ফাইল
* `app = FastAPI()` থাকে
* Routers include করা হয়

```python
from fastapi import FastAPI
from app.api.v1 import user

app = FastAPI()
app.include_router(user.router)
```

---

### 📁 `core/`

**কেন?**
Configuration, settings, security centralize রাখতে

**কী থাকে?**

* `config.py` ➤ environment variable loader (pydantic settings)
* `security.py` ➤ password hashing, JWT token, OAuth2 config

```python
# config.py
from pydantic import BaseSettings

class Settings(BaseSettings):
    DATABASE_URL: str
    SECRET_KEY: str

settings = Settings()
```

---

### 📁 `models/`

**কেন?**
SQLAlchemy ORM মডেল (Table structure) এখানে রাখলে সব একসাথে থাকে

**কী থাকে?**

* `user.py`, `product.py` ➤ টেবিল অনুযায়ী আলাদা ফাইল
* `Base` inherit করা ক্লাস

---

### 📁 `schemas/`

**কেন?**
Pydantic দিয়ে ইনপুট-আউটপুট ভ্যালিডেশন ও ফরম্যাটিং আলাদা রাখা যায়

**কী থাকে?**

* `user.py` ➤ `UserCreate`, `UserRead`, `UserUpdate`
* `product.py` ➤ `ProductCreate`, etc.

```python
class UserCreate(BaseModel):
    username: str
    email: str
```

---

### 📁 `crud/`

**কেন?**
ডেটাবেজের সাথে CRUD (Create Read Update Delete) ফাংশন এখানেই থাকবে

**কী থাকে?**

* `get_user_by_id()`
* `create_user()`

```python
def create_user(db: Session, user: UserCreate):
    db_user = User(**user.dict())
    db.add(db_user)
    db.commit()
    return db_user
```

---

### 📁 `api/v1/`

**কেন?**
Routes কে version অনুযায়ী আলাদা রাখলে later upgrade/simple deployment সম্ভব

**কী থাকে?**

* `user.py`, `product.py` ➤ আলাদা রাউট ফাইল
* `router = APIRouter()` দিয়ে route define

---

### 📁 `db/`

**কেন?**
Database config, session maker ইত্যাদি centralize করা যায়

**কী থাকে?**

* `session.py` ➤ `SessionLocal`, engine
* `init_db.py` ➤ table create, seed data

---

### 📁 `services/`

**কেন?**
যখন বিজনেস লজিক CRUD এর বাইরে যায় (e.g., email sending, pricing logic)

**কী থাকে?**

* `auth_service.py`, `payment_service.py`, ইত্যাদি

---

### 📁 `dependencies/`

**কেন?**
Reusable dependency injection functions এখানেই রাখা হয়

**কী থাকে?**

* `get_current_user()`
* `get_db()`

---

### 📁 `utils/`

**কেন?**
যেসব জেনারেল ফাংশন প্রকল্পে বারবার লাগে (e.g., JWT encode, random ID)

**কী থাকে?**

* `token.py`, `helpers.py`, `logger.py`

---

### 📁 `tests/`

**কেন?**
Unit, integration test রাখতে

**কী থাকে?**

* `test_user.py`, `test_auth.py`

---

## 🗂️ কবে কোন ফোল্ডার লাগবে?

| প্রয়োগ           | প্রয়োজনীয় ফোল্ডার                     |
| ---------------- | ------------------------------------- |
| Simple API       | `main.py`, `api/`, `schemas/`         |
| DB কাজ           | `models/`, `db/`, `crud/`             |
| Security         | `core/security.py`, `utils/token.py`  |
| Production-level | সব ফোল্ডার structure ব্যবহার করা উচিত |
| Test automation  | `tests/`                              |

---

## ✅ উপসংহার

এই স্ট্রাকচার:

* Clean architecture বজায় রাখে
* Maintain করা সহজ
* বড় অ্যাপে scale করা সহজ
* Team collaboration সহজ করে


