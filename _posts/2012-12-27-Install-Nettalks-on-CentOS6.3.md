---
layout: post
title:  "Installing Apple Nattalks on a PC running Linux CentOS 6.3"
subtitle: "How to install Apple Nattalks on a PC running Linux CentOS 6.3"
date:   2012-12-27 21:12:22
author: "Federico"
comments: true
tags:
  - blog
  - how-to
  - linux
  
categories: Linux
---

I have a variety of PCs in my house running Linux CentOS, Windows 7 and Mac OSX 10.8 Mountain Lion. Something was bothering me: I could not "see" my Linux laptop with my MacBook Pro like I "see" all the other PC/devices in my LAN.

I did some research and I found a great site that explain step by step how to install the Nettalk protocol on CentoOS so to solve the issue:

<a title="http://rathelm.wordpress.com/2012/02/03/cent-os6-2-and-netatalk-2-2-0/" href="http://rathelm.wordpress.com/2012/02/03/cent-os6-2-and-netatalk-2-2-0/" target="_blank">http://rathelm.wordpress.com/2012/02/03/cent-os6-2-and-netatalk-2-2-0/</a>

The explanations are very straight forward. I tested it personally and I found it very easy to follow. And it works. I have one of minor caveat for you to pay attention to:
<ol>
	<li>When updating the IP TABLE config file on "/etc/sysconfig/iptables" copy and paste the following:
<pre><em>-A INPUT -m state --state NEW -m tcp -p tcp --dport 548 -j ACCEPT</em></pre>
If you copy/paste the line directly from the blog you wind up with a syntax error because of the double dash requirement "- -"</li>
</ol>
When installed and turned on you should be able to "see" your Linux PC from your Mac. If you don't just go to <em>"Finder->Go->Connect To Server"</em>, type the IP and you're connected.

Enjoy!

   


<p>&nbsp;</p>
{% include twitter_plug.html %}
  
