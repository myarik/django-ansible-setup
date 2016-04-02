# django-ansible-setup
Ansible Playbook for setting up a Django app with Virtualenv, Supervisor, Nginx, Gunicorn, PostgreSQL and Redis.


This playbook installs and configures a Django application. The user can specify parameters they wish to apply.

Role Variables
--------------
* `main_pkg`: List of main pkgs
* `setup_zsh`: Setup zsh. Defaults is `true`.
* `project_name`: Project name. Defaults is `django_test`
* `git_user_name`: Git username. Defaults is project_name
* `git_email`: Git user email. Defaults is `git@project_name`
