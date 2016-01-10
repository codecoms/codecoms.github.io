---
layout: post
title:  Using Docker with Jekyll
author: countdigi
tags: [ docker, jekyll ]
---

We are using [Jekyll](https://jekyllrb.com/), a static blog generator, for [Codecoms.com](http://codecoms.com),
a site I maintain with a friend of mine as well as for my own [personal blog](http://digicat.org).

Jekyll is a pretty intuitive system and is supported by GitHub for dynamic page generation. All
you have to do is create a repository named `<username>.github.io` on GitHub and
it will automatically [compile and publish your blog](https://help.github.com/articles/using-jekyll-with-pages/).

While writing your articles, its convenient to have a local Jekyll environment running so you can edit and
quickly view your articles to get feedback on the look and feel. Although not rocket science, it
can be a little tough to install ruby, install the correct Gems and get everything running locally
especially if you are not familiar with the Ruby ecosystem.

Fortunately there is an official [Jekyll Docker Image](https://github.com/jekyll/docker) which really helps out with this.

Trying to simplify this even more I wrote a small utility script called
[bin/docker-run](https://github.com/codecoms/codecoms.github.io/tree/master/bin/docker-run)
that we added into our repository which encapsulates this into a quick script we can run on any system with Docker installed.

I added in options to cache all the libraries locally so after you run the script the first time it
will be quicker to restart the service. It can run the jekyll server in the foreground, background,
or simply compile the pages into the `_site` directory and you can sync them to any site you would like.

Make sure you add the following files to your `.gitignore` so that all of the Gems and generated
pages do not end up in your repo:

    _site
    vendor
    .bundle

I am choosing to run this in the foreground with the argument `fg` in a side terminal so I can
watch changes compile as I make them but the script also supports the arguments `bg` for
running Jekyll in the background or `build` to not run any server but simply build the artifacts.

    $ bin/docker-run fg

    Unable to find image 'jekyll/jekyll:latest' locally
    latest: Pulling from jekyll/jekyll
    c55d493d33bc: Pull complete
    8d3cc6ac7e3a: Pull complete

    .... lots of gems....

    Using github-pages 39
    Using libv8 3.16.14.13
    Using ref 2.0.0
    Using therubyracer 0.12.2
    Using bundler 1.10.6
    Bundle complete! 4 Gemfile dependencies, 58 gems now installed.
    Bundled gems are installed into ./vendor/bundle.
    Configuration file: /srv/jekyll/_config.yml
                Source: /srv/jekyll
          Destination: /srv/jekyll/_site
          Generating...
                        done.
    Auto-regeneration: enabled for '/srv/jekyll'
    Configuration file: /srv/jekyll/_config.yml
        Server address: http://0.0.0.0:4000/
      Server running... press ctrl-c to stop.

At this point just point to `http://localhost:4000` and check out your site!

