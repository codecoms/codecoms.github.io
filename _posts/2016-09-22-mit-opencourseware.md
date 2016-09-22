---
layout: post
title: MIT Open Courseware
author: countdigi
tags: [ 'compsci' ]
---

# MIT Open Courseware

## Overview

For many years the Massachusetts Institute of Technology has offered
[MIT Open Courseware](https://ocw.mit.edu/) with thousands of lectures freely available online.
In tribute here is a transcript of the opening part of a 1986 MIT Lecture for Hewlett Packard engineers
based on this ["spell-casting tome"](https://mitpress.mit.edu/books/structure-and-interpretation-computer-programs).

## Transcript

[Hal Ableson](https://en.wikipedia.org/wiki/Hal_Abelson) presenting [Lecture 1A, MIT 6.001 Structure and Interpretation](https://youtu.be/2Op3QLzMgSY):

I would like to welcome you to this course on Computer Science.
Actually that is a terrible way to start.
Computer Science is a terrible name for this business.
First of all, it is not a science.
Perhaps it might as well be named engineering or art.
For what we will see is that Computer Science has a lot in common with magic.
It is not a science about computers in the same sense that Physics is not about
particle accelerators.
And as Biology is not really about microscopes and petri dishes.
Computer Science is not about computers in the same sense that Geometry is
not really about using surveying instruments.

In fact, there is commonality between Computer Science and Geometry.
Geometry, first of all, is another subject with a lousy name.
The name comes from "Gaia" meaning the earth and "Metron" meaning to measure.
Geometry originally meant measuring the Earth or surveying.
And the reason was thousand of years ago the Egyptian priesthood developed the rudiments of Geometry
in order to figure out how to restore the boundaries of fields that were destroyed in the annual flooding of the Nile.

And to the Egyptians who did that Geometry really was the use of surveying instruments.
The reason we think Computer Science is about computers is pretty much the same reason that the Egyptians
thought Geometry was about surveying instruments.  That is when some field is just getting started
and you do not understand it very well its very easy to confuse the essence of what you
are doing with the tools that you use.  And indeed on some absolute scale of things we
probably know less about the essence of Computer Science than
the ancient Egyptians really knew about Geometry.

What do I mean by the "Essence of Computer Science" or the "Essence of Geometry?"

It is certainly true that these Egyptians used surveying instruments but when we look back on them
after a couple of thousands of years we realize the importance of what they were doing was to begin to
formalize notions about space and time.
To start a way of talking about mathematical truths formally that led to the axiomatic
method that led to modern mathematics.

Figuring out a way to talk precisely about so-called declarative knowledge, "what is true?"

Similarly, I think in the future people will look back and say, "Yes those primitives in the 20th century
were fiddling around with these gadgets called computers..." but really
what they were doing was starting to formalize intuitions about process, how to do things.
Starting to develop a way to talk precisely about "How-to" knowledge as
opposed to Geometry that talks about "What is True?"

Let me give you an example of that.

Here is a piece of mathematics that says what a square root is.
The square root of X is the number Y such that Y-squared is equal to X and Y is greater than zero.
Now that is a fine piece of mathematics but just telling you what a square root is
does not say anything about how you might go out and find one.
Let us contrast that with a piece of imperative knowledge.

This in fact also comes from Egypt.
This is an algorithm from Heron of Alexandria on how to find a square root by successive averaging.
In order to find a square root of X make a guess of the square root and improve the guess (using the formula displayed) until its good enough.
That is a method, that is how to do something as opposed to declarative knowledge that says what you are looking for.
That is a process.

So what is a process in general?  Its kind of hard to say.
You can think of it like a magical spirit that lives in the computer and does something.
And the thing that directs a process is a pattern of rules called a procedure.

A procedure are the spells if you like that controls these magical spirits that are processes.
Sorcerers using magical languages use ancient Arcadian, Sumerian, or Babylonian but we are going
to conjure our magical spirits in LISP which is a language designed for "casting the spells"
that are procedures to direct the processes.

In a few minutes I am going to teach you essentially all of the rules of LISP and you should not find that surprising.
It is the same as saying its very easy to learn the rules of Chess but of course
that is very different than saying you understand the implications of these rules and how you use those rules
to become a master chess player.

LISP is the same way. We are going to state the rules in a few minutes and it will be very easy to see
but what is real hard is the implication of those rules. How you exploit those rules to become a master programmer.
And the implications of those rules are going to take us the rest of this subject and beyond.

In Computer Science, we are in the business of formalizing how-to imperative knowledge.
How to do stuff and the real issues of Computer Science are not telling people how to do square roots.
The real problems come when we try to build very large systems. Computer programs that are thousands of pages long.
So big that no one can hold them in all in their heads once.
And the only way this is possible is that there are
techniques for controlling the complexity of these large systems and
theses techniques for controlling complexity are what this course is really about
and in some sense thats really what Computer Science is about.

Now that may see like a strange thing to say because after all a lot of people besides
computer scientists deal with controlling complexity.
A large airliner is an extremely complex system and the aeronautical engineers that design this
are dealing with immense complexity but there is a difference between that kind of complexity
and what we deal with in Computer Science.
And that is that Computer Science in some sense is not real.

You see when an engineer is designing a physical system that is made out of real parts,
the engineers that worry about that have to address problems of tolerance, approximation, and noise in the system.
For example as an electrical engineer I can easily go off and build a one stage amplifier or a two-stage amplifier and I can imagine
cascading them to build a million stage amplifier but its ridiculous to build such a thing because long
before the millionth stage the thermal noise in those components way at the beginning
is going to get amplified and make the whole thing meaningless.

Computer Science deals with idealized components.
We know as much as we want about these little program and data pieces that we are fitting together.
So we do not have to worry about tolerance and that means that in building a large program there is not all that much
difference between what I can build and what I can imagine because the parts are these abstract entities
that I know as much as I want. I know about them as precisely as I'd like so
as opposed to other kinds of engineering where the constraints on what you can build are the constraints of physical systems
, the constraints of physics and noise approximation, the constraints imposed in building large software systems
are the limitation of our own minds.

So in that sense Computer Science is like an abstract form of engineering.

It is the kind of engineering where you ignore the constraints that are imposed by reality.


