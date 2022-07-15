---
tags:
  - python
  - rest framework
  - rest api
  - api
  - django
  - backend
  - web development
---

# Djang Rest Framework CRUD

The following code is a simple example of an API made with the Django Rest Framework.  It is for a To Do application.

## Project setup

```bash
poetry new todo-crud
cd todo-crud
poetry add django django_rest_framework
```

```bash
django-admin startproject config .
poetry run python3 manage.py startapp api
poetry run python3 manage.py runserver
poetry run python3 manage.py createsuperuser
```

Add `api.apps.ApiConfig` and `rest_framework` to `settings.py`

To use the app from the backend, register it in the `admin.py` file

```python
from django.contrib import admin
from .models import Task

admin.site.register(Task)
```

## `models.py`

```python
from django.db import models

class Task(models.Model):
    title = models.CharField(max_length=200)
    completed = models.BooleanField(default=False, blank=True, null=True)
    
    def __str__(self):
        return self.title
```

Make sure to run:

```bash
poetry run python3 manage.py makemigrations
poetry run python3 manage.py migrate
```

## `serializers.py`

```python
from rest_framework import serializers
from .models import Task

class TaskSerializer(serializers.ModelSerializer):
    class Meta:
        model = Task
        fields = '__all__'
```

## `views.py`

```python
from django.shortcuts import render
from django.http import JsonResponse

from rest_framework.decorators import api_view
from rest_framework.response import Response
from .serializers import TaskSerializer

from .models import Task

@api_view(['GET'])
def apiOverview(request):
    api_urls = {
        'List': '/task-list/',
        'Detail View': '/task-detail/<str:pk>/',
        'Create': '/task-create/',
        'Update': '/task-update/<str:pk>/',
        'Delete': '/task-delete/<str:pk>/',
    }
    
    return Response(api_urls)

@api_view(['GET'])
def taskList(request):
    tasks = Task.objects.all()
    serializer = TaskSerializer(tasks, many=True)
    return Response(serializer.data)

@api_view(['GET'])
def taskDetail(request, pk):
    tasks = Task.objects.get(id=pk)
    serializer = TaskSerializer(tasks, many=False)
    return Response(serializer.data)

@api_view(['POST'])
def taskCreate(request):
    serializer = TaskSerializer(data=request.data)
    
    if serializer.is_valid():
        serializer.save()
        
    return Response(serializer.data)

@api_view(['POST'])
def taskUpdate(request, pk):
    task = Task.objects.get(id=pk)
    serializer = TaskSerializer(instance=task, data=request.data)
    
    if serializer.is_valid():
        serializer.save()
        
    return Response(serializer.data)

@api_view(['Delete'])
def taskDelete(request, pk):
    task = Task.objects.get(id=pk)
    task.delete()
        
    return Response('Item deleted!')
```

## URLS

=== "api.urls"
    
    ```python
    from django.urls import path
    from . import views

    urlpatterns = [
        path('', views.apiOverview, name="api-overview"),
        path('task-list/', views.taskList, name="task-list"),
        path('task-detail/<str:pk>/', views.taskDetail, name="task-detail"),
        path('task-create/', views.taskCreate, name="task-create"),
        path('task-update/<str:pk>/', views.taskUpdate, name="task-update"),
        path('task-delete/<str:pk>/', views.taskDelete, name="task-delete"),
    ]
    ```

=== "config.urls"

    ```python
    from django.contrib import admin
    from django.urls import path, include

    urlpatterns = [
        path('admin/', admin.site.urls),
        path('api/', include('api.urls')),
    ]
    ```