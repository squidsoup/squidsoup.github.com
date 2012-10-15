---
layout: post
title: "Managing multiple distinct logins in JMeter"
description: ""
category: performance 
tags: [jmeter, performance]
---
{% include JB/setup %}

I've recently been building a load model of the site I'm currently working on in JMeter, and struggled a bit to find a way to manage distinct user sessions in a thread group.

After some mild expletives, and a bit of digging around in the documentation I found the answer which I'll clarify here as it's not entirely obvious.

The best approach appears to be reading username and password pairs from a CSV.

First you will need to create a new csv with username and password pairs delimited by commas.

In Jmeter, add a CSV Data Set Config Element to your thread group, and specify the path to the CSV you just created, as well as setting "USERNAME, PASSWORD" in the Variable Names field.

![CSV Data Set](http://media.tumblr.com/tumblr_krdu46s3zP1qzey9z.png)

In your Thread Group configuration, set the number of threads to the number of users you've specified in your CSV.

![Thread Group](http://media.tumblr.com/tumblr_krduhxKufW1qzey9z.png)

Next you'll want to create a <i>Once Only Controller</i>, and set your HTTP Request sampler for your login process as a child. The Once Only logic controller will run only once per thread, so based on the configuration above, the HTTP POST to the sign in page will occur 10 times, whereas the HTTP Request sampler below will hit the app 500 times.

Finally, in your Sign In HTTP sampler, find the section labeled Send Parameters With the Request. Find the Name/Value pairs for your username, and password text boxes and set the respective values to ${USERNAME} and ${PASSWORD}.

![Request Params](http://media.tumblr.com/tumblr_krduupDc6L1qzey9z.png) 

### An even simpler solution
Provided you have a group of test users with the same prefix and an appended incrementing int (testuser1, testuser2 etc.), an even simpler approach is to forgo the CSV node entirely and simply pass something like this to the HTTP sampler:

```
    ${username-prefix}$(__threadNum}
```

Simply define ${username-prefix} in your test plan's user defined variables, and the $(__threadNum} function's return value will increment once for every new thread. 

Handy!
