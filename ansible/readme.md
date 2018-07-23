
# Setting up nginx and systemd

- copy `inventory.example.yml` to `inventory.yml` and change values
- `ansible-playbook django_setup.yml -i inventory.yml -K`

# Deploying new version

- change version number in `setup.py` and `inventory.yml`
- `git tag -a "vx.x.x" -m "Release x.x.x"`
- `python setup.py sdist`
- `ansible-playbook django_deploy.yml -i inventory.yml -K`