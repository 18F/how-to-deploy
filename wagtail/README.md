## How to deploy Wagtail to Cloud Foundry

### What is Wagtail?

[Wagtail](https://wagtail.io/) is a CMS written in Python.

### Steps

Generate A Wagtail Project

- Install wagtail by running: `pip install wagtail`
- Run `wagtail start <your_site_name>`
- `cd <your_site_name>`

#### Create user

We will create a user by pushing a local sqlite file with a created account.

  - `python manage.py migrate && python manage.py createsuperuser --username testuser --email test.user@email.gov`
  - Create the password for the account
(_Do not do this for production sites_)

#### Add a Procfile to the root of your project
```
web: python manage.py migrate && python manage.py runserver $HOST:$PORT
```

_Note: This will create a new superuser every deploy for now_

#### Deploying
- `cf push <your_app_name> -b https://github.com/cloudfoundry/python-buildpack#v1.5.1`
