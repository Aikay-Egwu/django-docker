# django-docker
Django configuration to run in a docker container with postgres database
###### https://testdriven.io/blog/dockerizing-django-with-postgres-gunicorn-and-nginx

# Set up
###### 1. Start by running 
docker-compose run web django-admin startproject core . 

###### make entry point executable
chmod +x config/python/entrypoint.sh

###### 2. Spin up the images
docker-compose up -d

###### 3. In settings.py, import os
import os

###### 4. Set SECRET_KEY to env 
SECRET_KEY = os.environ.get("SECRET_KEY")

###### 5. Set the value for debug
DEBUG = int(os.environ.get("DEBUG", default=0))

###### 6. Add allowed hosts
ALLOWED_HOSTS = os.environ.get("ALLOWED_HOSTS").split(",")

###### 7. Adjust database credientails
"ENGINE": os.environ.get("SQL_ENGINE", "django.db.backends.sqlite3"),
"NAME": os.environ.get("POSTGRES_DB", BASE_DIR / "db.sqlite3"),
"USER": os.environ.get("POSTGRES_USER", "user"),
"PASSWORD": os.environ.get("POSTGRES_PASSWORD", "password"),
"HOST": os.environ.get("SQL_HOST", "localhost"),
"PORT": os.environ.get("SQL_PORT", "5432"),

###### 8. Migrate the database
docker-compose exec web python manage.py migrate --noinput

###### 9. You can enter your database environment using the command
docker-compose exec db psql --username=database_user --dbname=database_name
*\l* List databases
*\c* Check your connection
*\dt* List of relations
*\q* Quit




## Production