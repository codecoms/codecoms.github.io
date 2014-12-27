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

