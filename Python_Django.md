## Commands
- Start project:
`django-admin startproject <project name>`
- Manage server
`python manage.py runserver`
- Create an app
```python manage.py startapp <app name>```


## Apps
- ```<app>/views.py``` 
- Installed app
```python
#[main]/settings.py
INSTALLED_APP = [
    '<app>.apps.<App>Config'
]

python manage.py makemigrations <app>
```
