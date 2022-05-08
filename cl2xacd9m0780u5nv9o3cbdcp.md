## Introducing Linky - Best link shortener for developers

# Want to make your own unique short-link generator?

We will be making that today!!! Stay with us!

We will be making the project from A to Z, the whole work will be covered!!!

The project is a simple website which you enter the long link then it converts it to a fancy short link!

Without further time wasted, let's start **coding**...

## Coding

- *Tech-stack which will be used:*
   - **Flask**
   - **Python**
   - **Heroku**

Before we start, be sure to install `Flask`, use the command 

`pip3 install Flask Flask-SQLAlchemy`

Be sure the `A` should be capital.

Start by making your project folder, we will start by coding `app.py` which is the main code for our app. Create in addition to a directory called `templates` which will be having HTML to view our Flask App.

Let's start creating the basic Flask App.

```py
from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello_world():
    return "HELLO WORLD"

@app.route('/omar')
def hello_omar():
    return "HI OMAR"

if __name__ == "__main__":
    app.run(port=5000, debug=True)
```

In the beginning, we are ending up importing Flask and initialize our Flask App. After initializing, we have a decorator function, if you don't know what is a decorator it is basically a super function which wraps around the functions inside it. For example `@app.route('/')` is a decorator,  which tells us whenever we go to whatever website/URL is it it like `https://example.com/` will return **HELLO WORLD**, but for example if we go to `https://example.com/omar` which decorator `@app.route('/omar')` is responsible for, it will be returning **HI OMAR**.

By default, Flask runs on port `5000` but we will just be specifying it anyways. It's better to set `debug` to on which will gives us extra information which will really help us when we experience issues.

Let's test the script by running it. The highlighted link is where the Flask app is running, go to it to test it, note it only works on your local pc.


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651998275987/MB8TyD1Nc.png align="left")

As we are on the main page, it should return **HELLO WORLD**.


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651998322920/mPePwe7As.png align="left")

Let's try going to `/omar`.


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651998356829/6HeM_qkdS.png align="left")

Make a new file in `templates` called `base.html` and copy the following template:

```html
<!doctype html>

<html lang="en">

<head>

	<meta charset="utf-8">
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" integrity="sha384-JcKb8q3iqJ61gNV9KGb8thSsNjpSL0n8PARn9HuZOnIxN0hoP+VmmDGMN5t9UJ0Z" crossorigin="anonymous">
	<title>{% block title %}{% endblock %}</title>

</head>

<body>

    <div class="container-fluid">
        <h1>Linky</h1>
        <hr>
        {% block content%}
        {% endblock %}
    </div>

    <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.1/dist/umd/popper.min.js" integrity="sha384-9/reFTGAW83EW2RDu2S0VKaIzap3H66lZH81PoYlFhbGU+6BZp6G7niu735Sk7lN" crossorigin="anonymous"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js" integrity="sha384-B4gt1jrGC7Jh4AgTPSdUtOBvfO8shuf57BaghqFfPlYxofvL8/KUEfYiJOMMV+rV" crossorigin="anonymous"></script>

  </body>
</body>
</html>
```

I added `bootstrap` which is basically it is a CSS library which has tons of pre-defined rules and a code written for us which we can instantly use. This is a basic HTML code except the `<title>` block,  the `<title>` block won't be same for each page we go to, so instead of writing the `<title>` block every time inside of our new HTML page, we will just give a block title, which allows us being directly accessing the block and changing only the elements which goes in this block instead of writing everything.

As we are in a `body`, we put everything in `div` to make everything look more better. As we see the 2 lines in the body which as follows:

```html
        <h1>Linky</h1>
        <hr>
```

will be same in all our web pages, so all of our web pages will have these 2 lines... The only difference will be what goes over here:

```html
        {% block content%}
        {% endblock %}
```

instead of writing all bootstrap stuff again, we can directly write whatever goes in here. So how to extend the information we have from `base.html`, make a file `home.html` and copy the following template:

```html
{% extends "base.html" %}
{% block title %}Shorten URL{% endblock %}

{% block content %}
<form action="#", method="post">
    <label for="url">Enter an https:// URL:</label>

    <input type="url" name="nm" id="url"
       placeholder="https://example.com"
       pattern="https://.*" size="50"
       required>
    <br>
    <input type="submit" value="submit" class="btn btn-primary">
</form>
{% endblock %}
```

This is the HTML page which will be displayed at our home page. Let's take a look:

First, we are going to extend `base.html` which actually means like the `base.html` is already in `home.html`. And here we have `{% block title %}` in `home.html` which refers to the block in `base.html` since it was called the name block title. As you can see, we are giving it a title of **Shorten URL**. So instead of writing all of this again, we just changed what is the title in `base.html` which whatever the title in `base.html` is, it will appear in ALL pages. As we have block content in `base.html`, everything in block content in `home.html` is as it is in `base.html`, imagine it as a variable.

