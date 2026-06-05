## Инициализация проекта:

`pip install django`

`django-admin startproject mysite`

`cd mysite`

`python3 manage.py startapp mysite-app`

---

## Поменять settings.py:

```
INSTALLED_APPS = [
    'mysite_app',
]
```

---

## Прописать модели в models.py

## Скачать:

`pip install -r requirements.txt`

---

## Применить миграции:

`python manage.py makemigrations`
`python manage.py migrate`

---

## Запустить проект:

`python manage.py runserver`

---

## Создать суперюзера:

`python manage.py createsuperuser`

---

## Добавляем REST_FRAMEWORK в settings.py:

```
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework.authentication.SessionAuthentication',
        'rest_framework.authentication.BasicAuthentication',
    ],
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.IsAuthenticated',
    ],
}
```

---

## Пишем serializers.py, затем views.py

---

## В новом urls.py настраиваем url-пути

---

## В urls.py обновляем url-пути

```
urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('mysite_app.urls')),
    path('', RedirectView.as_view(url='/admin/', permanent=False)),
]
```

---

## Добавляем SWAGGER_SETTINGS и INSTALLED_APPS в settings.py:

```
SWAGGER_SETTINGS = {
    'SECURITY_DEFINITIONS': {
        'Basic': {
            'type': 'basic'
        },
    },
    'USE_SESSION_AUTH': True,
    'VALIDATOR_URL': None,
    'DEFAULT_MODEL_RENDERING': 'model',
    'DEFAULT_MODEL_DEPTH': 3,
}
```

```
INSTALLED_APPS = [
    ..,
    'drf_yasg',
]
```

---

## В urls.py обновляем url-пути

```
urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('mysite_app.urls')),
    path('', RedirectView.as_view(url='/admin/', permanent=False)),

    re_path(r'^swagger(?P<format>\.json|\.yaml)$', schema_view.without_ui(cache_timeout=0), name='schema-json'),
    path('swagger/', schema_view.with_ui('swagger', cache_timeout=0), name='schema-swagger-ui'),
    path('redoc/', schema_view.with_ui('redoc', cache_timeout=0), name='schema-redoc'),

    path('', RedirectView.as_view(url='/swagger/', permanent=False)),
]
```

---

## В views.py обновляем методы под swagger

## Добавляем линтер flake8

`pip install coverage flake8`

## Запуск линтер flake8

`flake8 mysite_app/`

## Вывод отчета о покрытии тестами

`coverage report`

## Запуск тестов с покрытием

`coverage run --source='mysite_app' manage.py test mysite_app`

## Для графического представления БД
```
pip install pygraphviz
python manage.py graph_models -a -g -o my_project_visualized.png


settings.py:
GRAPH_MODELS={
    'all_applications': True,
    'graph_models': True}
```