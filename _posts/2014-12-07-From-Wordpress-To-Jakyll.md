---
layout: post
title:  "Moving from Wordpress to Jekyll with Github Pages"
subtitle: "Guide on how to move a website from Wordpress to Jekyll hosted by Github Pages"
date:   2014-12-07 19:12:22
author: "Federico"
tags:
  - Blog
  - Jekyll
  - How to
  - Jekyll
  - Wordpress
categories: Blog
---

I recently moved my blog sites to [Github Pages](http://github.io) and [Jekyll](http://www.jekyll.org). I have to admit it, was not an easy "plug-n-play" experience.

There is a lot of informations out there but it's disjointed and not very easy to follow if you don't have already experience with Jekyll or Markdown.
In this article I'm trying to guide a new user in switching from Wordpress to Jekyll.

First off I'd like to clarify a couple of things:

1. Jekyll is not a blog software like Wordpress so do not expect something similar. <br> "*Jekyll is a parsing engine bundled as a ruby gem used to build static websites from dynamic components such as templates, partials, liquid code, markdown, etc. Jekyll is known as "a simple, blog aware, static site generator*" [See here](http://jekyllbootstrap.com/lessons/jekyll-introduction.html).
2. You need to be familiar with the terminal (CLI)
3. You to learn to use the markdown "language" (very easy). Just go [here](http://daringfireball.net/projects/markdown/syntax) and start familiarize wit it 
4. If you need a good and free markdown editor for Mac I suggest [Mou](http://25.io/mou/)
5. You need to be familiar with Git and Github and have a Github account. You can find a good resource [here](http://sixrevisions.com/resources/git-tutorials-beginners/)
6. If you host the site on [Github Pages](https://help.github.com/articles/what-are-github-pages/) your blog and content will be publicly accessible (meaning: no private content)
7. I did not find an easy and automated way to move the posts from Wordpress to Jekyll so be prepared to do some work 
8. If you want to customize the available themes you need to be familiar with HTML 5 and CSS

## What I did

These are the steps that lead me to create a local sandbox and two websites ([www.federicopaini.com](http://www.federicopaini.com) and [www.codecoms.com](http://www.codecoms.com)):

1. I read the main [Jekyll](http://www.jekyll.org) webiste and various blogs form [andrewmunsell.com](https://learn.andrewmunsell.com/learn/jekyll-by-example/tutorial), [joshualande.com](http://joshualande.com/jekyll-github-pages-poole/) and [vitobotta.com](http://vitobotta.com/how-to-migrate-from-wordpress-to-jekyll/)
2. After that my head was spinning and I still did not understand how the thing worked so I proceeded doing the following: 
   * I installed Jekyll on my MackBook Pro by typing `sudo gem install jekyll`
   * I created a basic vanilla site to use as a sandbox by going into my Document folder and typing `jekyll new test-jeckyll-site`. Jekyll  created a directory with a folder named  "test-jackyll-site" with a bunch of files in it
   * I cd in that directory and typed `jekyll serve`
   * I went to my browser and looked at the address posted in the terminal: `http://127.0.0.1:4000`
   * I created a Github empty repository named `federicopaini.github.io` and sync it with my  MacBook using the [Github for Mac](https://mac.github.com/) app 
   * I looked for a nice [theme](http://jekyllthemes.org/) and the I downloaded, unzipped, and copied it in my sandbox
   * Run `jekyll serve` and verified that the theme was rendered correctly
   * Modified the template according to the instructions 
   * Copied a couple of old posts from my Wordpress site, turned them into "markdown" `.md or .markdown` files and then moved the .md posts into the `_post` folder 
   * Checked that the posts were rendered correctly on `http://127.0.0.1:4000`
   * Once the sandbox is ready and working I then copied the files from the sandbox to my local Github folder `federicopaini.github.io` 
   * Run `jekyll serve` to make sure no error were present. (**Note:** remember to kill off the running Jekyll instance otherwise you get an port conflict error)
   * Committed and synched the code into Github via the app
   * Directed my browser to `http://federicopaini.github.io` and watched my blog come to life 
   * Lastly I directed my domain `federicopaini.com` to `federicopaini.github.io` as explained very clearly in this article: [Setting up a custom domain with GitHub Pages](https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages/)
   
   
The basic site was there in plain view, working fine. Finally We're getting somewhere. 

<br>
![Fig.1](http://www.paini.org/federico/imgs/blog-imgs/Basic-Jekyll-Site-Rendered.png)
<p align=center>Fig.1 If you see this that means everything is A-OK!</p>
<br>

##How Jekyll works

On a basic level Jekyll will do it's magic any time you place a markdown file (in my case a blog post) on the `_post` directory. 
Naturally there is a lot more than that but this is a good start. You can try creating articles and put them in the `_post` directory. Assuming Jekyll is running you will see that Jekyll generate a message in the terminal similar to this: <br>

`Regenerating: 1 files at 2014-12-05 00:04:49 ...done.`. <br>

That's the sign your new article is ready to be presented in the browser. If there are any errors you'll see them in the terminal. Just follow the error message and you should be able to fix them pretty quickly.

The directory structure varies according to the theme you chose but the basic structure is as follows:

```
_config.yml
_includes
 _layouts
_posts
_sass
about.md
css

.
├── _config.yml
├── _includes
├── _layouts
|   ├── default.html
|   └── pages.html
|   └── post.html
├── _posts
|   ├── 2014-01-01-first-post.markdown
|   └── 2014-02-20-some-blog-post.md
├── _sass
├── _site
├── about.md
├── css
├── feed.xml
└── index.html

```

Jekyll uses the [Ruby](https://www.ruby-lang.org/en/) based [Liquid Templating Language](http://liquidmarkup.org/) to process templates. 

I already explained the `_post` directory. Regarding the others here is a brief introduction:
 
 * **_confic.yml**: this is the directory in which are saved all the configuration files. Here is where all the site variable are located. if, for example, `my_string: "string"` is saved in `_config.yml`, you can access the value in a page by using {{ site.my_string }}. 
 * **_includes**: Here you can include HTML files and these will be used when you post. In my site I have the file `twitter_plug.html` and I reference it by including it  at the end of each post article between curly brackets \{\% twitter_plug.html \}\% (remove the "\").
 * **_layouts**: This is the folder for the templates layout (header, footer, etc..). It is possible to have many different layouts for different pages.
 * **about.md**: This is the equivalent of a "page" in Wordpress. The layout of this markdown file is a little different then a port (see below). If you want to add another simply copy the file and change the `title:` and the `permalink:`.   

##Markdown Page File Template

```
---
layout: page
title: About
permalink: /About/
---

This is the base Jekyll theme. You can find out more info about customizing your Jekyll theme, as well as basic Jekyll usage documentation at [jekyllrb.com](http://jekyllrb.com/)

You can find the source code for the Jekyll new theme at: [github.com/jglovier/jekyll-new](https://github.com/jglovier/jekyll-new)

You can find the source code for Jekyll at [github.com/jekyll/jekyll](https://github.com/jekyll/jekyll)

```

   
##Markdown Post File Template

```
---
layout: post
title:  "Some Title"
subtitle: "Explanation"
author: "Name"
date:   2014-12-02 20:20:40
tags:
  - template
categories: sample

---


Markdown and/or HTML text here

\{\% twitter_plug.html \}\%

```   
   
Enjoy!


<p>&nbsp;</p>
{% include twitter_plug.html %}
  
