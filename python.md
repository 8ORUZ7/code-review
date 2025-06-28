
## core practice : https://gist.github.com/8ORUZ7/290d0abc62b187c22060a01fdf377565
### built-in functions used
| Function           | Purpose / Example                                 |
| ------------------ | ------------------------------------------------- |
| `print()`          | output to console — `print("Hello")`              |
| `len()`            | count elements — `len(["a", "b", "c"])` → `3`     |
| `type()`           | check type — `type(42)` → `<class 'int'>`         |
| `int()`, `float()` | type conversion — `float("3.14")` → `3.14`        |
| `str()`            | to string — `str(10)` → `"10"`                    |
| `sum()`            | add numbers — `sum([1, 2, 3])` → `6`              |
| `min()` / `max()`  | get min/max — `max([5, 9, 2])` → `9`              |
| `range()`          | loop range — `for i in range(3)`                  |
| `enumerate()`      | index while looping — `for i, v in enumerate(...` |
| `zip()`            | pair items — `zip(list1, list2)`                  |
| `map()`            | transform list — `map(str, [1, 2, 3])`            |
| `filter()`         | filter list — `filter(lambda x: x > 0, nums)`     |
| `input()`          | user input (cli apps)                             |
| `isinstance()`     | type checking — `isinstance(x, list)`             |


## automations using ai: 
### `transformers.pipeline()` — hugging face utility for loading ai models
```python
from transformers import pipeline

# Sentiment Analysis
sentiment = pipeline("sentiment-analysis")
sentiment("This is amazing!")  # → [{'label': 'POSITIVE', 'score': 0.999...}]

# Zero-Shot Classification
classifier = pipeline("zero-shot-classification")
output = classifier("I want a refund", candidate_labels=["billing", "technical", "complaint"])
print(output['labels'][0])  # 'billing'
```
### common dict access built-ins:
| function      | use case                                      |
| ------------- | --------------------------------------------- |
| `dict.get()`  | safe access: `output.get('labels')`           |
| `dict['key']` | direct access (use only if key is guaranteed) |
| `list[index]` | index access — `labels[0]`                    |

### useful `pandas` methods for cleaning and exploration:
```python
import pandas as pd
df = pd.read_csv("data.csv")
df.info()          # Structure summary
df.describe()      # Stats summary
df.head(3)         # Preview first 3 rows
df.dropna()        # Remove missing values
df['Sex'].map({'male': 0, 'female': 1})  # Encode categorical
```
### scikit-learn core functions:
```python
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier

X_train, X_test, y_train, y_test = train_test_split(X, y)
model = RandomForestClassifier()
model.fit(X_train, y_train)
model.score(X_test, y_test)  # → accuracy
```

## ai model training (no use of flask/fastapi): 
### core built-in & sklearn tools:
```python
from sklearn.datasets import load_iris
from sklearn.linear_model import LogisticRegression

iris = load_iris()
model = LogisticRegression(max_iter=200)
model.fit(iris.data, iris.target)
model.predict([input_data])  # Custom use
```

### custom predict() + label mapping:
```python
def predict_species(input_data):
    return model.predict([input_data])[0]

def predict_species_name(input_data):
    return iris.target_names[model.predict([input_data])[0]]
```

### dataset shape & structure:
```python
iris.data.shape        # e.g., (150, 4)
iris.target_names      # ['setosa', 'versicolor', 'virginica']
```

| concept             | good practice                                  |
| ------------------- | ---------------------------------------------- |
| pipeline reuse      | define it once — don't reinitialize repeatedly |
| safe dict access    | use `.get()` instead of `['key']` when unsure  |
| clean structure     | avoid nesting more than 2 levels               |
| variable naming     | use `camel_case` or `snake_case` consistently  |
| logic separation    | keep model training and prediction separate    |
| dataset inspection  | use `.shape`, `.info()`, `.head()` often       |
| functional approach | use small, pure functions (`def`) for tasks    |

---

### crud

```python
# In-memory CRUD for a list of dicts

database = []

# CREATE
def create_entry(entry):
    database.append(entry)
    print(f"Added: {entry}")

# READ
def read_entries():
    for idx, entry in enumerate(database):
        print(f"{idx}: {entry}")

# READ by id
def get_by_id(entry_id):
    for entry in database:
        if entry.get('id') == entry_id:
            return entry
    return None

# UPDATE by id
def update_entry_by_id(entry_id, new_entry):
    for entry in database:
        if entry.get('id') == entry_id:
            entry.update(new_entry)
            print(f"Updated by id {entry_id}: {entry}")
            return
    print("Entry not found.")

# DELETE by id
def delete_entry_by_id(entry_id):
    global database
    before = len(database)
    database = [entry for entry in database if entry.get('id') != entry_id]
    after = len(database)
    print(f"Deleted count: {before - after}")

# Example usage
create_entry({"id": 1, "name": "Alice"})
create_entry({"id": 2, "name": "Bob"})
read_entries()
print("Get by id:", get_by_id(2))
update_entry_by_id(2, {"name": "Bobby"})
delete_entry_by_id(1)
read_entries()
create_entry({"id": 3, "name": "Charlie"})
read_entries()
```

