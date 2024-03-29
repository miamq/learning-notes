# Django Fundamentals

### Introduction
Django is a free and open-source framework for building **web applications** with **Python.** 

> It is also the most famous Python backend framework. Companies such as YouTube, Instagram, Spotify and Dropbox all use (or partially use) Django for supporting their backend.

### Django Features:
- The admin site
- Object-relational Mapper (ORM): no need to write SQL code anymore!
- Authentication
- Caching

### Build Up the Project Environment
1. Install the latest-version of Python
2. Install pipenv (a dependency manager) using ```pip install pipenv```
3. Create a new project folder and ```cd``` into it
4. Use ```pipenv install django``` to create an virtual enviroment (saved in the C: disk) and install Django
5. The above command will also create two files ```Pipefile (like the package.json for JavaScript project)``` and ```Pipefile.lock```
6. Activate the virtual enviroment using ```pipenv shell```
7. Create the Django project using the current directory using ```django-admin startproject yourprojectname .```
8. The manage.py is a **wrapper** of django-admin and it will consider the project setting

### Project Structure
1. ```__init__.py```: defines the directory as a python package
2. ```asgi.py```: for deployment
3. ```settings.py```: where we define the application settings
4. ```urls.py```: where we define the urls of application
5. ```wsgi.py```: for deployment

### Create Application
App represents a certain functionality of the system. After creating a new app, we need to add it into ```INSTALLED_APPS``` of ```settings.py```
Use ```python manage.py startapp playground``` to create the app ```playground```

1. ```__init__.py```: defines the directory as a python package
2. ```admin```: django admin system
3. ```apps.py```: configuration
4. ```models.py```: where we define model classes from which we pull out data from database
5. ```tests.py```: where we write unit tests
6. ```views.py```: where we write request handlers

### View
The ```view function``` takes a request and return a response. It is a request handler.

First, we define a view function.
```python3
'''
When the user visit the url "xxx/playground/hello",
this function should be called
'''
def say_hello(request):
    return HttpResponse('Hello World')
```

Secondly, we need to create a file named ```urls.py``` to construct the mappings from URLs to view functions
```python3
from django.urls import path
from . import views

# URLConf
urlpatterns = [
    path('hello/', views.say_hello)
]
```

Finally, we edit the ```urls.py``` of the ```main application``` (the main URL handler) which processes and redirects the original URL to other application's URL handlers.
```python3
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('playground/', include('playground.urls')),
]
```
For example, if the original URL is ```xxx/playground/hello```, the main URL handler will first chop off the ```xxx/playground``` part and then redirect the rest part ```hello``` to the playground URL handler which will call the view function ```views.say_hello``` that we defined before. 

### Debugging




