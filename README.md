# python
অবশ্যই! নিচে আমি আপনাকে বাংলায় **FastAPI Cheat Sheet** দিচ্ছি — এতে FastAPI-এর প্রায় সব গুরুত্বপূর্ণ বিষয় **সংক্ষিপ্তভাবে, সহজ ভাষায়, ও উদাহরণসহ** দেওয়া হয়েছে। যারা নতুন শিখছেন বা মাঝপথে মনে করিয়ে নিতে চান — তাদের জন্য এটি অনেক উপকারী হবে।

---

# 🐍 FastAPI Cheat Sheet (বাংলায় সহজভাবে)

---

## 📦 ইনস্টলেশন

```bash
pip install fastapi
pip install "uvicorn[standard]"  # Run করার জন্য
```

---

## 🚀 FastAPI অ্যাপ চালানো

```bash
uvicorn main:app --reload
```

* `main`: ফাইলের নাম
* `app`: FastAPI অ্যাপ অবজেক্টের নাম
* `--reload`: কোড পরিবর্তন হলে অটো রিফ্রেশ

---

## 🏁 বেসিক অ্যাপ

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"message": "হ্যালো বাংলাদেশ"}
```

---

## 🎯 রাউট (Route) টাইপ

```python
@app.get("/item")      # GET: ডেটা পড়া
@app.post("/item")     # POST: নতুন ডেটা তৈরি
@app.put("/item/{id}") # PUT: ডেটা আপডেট
@app.delete("/item/{id}") # DELETE: ডেটা মুছে ফেলা
```

---

## 📥 রিকোয়েস্ট প্যারামিটার

### ✅ **Query Parameters**

```python
@app.get("/search")
def search_items(q: str = ""):
    return {"query": q}
```

➡️ `/search?q=apple`

---

### ✅ **Path Parameters**

```python
@app.get("/items/{item_id}")
def get_item(item_id: int):
    return {"item_id": item_id}
```

➡️ `/items/5`

---

### ✅ **Request Body (Pydantic ব্যবহার)**

```python
from pydantic import BaseModel

class Item(BaseModel):
    name: str
    price: float

@app.post("/items/")
def create_item(item: Item):
    return item
```

➡️ JSON Body:

```json
{
  "name": "চাল",
  "price": 50.5
}
```

---

## 🔁 Response Model

```python
class ItemOut(BaseModel):
    name: str
    price: float

@app.get("/item", response_model=ItemOut)
def get_item():
    return {"name": "চিনি", "price": 80}
```

---

## 🧱 Dependency Injection (যেমন ডাটাবেজ কানেকশন)

```python
from fastapi import Depends

def get_db():
    db = "Fake DB"
    return db

@app.get("/data")
def read_data(db=Depends(get_db)):
    return {"db": db}
```

---

## 🛡️ Form Data, File Upload

### ✅ Form

```python
from fastapi import Form

@app.post("/login")
def login(username: str = Form(...), password: str = Form(...)):
    return {"user": username}
```

### ✅ File Upload

```python
from fastapi import File, UploadFile

@app.post("/upload")
def upload(file: UploadFile = File(...)):
    return {"filename": file.filename}
```

---

## 🧪 Validate Data with Pydantic

```python
class Product(BaseModel):
    name: str
    price: float
    quantity: int

    @validator("price")
    def check_price(cls, value):
        if value <= 0:
            raise ValueError("দাম ০ এর নিচে হতে পারে না")
        return value
```

---

## 🧾 Custom Response (JSON, HTML)

```python
from fastapi.responses import HTMLResponse, JSONResponse

@app.get("/html", response_class=HTMLResponse)
def html():
    return "<h1>হ্যালো</h1>"

@app.get("/json")
def json():
    return JSONResponse(content={"message": "OK"})
```

---

## 🔐 Security (OAuth2, Token)

```python
from fastapi.security import OAuth2PasswordBearer

oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")

@app.get("/users/me")
def read_users_me(token: str = Depends(oauth2_scheme)):
    return {"token": token}
```

---

## 🔧 Exception Handling

```python
from fastapi import HTTPException

@app.get("/error")
def cause_error():
    raise HTTPException(status_code=404, detail="তথ্য পাওয়া যায়নি")
```

---

## 📁 Static Files & Templates

```python
from fastapi.staticfiles import StaticFiles

app.mount("/static", StaticFiles(directory="static"), name="static")
```

---

## 🧪 Test with curl or HTTPie

```bash
http POST http://127.0.0.1:8000/items/ name="ডাল" price=65
```

---

## 📘 Documentation

* Swagger UI ➡️ `http://localhost:8000/docs`
* ReDoc ➡️ `http://localhost:8000/redoc`

---

## 🎓 সংক্ষেপে টপিক-ওয়ারি রেফারেন্স

| বিষয়              | কী করে                  |
| ----------------- | ----------------------- |
| `@app.get()`      | GET রাউট                |
| `@app.post()`     | POST রাউট               |
| `BaseModel`       | ডেটা ভ্যালিডেশন         |
| `Depends()`       | Dependency Injection    |
| `HTTPException`   | কাস্টম এরর              |
| `UploadFile`      | ফাইল আপলোড              |
| `Form()`          | ফর্ম ডেটা               |
| `response_model=` | আউটপুট ফরম্যাট কন্ট্রোল |