Second, in `home.html` we have a form, which has 2 inputs, first we have a label which says "**Enter an https:// URL:**", next an input type which is set to type **URL** so it will only accept a URL and it's name is nm which we will be referring to it later on, the user will provide the long URL, and finally an input which is for submit the URL to get the short URL.

Let's link all the HTML we have to our app, return to `app.py`

One thing we have to import from Flask is `render_template`.

In decorator `@app.route('/')`, instead of returning HELLO WORLD, return `render_template("home.html")`, in this case we would like to display `home.html`.


New code:
```py
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def hello_world():
    return render_template("home.html")

@app.route('/omar')
def hello_omar():
    return "HI OMAR"

if __name__ == "__main__":
    app.run(port=5000, debug=True)
```

Let's try running our Flask App. As we are on the main page, it should display `home.html`


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1652000855526/XQ74rFiUn.png align="left")

Now, let's cleanup our code and make changes.

```py
from flask import Flask, render_template, request

app = Flask(__name__)

@app.route('/', methods=['POST', 'GET'])
def home():
    if request.method == "POST":
        url_received = request.form["nm"]
        return url_received
    else:
        return render_template('home.html')

if __name__ == "__main__":
    app.run(port=5000, debug=True)
```

As you notice, we imported `request` from Flask, and what will it help us is to get the information from the website. Before, we were only using by default GET methods, but now we will define the 2 methods, GET and POST. What does this actually mean?

POST and GET are 2 different methods to transfer data for using HTML inside a web browser, the only difference that POST is more secure method when compared to GET, why? Because in a POST method, you can't see the information in the URL, but for GET, the info can be found in the URL. For example when we where going to `http://127.0.0.1:5000/omar`, we can see the information in the URL, so it is a GET method, but for POST, for example when we put a link in main page and submit, the data is actually being transferred but they cannot be found in the URL, so it is a POST.

So if the request method is POST, it means we got a link from the form for further processing, the URL will be stored in `url_received`, as you see, I used `return url_received` for now to test if it does work or not... For example:



![ezgif-3-a7aa5c7255.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1652003381798/zXe9niH6y.gif align="left")

If it's not a POST method, we will stay on the same page until another thing is submitted which will be processed to see what's next.

We will be using Database, let me introduce you to the idea.

The database we are using is called SQL Alchemy, so SQL Alchemy is specific for Python. The reason using the database is that you can kind of treat each of our items as a Python object, which makes it a lot easier to interact with and another point to put into consideration that is by using SQL Alchemy is that we can do everything by Python code. So if you don't know how to code SQL queries, don't worry you can code most of them in Python and also the lines of code to make a query is a lot less so a lot easier.

Copy the following code and let's work on some configurations:

```py
from flask import Flask, render_template, request, redirect, url_for
from flask_sqlalchemy import SQLAlchemy
import random
import string
import os

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = os.environ.get('DATABASE_URL')
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False

db = SQLAlchemy(app)

@app.before_first_request
def create_tables():
    db.create_all()

class Urls(db.Model):
    id_ = db.Column("id_", db.Integer, primary_key=True)
    long = db.Column("long", db.String())
    short = db.Column("short", db.String(10))

    def __init__(self, long, short):
        self.long = long
        self.short = short

def shorten_url():
    letters = string.ascii_lowercase + string.ascii_uppercase
    while True:
        rand_letters = random.choices(letters, k=3)
        rand_letters = "".join(rand_letters)
        short_url = Urls.query.filter_by(short=rand_letters).first()
        if not short_url:
            return rand_letters


@app.route('/', methods=['POST', 'GET'])
def home():
    if request.method == "POST":
        url_received = request.form["nm"]
        found_url = Urls.query.filter_by(long=url_received).first()

        if found_url:
            return redirect(url_for("display_short_url", url=found_url.short))
        else:
            short_url = shorten_url()
            print(short_url)
            new_url = Urls(url_received, short_url)
            db.session.add(new_url)
            db.session.commit()
            return redirect(url_for("display_short_url", url=short_url))
    else:
        return render_template('url_page.html')

@app.route('/<short_url>')
def redirection(short_url):
    long_url = Urls.query.filter_by(short=short_url).first()
    if long_url:
        return redirect(long_url.long)
    else:
        return f'<h1>Url doesnt exist</h1>'

@app.route('/display/<url>')
def display_short_url(url):
    return render_template('shorturl.html', short_url_display=url)

@app.route('/all_urls')
def display_all():
    return render_template('all_urls.html', vals=Urls.query.all())

if __name__ == '__main__':
    app.run(port=5000, debug=True)
```

Change `os.environ.get('DATABASE_URL')` to `'sqlite:///urls.db'`. We are done, just go to the GitHub Repo, and get the HTML files inside templates, be sure to rename the files or change there names to your own unique name in the Python code.

## The End!

Thanks for reading this blog, hope you like it and learnt something you!!!

- **Live Demo:** linky-web.herokuapp.com
- **GitHub Repo:** [OmarDev100/linky](https://github.com/omardev100/linky)