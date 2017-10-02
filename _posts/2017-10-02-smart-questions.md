---
layout: post
title:
author: countdigi
tags: [ 'foo' ]
---

# Smart Questions

Years ago in my Linux studies I discovered Eric S. Raymond's advice on asking technical questions
entitled "[How To Ask Questions The Smart Way](http://www.catb.org/esr/faqs/smart-questions.html)".

This advice was tailored within the context of an Open Source enthusiast who often seeks out help
from other people with similar interests.

I wanted to create a short, customized version of this advice tailoring it to something I can
can quickly share with my colleagues and they can grok in under a minute:

1\. *Use Google or Stack Exchange*. Take a moment to search on the Internet.
   Also learn how to have more control over your google search
   (e.g., [Google Advance Search](https://www.google.com/advanced_search) or
    read this [lifehack.org article](http://www.lifehack.org/articles/technology/20-tips-use-google-search-efficiently.html)).


2\. *Be precise and informative about your problem*

- Describe exactly what you did (if a command-line or script error, include full command-line and output)
- Describe the environment it occurs in:
  - On what server?
  - As what user?
  - From what current working directory?
  - Any set-up steps required
- If possible, provide a way to reproduce the problem
- Describe any research you did trying to solve the issue
- Describe any diagnostic steps you took to try and pin down the problem yourself
- Do the best to anticipate follow-up questions that might be asked


3\. *Describe the goal, not the step*. Often, people who need technical help have a high-level goal in mind and get stuck on what
   they think is one particular path towards the goal. They come for help with the step, but don't realize that the path is wrong.

- Bad: "How do I get the color-picker on the FooDraw program to take a hexadecimal RGB value?"
- Good: "I'm trying to replace the color table on an image with values of my choosing. Right now the only way I can see to do
         this is by editing each table slot, but I can't get FooDraw's color picker to take a hexadecimal RGB value."


4\. *Follow up with a brief note on the solution.*

- If you figure it out yourself, share the solution with whom you previously asked.
- If you were provided a solution, give feedback especially if the solution works.
- In both cases, if you asked for help, the person helping might continue spending time researching
  because you had not shared with them the problem was already solved.

---

Examples

*Bad*: "Where can I find out stuff about the Foonly Flurbamatic?"

*Good*: "I used Google to try to find “Foonly Flurbamatic 2600” on the Web, but I got no useful hits. Can I get a pointer to
       programming information on this device?"

---

*Bad*: "I can't get the code from project foo to compile. Why is it broken?"

*Good*: "The code from project foo doesn't compile under Nulix version 6.2. I've read the FAQ, but it doesn't have anything in it
       about Nulix-related problems. Here's a transcript of my compilation attempt; is it something I did?"

---

*Bad*: "I'm having problems with my motherboard. Can anybody help?"

*Good*: "I tried X, Y, and Z on the S2464 motherboard. When that didn't work, I tried A, B, and C. Note the curious symptom when I
         tried C. Obviously the florbish is grommicking, but the results aren't what one might expect. What are the usual causes of
         grommicking on Athlon MP motherboards? Anybody got ideas for more tests I can run to pin down the problem?"


<br/>