- add validation to prevent duplicate ids  
- implement searching by name  
- store more complex data (lists, nested dicts) per entry


### ai

```python
# Simple Linear Regression with scikit-learn

from sklearn.linear_model import LinearRegression
import numpy as np

# Data: Hours studied vs. score
X = np.array([[1], [2], [3], [4], [5]])
y = np.array([50, 55, 65, 70, 75])

model = LinearRegression()
model.fit(X, y)

# Predict for 6 hours
prediction = model.predict([[6]])
print("Predicted score for 6 hours:", prediction[0])

# Experiment: Predict for multiple hours
X_test = np.array([[1], [2], [3], [7], [10]])
y_pred = model.predict(X_test)
print("Predictions for hours [1,2,3,7,10]:", y_pred)
```

- change the dataset to something else
- try polynomial regression  
- save/load model with `joblib`


### custom dataset example

```python
import pandas as pd

data = {
    "Name": ["A", "B", "C", "D"],
    "Score": [90, 85, 78, 92],
    "Passed": [True, True, False, True]
}
df = pd.DataFrame(data)

print(df.describe())
print("Passed Students:\n", df[df["Passed"]])

# Experiment: Add more columns, filter, group, plot
df["Grade"] = pd.cut(df["Score"], bins=[0, 80, 90, 100], labels=["C", "B", "A"])
print(df)
print("Group by Grade:\n", df.groupby("Grade").size())
df.hist(column="Score")
import matplotlib.pyplot as plt
plt.show()
```

- try loading a csv file  
- use `df.groupby` for aggregates  
- generate summary statistics for other types


### backend/api

```python
from http.server import BaseHTTPRequestHandler, HTTPServer
import json

class SimpleHandler(BaseHTTPRequestHandler):
    messages = []
    def do_GET(self):
        if self.path == '/hello':
            self.send_response(200)
            self.send_header('Content-type', 'application/json')
            self.end_headers()
            response = {'message': 'Hello, World!'}
            self.wfile.write(json.dumps(response).encode())
        elif self.path == '/messages':
            self.send_response(200)
            self.send_header('Content-type', 'application/json')
            self.end_headers()
            response = {'messages': self.messages}
            self.wfile.write(json.dumps(response).encode())
        else:
            self.send_response(404)
            self.end_headers()
    def do_POST(self):
        if self.path == '/messages':
            content_length = int(self.headers['Content-Length'])
            post_data = self.rfile.read(content_length)
            data = json.loads(post_data)
            self.messages.append(data)
            self.send_response(201)
            self.send_header('Content-type', 'application/json')
            self.end_headers()
            response = {'received': data}
            self.wfile.write(json.dumps(response).encode())
        else:
            self.send_response(404)
            self.end_headers()

# To run:
# if __name__ == "__main__":
#     server = HTTPServer(('localhost', 8080), SimpleHandler)
#     print('Starting server at http://localhost:8080')
#     server.serve_forever()
```
 
- add a PUT method for updating messages  
- use a global variable for in-memory storage  
- write a client that uses `requests.post` and `requests.get`


### database design and SQL

```python
import sqlite3

# Connect or create db
conn = sqlite3.connect(':memory:')
cursor = conn.cursor()

# Create table
cursor.execute('''CREATE TABLE users (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL,
    email TEXT UNIQUE NOT NULL
)''')

# Insert
cursor.execute("INSERT INTO users (name, email) VALUES (?, ?)", ("Alice", "alice@example.com"))
cursor.execute("INSERT INTO users (name, email) VALUES (?, ?)", ("Bob", "bob@example.com"))
conn.commit()

# Query
cursor.execute("SELECT * FROM users")
print("All users:")
for row in cursor.fetchall():
    print(row)

# Update
cursor.execute("UPDATE users SET email=? WHERE name=?", ("alice@new.com", "Alice"))
conn.commit()

# Delete
cursor.execute("DELETE FROM users WHERE name=?", ("Bob",))
conn.commit()

# Read after delete
cursor.execute("SELECT * FROM users")
print("After delete:", cursor.fetchall())

# Experiment: Add more tables, foreign keys
cursor.execute('''CREATE TABLE posts (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    user_id INTEGER,
    title TEXT,
    FOREIGN KEY (user_id) REFERENCES users(id)
)''')
cursor.execute("INSERT INTO posts (user_id, title) VALUES (?, ?)", (1, "First post"))
conn.commit()
cursor.execute("SELECT * FROM posts")
print("Posts:", cursor.fetchall())

conn.close()
```

