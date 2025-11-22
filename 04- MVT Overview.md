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