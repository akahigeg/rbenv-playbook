Ansible playbook for installing ruby by rbenv.

This playbook is created on Debian 7.4.

# How to use

Fetch [rbenv-playbook/tasks/main.yml]()

    ---
    - hosts: servers
      sudo: true
      user: vagrant
      vars:
        rbenv_root: /opt/rbenv
        rbenv_user: rbenv
        rbenv_group: rbenv
        rbenv_global_ruby_version: 2.1.2
      tasks:
        - include: rbenv-playbook/tasks/main.yml


# Vars

|var|required|default|choices|comments|
|---|--------|-------|-------|--------|
|rbenv_root| /opt/rbenv
|rbenv_user| rbenv
|rbenv_group| rbenv
|rbenv_extra_users| [vagrant]
|rbenv_global_ruby_version| 2.1.2
|rbenv_other_ruby_versions |
  - { version: "2.1.1" }
|rbenv_global_gems|
  - { name: "bundler", version: "" }
  - { name: "pry", version: "" }
  - { name: "rbenv-rehash", version: "" }
  - { name: "nokogiri", version: "1.5.10" }
|rbenv_keep_group_write_by_cron| yes

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
