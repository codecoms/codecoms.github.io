---
layout: post
title:  "The FizzBuzz Programming Challenge "
subtitle: "FizzBuzz Programming challenge in PHP, Python, Swift, and Objective-C"
date:   2012-03-18 14:40:59
author: "Federico"
comments: true
tags:
  - PHP
  - Code challenge
  - How-to
categories: PHP
---

I came across a March 5th post on Jeff Atwood's website <a title="Coding Horror" href="http://www.codinghorror.com" target="_blank">Coding Horror</a> title <a title="How to Hire a programmer" href="http://www.codinghorror.com/blog/2012/03/how-to-hire-a-programmer.html" target="_blank">How to hire a programmer</a>. <br>
I wasn't surprise to what he had to say.  Most people who define themselves as programmer fail to perform basic programming tasks when asked on the spot (a job interview, ouch!!). <br>
In the article Jeff talks about the "FizzBuzz" test, so I took up the challenge and tried to create the program on the spot in PHP. I'm not a professional programmer, just a passionate hobbyist coder, and it took me about 10 minutes to code and run the program (if you want to see the result go <a title="FizzBuzz" href="http://www.paini.org/federico/fizzbuzz.php">here</a>).

<strong>FizzBuzz challenge</strong>: <em>Write a program that prints the numbers from 1 to 100. But for multiples of three print "Fizz" instead of the number and for the multiples of five print "Buzz". For numbers which are multiples of both three and five print "FizzBuzz".</em>

This is my code in. I admit is not the most elegant solution but it does the trick.

PHP:
{% highlight php %}

for ($i = 1; $i <= 100; $i++) {

  if (is_int($i/3) && is_int($i/5)) {
      print "FizzBuzz! <br> \n";
  }elseif (is_int($i/3)){
      print "Fizz! <br>";
  }elseif  (is_int($i/5)){
      print "Buzz! <br> \n";
  } else {
      print "$i <br> \n";
  }
}

?>

{% endhighlight %}


Apple Swift:

{% highlight swift %}

var three = 3
var five = 5

var n = 0

for n in 1...99 {
    if (n % three == 0) && (n % five == 0) {
        println("FizzBuzz!")
    } else if n % three == 0 {
        println("Fizz")
    } else if n % five  == 0 {
        println("Buzz")
    } else {
        println(n)
    }
    
}

{% endhighlight %}


Objective-C:

{% highlight objective-c %}
int main (int argc, const char * argv[])
 
{
 
 @autoreleasepool {
 
  int n, three = 3, five = 5;
 
  for (n=1; <=100; n=n+1) {
 
    if (n%three == 0 && n%five == 0) {
 
       NSLog(@"FizzBuzz \n");
 
    } else if (n%three == 0) {
 
      NSLog(@"Fizz \n");
 
    } else  if (n%five == 0) {
 
      NSLog(@"Buzz \n");
 
    } else {
 
      NSLog(@"%i \n",n);
 
   }
 
 }
 
}
 
return 0;
 
}

{% endhighlight %}


Python:

{% highlight python %}

#!/usr/bin/python

def FizzBuzz(number):

	for x in xrange(1, number+1):
		if (x % 3) == 0 and (x % 5) == 0:
			print "FizzBuzz!"
		elif (x % 3) == 0:
			print "Fizz"
		elif (x % 5) == 0:
			print "Buzz"
		else:
			print x

number = int(raw_input("Number Range for FizzBuzz Challenge? "))
FizzBuzz(number)

{% endhighlight %}

<p>&nbsp;</p>

{% include twitter_plug.html %}