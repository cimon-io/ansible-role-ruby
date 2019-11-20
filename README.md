# Ansible ruby role

An ansible role that installs and configures Ruby with rbenv.

The role includes the following tasks:

1. Install necessary ruby dependencies specified by the `ruby_software_dependencies` variable.
2. Install/update rbenv as `ruby_user` at `$HOME/.rbenv`.
3. Install ruby-build plugin at `$HOME/.rbenv/plugins`.
4. Append rbenv bin to the PATH variable.
5. Initiate rbenv for ssh sessions.
6. Install ruby versions listed in the `ruby_versions` variable. Set the required `ruby_global_version` as global.
7. Install/update RubyGems.

This role can be run under all versions of Ubuntu and Debian.

## Requirements

None

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
ruby_user: deploy    # A user for whom ruby is installed
ruby_group: deploy   # The user name and group must be present in the system
```

Specify rbenv and ruby versions which should be installed:

```yaml
ruby_rbenv_version: "v1.1.2"  # rbenv version
ruby_versions:                # list of ruby versions
  - "2.6.4"
```

The first of the requested ruby versions (if there is any) will be set as global:

```yaml
ruby_global_version: "{{ ruby_versions[0] | default('') }}"

ruby_global_gems: []    # list of ruby global gems to install
```

All necessary dependencies and other variables are specified at `vars/main`:

```yaml
ansible_become: yes

apt_cache_valid_time: 86400

ruby_software_dependencies:
  - build-essential
  - libcurl4-openssl-dev
  - libmysqlclient-dev
  - libreadline-dev
  - libreadline6-dev
  - libssl-dev
  - libxml2-dev
  - libxslt1-dev
  - zlib1g-dev
  - libmagickwand-dev
```

## Dependencies

 - Role: [users]() - an ansible role for managing user and group accounts. A list of `users_accounts` must include a user with a name and a group equal to `ruby_user` and `ruby_group` variables respectively.

## Example Playbook

A playbook example:

```yaml
- hosts: web
  roles:
    - role: ruby
      ruby_versions:
        - "2.6.3"
        - "2.6.4"
```

An example of variables:

```yaml
ruby_user: developer           # A user under whom the role is run
ruby_group: developer          # The user name and group must be present in the system
ruby_versions: ["2.5.3", "2.6.4"]  # Ruby version which will be installed
```

## License

Licensed under the [MIT License](https://opensource.org/licenses/MIT).
