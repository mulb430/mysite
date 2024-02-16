Django Blog/CRUD-App: Readme
Dieses Readme-Dokument beschreibt die Erstellung einer einfachen CRUD-App (Create, Read, Update, Delete) mit Django. Die Anwendung dient als Prototyp für eine Verwaltungsanwendung und ermöglicht das Hinzufügen, Anzeigen, Aktualisieren und Löschen von Aufgaben oder anderen Inhalten.




Projektstruktur
Unsere Django-Anwendung besteht aus folgenden Komponenten:
1.	Projekt: Das Django-Projekt enthält die gesamte Anwendung. Hier werden die Einstellungen, URLs und globale Konfigurationen definiert.
2.	App: Die App innerhalb des Projekts ist für die spezifische Funktionalität verantwortlich. In unserem Fall handelt es sich um eine Aufgabenverwaltungs-App.
3.	Datenbankmodell: Das Modell definiert die Struktur der Datenbanktabelle. Wir haben ein einfaches Modell für Aufgaben erstellt.
4.	Views: Die Views sind für die Präsentation der Daten verantwortlich. Wir haben Views für das Anzeigen der Aufgabenliste und das Bearbeiten einzelner Aufgaben.
5.	Templates: Die HTML-Templates definieren das Aussehen der Webseiten. Wir haben Templates für die Listenansicht und die Detailansicht der Aufgaben.
   
Installation
    Virtuelle Umgebung erstellen:
    	python3 -m venv myenv
    	source myenv/bin/activate


    Django installieren:
    	pip install django
    	Projekt erstellen:
    	django-admin startproject mysite
  	    cd mysite
  	
    App erstellen:
        python manage.py startapp blog


Datenbankmodell
In der blog/models.py-Datei haben wir das Modell für Aufgaben definiert:
from django.db import models

class Post(models.Model):
    title = models.CharField(max_length=200)
    description = models.TextField()
    completed = models.BooleanField(default=False)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    def __str__(self):
        return self.title
        
Views
In der blog/views.py-Datei haben wir Views für die Aufgabenliste und die Detailansicht erstellt:
from django.shortcuts import render, get_object_or_404
from .models import Post

def post_list(request):
    tasks = Task.objects.all()
    return render(request, 'blog/post/list.html', {'post': posts})

def post_detail(request, pk):
    task = get_object_or_404(Task, pk=pk)
    return render(request, 'blog/detail.html', {'post': post})
    
URLs
In der blog/urls.py-Datei haben wir die URLs für unsere Views definiert:
from django.urls import path
from . import views

urlpatterns = [
    path('', views.post_list, name='post_list'),
    path('<int:pk>/', views.list_detail, name='list_detail'),
]

Templates
Die HTML-Templates befinden sich im /templates/blog/-Verzeichnis. Wir haben Templates für die Listenansicht (list.html) und die Detailansicht (detail.html) erstellt.
Lokale Ausführung
Die App kann lokal ausgeführt werden, indem Sie den Django-Entwicklungsserver starten:
python manage.py runserver
Besuchen Sie dann http://localhost:8000/ in Ihrem Browser, um die CRUD-APP anzuzeigen.

