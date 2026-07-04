API (Application Programming Interface) allow different applications to share data and work together, saving time and effort. There are many different frameworks for building APIs in Python. 

Some of the most popular frameworks for creating APIs in Python are Django, Flask, and FastAPI.
All three of these frameworks are Python web frameworks that you can use to develop web applications. Django is a full-featured framework that includes everything you need to get started, including a built-in ORM and an admin panel.

An API is a software intermediary that allows two applications to talk to each other. When you use an application on your phone, the application connects to the Internet and sends data to a server. The server then processes the data and sends it back to your phone. The application on your phone then interprets the data and presents it to you in a readable way.

### FastAPI

FastAPI is a high-performing web framework for building APIs with Python.

```
# install fastapi
pip install fastapi

# run the api
uvicorn main:app –reload
OR
fastapi dev dashboard/main.py     
```

`main` is the name of the Python file, and `app` is the variable that stores the FastAPI class.

While building an API, the "path" defines the route or endpoint of the request. However, there is one more choice we have to make here, i.e., “Operation.” The word `operation` here refers to one of the HTTP "methods."
- **POST**: to create data.
- **GET**: to read data.
- **PUT**: to update data.
- **DELETE**: to delete data.

```
from typing import Union

from fastapi import FastAPI

app = FastAPI()


@app.get("/")
def read_root():
    return {"Hello": "World"}


@app.get("/items/{item_id}")
def read_item(item_id: int, q: Union[str, None] = None):
    return {"item_id": item_id, "q": q

```

You already created an API that:

- Receives HTTP requests in the _paths_ `/` and `/items/{item_id}`.
- Both _paths_ take `GET` _operations_ (also known as HTTP _methods_).
- The _path_ `/items/{item_id}` has a _path parameter_ `item_id` that should be an `int`.
- The _path_ `/items/{item_id}` has an optional `str` _query parameter_ .



#### Path parameters vs Query parameters

**path parameters** are used to **identify a specific resource or resources**, while **query parameters** are used to **sort/filter those resources**.

**Path parameters** are embedded directly within the URL path and act as placeholders for specific values. They are used to target and identify unique resources within the API. For example, in the URL _/users/{id}_, _{id}_ is a path parameter representing a specific user ID.

**Query parameters** are additional information attached to a URL after a question mark _?_. They come in key-value pairs, separated by an ampersand _&_, and are used to modify API request behavior without altering the core resource. For example, in the URL _/users?sort=name&limit=10_, _sort_ and _limit_ are query parameters.

### What is htmx

When building interactive web experiences, developers have traditionally had two main options, each with its own trade-offs. On one hand, there are multi-page applications (MPAs) which refresh the entire page every time a user interacts with it. This approach ensures that the server controls the application state and the client faithfully represents it. However, the full page reloads can lead to a slow and clunky user experience.

On the other hand, there are single-page applications (SPAs) which rely on JavaScript running in the browser to manage the application state. They communicate with the server using API calls, which return data, often in JSON format. The SPA then uses this data to update the user interface without a page refresh, providing a much smoother user experience somewhat akin to a native desktop or mobile app. However, this approach isn’t perfect either. The computational overhead is usually higher due to substantial client-side processing, the initial load times can be slower as the client has to download and parse large JavaScript bundles before rendering the first page, and setting up the development environment often involves dealing with intricate build tools and workflows.

**HTMX allows partial updates by making requests to the server for just the part of the page that needs updating**

htmx provides a middle ground between these two extremes. It offers the user experience benefits of SPAs — with no need for full page reloads — while maintaining the server-side simplicity of MPAs. **In this model, instead of returning data that the client needs to interpret and render, _the server responds with HTML fragments_**. htmx then simply swaps in these fragments to update the user interface.

In order to use htmx , just include the following script tag in your HTML file:

```markup
<script src="https://unpkg.com/htmx.org@1.9.4"></script> 
```

One of the main selling points of htmx is that it gives developers the ability to **send Ajax requests** directly from HTML elements by utilizing a set of distinct attributes. Each attribute represents a different HTTP request method:

- `hx-get`: issues a GET request to a specified URL.
- `hx-post`: issues a POST request to a stated URL.
- `hx-put`: issues a PUT request to a certain URL.
- `hx-patch`: issues a PATCH request to a set URL.
- `hx-delete`: issues off a DELETE request to a declared URL.

#### hx-get
```markup
<button hx-get="/api/resource">Load Data</button>
```

In the above example, the `button` element is assigned an `hx-get` attribute. Once the button is clicked, a GET request is fired off to the `/api/resource` URL.

#### hx-target
In some cases, we might want to update a different element than the one that initiated the request. htmx allows us to target specific elements for the Ajax response with the `hx-target` attribute. **This attribute can take a CSS selector**, and htmx will use this to find the element(s) to update. For example, if we have a form that posts a new comment to our blog, we might want to append the new comment to a comment list rather than updating the form itself.

```markup
<button
  hx-get="https://v2.jokeapi.dev/joke/Any?format=txt&safe-mode&type=single"
  hx-target="#joke-container"
>
  Make me laugh!
</button>
```

Instead of the button replacing its own content, the `hx-target` attribute states that the response should replace the content of the element with an ID of “joke-container”.

#### hx-trigger
htmx initiates an Ajax request in response to specific events happening on certain elements:

- For `input`, `textarea` and `select` elements, this is the `change` event.
- For `form` elements, this is the `submit` event.
- For all other elements, this is the `click` event.

we can add an htmx `trigger` attribute to our `<input>` element:

```markup
<input
  ...
  hx-trigger="keyup"
/>
```

Now the results are updated immediately.

### Validation Data with Pydantic

Pydantic to define data models, also known as user-defined schemas. These models can include data types, validation rules, and default values. By establishing these models, developers can ensure that incoming data adheres to the expected structure and types. This validation process guarantees the reliability and integrity of the data used in your API.

In addition to data validation, Pydantic is adept at automatically converting and parsing data from various formats, such as JSON or form data, into Python objects. These conversions are based on the previously defined models or user-defined schemas.

Response models in FastAPI are Pydantic models that define the structure and data types of responses sent back to clients.
#### fastapi Endpoint for handling data / decorator methods

Then you should create an endpoint to handle the data

```
@app.post("/submit-form/")
async def handle_form(username: str = Form(...), age: int = Form(...), email: str = Form(...)):
    return UserForm(username=username, age=age, email=email)
```
In this example, the form fields **username**, **age**, and **email** are defined. The **Form(...)** indicates that these are required fields.

#### Endpoint with pydantic models

###### 1. define a pydantic model

```
class UserForm(BaseModel):
    username: str
    age: int | None = None
    email: str
```

###### 2. handle data

```
@app.post("/submit-form-model/", response_model=UserForm)
async def handle_form_model(user_form: UserForm) -> UserForm:
    return user_form
```
you can directly use a Pydantic model in the endpoint.

### Optional Fields

To make a field optional, use **None** as the default value:

@app.post("/submit-form-optional/")
async def handle_form_optional(username: str = Form(...), age: int = Form(None), email: str = Form(None)):
    return {"username": username, "age": age, "email": email}

