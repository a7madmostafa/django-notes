# Django Migrations Tutorial

Django translates **models** into database tables using a mechanism called **migrations**. Migrations also propagate any changes in the model structure, such as:

- Adding a field
- Modifying a field
- Removing a field  

This ensures the **database schema** stays in sync with your Django models.

---

## Migration Commands

Django provides the following migration commands:

| Command | Description |
|---------|-------------|
| `makemigrations` | Creates migration scripts based on changes in models |
| `migrate` | Applies migration scripts to the database |
| `sqlmigrate` | Shows the SQL statements a migration will execute |
| `showmigrations` | Displays applied and pending migrations |

---

## Migration Workflow

Django’s migration system works like **version control** for your database:

1. **Add or modify a model**  
2. Run `makemigrations` → creates a migration script  
3. Run `migrate` → applies the migration to the database  

> Every migration script has a version number and describes the changes to be applied.

---

## Migrating Models of INSTALLED_APPS

When you create a Django project using `startproject`, several apps are installed by default. These are listed in `INSTALLED_APPS` in `settings.py`:

```python
INSTALLED_APPS = [ 
    'django.contrib.admin', 
    'django.contrib.auth', 
    'django.contrib.contenttypes', 
    'django.contrib.sessions', 
    'django.contrib.messages', 
    'django.contrib.staticfiles', 
]
```
Django requires database tables for these apps to function correctly (e.g., `auth` controls users, groups, permissions). By default, Django uses ***SQLite***. To create the required tables:
```bash
python manage.py migrate
```
This command applies all migrations for the installed apps, creating necessary tables in the database.

---

## Creating a Custom App

Create a new app inside your project:
```bash
python manage.py startapp myapp
```
Add the new app to `INSTALLED_APPS` in `settings.py`:
```python
INSTALLED_APPS = [ 
    ...
    'myapp',
]
```
Now, create models in `myapp/models.py`:
```python
from django.db import models

class Person(models.Model):
    name = models.CharField(max_length=20)
    email = models.EmailField()
    phone = models.CharField(max_length=20)
```
To create the corresponding database table for the `Person` model:
1. Run `makemigrations` to create migration scripts:
```bash 
python manage.py makemigrations myapp
```
Output:
```Migrations for 'myapp':
  myapp/migrations/0001_initial.py
    - Create model Person
```
* The `0001_initial.py` script describes creating the `Person` table.

* Opening this file shows a migration class:

```python
from django.db import migrations, models

class Migration(migrations.Migration):

    initial = True

    dependencies = []

    operations = [
        migrations.CreateModel(
            name='Person',
            fields=[
                ('id', models.AutoField(primary_key=True)),
                ('name', models.CharField(max_length=20)),
                ('email', models.EmailField(max_length=254)),
                ('phone', models.CharField(max_length=20)),
            ],
        ),
    ]
```
2. Run `migrate` to apply the migration and create the `Person` table:

```bash
python manage.py migrate myapp
```
Output:

```
Operations to perform: 
  Apply all migrations: admin, auth, contenttypes, myapp, sessions
Running migrations:
  Applying myapp.0001_initial... OK
```
* The `Person` table is now created in `db.sqlite3` with fields: `id`, `name`, `email`, `phone`.

---

## Version Control Example

### Renaming a Field
***Modify the Person model:***

```python
class Person(models.Model):
    person_name = models.CharField(max_length=20)  # renamed from name
    email = models.EmailField()
    phone = models.CharField(max_length=20)
```
***1. Run `makemigrations` to create migration scripts:***
```bash
python manage.py makemigrations myapp
```
Output:
```
Was person.name renamed to person.person_name (a CharField)? [y/N] y
Migrations for 'myapp':
  myapp\migrations\0002_rename_name_person_person_name.py
    - Rename field name on person to person_name

```

***2. Modify the `Person` model to add a new field:***
```python
age = models.IntegerField(default=0)
```
***3. Run `makemigrations` again:***

```bash
python manage.py makemigrations myapp
```
Output:
```
Migrations for 'myapp':
  myapp\migrations\0003_person_age.py
    - Add field age to person
```

***4. Check migration status:***
```bash
python manage.py showmigrations myapp
```
Output:
```
myapp
 [X] 0001_initial   
 [ ] 0002_rename_name_person_person_name
 [ ] 0003_person_age
```
* [X] indicates applied migrations.
* [ ] indicates pending migrations.

5. Apply pending migrations:
```bash
python manage.py migrate myapp
```
Output:
```
Applying myapp.0002_rename_name_person_person_name... OK
Applying myapp.0003_person_age... OK
``` 

***5. Rolling Back Migrations***
To roll back to a previous migration state, specify the migration name:
```bash
python manage.py migrate myapp 0002_rename_name_person_person_name

``` 
Output:
```
Applying myapp.0002_rename_name_person_person_name... OK
```

This command reverts the database schema to the state after applying `0002_rename_name_person_person_name`, removing the `age` field added in `0003_person_age`.

---

## Viewing SQL of a Migration
To see the SQL statements a migration will execute, use `sqlmigrate`:
```bash
python manage.py sqlmigrate myapp 0002_rename_name_person_person_name
```
Output:
```sql
BEGIN;
ALTER TABLE "myapp_person" RENAME COLUMN "name" TO "person_name";
COMMIT;
``` 
This shows the SQL command to rename the `name` column to `person_name` in the `myapp_person` table.

---
## Summary
Django migrations provide a powerful way to manage database schema changes in sync with your models. By using commands like `makemigrations`, `migrate`, and `sqlmigrate`, you can easily create, modify, and roll back database structures as your application evolves.

| Command          | Purpose                                     |
| ---------------- | ------------------------------------------- |
| `makemigrations` | Creates migration scripts for model changes |
| `migrate`        | Applies migration scripts to the database   |
| `sqlmigrate`     | Shows SQL for a migration script            |
| `showmigrations` | Lists applied and pending migrations        |

### Key Points
- Migrations keep your database schema in sync with Django models
- Each migration script represents a version of the database schema
- You can roll back to previous migration states as needed
- Always run `makemigrations` after modifying models to create migration scripts
- Use `migrate` to apply changes to the database