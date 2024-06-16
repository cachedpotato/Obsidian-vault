---
tags:
---
# Django
Django is a Python-based framework. 

## Starting a Django project
```bash
django-admin startproject projectname
```
This will create directory with bunch of pre-built files that will help us create a web application, one of which includes `manage.py`. to actually run this on a server, we need to do the following command:
```bash
python path/to/projectname/manage.py runserver
```
This will open an HTML file with loopback IP address at port 8000.

## Creating a new app
Websites google can be thought of as a collection of web applications. For example, Google has Search application, Image Application, Map application, etc., and each of them are accessed by different URLs. to create a new app in Django:
```bash
python manage.py startapp appname
```
This will create a separate directory _AT THE SAME LEVEL OF THE PROJECT DIRECTORY_.

Within our app directory, we can see some pre-made files such as views.py. This file is the "main body" of the app. To hook this to a URL, we need to create `urls.py`, and add the following lines:
```python
from django.urls import path
from . import views

urlpatterns = [
    path("", views.index, name="index")
]
```
Think of URLs as _table of contents_ for our website.

Because this app is at the same level as our project folder, we need to connect this to our project as well. inside `project/urls.py`,
```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('myapp/', include("myapp.urls"))
]
```
This will let Django look for `urls.py` inside our `myapp` directory.

---
Categories: [[030-Web Development]], [[CS50 - Web Dev]]
References:
