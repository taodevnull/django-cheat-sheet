## Preconditions
- Download and install [Python language](https://www.python.org/downloads/)
- Download and install your favorite IDE or text editor

## Django

Activate virtual env (and use the virtual environment's interpreter, located at app_ven/Scripts):
 
```bash
$ python -m venv app_venv
```

Start a Django project:
 
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

Create the view at one_app/views.py:

```python

def post_list(request):
        posts = Post.objects.all()
        return render(request, 'This is a simple text', {'posts':posts})
```

Add the app to the apps list in settings.py into INSTALLED_APPS variable

Name the app in urls.py as

```python
app = 'one_app'
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

Ok, at this point you've done this steps:
- Define an URL
- Relate thar URL with a controller (a view in Django)
- Map the model and database schema through Django ORM
- Run the server

Next, login into admin site (localhost:8000) or run shell (python manage.py shell) to add posts

## Add posts through shell

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