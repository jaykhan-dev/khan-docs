---
tags:
  - python
  - django
  - django ninja
  - crud
  - api
  - json
  - rest api
  - vue js
  - javascript
  - html
  - css
  - tailwind css
  - heroku
  - github
  - cloud
---

# Ninja CRUD

## Django Ninja
[Ninja](https://django-ninja.rest-framework.com/) is a way of creating API's with Django.  It is similar to [FastAPI](https://fastapi.tiangolo.com/). 

This blog is a comprehensive tutorial for building a CRUD app, a fundamental component of web applications.  It also shows how to deploy the app as a prototype.  Larger apps that require production heavy utilities are not covered here. 

## Project Setup

### Virtual Environments

=== "poetry"

    ```bash
    poetry new mlabs-prototype
    cd mlabs-prototype
    poetry add django pillow psycopg2 gunicorn django-ninja django-cors-headers jazzmin
    poetry run django-admin startproject prototype
    poetry run python3 manage.py runserver
    ```

=== "venv"

    ```bash
    mkdir mlabs-prototype
    cd mlabs-prototype
    python3 -m venv venv
    source venv/bin/activate
    pip3 install django pillow psycopg2 gunicorn django-ninja django-cors-headers jazzmin
    django-admin startproject config .
    ./manage.py runserver
    ```

### PostgreSQL

```bash
sudo -u postgres psql
```

```bash
CREATE DATABASE mlabs;
```

```bash
CREATE USER jaykhan WITH ENCRYPTED PASSWORD 'mypass';
GRANT ALL PRIVILEGES ON DATABASE mlabs TO jaykhan;
```

### Settings

=== "base.py"

    #### PostgreSQL

    ```python

    INSTALLED_APPS = [
        ...
        'api',
    ]

    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.postgresql_psycopg2',
            'NAME': 'mlabs',
            'USER': 'jaykhan',
            'PASSWORD': 'mypass',
            'HOST': 'localhost',
            'PORT': '',
        }
    }
    ```

=== "dev.py"

=== "production.py"



### Environments

=== "dev"
    
    ```python
    # in base.py
    ```

=== "production"
    
    ```python
    # production.py
    ```

## Ninja 

### `urls.py`


### `models.py`

#### Data models

```python
from django.db import models

class Project(models.Model):
    title = models.CharField(max_length=255)
    blurb = models.TextField()
    date = models.DateField()
    prototype = models.URLField()
    live_app = models.URLField()
    
    def __str__(self):
        return self.title
```

### `ninja.py`

#### Imports

```python
from datetime import datetime, date
from typing import List, Optional, Generic, TypeVar
import datetime
from unicodedata import category
from pydantic import Field
from ninja import NinjaAPI, Schema, ModelSchema, Path, Query, Form, File
from ninja.files import UploadedFile
from django.shortcuts import get_object_or_404
from .schema import ProjectSchema, NotFoundSchema
from .models import Project

api = NinjaAPI()
```

#### Schema

```python
from datetime import date
from ninja import Schema

# PROJECTS
class ProjectSchema(Schema):
    id: int
    title: str
    date: date 
    blurb: str 
    prototype: str
    live_app: str
    
class NotFoundSchema(Schema):
    message: str
```

#### CRUD

=== "CREATE"

    ```python
    @api.post("/projects")
    def create_project(request, payload: ProjectSchema = Form(...)):
        project = Project.objects.create(**payload.dict())
        return {"id": project.id}
    ```

=== "RETRIEVE"

    ```python
    # ALL PROJECTS
    @api.get("/projects", response=ProjectSchema)
    def get_project(request):
        project = get_object_or_404(Project)
        return project

    # WITH ID
    @api.get("/projects/{project_id}", response=ProjectSchema)
    def get_project(request, project_id: int):
        project = get_object_or_404(Project, id=project_id)
        return project
    ```

=== "UPDATE"

    ```python
    @api.put("/projects/{project_id}")
    def update_project(request, project_id: int, payload: ProjectSchema):
        project = get_object_or_404(Project, id=project_id)
        for attr, value in payload.dict().items():
            setattr(project, attr, value)
        project.save()
        return {"success": True}
    ```

=== "DELETE"

    ```python
    @api.delete("/project/{project_id}")
    def delete_project(request, project_id: int):
        project = get_object_or_404(Project, id=project_id)
        project.delete()
        return {"success": True}

    ```

## Vue JS

```bash
npm init vue@latest mlabs-prototype
cd mlabs-prototype
npm install
npm run lint
npm run dev
```

### Tailwind CSS

#### Install commands

```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

#### Configure

```js
module.exports = {
  content: [
    "./index.html",
    "./src/**/*.{vue,js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

#### `index.css`

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

#### `main.js`

```js
import { createApp } from 'vue'
import App from './App.vue'
import './index.css'

createApp(App).mount('#app')
```

#### run application

```bash
npm run dev
```

### Pinia 
Setup the store to get the information from the Ninja API


```js
import { defineStore } from "pinia";
import axios from "axios";

export const NinjaStore = defineStore("NinjaStore", {
  state: () => ({
    projects: [],
  }),
  getters: {
    getProjects(state) {
      return state.projects;
    },
  },
  actions: {
    async fetchProjects() {
      try {
        const data = await axios.get(
          "https://mlabs-prototype.herokuapp.com/ninja/projects"
        );
        this.projects = data.data;
      } catch (error) {
        alert(error);
        console.log(error);
      }
    },
  },
});
```

### Components

=== "CREATE"

=== "RETRIEVE"

=== "UPDATE"

=== "DELETE"

```html
<script>
import axios from "axios";
export default {
  name: "ProjectAPI",
  components: {},
  data() {
    return {
      projects: [],
      project: [],
    };
  },
  methods: {
    getProjects() {
      axios
        .get("http://localhost:8000/api/")
        .then(
          function (response) {
            this.projects = response.data;
          }.bind(this)
        )
        .catch((error) => alert(error));
    },
    deleteProject(project) {
      axios
        .delete("http://localhost:8000/api/" + project.id)
        .then(function (response) {
          this.project = response.data;
        })
        .catch((error) => alert(error));
    },
  },
  mounted() {
    this.getProjects();
  },
};
</script>
```



## Deploy

### Github

=== "django"
    
    ```python
    # runtime.txt
    python-3.7.6
    ```

    ```bash
    pip3 freeze > requirements.txt
    ```

    ```python
    # Procfile
    web: gunicorn mlabs-prototype.wsgi:application --log-file -
    ```

=== "vue"
    ```bash
    git init
    git status
    git add .
    git commit -m "first commit"
    git remote add origin https://github.com/jaykhan-dev/mlabs-prototype.git
    git push -u origin master
    ```

## Heroku Pipeline
