# Django Models and CRUD Operations Tutorial

If you are building a **dynamic web application**, using a database for data storage is essential. The **presentation layer** is the layer that the user interacts with. Any data posted from the presentation layer needs to be:

- Persisted
- Retrieved later for use

For example, a website with user login functionality must keep track of:

- Who the users are
- What data they are allowed to view, edit, or create

The solution in Django is to use a **Model**.

---

## What is a Model?

A **model** is:

- The object equivalent of a database table in Django
- A **single definitive source of information** about your data
- Used to perform **CRUD operations** (Create, Read, Update, Delete)
- A Python class that subclasses `django.db.models.Model`

---

## Why Use Models?

There are **two ways to work with databases** as a backend developer:

1. **Direct SQL Approach**  
   - Create tables manually in the database  
   - Write custom SQL queries to store and retrieve data  

2. **Framework Approach (Django)**  
   - Frameworks like Django assist developers with **rapid development**  
   - Models allow you to interact with the database **without writing SQL manually**  
   - The model contains the essential fields and behaviors of your data

> In Django, **each model usually maps to a single database table**.

---

## Model Structure in Django

A Django model is a Python class:

```python
from django.db import models

class User(models.Model):
    first_name = models.CharField(max_length=50)
    last_name = models.CharField(max_length=50)
 ```
- each attribute of the class represents a database field
- Django provides various field types like `CharField`, `IntegerField`, `DateField`, etc.
- Django automatically adds an `id` field as the primary key unless specified otherwise

## CRUD Operations with Django Models
Django models provide an easy way to perform CRUD operations:

### Create
To create a new record in the database:
* Using raw SQL:
```sql
INSERT INTO user (first_name, last_name) VALUES ('John', 'Doe');
```
* Using Django ORM:
```python
new_user = User(first_name="John", last_name="Doe")
new_user.save()
```
### Read
1. To read records from the database:
* Using raw SQL:
```sql
SELECT * FROM user WHERE id = 1;
```

* Using Django ORM:
```python
user = User.objects.get(id=1)
```

2. To retrieve all users:
```sql
SELECT * FROM user;
```
* Using Django ORM:
```python
users = User.objects.all()
for user in users:
    print(user.first_name, user.last_name)
```
3. TO filter users by last name:
* Using raw SQL:
```sql
SELECT * FROM user WHERE last_name = 'Doe';
```
* Using Django ORM:
```python
doe_users = User.objects.filter(last_name='Doe')
for user in doe_users:
    print(user.first_name, user.last_name)
```
### Update
1. To update an existing record:
* Using raw SQL:
```sql
UPDATE user SET first_name = 'Jane' WHERE id = 1;
```
* Using Django ORM:
```python
user = User.objects.get(id=1)   
user.first_name = 'Jane'
user.save()
```
2. Update multiple records:
* Using raw SQL:
```sql
UPDATE user SET last_name = 'Smith' WHERE last_name = 'Doe';
```
* Using Django ORM:
```python
User.objects.filter(last_name='Doe').update(last_name='Smith')
```
### Delete
1. To delete a record:
* Using raw SQL:
```sql
DELETE FROM user WHERE id = 1;
```
* Using Django ORM: 
```python
user = User.objects.get(id=1)
user.delete()
```
2. To delete multiple records:
* Using raw SQL:
```sql
DELETE FROM user WHERE last_name = 'Smith';
```
* Using Django ORM:
```python
User.objects.filter(last_name='Smith').delete()
```     
