---
vim: ft=markdown
layout: post
title: "A Hierachical Group Structure with Ansible"
description: "Creating a hierachical group structure with an Ansible dynamic inventory source"
comments: false
categories: devops
tags:
  - devops
  - ansible
author: "Kevin M. Counts"
blurb: "Creating a hierachical group structure with an Ansible dynamic inventory source"
---

In my new position at the University of South Florida's Health Informatics Institute,
I've had the opportunity to develop a project entitled "Deployer" to help manage the
UNIX infrastructure.

Before taking too much credit for this, in reality, deployer is fundamentally
some bash and python code running along side ansible playbooks and roles
but structured in a particular way to suit my organization's culture and workflow.

When setting up ansible for the first time and after moving beyond
examples of managing ssh or installing ntp, I seemed to hit a mental block.
I had actually been using ansible in a smaller way for over a year and had
extensive experience with Puppet, Chef and CFengine.

Ansible is a powerful and extremely flexible configuration management tool,
but in a way this creates a bit of a vacuum when deciding how to structure
a larger infrastructure project where you are thinking about how many different
components are going to interact as well as laying out some way to deploy to dev, test, and production.

But deploying ansible bare-bones and asking others to hit the ground running is not always realistic without some consideration of the environment you are coming into.

Many factors play into this including engineers who are intelligent and experienced however may lack exposure to insfrastructure-as-code methodologies.

The heart of deployer is, you might have guessed, the command `deployer`.

`deployer` is a bash wrapper around the `ansible-playbook` command which provides
some additional semantics particular to our environment.

We established our concept of an environment and this is set the `--env=<environment>` option
with a default of `dev`.

Setting `deployer`'s environment's serves several functions:

  1. Isolate ansible-playbook runs to only hosts defined within that environment within our dynamic inventory source.
  1. Allows setting the name of the environment as a group to which all other groups belong providing
     a way to define environment specific settings.
  1. Adds the variable `deployer_env` to the playbook run for conditional logic.


## Dynamic Inventory Source

In retrospect, I believe I went a little too far at first with the wrapper layer in deployer
and was starting to lose sight of the "ansible way". This included ... however my reasons
were trying to which I see on the mailing list from time to time, which is how to deal
with development, test, and production environments. Ansible is great in giving you flexibility
but as a consequence, leaves it up to you to a certain degree to put key pieces in
the right place for your particular situation.

One of the driving pressures for implementing deployer was reducing the "fear factor"
of trying out something new by engineers learning the ropes. Strategies like having multiple
git branches or directory trees to separate inventories and variables seemed too heavy weight.

I decided on continuing to utilze the wrapper concept but only and setting an environmental variable `$DEPLOYER_ENV`




the wrapper (via extra-vars, environmental variables, etc.) and started to lose sight of "the
ansible way".




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


