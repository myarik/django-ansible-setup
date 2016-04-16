# Ansible playbook for deploying Django.

Ansible Playbook for setting up a Django app. This playbook installs and configures a Django application with the following technologies:

- Nginx
- Gunicorn
- Supervisor
- Virtualenv
- PostgreSQL

**OS:** Ubuntu, Debian

**Tested with Cloud Providers:** [Digital Ocean](https://www.digitalocean.com/), [Amazon](https://aws.amazon.com)

Usage
-----

First, create an inventory file for the environment, for example:

```yml
[webservers]
django_test ansible_ssh_user=test
```

Next, define variables

```yml
- git_repo: "https://github.com/myarik/demo_django_ansible_setup.git"

```

Run the playbook:

```
ansible-playbook main.yml -i server.ini
```

When doing deployments, you can simply use the `--tags` option to only run those tasks with these tags.


Role Variables
--------------

The user can specify parameters they wish to apply.

**Configuration**

* `application_name`: Application name. Defaults is `django_test`
* `application_path`: Application path. Defaults is `/opt/{{application_name}}`
* `application_static_path`: A static path. Defaults is `/opt/{{application_name}}/staticfiles`
* `application_media_path`: A media path. Defaults is `/opt/{{application_name}}/media`
* `virtualenv_path`: Application virtualenv. Defaults is `/opt/{{application_name}}/.env`
* `setup_nginx`: Install and configure nginx. Default is True
* `setup_postgresql`: Install PostgreSQL. Default is False

**Common settings**

* `main_pkg`: List of main pkgs
* `setup_zsh`: Setup zsh. Defaults is `true`.
* `git_user_name`: Git username. Defaults is django_test
* `git_email`: Git user email. Defaults is `git@django_test`


**Application settings**

* `add_pkgs`: List of additional packeges.
* `git_repo`: Git Repository
* `git_branch`: Git branch. Defaults is master
* `gunicorn_num_workers`: The number of worker processes for handling requests. Default is 2
* `gunicorn_max_requests`: The maximum number of requests a worker will process. Default is 0

**Django settings**

* `django_environment`: Django Environment variables
* `requirements_file`: Django requirement file. Default is `{{application_path}}/requirements.txt`
* `django_settings_file`: Django settings file. Default is `{{application_path}}/config/settings/production`
* `django_wsgi`: Django wsgi file. Default is config.wsgi
* `django_manage_commands`: List of django manage commands. Default is `migrate` and `collectstatic`


**PostgreSQL settings**
* `postgresql_pgtune`: Install pgtune. Default is False
* `postgresql_encoding`: Default is UTF-8
* `database_name`: Database name
* `database_user`: Database user
* `database_password`: Database password


Examples
========

For creating demo project, I used a [cookiecutter template for Django](https://github.com/pydanny/cookiecutter-django)

1) Install and configre enviroment with PostgreSQL database. *(Setup enviroment in Digital Ocean)*

`server.ini`

```yaml
[webservers]
digital_ocean_test ansible_ssh_user=root
```

```yml
vars:
  - git_repo: "https://github.com/myarik/demo_django_ansible_setup.git"
  - setup_postgresql: true
  - database_name: "demo_test"
  - database_user: "demo"
  - database_password: "demo"
  - django_environment:
      DEBUG: False
      DATABASE_URL: "postgres://demo:demo@localhost:5432/demo_test"
      DJANGO_SECRET_KEY: be&9u)d64q^@a__^1oswsezz((%li@j^5#=f!lm32n+21x!*2@
      DJANGO_ALLOWED_HOSTS: "*"
```

2) Install and configre enviroment with Sqlite database. *(Setup enviroment in AWS)*

`server.ini`

```yaml
[webservers]
aws_test ansible_ssh_user=ubuntu
```

```yml
vars:
  - git_repo: "https://github.com/myarik/demo_django_ansible_setup.git"
  - application_name: my_project
  - application_path: /home/ubuntu/{{application_name}}
  - django_environment:
      DEBUG: False
      DATABASE_URL: sqlite:////tmp/my-tmp-sqlite.db
      DJANGO_SECRET_KEY: be&9u)d64q^@a__^1oswsezz((%li@j^5#=f!lm32n+21x!*2@
      DJANGO_ALLOWED_HOSTS: "*"
```
