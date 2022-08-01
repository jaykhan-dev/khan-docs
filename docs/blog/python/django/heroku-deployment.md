---
tags:
  - django
  - heroku
  - deploy
  - setup
  - steps
  - guide
---

# How to deploy Django to heroku

This guide is specifically for deploying a django api app (no frontend) to the heroku cloud platform.

## Setup

### Windows

```bash
mkdir django-prototypes
cd django-prototypes
python -m venv venv
venv\Scripts\activate
```

```bash
pip install django django_rest_framework whitenoise psycopg2 dj-database-url dj-static gunicorn django-cors-headers django-ninja
```

Run `pip freeze > requirements.txt`

The `requirements.txt` file should look similar to this:

```
asgiref==3.5.2
dj-database-url==0.5.0
dj-static==0.0.6
Django==4.0.6
django-cors-headers==3.13.0
django-ninja==0.19.1
django-rest-framework==0.1.0
djangorestframework==3.13.1
gunicorn==20.1.0
psycopg2==2.9.3
pydantic==1.9.1
pytz==2022.1
sqlparse==0.4.2
static3==0.7.0
typing_extensions==4.3.0
tzdata==2022.1
whitenoise==6.2.0
```

```bash
django-admin startproject config .
python manage.py startapp app
```

## Change `manage.py`

```python
os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'config.dev')
```

## `Procfile`

```
web: gunicorn config.wsgi --log-file -
```

## `runtime.txt`

```
python-3.9.9
```

## `.gitignore`

```
*.pyc
.DS_Store
*.swp
/config/static/
/media/
.env
/config/settings/dev.py
db.sqlite3
/venv/
```

## `.env`

```
DJANGO_SETTINGS_MODULE=config.production
SECRET_KEY = 'SECRET-KEY'
```

## `settings.py`

### BASE_DIR

```python
from pathlib import Path
import os

# Build paths inside the project like this: BASE_DIR / 'subdir'.
BASE_DIR = Path(__file__).resolve().parent.parent
```

### MIDDLEWARE

```python
MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'whitenoise.middleware.WhiteNoiseMiddleware',
]
```

### STATIC Files

```bash
python manage.py collectstatic --noinput
```

```python
#PROJECT_ROOT = os.path.join(os.path.abspath(__file__))
STATIC_ROOT = BASE_DIR / 'staticfiles'
STATIC_URL = '/static/'


#  Add configuration for static files storage using whitenoise
STATICFILES_STORAGE = "whitenoise.storage.CompressedManifestStaticFilesStorage"
```

## `dev.py`

```python
from .settings import *

# SECURITY WARNING: don't run with debug turned on in production!
DEBUG = True

# SECURITY WARNING: keep the secret key used in production secret!
SECRET_KEY = 'SECRET KEY'

# SECURITY WARNING: define the correct hosts in production!
ALLOWED_HOSTS = ['*']

EMAIL_BACKEND = 'django.core.mail.backends.console.EmailBackend'

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'prototypes',
        'USER': '********',
        'PASSWORD': '******',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}


try:
    from .local import *
except ImportError:
    pass
```

## `production.py`

```python
from __future__ import absolute_import, unicode_literals
from .settings import *
import dj_database_url
import os

env = os.environ.copy()
SECRET_KEY = env['SECRET_KEY']

DATABASES = {'default': dj_database_url.config(conn_max_age=600)}

# Honor the 'X-Forwarded-Proto' header for request.is_secure()
SECURE_PROXY_SSL_HEADER = ('HTTP_X_FORWARDED_PROTO', 'https')

# Whitenoise
STATICFILES_STORAGE = 'whitenoise.storage.CompressedManifestStaticFilesStorage'

COMPRESS_OFFLINE = True
COMPRESS_CSS_FILTERS = [
    'compressor.filters.css_default.CssAbsoluteFilter',
    'compressor.filters.cssmin.CSSMinFilter',
]
COMPRESS_CSS_HASHING_METHOD = 'content'

# Allow all host headers
ALLOWED_HOSTS = ['*']

DEBUG = False

try:
    from .local import *
except ImportError:
    pass
```

## `urls.py`

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('api/', include('tasks.urls')),
]
```
