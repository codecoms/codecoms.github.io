---
vim: ft=markdown
layout: post
title: "A Hierachical Inventory with Ansible"
description: "Creating a hierachical group structure with an ansible dynamic inventory"
comments: false
categories: devops
tags:
  - devops
  - ansible
author: "Kevin M. Counts"
blurb: "Creating a hierachical group structure with an ansible dynamic inventory"
---

## toc

  - current environment
    - challenges
    - dev, test, prod
    - ansible inventory
      - ini file
      - dynamic inventory
        - Jeroen Hoekx: https://github.com/jhoekx/ansible-yaml-inventory/blob/master/yaml-hosts.py



## scratch


Ansible provides an enormous amount of flexibility, probably the most I've seen in a configuration management system.

Although its all fine and good to bring in a "devops" system, it can be very challenging especially when others
in the environment, although bright and highly technical, have not been exposed to the devops culture as deeply
as I have.

One of the pain points I ran into for organizing an ansible deploy in the environment was developing an
inventory view that made sense.

This was also paired with a common question asked on the ansible mailing list on how to structure dev, test, and production.

I actually tried controlling dev, test, and production by utilizing a wrapper around ansible called 'deployer'.

I believe having a wrapper script can be a idea, but I was trying to grab hold of more than I should of and
was feeling friction against the "ansible way"

What I did end up doing was using a deployer script which had a few key options:

  --env=<environment> (default: dev)

We chose a short version of `env` because the  keyword `environment` is used in
ansible plays to specify UNIX environmental variables for modules like `command` and `shell`.

Within the deployer script, `$DEPLOYER_ENV` is then set (which will be passed to the dynamic
inventory command) and actually added to ansible-playbook
via `--extra-var='deployer_env=<environment>'` on the command line so this variable is available
to all playbooks runs. With that said, ansible does a pretty good job if you follow the
"ansible way" of having default behaviours that let you put a host in dev, test, or prod
so we may not need `deployer_env` but it made sense to me to make it available for an outlier situation
within a playbook.

One thing to note is by default, if you don't specifiy an environment deployer will
set `$DEPLOYER_ENV` to `dev`.

You will be in the development `dev` environment and with a correctly configured `groups.yml` you can feel safe to run something
which will only run the playbook on your development machines.

Additional ansible-playbook options may be added following a `--`, e.g.:

    $ deployer --env=test --playbook=nagios -- --list-tasks

    $ cat config/groups.yml

    #========================================================================
    # Development Environment
    #========================================================================

    dev:
      sso:
        sso_master: %user%1.foobar.org
        sso_secondary: %user%2.foobar.org

      nagios:
        nagios_master: %user%5.foobar.org

      frontend:
        frontend_master: %user%1.foobar.org
        frontend_secondary: %user%2.foobar.org

      sasgrid:
        sasgrid_md: %user%1.foobar.org
        sasgrid_node:
          - %user%1.foobar.org

      hadoop:
        hadoop_nn: %user%1.foobar.org
        hadoop_snn: %user%2.foobar.org
        hadoop_yarn: %user%2.foobar.org
        hadoop_hive: %user%2.foobar.org
        hadoop_db: %user%2.foobar.org
        hadoop_dn:
          hadoop_dn1: %user%3.foobar.org
          hadoop_dn2: %user%4.foobar.org

    #========================================================================
    # Test Environment
    #========================================================================

    test:
      sso:
        sso_master: systest1.foobar.org
        sso_secondary: systest2.foobar.org

      nagios:
        nagios_master: systest5.foobar.org

      frontend:
        frontend_master: systest1.foobar.org
        frontend_secondary: systest2.foobar.org

      sasgrid:
        sasgrid_md: systest1.foobar.org
        sasgrid_node:
          - systest1.foobar.org

      hadoop:
        hadoop_nn: systest1.foobar.org
        hadoop_snn: systest2.foobar.org
        hadoop_yarn: systest2.foobar.org
        hadoop_hive: systest2.foobar.org
        hadoop_db: systest2.foobar.org
        hadoop_dn:
          hadoop_dn1: systest3.foobar.org
          hadoop_dn2: systest4.foobar.org

[hadoop]


---
layout: post
title: "An Opinionated Ansible Layout"
description: "An Introduction to Pyenv"
comments: true
categories: devops
tags:
  - devops
  - ansible
author: "Kevin M. Counts"
blurb: >
  Setting up a top-level project for managing your infrastructure with a configuration
  management system can take many forms. This post illustrates an opinionated layout
  for ansible.
---

- [ansible best practices directory layout](http://docs.ansible.com/playbooks_best_practices.html#directory-layout)

```
<project-root>
  - Makefile
  - Vagrantfile
  - config/
  - packer/
  - ansible/
    - roles/
    - site/
      - sys/
          - main.yml
          - dev/
             - vars
             - inventory

```

Site Directory

```
- site/
    - <site-name>
      - main.yml <-- (playbook)
      - <env>
        - inventory
        - vars


Convenience symlink directories.

  - site -> ansible/site
  - roles -> ansible/roles
  - vars -> ansible/vars
  - tasks -> ansible/tasks

- Command-T for VIM

