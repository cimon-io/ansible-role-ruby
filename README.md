Ruby role
=========

An Ansible Role that installs ruby with rbenv.

Requirements
----------------

None.

Role Variables
----------------

Available variables are listed below, along with default values (see `defaults/main.yml`):

```
deploy_user: deploy
deploy_group: deploy
deploy_home_dir: "/home/deploy"

ruby_version: 1.9.3-p484
rbenv_root: "/home/deploy/.rbenv"
```

Install ruby version `ruby_version` for `deploy_user` user. Rbenv will be installed to `rbenv_root` folder.


Dependencies
----------------

Role: `deploy-user`.

Example Playbook
----------------

Example:

    - hosts: web
      roles:
         - role: ruby
           ruby_version: 2.2.4

License
-------

MIT

