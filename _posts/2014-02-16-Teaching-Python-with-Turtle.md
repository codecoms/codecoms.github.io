---
layout: post
title:  "Teaching Python with a Turtle’s aid"
subtitle: "Use Turtle to teach Python to kids"
author: "Federico"
date:   2014-02-16 20:20:40
comments: true
tags:
  - Python
  - Programming
categories: Python

---


Let’s start by saying that I don’t want to start a religious war. I like Ruby but I also like Python. These two languages are very good in their own right and are equally powerful and useful.
Personally I have a slight preference for Ruby. I find it more whimsical and more “creative” than Python. Having said that this trait can also be a downside.

The story goes as follow: I was looking for a programming language to teach to my 8-year-old son (it’s never too early to start). So, after having done some research few trial and errors I decided to teach him Python. Why? 

Here is why:

Python’s has “Turtle” a Logo-style interactive graphic shell when you can write commands and make geometric shapes. The child sees his/her results right away. Instant gratification. You can combine a geometry lesson with a programming lesson all at once.
Python’s syntax is quite rigid and there is only one (right) way to do things. This is good for a beginner, less room for error.
Python’s is very clean and easy to read.
I always wanted to learn more about it so it was a good excuse for me to start.
This is my first lesson: drawing a square and a triangle with Turtle.
My son liked it a lot and had fun doing it. After we finished he asked me to keep going with the programming lessons.

The result as appears on the screen:

![Fig.1](http://paini.org/codecoms/wp-content/uploads/2014/02/turtle.png)
<p align="center">Fig.1 - This is the screen capture of the executed code <br> </p>


##The source code:

{% highlight python %}

#!/usr/bin/python

import turtle

#new Turtle object
wn = turtle.Screen()
wn.title("Shapes")

#craete a square object
square = turtle.Turtle()
square.color("green")
square.pensize(1)

#craete a rectangle object
rectangle = turtle.Turtle()
rectangle.color("red")
rectangle.pensize(3)

#exercise: draw a square
square.forward(100)
square.right(90)
square.forward(100)
square.right(90)
square.forward(100)
square.right(90)
square.forward(100)

rectangle.penup() #list the pen from the canvas
rectangle.forward(100) #move the pen forward
rectangle.pendown() #place the pen down for writing

#exercise: draw a rectangle
rectangle.forward(100)
rectangle.right(90)
rectangle.forward(50)
rectangle.right(90)
rectangle.forward(100)
rectangle.right(90)
rectangle.forward(50)

turtle.exitonclick() #makes the shell exit on click

{% endhighlight %}

##Resources

A couple of good links to start if you want to know more about either Python or Turtle:

 * [pythonturtle.org](http://pythonturtle.org/)
 * [Turtle’s built in commands](http://www.eg.bucknell.edu/~hyde/Python3/TurtleDirections.html)
 * [Kids Coding Lesson with Python](http://www.hanginghyena.com/blog/2013/05/07/python-turtles-a-fun-way-to-introduce-kids-to-coding/)
 * [Book: Python for Kids](http://www.nostarch.com/pythonforkids)
 * [Python.org](https://www.python.org/)
 * [learnpython.org](http://www.learnpython.org/)
 * [Short programming projects for kids](http://bytes.com/topic/python/answers/40648-short-programming-projects-kids)


<p>&nbsp;</p>
{% include twitter_plug.html %}