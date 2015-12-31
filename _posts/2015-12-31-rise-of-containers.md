---
layout: post
title: Rise of Containers
author: "countdigi"
tags: [ 'cloud', 'docker', 'containers', 'kubernetes' ]

---

The new year is upon us and one of the things I look forward to is the continuing
"Rise of Containers" in 2016. I recently watched a great [video](https://www.youtube.com/watch?v=fcrepNIF_G0)
by Bryan Cantrill in which he recounts the history of the container concept bringing us back
decades to the origin of the `chroot` system call, onward to BSD jails and finally
to the peak of the era with Solaris [Zones](https://en.wikipedia.org/wiki/Solaris_Containers) introduced in 2005.

One of the main takeaways from his presentation was technology was more or less in place
almost a decade before [Docker](https://en.wikipedia.org/wiki/Docker_(software))
was released in 2013. The problem was that implementing
it still required a similar models that developed the traditional
relationship between operations and development that the DevOps movement was trying to alleviate.

Docker's key innovation was providing an intuitive and accessible interface
that could build, store, retrieve, and run a self-contained application
with all necessary dependencies on any modern Linux system.
This model is inherently a win from both the operational and development aspect
and is why Docker has gained such momentum in such a short time. Bryan makes the funny yet
fairly accurate analogy that "Docker did to containers what the apt package manager did to tar."

As a systems engineer who inherently has the operational aspect in the back of my mind I noticed
that this win-win quickly breaks down as you move to the "real-world" of deploying applications
into a production environment across multiple nodes when I was playing with Docker in 2014.
Connecting containers between each other on remote hosts was one of the sore spots among others.

What we are now seeing as we move into 2016 is the Rise of Container Cluster Management Systems
to address these challenges in real-world production environments. Docker is implementing technologies such
as Docker Swarm and Universal Control Plane but another one that I am really keeping an eye on
is [Kubernetes](kubernetes.io) from Google.

Kubernetes is an open-source container cluster management system inspired by Google's internal
system called [Borg](http://research.google.com/pubs/pub43438.html). Its an opinionated system
which maintains a core set of concepts such as Pods, Labels, Services, and Replication Controllers
which are coordinated together in a simplified flat networking space to provide
resilient services composed of Docker containers.

I'm certain 2016 will be another exciting year and with many new developments emerging in short order.
Although not a fit for every application, I believe operations and development will find
containers to become more and more the "lingua franca" used when developing, testing, deploying,
maintaining, and monitoring the software and services of their organization.
