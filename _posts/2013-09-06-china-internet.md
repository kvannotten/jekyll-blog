---
layout: post
title: "Internet Issues in China"
description: "Blog about my internet issues in China"
category: china internet script
tags: [china internet script]
---
{% include JB/setup %}

## The issue

So the past few days my internet was really, really bad. I will illustrate this with the output of the script I wrote to monitor my connection:

	I, [2013-09-04T19:00:01.810680 #58738]  INFO -- : Internet is up!
	I, [2013-09-04T19:04:49.426047 #58738]  INFO -- : Internet down!
	I, [2013-09-04T19:06:11.865051 #58738]  INFO -- : Internet is up!
	I, [2013-09-04T19:07:26.452834 #58738]  INFO -- : Internet down!
	I, [2013-09-04T19:07:32.854117 #58738]  INFO -- : Internet is up!
	I, [2013-09-04T19:12:06.356444 #58738]  INFO -- : Internet down!
	I, [2013-09-04T19:12:34.224192 #58738]  INFO -- : Internet is up!
	I, [2013-09-04T19:14:01.071976 #58738]  INFO -- : Internet down!
	I, [2013-09-04T19:14:07.528719 #58738]  INFO -- : Internet is up!
	I, [2013-09-04T19:15:22.179518 #58738]  INFO -- : Internet down!
	I, [2013-09-04T19:15:28.663526 #58738]  INFO -- : Internet is up!


... This goes on for a while.

You can clearly see the internet is failing constantly, albeit for even a second or so (the script only checks every 5-ish seconds)

## How to diagnose?

In order to diagnose the issue, I had to somehow automate the detection of the symptoms. I use a rather complex setup here in China with a VPN and sorts (to connect to a server that connects over VPN to the company network).

So the idea was to regularly ping a site (I used baidu, a famous Chinese search engine) of which I was certain it would be up all the time, and then check if I could reach it or not, if it fails after 3 tries, something is wrong. 

As an added bonus, I would let my computer use the OS X application 'say' to say out loud that my internet was down.

## The script

So the script does what it says up there, but it also daemonizes itself (with thanks to a noble anonymous guy for providing some code for that) and writes everything to a rotating log file. 

It was funny to hear my computer say: "Internet down", when we were streaming some TV-show, and we knew the result was that it was gonna stop in a few seconds.

Anyways, you can find the script down here, feel free to do whatever you like with it!

## The code

<script src="https://gist.github.com/kvannotten/6433327.js"></script>

