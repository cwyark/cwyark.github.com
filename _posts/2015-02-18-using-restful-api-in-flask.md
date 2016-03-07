---
title: "Using RESTful API in Flask"
description: ""
category: tutorial
tags: [python, flask, restful-api]
---

#### Why RESTful API? ####
In traditional way, the page's view (that means the view which shown on the browser) are generated from the backend service. For example, if we use flask and jinja template engine ...
    
``` python
@app.route("/", method=["GET", "POST"])
def index():
    users = User.query.all()
    return render_template('index.html', r_users=users)
```

The `index.html` template (which will be processed by jinja) is something like this

``` html
<html>
    <head>
        <title>My Title</title>
    </head>
    <body>
        <ul>
        { % for user in r_users % }
            <li> My name is { { user.name } }, and I'm { {user.age} } years old </li>
        { % endfor % }
        </ul>
    </body>
</html>
```

While every `request` receieved, it tells the backend service to query the `User model` from the database and put it in the `index.html` template.

However, under this structure, server(backend service) and client(your browser) are binding with each other. For developers, once the backend service's rule has changed, the template should have be modified. 

And there is another example, if there are two types of model (`user` and `fruit`) in your template.

``` html
<html>
    <head>
        <title> My Title </title>
    </head>
    <body>
        <ul>
        { % for user in r_users % }
            <li>My name is { { user.name } }, and I'm { {user.age} } years old</li>
        { % endfor % }
        </ul>

        <ul>
        { % for fruit in r_fruits % }
            <li>This is a/an { { fruit.name } }, and I like it</li>
        { % endfor % }
        </ul>
    </body>
</html>
```

Your backend service should be like this...

``` python
@app.route("/", method=["GET", "POST"])
def index():
    users = User.query.all()
    fruits = Fruit.query.all()
    return render_template('index.html', r_users=users, r_fruits=fruits)
```

See! You need to query two models at once if you want to render this template! Which means whenever you refresh this page, backend service should query all of the models from the database everytime. 

And there's one thing you should know, querying from database may cost your server's resource. Moreover, most of PaaS platforms cost money when you are interactive with their database.

RESTful API may help you to seperate the server and the client, which makes your web applications more flexiable and extensiable. 

### Designing RESTful API(s) by using flask-restful ###

This is the example restful api project structure.

    .
    ├── app
    │   ├── api.py
    │   ├── db.py
    │   └── __init__.py
    └── README.md

#### _Install required packages_ ####

``` python
user$ pip install flask
user$ pip install flask-restful
user$ pip install flask-sqlalchemy
user$ pip install gunicorn
```

#### _Create a WSGI entry_ ####

In \__init__.py, simply create a WSGI entry called `app`

``` python
from flask import Flask
app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///./test.db'
from app import api, db
```

Now try to `cd` to your project root and run the web application by using `gunicorn`:

``` bash
user$ gunicorn app:app --reload
```

If there's no error occured, you successfully create a WSGI entry `app`.

#### _Declare the Data Model_ ####

in db.py, declare a `User` Model using flask-sqlalchem and create it.
   
``` python
from flask_sqlalchemy import SQLAchemy
from app import app
db = SQLAlchemy(app)

class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String)
    age = db.Column(db.Integer)

    def __init__(self, name, age = None):
        self.name = name
        self.age = age

    def __repr__(self):
        return 'User<%s><%d>' % (self.name, self.age)

db.create_all()
```

#### _Design your RESTful API_ ####

In api.py , design the `UserApi` class as your RESTful API. In `UserApi`, we define `GET` and `POST` methods that on;y these two methods can access the API.

`GET` method can get user's id name, age and `POST` can add a new user.

``` python
from flask_restful import Resource, Api
from flask import request
from app import app
from db import db, User

api = Api(app)

class UserApi(Resource):
    def get(self, name):
        ret = list()
        users = User.query.filter(User.name == name).all()
        for user in users:
            ret.append(
                {'id': user.id, 'name': user.name, 'age': user.age}
            )
        return {'user': ret}

    def post(self, name):
        age = request.form['age']
        user = User(name=name, age=age)
        db.session.add(user)
        db.session.commit()
        return {'user': {'id': user.id, 'name': user.name, 'age': user.age}}


api.add_resource(UserApi, "/api/users/<name>")
```

For example, you can add a new user `Marry` by using `POST` method to http://your.domain.com/api/users/Marry(And also there should be a `age` in the form). If you want to know the user `Marry`'s age, you can use `GET` method to http://your.domain.com/api/users/Marry.

#### _Test your restful api_ ####

Now use the gunicorn to active the application, `cd` to the project root and run ...
``` bash
user$ gunicorn app:app --reload --access-logfile -
```

Then use `curl` command (if you are using Unix like system) to post some fake data.

``` bash
user$ curl -i -d "age=14" -X POST http://127.0.0.1:8000/api/users/john
user$ curl -i -d "age=65" -X POST http://127.0.0.1:8000/api/users/Marry
```

You can now use the sqlite tool to check the fake data(if you are using Unix like system).

``` bash
user$ sqlite3 test.db "select * from user"
1|john|14
2|Marry|65
```

See! Now you can interactive with the database through the designed RESTful API!

Then you can use the `GET` method to get the user: `john`'s infomation

``` bash
user$ curl -i -X GET http://127.0.0.1:8000/api/users/john
HTTP/1.1 200 OK
Server: gunicorn/19.2.1
Date: Thu, 19 Feb 2015 11:10:41 GMT
Connection: close
Content-Type: application/json
Content-Length: 48

{"user": [{"age": 14, "id": 1, "name": "john"}]}
```
