# Django

> The web framework for perfectionists with deadlines. Batteries included.

---

## Purpose

Build full-stack web apps with Django: ORM, admin, auth, templates, forms.

## Prerequisites

- [Python/](../Python/).

## Learning Outcome

You can build, deploy, and scale a Django app.

## Dependencies

- Python.

## Related Files

- [Python/](../Python/) · [FastAPI/](../FastAPI/) · [Backend/](../Backend/) · [PostgreSQL/](../PostgreSQL/)

## AI Instructions

When using Django:
1. Use Django 5+.
2. Use the ORM (don't write raw SQL unless needed).
3. Use Django admin for CRUD.
4. Use Django templates or DRF for API.
5. Use `django-storages` for S3/R2.
6. Use Celery for background jobs.
7. Use `django-environ` for env vars.

## Human Notes

### Why Django
- Batteries: auth, admin, ORM, sessions, forms, security.
- Convention over configuration.
- Huge ecosystem.
- Great for content / CRUD apps.

### Project structure
```
myproject/
  manage.py
  myproject/
    settings.py
    urls.py
    wsgi.py
  blog/
    models.py
    views.py
    urls.py
    admin.py
    templates/blog/
    migrations/
```

### Models
```python
from django.db import models
from django.contrib.auth.models import User

class Post(models.Model):
    title = models.CharField(max_length=200)
    body = models.TextField()
    author = models.ForeignKey(User, on_delete=models.CASCADE)
    published_at = models.DateTimeField(null=True, blank=True)

    class Meta:
        ordering = ['-published_at']
```

### Migrations
```bash
python manage.py makemigrations
python manage.py migrate
```

### Views (function-based)
```python
from django.shortcuts import render, get_object_or_404
from .models import Post

def post_list(request):
    posts = Post.objects.filter(published_at__isnull=False)
    return render(request, 'blog/list.html', {'posts': posts})
```

### Views (class-based)
```python
from django.views.generic import ListView
from .models import Post

class PostListView(ListView):
    model = Post
    context_object_name = 'posts'
    template_name = 'blog/list.html'
```

### URLs
```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.PostListView.as_view(), name='post_list'),
    path('<int:pk>/', views.PostDetailView.as_view(), name='post_detail'),
]
```

### Admin
Register models:
```python
from django.contrib import admin
from .models import Post

@admin.register(Post)
class PostAdmin(admin.ModelAdmin):
    list_display = ('title', 'author', 'published_at')
    list_filter = ('published_at',)
    search_fields = ('title', 'body')
```

### Django REST Framework (DRF)
For APIs:
```python
from rest_framework import serializers, viewsets
from rest_framework.routers import DefaultRouter
from .models import Post

class PostSerializer(serializers.ModelSerializer):
    class Meta:
        model = Post
        fields = '__all__'

class PostViewSet(viewsets.ModelViewSet):
    queryset = Post.objects.all()
    serializer_class = PostSerializer

router = DefaultRouter()
router.register('posts', PostViewSet)
```

### Auth
Built-in: User model, login/logout, password reset, permissions.

### Forms
```python
from django import forms
from .models import Post

class PostForm(forms.ModelForm):
    class Meta:
        model = Post
        fields = ['title', 'body']
```

### Templates
```html
{% extends "base.html" %}
{% block content %}
  {% for post in posts %}
    <h2>{{ post.title }}</h2>
    <p>{{ post.body|truncatewords:30 }}</p>
  {% endfor %}
{% endblock %}
```

### Async views (Django 3.1+)
```python
async def async_view(request):
    data = await fetch_data()
    return JsonResponse(data)
```

### Background jobs
Celery + Redis/RabbitMQ.

### Testing
```python
from django.test import TestCase
from .models import Post

class PostModelTest(TestCase):
    def test_str(self):
        post = Post(title="Hello")
        self.assertEqual(str(post), "Hello")
```

### When NOT to use Django
- Pure API (FastAPI is lighter).
- Real-time-heavy (use async framework).

## Common Mistakes

- ❌ N+1 queries (use `select_related`, `prefetch_related`).
- ❌ Blocking I/O in async views.
- ❌ Storing secrets in `settings.py`.
- ❌ Not using migrations.
- ❌ Putting business logic in views.

## Tools

- Django docs: https://docs.djangoproject.com/
- DRF: https://www.django-rest-framework.org/
- Celery: https://docs.celeryq.dev/
- django-storages: https://django-storages.readthedocs.io/

## Further Reading

- *Two Scoops of Django* — Daniel Feldroy
- *Django for Everybody* — Charles Severance

## Exercises

1. Build a blog with Django + admin.
2. Add DRF API.
3. Add Celery for email.

## Projects

- Build a SaaS with Django + Stripe + Celery.

---

**Previous:** [Python/](../Python/) · **Next:** [FastAPI/](../FastAPI/) · **Related:** [Backend/](../Backend/)
