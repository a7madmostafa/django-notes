# **MVT Overview**

The Model-View-Template (MVT) architecture is a design pattern used in web development, particularly in frameworks like Django. It separates the application into three main components:
1. **Model**: Represents the `data` structure and handles database interactions. 
2. **View**: Manages the `logic` and control flow of the application. It processes user requests, interacts with the model to retrieve or modify data, and selects the appropriate template to render the response.
3. **Template**: Responsible for the `presentation` layer. It defines how the data is displayed to the user, typically using HTML with embedded template tags to dynamically generate content.

The following diagram explains the interplay of these three layers.

![MVT Architecture](imgs/MVT-Overview-1.png)

### **How MVC Works**

- The controller intercepts the user requests. 

- It coordinates with the view and model layers to send the appropriate response back to the client.

- The model is responsible for data definitions, processing logic and interaction with the backend database.

- The view is the presentation layer of the application. 

- It takes care of the placement and formatting of the result and sends it to the controller, which in turn, redirects it to the client as the application's response.

### **Django's MVT Implementation**

![Django's MVT Architecture](imgs/MVT-Overview-2.png)

- A Django application consists of the following components: 

    + `URL Dispatcher`
    + `Views`
    + `Models` 
    + `Templates`

#### **URL dispatcher**

+ Django's URL dispatcher mechanism is equivalent to the controller in the MVC architecture.

+ The `urls.py` module in the Django project's package folder acts as the dispatcher.

+ It defines the URL patterns. Each URL pattern is mapped with a view function to be invoked when the client's request URL is found to be matching with it.

+ The URL patterns defined in each app under the project are also included. Here’s the urls.py file in the app folder.

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.home, name='home'),
]
```
When the server receives a request in the client URL, the dispatcher matches its pattern with the patterns available in the urls.py. 

It then routes the flow of the application toward its associated view.


#### **Views**

+ The view function reads the path, query, and body parameters included in the client's request If required, it uses this data to `interact with the models` to perform CRUD operations.

+ A view can be a user-defined function or a class.

+ You create View definitions in the `views.py` file of the respective `app package folder`. 

+ The following code in the `views.py` file defines the `index()` view function:

```python
from django.http import HttpResponse

def index(request):
    return HttpResponse("Welcome to the Home Page of MyApp!")
``` 

#### **Models**

+ A model is a Python class.  

+ An app may have one or more model classes, conventionally put in the `models.py` file. 

+ Django migrates the attributes of the model class to construct a database table of a matching structure.

+ Django's `Object Relational Mapper (ORM)` helps perform `CRUD operations` in an `object-oriented` way instead of invoking `SQL queries`.

+ The view uses the client's and the model's `data` and renders its `response` using a `template`.

#### **Templates**

+ A template is a web page containing a mix of `static HTML` and `Django Template Language code blocks`.

+ You place Template web pages in the `templates folder` with the `.html` extension.

+ Django's template processor uses any context data from the view inserted in these blocks to formulate a dynamic response.

+ The view, in turn, returns the response to the user.

+ This explains how Django's MVT architecture handles the request-response cycle in a web application.

## **Django MVT vs. MVC Architecture**

###  1. MVC Architecture (Traditional)

    Model --------- Controller --------- View
      |                                    |
    Database                           HTML/UI


#### ✔️ Model
Represents application data and interacts with the database.

#### ✔️ View
The user interface (HTML, templates, frontend pages).

#### ✔️ Controller
Contains business logic, handles requests, and chooses which View to display.

---

###  2. Django MVT Architecture

    Model --------- View --------- Template 
      |                                | 
    Database                        HTML/UI


#### ✔️ Model (same as MVC)
- Python classes representing database tables  
- Located in `models.py`

#### ✔️ Template (View in MVC)
- HTML + Django Template Language  
- Located in the `templates/` directory

#### ✔️ View (Controller in MVC)
- Handles request/response logic  
- Fetches data from the model  
- Renders templates  
- Located in `views.py`

---

##  Key Difference

In Django, the **Controller is handled by the Django framework itself**, not by the developer.

➡️ This is why Django's “View” acts like the **Controller**,  
and Django's “Template” acts like the **View**.

---

## 🧠 Mapping Django MVT to MVC

| Django (MVT) | MVC Equivalent |
|--------------|----------------|
| Model        | Model          |
| View         | Controller     |
| Template     | View           |

---

## 🧩 Request Flow in Django

1. User requests a URL  
2. `urls.py` routes the request  
3. View (controller logic) handles it  
4. View interacts with the Model  
5. View renders a Template  
6. Response returned to browser

---

## 📝 Summary

- Django uses **MVT**, not MVC  
- **Django View = MVC Controller**  
- **Django Template = MVC View**  
- Django framework acts as the **Controller** behind the scenes  
- MVT keeps logic (View) separated from presentation (Template)


