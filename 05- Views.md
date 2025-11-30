# Views

## How to create a view?

00. Make sure you have an app created using the command:

```bash
python manage.py startapp myapp
```
and that your app is added to the `INSTALLED_APPS` list in `settings.py`.

```python
INSTALLED_APPS = [
    ...
    'myapp'  # or 'myapp.apps.MyappConfig' if you have a custom AppConfig,
]
``` 

01. Open the `views.py` file in your Django app directory.

02. Create a function that returns a `HttpResponse` object.

```python
from django.http import HttpResponse

def home(request):
    return HttpResponse("Hello, this is my first view!")
```

03. Map the view to a URL in your app's `urls.py` file.

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.home, name='home'),
]
```

04. Add the app's URLs to the project's main `urls.py` file.

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('myapp.urls')),
]
```

05. Start the development server and navigate to the URL in your web browser.

```bash
python manage.py runserver
```
Visit `http://localhost:8000/` in your web browser to see the "Hello, this is my first view!" message.