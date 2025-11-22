
# **More Concepts**

## **What is `django-admin`?**

`django-admin` is a **command-line utility** provided by Django for performing administrative tasks.

It is used to manage projects, apps, database migrations, static files, and more.

### 📌 Key Features

- Create Django projects
- Create apps
- Run database migrations
- Check project status and errors
- Start the development server
- Collect and manage static files

### **Project Structure**

> Django uses the same folder structure as a standard Django project.

```
mysite/
    manage.py
    mysite/
        __init__.py
        settings.py
        urls.py
        wsgi.py
```
- `manage.py`: A command-line utility that lets you interact with this Django project.
- `mysite/`: The actual Python package for your project.
- `settings.py`: Configuration settings for this Django project.
- `urls.py`: The URL declarations for this Django project; a "table of contents" of your Django-powered site.
- `wsgi.py`: An entry-point for WSGI-compatible web servers to serve your project.

### `manage.py` vs `django-admin`

- `manage.py` is the command-line utility for Django projects. It sets the `DJANGO_SETTINGS_MODULE` environment variable so that it points to your project's settings file.
- `django-admin` is a more general utility that can be used for any Django project but requires you to manually set the `DJANGO_SETTINGS_MODULE` environment variable if you're working within a specific project.

> In most cases, you'll use `manage.py` when working within a Django project.
* First: Create a project using `django-admin startproject mysite`.
* Then: Use `manage.py` for project-specific tasks like running the server or making migrations.

```bash
# Using django-admin to create a project
django-admin startproject mysite

# Using manage.py to run the development server
python manage.py runserver
```