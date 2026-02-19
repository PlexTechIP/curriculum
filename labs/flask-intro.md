---
layout: default
title: "Week 5: Flask Introduction"
---

# Flask Introduction

In this lab you'll build your first backend server using Flask, a lightweight Python web framework. You'll learn HTTP fundamentals, routing, and how to handle different types of requests and responses.

---

## Setup

### 1. Pull Starter Code

```bash
git pull starter main
```

### 2. Download Postman

Download [Postman](https://www.postman.com/downloads/) (the desktop app or web version both work). You'll use it to test your API endpoints.

### 3. Create a Virtual Environment

A virtual environment keeps this project's dependencies isolated from your global Python installation.

```bash
# Inside your Flask Intro folder:
python -m venv env
source env/bin/activate      # Mac/Linux
# env\Scripts\activate       # Windows

pip install flask
```

> You must activate the virtual environment each time you start working: `source env/bin/activate`

---

## What is Postman vs. a Browser?

| | Browser | Postman |
|---|---------|---------|
| Methods | GET only (by default) | GET, POST, PUT, DELETE, etc. |
| Payloads | URL only | Raw text, JSON, form data |
| Use case | Viewing pages | Testing APIs |

Try it: enter `google.com` in your browser, then the same URL in Postman with GET. What's different?

---

## Hello World

Create `solution.py`:

```python
from flask import Flask

app = Flask(__name__)

@app.route('/hello')
def index():
    return 'Web App with Python Flask!'

app.run(host='0.0.0.0', port=81)
```

Run it, then visit `http://localhost:81/hello` in your browser and in Postman.

---

## Responses

HTTP responses can return different formats:

```python
# Plain text
@app.route('/hello')
def hello():
    return 'Hello World'

# JSON
@app.route('/hello-json')
def hello_json():
    return {"text": "Hello World from Dictionary"}

# HTML
@app.route('/hello-html')
def hello_html():
    return "<h1>Hello World</h1><p>Subtext</p>"

# Custom status code (second element of a tuple)
@app.route('/hello-html-error')
def hello_html_error():
    return "<h1>Hello World</h1><p>Subtext</p>", 404
```

**Your Task:** Implement all four routes above and test them in your browser and Postman.

---

## Requests

### Path Variables

```python
@app.route('/hello/<name>')
def hello_name(name):
    return 'Hello ' + str(name)
```

Try `/hello/Adam` in your browser.

**Your Task:** Implement a route so that:
- `/hello/Adam/change/10` → `"Hello Adam, your change is 0"`
- `/hello/Dev/change/9` → `"Hello Dev, your change is 1"` *(change for a $10 total)*

---

### Query Parameters

Queries look like: `youtube.com/watch?v=VIDEO_ID`

Access them with `request.args`:

```python
from flask import request

@app.route('/hello')
def hello():
    name = request.args.get('name')
    if name:
        return 'Hello ' + name
    return 'Hello World'
```

**Your Task:** Modify `/hello` so that:
- `/hello` → `"Hello World"`
- `/hello?key=value` → `"Hello World"`
- `/hello?name=Shamith` → `"Hello Shamith"`

---

### HTTP Methods

`GET` is for retrieving data. Other methods like `POST` send data to the server.

```python
@app.route('/login', methods=['POST', 'GET'])
def login():
    ...
```

---

### Plain Text Payload

*(Use Postman → Body → raw → Text)*

```python
@app.route('/reflect', methods=['POST'])
def reflect():
    payload = request.data.decode('utf-8')
    return 'Hello ' + payload
```

---

### JSON Payload

*(Use Postman → Body → raw → JSON)*

```python
@app.route('/reflect/plex', methods=['POST'])
def reflect_plex():
    data = request.json
    result = {}
    for key, value in data.items():
        new_key = 'plex_' + key
        new_value = 'plex_' + value if isinstance(value, str) else value
        result[new_key] = new_value
    return result
```

**Your Task:** Implement `/reflect/plex` so that:
- Input: `{"name": "X", "age": 12}`
- Output: `{"plex_name": "plex_X", "plex_age": 12}`

---

### Form Submission

Create an HTML file with a form that submits to your server:

```html
<html>
    <body>
        <form action="http://localhost:81/login" method="POST">
            <p>Enter Name:</p>
            <p><input type="text" name="username" /></p>
            <p><input type="submit" value="submit" /></p>
        </form>
    </body>
</html>
```

Access form data with `request.form`:

```python
@app.route('/reflect/plex/form', methods=['POST'])
def reflect_plex_form():
    data = request.form
    result = {}
    for key, value in data.items():
        result['plex_' + key] = 'plex_' + str(value)
    return result
```

**Your Task:** Implement `/reflect/plex/form` — same logic as `/reflect/plex` but treat all values as strings.

---

## Summary: All Routes to Implement

| Route | Method | Description |
|-------|--------|-------------|
| `/hello` | GET | "Hello World" |
| `/hello-json` | GET | Returns JSON with "Hello World" |
| `/hello-html` | GET | Returns `<h1>` HTML |
| `/hello-html-error` | GET | Same HTML, 404 status |
| `/hello/<name>` | GET | Greets by name from path |
| `/hello/<name>/change/<amount>` | GET | Returns change from $10 |
| `/hello` (with query) | GET | Greets by `?name=` query param |
| `/reflect` | POST | Echoes text payload |
| `/reflect/plex` | POST | Prefixes JSON keys/string values with `plex_` |
| `/reflect/plex/form` | POST | Same as above, from form data |

---

## Submission

Push your completed `solution.py` to your forked repository:

```bash
git add solution.py
git commit -m "complete flask intro"
git push origin main
```

We will run automated tests on your routes and give feedback at the next Curriculum meeting!

---

## Resources

- [Flask Official Docs](https://flask.palletsprojects.com/)
- [Python Basics Flask Tutorial](https://pythonbasics.org/flask-tutorial-hello-world/)
- [Postman Download](https://www.postman.com/downloads/)
- [HTTP Status Codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)
