---
layout: post
title: Rise of Containers
author: "countdigi"
tags: [ 'cloud', 'docker', 'containers', 'kubernetes' ]
---

The new year is upon us and one thing I truly look forward to is the continuing
"Rise of Containers" in 2016. I recently watched a presentation
from Bryan Cantrill entitled [Rise of Containers](https://www.youtube.com/watch?v=fcrepNIF_G0)
in which he recounts the history of the concept dating back
decades from the origin of [chroot](https://en.wikipedia.org/wiki/Chroot) moving onward to
[BSD Jails](https://en.wikipedia.org/wiki/FreeBSD_jail) and arriving
to the peak of the era perhaps all but forgotten with Solaris [Zones](https://en.wikipedia.org/wiki/Solaris_Containers).

One of my take-aways from his presentation was that container technology has been more or less
in a mature state for almost a decade prior to [Docker](https://en.wikipedia.org/wiki/Docker_(software)) entering
the scene.  But the implementation of containers during that time still involved the nuts and bolts that
have historically introduced conflicting goals between development and operations and
from which movements such as [DevOps](https://en.wikipedia.org/wiki/DevOps) have emerged
in an attempt to reconcile these opposing perspectives.

I believe Docker's key innovation has been in presenting an intuitive interface that
provides a "lingua franca" for application deployment. A developer
can work out the devil-in-the-details of packaging their application and turn it over
to operations who can easily see how it was constructed by reading the Dockerfile
which at most contains familiar Bash commands that express the steps necessary
to construct a functioning application.  Bryan makes the funny yet uncanny analogy that "Docker did to containers
what the [apt](https://en.wikipedia.org/wiki/Advanced_Packaging_Tool) package manager did to
[tar](https://en.wikipedia.org/wiki/Tar_(computing))."

With that said, when I first started playing with Docker several years ago, the systems engineering side
of my brain quickly realized that as you move from concept to real-world deployments,
the Docker model can quickly break down due to production considerations.
Connecting containers between Docker hosts who each implement their own private NAT network
was one of the obvious sore spots among others.

But with the undeniable advantages of this innovative model what we are now
seeing as we move into 2016 is the Rise of Container Cluster Management Systems to
address these challenges in real-world production environments. Docker is implementing
technologies such as [Docker Swarm](https://docs.docker.com/swarm/)  and [Universal Control
Plane](https://www.docker.com/universal-control-plane) but another one that I am really keeping
an eye on is [Kubernetes](http://kubernetes.io) from Google.

Kubernetes is an open-source container cluster management system inspired by Google's internal
system called [Borg](http://research.google.com/pubs/pub43438.html). Its an opinionated system
which maintains a core set of concepts such as [Pods](https://cloud.google.com/container-engine/docs/pods/),
[Services](https://cloud.google.com/container-engine/docs/services/),
and [Replication Controllers](https://cloud.google.com/container-engine/docs/replicationcontrollers/)
which are coordinated together in a simplified flat networking space to provide
resilient services composed from Docker containers.

I'm certain 2016 will be bring another exciting year of ongoing developments in the container space
and I am also excited to see how containers fit within High Performance Computing.
Although not a fit for every application, I believe development and operations will find
containers to more and more become the "lingua franca" when developing, testing, deploying,
and monitoring the software and services on which their organizations depend.
