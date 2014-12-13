---
layout: post
title:  "Test Driven Development with Ruby rspec"
subtitle: "Example on how to use Ruby rspec"
date:   2013-06-13 21:12:22
author: "Federico"
comments: true
tags:
  - blog
  - ruby
  - programming
  
categories: ruby
---

Test Driven Development (TDD) is defined as the "<em>software development process that relies on the repetition of a very short development cycle: first the developer writes an (initially failing) automated test case that defines a desired improvement or new function, then produces the minimum amount of code to pass that test, and finally refactors the new code to acceptable standards"</em> <a title="Test Driven Development on Wikipedia" href="http://en.wikipedia.org/wiki/Test-driven_development" target="_blank">[Wikipedia]</a>.


<img class="size-medium wp-image-559 " alt="Test Driven Development Cycle" src="http://paini.org/codecoms/wp-content/uploads/2013/06/Test-driven_development-300x215.png" width="300" height="215" />
<br>
<p>Fig.1 - Test Driven Development Cycle</p>


TDD is a great way to create simple, elegant and powerful code. I'm a big fan of simplicity  in coding. Contrary to what one may think creating simple code is very hard. Researching simplicity it's a very time consuming and arduous task. It's much easier to create complicate code that nobody can understand . One way you can easily use TDD in ruby is by installing <a title="RSpec" href="https://www.relishapp.com/rspec" target="_blank">rspec</a>. The script I'm using to show how rspec works is a program that takes a list of words in an array and extract the first and last letter of each word and put them in a new array. The method returns the new array. This is the behavior we want to test.

 * Install rspec: I assume you have installed  Ruby 1.9 with gems.<br> 
 Just type what is shown below and rspec should install with no issues. Run `rspec -v` on the command line and it should show the version installed. That's the proof rspec was installed.

	

```	
	
$ gem update
$ gem install rspec
$ rspec -v
2.11.1

```

 * Cut/paste the code below, save it as `rspecTest.rb` (change the name if you like) and then run it as shown:


```

#Test method called in rspec
def test
  "testing"
end

#Method we want to test with rspec
def get_first_last_letter(word_list)

  first_last_letter = [] #array initialization

  #extract the first and last letter from each word
  word_list.each { |x| first_last_letter &lt;&lt; "#{x[0]}#{x[-1]}" }

  return first_last_letter
end

#Executing the script without rspec testing
  if (File.basename($0)) == File.basename(__FILE__)

    word_list = ["cocoa", "animal", "felt", "fertile"]
    puts get_first_last_letter(word_list)
    exit 0
end

#testing with rspec
describe "testDev" do
  it "testing" do

  word_list = ["cocoa", "animal", "felt", "fertile"]

  #testing expected outcome
  get_first_last_letter(word_list).should eql (["ca","al","ft", "fe"])

  end
end

```

When you run the code by typing `rspec rspecTest.rb` you should see the following outcome:

```

rspec rspecTest.rb

Finished in 0.00103 seconds
1 example, 0 failures

```

Now let's make the test fail! For this we are going to change line #32 in the program to expect a different outcome. In the array after the "eql" write "cb" instead of "ca":

```

#Original line
get_first_last_letter(word_list).should eql (["ca","al","ft", "fe"])

#Changed line
get_first_last_letter(word_list).should eql (["cb","al","ft", "fe"])


```

Now run the test again and this is what you should see:

```

Failures:

  1) testDev testing
     Failure/Error: get_first_last_letter(word_list).should eql (["cb","al","ft", "fe"])

       expected: ["cb", "al", "ft", "fe"]
            got: ["ca", "al", "ft", "fe"]

       (compared using eql?)
     # ./rspecTest.rb:28:in `block (2 levels) in '

Finished in 0.00119 seconds
1 example, 1 failure

Failed examples:

rspec ./rspecTest.rb:24 # testDev testing

shell returned 1

```

We can run the code normally by typing `ruby rspecTest.rb` the way we would do with any ruby code. This is what you should see:

```

$ ruby rspecTest.rb
ca
al
ft
fe

```

There you go! You are now using rspec to test your code (or method to be precise).



There sare many resources online if you want to know more about rspec. A good book to start  is the following:
<a title="The RSpec Book: Behaviour Driven Development with Rspec, Cucumber, and Friends (The Facets of Ruby Series)" href="http://www.amazon.com/gp/product/1934356379/ref=as_li_ss_tl?ie=UTF8&amp;camp=1789&amp;creative=390957&amp;creativeASIN=1934356379&amp;linkCode=as2&amp;tag=codecoms04-20" target="_blank">The RSpec Book: Behaviour Driven Development with Rspec, Cucumber, and Friends (The Facets of Ruby Series)</a>

Happy TDD!

<p>&nbsp;</p>
{% include twitter_plug.html %}
  
