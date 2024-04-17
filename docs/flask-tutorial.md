# Flask Tutorial

[flask tutorial](https://flask.palletsprojects.com/en/3.0.x/tutorial/)

## run flask

``` shell
flask --app flaskr run --debug # if named app, then --app is no need
```

## What is `g`?

`g` is a special object that is unique for each request. It is used to store data
 that might be accessed by multiple functions during the request. The connection
 is stored and reused instead of creating a new connection if get_db is called a
 second time in the same request.

## What is `current_app`?

`current_app` is another special object that points to the Flask application handling
 the request. Since you used an application factory, there is no application object
 when writing the rest of your code. get_db will be called when the application has
 been created and is handling a request, so current_app can be used.

## What is a view function?

In Flask, a view function is a Python function that responds to a particular URL route. It's responsible for handling HTTP requests made to the application and returning an HTTP response.

Here's a basic example of a view function in Flask:

``` python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def index():
    return 'Hello, World!'

if __name__ == '__main__':
    app.run()

```

In this example:

- `@app.route('/')` is a decorator that associates the `/` URL route with the `index` function.
- The `index` function is a view function that returns the string `'Hello, World!'`.

When a user visits the root URL of the Flask application (e.g., `http://localhost:5000/`), Flask calls the `index` function, and the returned string `'Hello, World!'` is sent back as the HTTP response.

View functions can perform various tasks, such as rendering templates, processing
 form data, interacting with databases, and returning JSON responses. They are the
 core building blocks of Flask applications, responsible for generating dynamic
 content based on the request.

## `url_for()` function

The `url_for()` function generates the URL to a view based on a name and arguments. The name associated with a view is also called the *endpoint*, and by default it’s the same as the name of the view function.

For example, the `hello()` view that was added to the app factory earlier in the tutorial has the name `'hello'` and can be linked to with `url_for('hello')`. If it took an argument, which you’ll see later, it would be linked to using `url_for('hello', who='World')`.

When using a blueprint, the name of the blueprint is prepended to the name of the function, so the endpoint for the `login` function you wrote above is `'auth.login'` because you added it to the `'auth'` blueprint.

## You should know [`Jinja`](https://jinja.palletsprojects.com/templates/)

Jinja looks and behaves mostly like Python. Special delimiters are used to distinguish Jinja syntax from the static data in the template. Anything between `{{` and `}}` is an expression that will be output to the final document. `{%` and `%}` denotes a control flow statement like `if` and `for`. Unlike Python, blocks are denoted by start and end tags rather than indentation since static text within a block could change indentation.

## [`add_url_rule`](https://flask.palletsprojects.com/en/3.0.x/api/#flask.Flask.add_url_rule)

Register a rule for routing incoming requests and building URLs. The `route()` decorator is a shortcut to call this with the `view_func` argument. These are equivalent:

``` python
@app.route("/")
def index():
    ...
```

``` python
def index():
    ...

app.add_url_rule("/", view_func=index)
```

See [URL Route Registrations](https://flask.palletsprojects.com/en/3.0.x/api/#url-route-registrations).

The endpoint name for the route defaults to the name of the view function if the `endpoint` parameter isn’t passed. An error will be raised if a function has already been registered for the endpoint.

The `methods` parameter defaults to `["GET"]`. `HEAD` is always added automatically, and `OPTIONS` is added automatically by default.

`view_func` does not necessarily need to be passed, but if the rule should participate in routing an endpoint name must be associated with a view function at some point with the `endpoint()` decorator.

``` python
app.add_url_rule("/", endpoint="index")

@app.endpoint("index")
def index():
    ...
```

If `view_func` has a `required_methods` attribute, those methods are added to the passed and automatic methods. If it has a `provide_automatic_methods` attribute, it is used as the default if the parameter is not passed.

## About Tests

Related package: `pytest` and `coverage`

## Deployment
