# django-ansible-setup
Ansible Playbook for setting up a Django app with Virtualenv, Supervisor, Nginx, Gunicorn, PostgreSQL and Redis.


This playbook installs and configures a Django application. The user can specify parameters they wish to apply.

Role Variables
--------------
*Configuration*

* `application_name`: Application name. Defaults is `django_test`
* `application_path`: Application path. Defaults is `/opt/{{application_name}}`

*Common settings*

* `main_pkg`: List of main pkgs
* `setup_zsh`: Setup zsh. Defaults is `true`.
* `git_user_name`: Git username. Defaults is django_test
* `git_email`: Git user email. Defaults is `git@django_test`


*Application settings*

* `add_pkgs`: List of additional packeges.
* `git_repo`: Git Repository
* `git_branch`: Git branch. Defaults is master
* `virtualenv_path`: Application virtualenv. Defaults is `/opt/{{application_name}}/.env`
* `gunicorn_num_workers`: The number of worker processes for handling requests. Default is 2
* `gunicorn_max_requests`: The maximum number of requests a worker will process. Default is 0

*Django settings*

* `django_environment`: Django Environment variables
* `requirements_file`: Django requirement file. Default is `{{application_path}}/requirements.txt`
* `django_settings_file`: Django settings file. Defaulr is {{application_path}}/config/settings/production.py
* `django_wsgi`: Django wsgi file. Default is config.wsgi
* `django_manage_commands`: List of django manage commands. Default is migrate and collectstatic