- add transaction handling  
- use SQL joins  
- try using a persistent database file

### devops/deployment

```python
import shutil
import os

def deploy_app(src, dest):
    if os.path.exists(dest):
        shutil.rmtree(dest)
    shutil.copytree(src, dest)
    print(f"Deployed from {src} to {dest}")

# Experiment: Add versioning, logging, backup
def backup_and_deploy(src, dest, backup_dir):
    if os.path.exists(dest):
        shutil.move(dest, os.path.join(backup_dir, f"backup_{os.path.basename(dest)}"))
    shutil.copytree(src, dest)
    print(f"Deployed with backup from {src} to {dest}")

# Example usage
# deploy_app('my_app', '/tmp/deployed_app')
# backup_and_deploy('my_app', '/tmp/deployed_app', '/tmp/backup_dir')
```
- add a function to restart a service  
- write scripts to compress files before deployment


### security-based tasks

```python
import hashlib
import secrets

def hash_password(password):
    return hashlib.sha256(password.encode()).hexdigest()

print(hash_password("mypassword"))

# Generate a token
token = secrets.token_hex(16)
print(f"Secure token: {token}")

# Encrypt/decrypt example (using Fernet)
from cryptography.fernet import Fernet

key = Fernet.generate_key()
cipher = Fernet(key)
enc = cipher.encrypt(b"my secret data")
print(f"Encrypted: {enc}")
print(f"Decrypted: {cipher.decrypt(enc)}")

# Experiment: Use bcrypt for password hashing
import bcrypt
hashed = bcrypt.hashpw(b"mypassword", bcrypt.gensalt())
print("Bcrypt:", hashed)
assert bcrypt.checkpw(b"mypassword", hashed)
```
- experiment with different hash functions (MD5, SHA512)  
- use HMAC for message authentication  
- use PyJWT to generate and verify tokens


### system design or architecture questions 

```python
# Simple Service Registry with Python dict

class ServiceRegistry:
    def __init__(self):
        self.services = {}
    def register(self, name, address):
        self.services[name] = address
    def get(self, name):
        return self.services.get(name)
    def all_services(self):
        return self.services.copy()

registry = ServiceRegistry()
registry.register("user-service", "localhost:5000")
registry.register("order-service", "localhost:5001")
print("All services:", registry.all_services())

# Experiment: Add health checks, deregister, list all
def deregister(registry, name):
    if name in registry.services:
        del registry.services[name]
        print(f"Deregistered {name}")

deregister(registry, "order-service")
print("After deregister:", registry.all_services())
```
- implement a load balancer  
- simulate microservices with multiple registries

### file and i/o manipulation

```python
# Write to a file
with open("example.txt", "w") as f:
    f.write("Hello, file!\nSecond line.")

# Read from a file
with open("example.txt", "r") as f:
    content = f.read()
    print("File content:\n", content)

# Append to a file
with open("example.txt", "a") as f:
    f.write("\nAppended line.")

# Read lines
with open("example.txt", "r") as f:
    for line in f:
        print("Line:", line.strip())

# Experiment: Read CSV, write JSON
import csv, json
with open("data.csv", "w", newline="") as f:
    writer = csv.writer(f)
    writer.writerow(["name", "score"])
    writer.writerow(["Alice", 90])
    writer.writerow(["Bob", 85])

data = []
with open("data.csv", "r") as f:
    reader = csv.DictReader(f)
    data = [row for row in reader]
print("CSV as list of dicts:", data)
with open("data.json", "w") as f:
    json.dump(data, f)
```
- try reading and writing binary files  
- use `os.listdir` to list all files in a directory

### testing and debugging

```python
# Simple test function
def add(a, b):
    return a + b

def test_add():
    assert add(2, 3) == 5
    assert add(-1, 1) == 0
    print("All tests passed.")

test_add()

# Debugging with print and pdb
def buggy_function(x):
    print("Debug: x =", x)
    # import pdb; pdb.set_trace()
    return 10 / x

try:
    print(buggy_function(0))
except Exception as e:
    print("Caught exception:", e)

# Experiment: Use unittest
import unittest

class TestMath(unittest.TestCase):
    def test_add(self):
        self.assertEqual(add(2, 3), 5)
        self.assertEqual(add(-1, 1), 0)
    def test_zero(self):
        self.assertEqual(add(0, 0), 0)

# Run with: python -m unittest <filename>
```
- try pytest for more advanced testing  
- use mocking to simulate external APIs  
- intentionally add a bug, find it with `pdb`


