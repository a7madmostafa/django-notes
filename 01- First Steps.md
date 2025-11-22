# **First Steps**

## 1- **Create project directory**

```bash
mkdir my_django_project
cd my_django_project
```

## 2- **Create virtual environments**

```bash
python -m venv myenv
source myenv/bin/activate  # On Windows use `myenv\Scripts\activate`
pip install django
```
### *Check Django installation*

```bash
python -m django --version
```

## 3- **Create django project**

```bash
django-admin startproject mysite
cd mysite
```
## 4- **Run development server**

```bash
python manage.py runserver
```
> Open your web browser and go to `http://127.0.0.1:8000/` to see the Django welcome page.

---

## 5- **Create a Django app**

```bash
python manage.py startapp myapp #  linked to a project 
```
or
```bash
django-admin startapp myapp  # linked to a project
```
or
```bash
python -m django startapp myapp  # standalone app
```

### ✅ Key Differences:

```bash
1️⃣ python manage.py startapp <app_name>
```
+ Runs inside a Django project directory.

+ Uses the project’s settings automatically.

+ Creates the app inside the current project folder.

+ Typical workflow:
    1. Create a project using `django-admin startproject mysite`.
    2. Navigate into the project directory: `cd mysite`.
    3. Create apps using `python manage.py startapp myapp`. 

```bash
2️⃣ python -m django startapp <app_name>
```
+ Can be run anywhere; does not require a project directory.

+ Creates a standalone app folder.

+ Does not automatically link the app to a project — you must add it to `INSTALLED_APPS` manually later.

+ Useful for creating reusable apps outside of a specific project.

+ Typical workflow:
    1. Create a standalone app using `python -m django startapp myapp`.
    2. Manually add the app to a project’s `INSTALLED_APPS` setting when needed.