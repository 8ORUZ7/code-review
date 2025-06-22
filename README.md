#### this will be a github pages website once i finish uploading my notes. the content will cover the basics of application development, automation in coding projects (data analysis), and the use of ai model training. 

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



