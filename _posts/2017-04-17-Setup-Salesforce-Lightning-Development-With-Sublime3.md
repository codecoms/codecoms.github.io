---
layout: post
title:  "Salesforce Lightning development with Sublime 3"
subtitle: "Guide on how to setup Sublime 3 to develop in Salesforce Lightning"
date:   2017-04-17 20:12:22
author: "Federico"
comments: true
tags:
  - Blog
  - Salesforce
  - How to
  - Lightning
  - Development
  - Coding
categories: Blog
---

Lightning is an awesome (relatively) new framework to develop Salesforce applications. Started in 2012 it's now the new standard in how to develop in Salesforce.

If you're using Salesforce you're using Lightning without knowing it.

### Brief Introduction to Lightning
- Lightning is an **Experience**, a **Framework** and an **Ecosystem**
- Built on the [Aura Framework](http://documentation.auraframework.org/auradocs)
	- Aura is an open-source UI framework that we use to build the Salesforce Lightning Experience UI
	- Aura was built for Salesforce, but it can be used by any developer
	- Aura components use four languages: XML, CSS, JavaScript, and Java
	- Aura powers Lightning Experience

- Lighting is designed to follow an app-centric model
- Lightning Components and Applications come in "Bundles" that store all of the necessary files to run Reusable, single-page applications

If you're reading this article probably you already know about Lightning. So without further ado I'll get to the subject of this blog. How do you setup Sublime 3 to develop Lightning applications?

Here is how you do it.

## Pre Requisite
1. Sublime 3 with the [Package Manager](https://packagecontrol.io) installed
2. The latest OSX

## Setup
1. Download the [Force CLI](https://www.force-cli.heroku.com) executable from Heroku
2. Open a terminal window, go to the downloaded file and make it executable typing `chmod 777`
3. Copy/move the executable in the folder `/usr/local/bin`
4. Install the following plugin: **Fix Mac Path** and **Lightning**
5. Restart Sublime
6. Create a new folder where you want the Lightning code to reside
7. Open the folder just created form the `Open Files` sidebar right click on the folder. A menu will appear, chose `Lightning`->`Salesforce Login`
8. Login to the Salesforce org as shown in the picture below
9. You're ready rock and roll!!

## How it works
1. Access the the menu by right click on your folder of choice
2. Select `Fetch` and then select the component and/or app you want to modify
3. Select `Add` to add a controller and/or a helper
4. Select `Create` to create an `App`, a `Component` or an `Interface`
5. Your code will be synced on save

