# A Django project

## Setup

1. Create virtual environment. The location is significant.

- `python3.6 -m venv venv`
- `source venv/bin/activate`
- `pip install -U pip`
- `pip install -e .`

2. Create database and user

- `createdb -h 127.0.0.1 -U postgres {{ project_name }}`
- `createuser -h 127.0.0.1 -U postgres -P {{ project_name }}` (enter password)

3. Edit .env to add the following

- `DJANGO_SETTINGS_MODULE={{ project_name }}.settings.local`
- `DATABASE_URL=postgres://{{ project_name }}:password@127.0.0.1/{{ project_name }}`

4. Prepare database

- `./manage.py migrate`
- `./manage.py createsuperuser`

4. Run server

```
./manage.py runserver
```


## Deploy

Two playbooks — `setup` and `deploy` — are provided in `ansible` folder.

Assumes the following are installed:

- `libpq5`
- `nginx`
- `redis-server`
- `postgresql-10`

## Notes

Because the project is build as a single sdist, all templates must be within
an app - any entry to `TEMPLATE.DIRS` will not work.