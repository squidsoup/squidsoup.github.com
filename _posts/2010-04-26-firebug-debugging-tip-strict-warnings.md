---
layout: post
title: "Firebug debugging tip: Strict Warnings"
description: ""
category: javascript 
tags: [javascript, firebug, firefox]
---
{% include JB/setup %}

I recently ran into an issue while setting up [jqGrid](http://www.trirand.com/blog/) for inline editing that I thought I might share here. For some reason the grid event for editing would fire, however the grid was never put in to an editable state. The Firebug console unfortunately did not return _any errors_, which made debugging a bit of a challenge. 


![](http://media.tumblr.com/tumblr_l1gnowLVio1qzey9z.png)

I then tried enabling Strict Warnings in firebug at which point I found the error: 

    reference to undefined property g[j].editable ...

It turns out that I was passing a string to the _editable_ property instead of the expected boolean:

    <script src="http://gist.github.com/378885.js"></script>

This of course should have read:

    editable: true,

Had I not enabled strict warnings I suspect I would have been tearing my hair out for somewhat longer. At any rate, if you find you have a js issue of some sort, perhaps try this Firebug feature - you may have a type issue that is silently failing.
