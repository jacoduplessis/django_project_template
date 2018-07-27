# A Django project

## Setup

1. Create virtual environment. The location is significant — it must be called `venv` and be
placed in the root project folder.

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

5. Run server

```
./manage.py runserver
```

## Releasing

Make sure the `bumpversion` tool is available. Install with `pipsi` if not.

```
bumpversion {major|minor|patch}
```

This will update the version number in `setup.py` and `ansible/inventory.yml`, create a commit and create a git
tag.

For a test run to see what will happen:

```
bumpversion {major|minor|patch} --verbose --dry-run
```

## Deploy

Two playbooks — `setup` and `deploy` — are provided in `ansible` folder.

Assumes the following are installed:

- `libpq5`
- `nginx`
- `redis-server`
- `postgresql-10`

When writing scripts that run via `manage.py`, be sure to reference it as `.../venv/bin/manage.py`.

## Notes

Because the project is build as a single sdist, all templates must be within
an app - any entry to `TEMPLATE.DIRS` will not work. The same goes for
`STATICFILE_DIRS`.

Additionally, all template, static and data files need to be referenced in `MANIFEST.in`
to be included in the release.