# django-docker
Django configuration to run in a docker container with postgres database

# Set up
1. Start by running 
docker-compose run web django-admin startproject core . 

2. Spin up the images
docker-compose up -d

3. In settings.py, import os
import os

4. Set SECRET_KEY to env 
SECRET_KEY = os.environ.get("SECRET_KEY")

5. Set the value for debug
DEBUG = int(os.environ.get("DEBUG", default=0))

6. Add allowed hosts
ALLOWED_HOSTS = os.environ.get("ALLOWED_HOSTS").split(",")

7. Adjust database credientails
"ENGINE": os.environ.get("SQL_ENGINE", "django.db.backends.sqlite3"),
"NAME": os.environ.get("SQL_DATABASE", BASE_DIR / "db.sqlite3"),
"USER": os.environ.get("SQL_USER", "user"),
"PASSWORD": os.environ.get("SQL_PASSWORD", "password"),
"HOST": os.environ.get("SQL_HOST", "localhost"),
"PORT": os.environ.get("SQL_PORT", "5432"),