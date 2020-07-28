## Motivation
You want to start asap with Django and you don't have too much time to read the official documentation.
I assume that you have any knowledge about how to use a console (cmd, bash, sh and so on).

Human universe  
- Model View Controller

Django universe  
- Model Template View

### Preconditions
- Download and install [Python language](https://www.python.org/downloads/)
- Download and install your favorite IDE or text editor

### Django

Activate virtual env (and use the virtual environment's interpreter, located at app_ven/Scripts):
 
```bash
# create a virtual environment
$ python -m venv app_venv
# activate it (notice that the prompt changes)
$ app_venv/Scripts/activate
$ (app_venv) # <-- This is the new prompt
```

Ok, you have a virtual environment (it means: python libraries isolated to your python-system-libraries).
Now, start a Django project:
 
```bash
$ django-admin startproject one
$ cd one
```

And start a Django application:

```bash
$ django-admin startapp one_app
```

You can store the packages installed if you want. Just type the freeze command:

```bash
$ pip freeze > requirements.txt
```

Now, create the file one_app/urls.py. Define the first URL:

```python
from django.urls import path
# This list contains all the url to your app
urlpatterns = [ path('', views.post_list, name='post_list')]
```

Create the view at one_app/views.py:

```python
# This function is the controller to the url (in Django world we name it as view)
def post_list(request):
        posts = Post.objects.all()
        return render(request, 'This is a simple text', {'posts':posts})
```

Add the app to the apps list in settings.py into INSTALLED_APPS variable

Name the app in urls.py as

```python
app = 'one_app'
```

Then, create the first model at one_app/models.py:

```python
from django.db import models

class Post(models.Model):
	title = models.CharField(max_length=264, null=False, blank=False)
	text = models.TextField(null=False, blank=False)
	
	def __str__(self):
		return self.title
	
	class Meta:
		verbose_name = 'Post'
		verbose_name = 'Posts'
		db_table = 'Posts'
		ordering = ['id']
```

Migrate the changes (it is mapping the model with de ORM and create the related structure on the database):

```bash
$ python manage.py makemigrations
$ python manage.py migrate
```

Register the model in the admin.py module:

```python
from . models import Post

admin.site.register(Post)
```

Run the server:

```bash
$ python manage.py runserver
```

Let's pause to see the progress. At this point you've done this steps:
- Define an URL
- Relate the URL with a controller (a view in Django)
- Map the model and database schema through Django ORM
- Run the server

Next, log in to admin site (localhost:8000/admin) or run shell (python manage.py shell) to add posts

### Admin site: create an user before

```bash
# with this user you can log in at admin site.
# you can access in localhost:8000/admin
$ python manage.py createsuperuser
```

### Shell: add posts through shell

Insert:

```bash
>> from . models import Post
>> p = Post(title='The first one post', text='This is a simple content.')
>> p.save()
```

Select all:
```bash
>> posts = Post.objects.all()
```

### Verify the advance

Log in to the admin site: localhost:8000 (use the credentials created with _createsuperuser_ command)
Ok, you'll can see the post created previously.

It's time for a break! Then, [read the documentation](https://docs.djangoproject.com/en/3.0/) to delve into the concepts.