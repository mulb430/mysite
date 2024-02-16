Django CRUD-App: Readme
Dieses Readme-Dokument beschreibt die Erstellung einer
einfachen CRUD-App (Create, Read, Update, Delete) mit Django. Die Anwendung dient als Prototyp für eine Verwaltungsanwendung und ermöglicht das Hinzufügen, Anzeigen, Aktualisieren und Löschen von Aufgaben.


Projektstruktur
Unsere Django-Anwendung besteht aus folgenden Komponenten:
1.	Projekt: Das Django-Projekt enthält die gesamte Anwendung. Hier werden die Einstellungen, URLs und globale Konfigurationen definiert.
2.	App: Die App innerhalb des Projekts ist für die spezifische Funktionalität verantwortlich. In unserem Fall handelt es sich um eine Aufgabenverwaltungs-App.
3.	Datenbankmodell: Das Modell definiert die Struktur der Datenbanktabelle. Wir haben ein einfaches Modell für Aufgaben erstellt.
4.	Views: Die Views sind für die Präsentation der Daten verantwortlich. Wir haben Views für das Anzeigen der Aufgabenliste und das Bearbeiten einzelner Aufgaben.
5.	Templates: Die HTML-Templates definieren das Aussehen der Webseiten. Wir haben Templates für die Listenansicht und die Detailansicht der Aufgaben.
Installation
1.	Virtuelle Umgebung erstellen:
2.	python3 -m venv myenv
3.	source myenv/bin/activate
4.	Django installieren:
5.	pip install django
6.	Projekt erstellen:
7.	django-admin startproject mysite
8.	cd mysite
9.	App erstellen:
10.	python manage.py startapp blog


Datenbankmodell
In der tasks/models.py-Datei haben wir das Modell für Aufgaben definiert:
from django.db import models

class Task(models.Model):
    title = models.CharField(max_length=200)
    description = models.TextField()
    completed = models.BooleanField(default=False)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    def __str__(self):
        return self.title
Views
In der tasks/views.py-Datei haben wir Views für die Aufgabenliste und die Detailansicht erstellt:
from django.shortcuts import render, get_object_or_404
from .models import Task

def task_list(request):
    tasks = Task.objects.all()
    return render(request, 'tasks/task_list.html', {'tasks': tasks})

def task_detail(request, pk):
    task = get_object_or_404(Task, pk=pk)
    return render(request, 'tasks/task_detail.html', {'task': task})
URLs
In der tasks/urls.py-Datei haben wir die URLs für unsere Views definiert:
from django.urls import path
from . import views

urlpatterns = [
    path('', views.task_list, name='task_list'),
    path('<int:pk>/', views.task_detail, name='task_detail'),
]

Templates
Die HTML-Templates befinden sich im tasks/templates/tasks/-Verzeichnis. Wir haben Templates für die Listenansicht (task_list.html) und die Detailansicht (task_detail.html) erstellt.
Lokale Ausführung
Die App kann lokal ausgeführt werden, indem Sie den Django-Entwicklungsserver starten:
python manage.py runserver
Besuchen Sie dann http://localhost:8000/ in Ihrem Browser, um die Aufgabenliste anzuzeigen.
Literatur
•	Django-Dokumentation: Offizielle Dokumentation mit umfassenden Informationen zu Django.
•	Django-Superkraft: Eine CRUD-Web-App in 60 Minuten: Ein Tutorial zur Erstellung einer CRUD-App.
•	Building a Django CRUD application in minutes: Ein weiteres Tutorial zur Erstellung einer CRUD-App.

