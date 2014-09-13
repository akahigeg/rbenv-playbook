Ansible playbook for installing ruby by rbenv.

This playbook is created on Debian 7.4.
Maybe works on RedHat.

# How to use

Fetch [rbenv-playbook/tasks/main.yml]()

## Just install

    ---
    - hosts: servers
      sudo: true
      user: vagrant
      tasks:
        - include: rbenv-playbook/tasks/main.yml

It's Default install.

## Specify the global Ruby version and install extra versions

    ---
    - hosts: servers
      sudo: true
      user: vagrant
      vars:
        global_ruby_version: 2.0.0-p247
        rbenv_other_ruby_versions: 
          - { version: "2.1.1" }
          - { version: "2.1.2" }
      tasks:
        - include: rbenv-playbook/tasks/main.yml

## Install gems for the global Ruby

    ---
    - hosts: servers
      sudo: true
      user: vagrant
      vars: 
        rbenv_global_gems:
          - { name: "bundler", version: "" }
          - { name: "pry", version: "" }
          - { name: "rbenv-rehash", version: "" }
          - { name: "nokogiri", version: "1.5.10" }
      tasks:
        - include: rbenv-playbook/tasks/main.yml

## For installing gems by multipul users without permissions conflict

    ---
    - hosts: servers
      sudo: true
      user: vagrant
      vars: 
        rbenv_extra_users: [taro, jiro, saburo]
        rbenv_keep_group_write: yes
      tasks:
        - include: rbenv-playbook/tasks/main.yml


# Vars

|var                      |required|default     |comments|
|-------------------------|--------|------------|--------|
|rbenv_root               | no     | /opt/rbenv | RBENV_ROOT |
|rbenv_user               | no     | rbenv      | User own RBENV_ROOT owner |
|rbenv_group              | no     | rbenv      | RBENV_ROOT group |
|rbenv_extra_users        | no     |            | Extra users belong to rbenv_group |
|rbenv_global_ruby_version| no     | 2.1.2      | The global Ruby version on rbenv |
|rbenv_other_ruby_versions| no     |            | Extra versions of ruby installed by rbenv |
|rbenv_global_gems        | no     | [{ name: "bunder", version: "" }] | Preinstalled gems for the global Ruby |
|rbenv_keep_group_write   | no     | no         | To keep RBENV_ROOT onwer, group and group write permission |

# Specs

This cookbook is tested by below things.

* [serverspec](http://serverspec.org/)
* [Vagrant](http://www.vagrantup.com/)

## How to run specs

    $ git clone https://github.com/akahigeg/rbenv-playbook.git
    $ cd rbenv-playbook
    $ vagrant up
    $ bundle install
    $ bundle exec rake spec
