arquivos do projeto views.py + urls.py + sgi.py ok

arquivo para personalizar o projeto pasta de origem "asyncviews"

views.py

import asyncio
from time import sleep
import httpx
from django.http import HttpResponse

async def http_call_async():
    for num in range(1, 6):
        await asyncio.sleep(1)
        print(num)
    async with httpx.AsyncClient() as client:
        r = await client.get("https://httpbin.org/")
        print(r)

def http_call_sync():
    for num in range(1, 6):
        sleep(1)
        print(num)
    r = httpx.get("https://httpbin.org/")
    print(r)

async def async_view(request):
    loop = asyncio.get_event_loop()
    loop.create_task(http_call_async())
    return HttpResponse("Non-blocking HTTP request")

def sync_view(request):
    http_call_sync()
    return HttpResponse("Blocking HTTP request")

def home_view(request):
    return HttpResponse("<br> Aula 5: Views Assincronas com Django Async Views OK <br> 127.0.0.1:8000/ home_view pagina inicial OK<br>127.0.0.1:8000/api/ Non-blocking HTTP request OK <br>127.0.0.1:8000/sync/ Blocking HTTP request OK ")

xxx

arquivo para personalizar o projeto pasta de origem "asyncviews"
urls.py

from django.contrib import admin
from django.urls import path
from . import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('api/', views.async_view),
    path('sync/', views.sync_view),
    path('', views.home_view),  # Adicione esta linha
]

xxx

arquivo para personalizar o projeto pasta de origem "asyncviews"

asgi.py

import os

from django.core.asgi import get_asgi_application

os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'asyncviews.settings')

application = get_asgi_application()

xxx

"C:\Users\"nome-do-seu-pc-aqui-dentro","\pasta-do-projeto-aqui","pasta-do-exercicio-aqui"

"C:\Users\VENDASS\a_a_a\ebac"

-criar pasta da "ebac" no diretório do pc 

criar a pasta do projeto ou onde esta o seu projeto mysite
-ebac -----------------------mkdir mysite

voltar uma pasta
-ebac -----------------------cd ..

criar a pasta assincrona
-ebac -----------------------mkdir async-views

limpar cmd
-ebac async-views -----------cls

criar o ambiente virtual
-async-views ----------------python -m venv env

ativar o ambiente virtual
-async-views ----------------env\Scripts\activate

limpar cmd
-(env) asnc-views -----------cls

olhar a versão do python instalada
-(env) asnc-views -----------python --version

resposta da maquina
= RESPOSTA python 3.9.6

* criar o projeto agora

instalar as dependências do python
-(env) asnc-views -----------pip install django

cria o projeto
-(env) asnc-views -----------django-admin startproject asyncviews .

limpar cmd
-(env) asnc-views -----------cls

listar pastas do diretorio
-(env) asnc-views -----------dir

*pasta aberta
(
asyncviews
env
db.sqlite3
manage.py
)

migrar oque foi feito no projeto
-(env) async-views ----------python manage.py migrate

rodar o projeto usando o django
-(env) async-views ----------python manage.py runserver

instalar o pacote
-(env) async-views ----------pip install uvicorn

instalar o pacote
-(env) async-views ----------pip install httpx

rodar o projeto usando o uvicorn
-(env) async-views ----------uvicorn --reload asyncviews.asgi:application

caminho web
*127.0.0.1:8000

("pagina_inicial")

caminho web
*127.0.0.1:8000/api

("Non-blocking HTTP request")

caminho web
*127.0.0.1:8000/sync/

("Blocking HTTP request")

fim do projeto

ativar projeto
pasta raiz 
cmd
-async-views -------------python -m venv env
-async-views -------------env\Scripts\activate
-(env) async-views -------pip install -r requirements.txt
-(env) async-views -------pip install django
-(env) async-views -------pip install uvicorn
-(env) async-views -------pip install httpx
-(env) async-views -------python manage.py migrate
-(env) async-views -------uvicorn --reload asyncviews.asgi:application

