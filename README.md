# Photo-Album

A Django-based web application for sharing and managing photos.

## Features

- Upload photos
- View gallery of photos
- View individual photos

## Requirements

- Python 3.x
- Django 3.x or higher

## Setup Instructions
### 1. Clone the Repository

```bash
git clone https://github.com/your-username/photo-album.git
cd photo-album

2. Create a Virtual Environment
python -m venv myenv

3. Activate the Virtual Environment
myenv\Scripts\activate
On macOS and Linux:

bash
Copy code
source myenv/bin/activate


4. Apply Migrations
python manage.py migrate

5. Create a Superuser
python manage.py createsuperuser

6. Run the Development Server
python manage.py runserver
Open your web browser and go to http://127.0.0.1:8000/ to see the application.



Project Overview
URLs Configuration
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('photos.urls')),
]
photos/urls.py:
from django.urls import path
from . import views

urlpatterns = [
    path('', views.gallery, name='gallery'),
    path('photo/<str:pk>/', views.viewPhoto, name='photo'),
    path('add/', views.addPhoto, name='add'),
]

Views
from django.shortcuts import render

def gallery(request):
    return render(request, 'photos/gallery.html')

def viewPhoto(request, pk):
    return render(request, 'photos/photo.html')

def addPhoto(request):
    return render(request, 'photos/add.html')


Models
photos/models.py
from django.db import models

class Category(models.Model):
    name = models.CharField(max_length=100, null=False, blank=False)
    
    def __str__(self):
        return self.name
    
class Photo(models.Model):
    category = models.ForeignKey(Category, on_delete=models.SET_NULL, null=True, blank=True)
    image = models.ImageField(null=False, blank=False)
    description = models.TextField()
    
    def __str__(self):
        return self.description

Templates
photos/templates/photos/gallery.html
photos/templates/photos/photo.html
photos/templates/photos/add.html
Static Files
photoshare/static/images/


