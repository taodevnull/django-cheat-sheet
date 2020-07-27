## Preconditions
- Download and install [Python language](https://www.python.org/downloads/)
- Download and install your favorite IDE or text editor

## Django

Activate virtual env:
 
```bash
$ python -m venv app_venv
```

 
```bash
$ django-admin startproject one
```

```bash
$ django-admin startapp one_app
```

Create the file one_app/urls.py. Define the first URL:

```python
from django.urls import path

urlpatterns = [ path('', views.post_list, name='post_list')]
```

Create the first model at one_app/models.py:

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

Migrate the changes:

```bash
$ python manage.py makemigrations

```

```bash
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

Login into admin site or run shell (python manage.py shell) to add posts