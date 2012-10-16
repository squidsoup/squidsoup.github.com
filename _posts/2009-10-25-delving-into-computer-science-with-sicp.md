---
layout: post
title: "Delving into Computer Science with SICP"
category: Lisp, Computer Science
tags: [List, CompSci]
---
{% include JB/setup %}

<div style="float:left; padding: 0 10px 10px 0;margin:0;"><img src="http://media.tumblr.com/tumblr_ks0psmtcWL1qzey9z.png"></div>

The _Structure and Interpretation of Computer Programs_ by Harold Abelson and Gerald Jay Sussman is often cited by experienced developers as one of the books that fundamentally changed the way they think about computer science and software development. 

SICP is also a somewhat intimidating tome that demands a fair bit of perseverance and dedication from its reader. Like most things in life of course, things worth doing typically take time and effort!

<br style="clear:both;" />


###Why study sicp?
I suspect many developers today would see learning a language like Scheme as anachronistic, and potentially less than practical. Interestingly, there seems to have been a recent resurgence of interest in functional programming. 

Javascript, which in the past has been a somewhat misunderstood language, is beginning to be recognised as capable of some fairly sophisticated constructs and a lot more than just behavioural glue for the DOM. Languages such as F# and Haskell are slowly beginning to work their way into the mainstream software development world. The latest version of Microsoft's IDE, Visual Studio, is shipping with F# as a first class citizen, supporting .Net F# projects out of the box.

[Chris Hanson](http://stackoverflow.com/questions/13182/sicp-better-programming) posted the following on StackOverflow in response to a user enquiring about the value of working through SICP:

>Even if you don't do the exercises, it's worth reading through Structure and Interpretation of Computer Programs at least once. Unlike The Art of Computer Programming it's written not to appease some bizarre notion of machine architecture but to demonstrate the fundamentals of computational processes, and it excels at that.

>Some of what you'll learn simply by reading through SICP:

> * Functional decomposition and modeling problems
> * Recursion, its uses, pros and cons
> * Imperative and functional programming
> * Control structures, and why they have the behavior they do
> * Language design
> * Computer architecture
> * Compiler implementation.

>The compiler implementation bits later on in the book will be especially enlightening to many working software developers, who if they haven't had a class on the topic often think compilers are strange and mysterious beasts and that creating languages is "hard."

>My feeling is that a lot of people suggest reading _The Art of Computer Programming_ because having waded through it makes you feel smart, but that people suggest reading _Structure and Interpretation of Computer Programming_ because it clearly presents knowledge every software developer needs a thorough command of. 

###Expectations

I'm hoping to document my experience here on my blog to see if understanding the concepts in SICP will have any appreciable effect on the way I approach web development. Given that javascript is essentially a functional language, I suspect a lot of the concepts *will* be relevant. At the very least I hope to have a better understanding of computer science in general.

I won't be alone in my journey - a number of others have blogged about their experience as they've worked through the book and the course material. Both 
[Bill the Lizard](http://www.billthelizard.com/2009/10/sicp-challenge.html) and 
[Eli Bendersky](http://eli.thegreenplace.net/2007/06/19/introducing-the-sicp-reading-notes/) have some excellent posts both on the content of the lectures and working through the exercises.

###Course resources

Complete SICP book [html](http://mitpress.mit.edu/sicp/full-text/book/book.html) [pdf](http://deptinfo.unice.fr/~roy/sicp.pdf)

[Lecture notes, Exams, Projects](http://ocw.mit.edu/OcwWeb/Electrical-Engineering-and-Computer-Science/6-001Spring-2005/CourseHome/)

[Lecture Videos](http://groups.csail.mit.edu/mac/classes/6.001/abelson-sussman-lectures/) Also provided from the OCW site, but this page provides links to torrents.

[SICP Tutor](http://icampustutor.csail.mit.edu/6.001-public/)


###Selecting a Scheme interpreter

There are an astounding number of Scheme implementations available today, and to the beginner this can be somewhat overwhelming. The [Community Scheme Wiki](http://community.schemewiki.org/) has the following advice regarding choosing an implementation for learning Scheme: 

>Beginners should select an implementation that is well-documented, adheres closely to the standard, has good error handling and debugging capabilities, is easy to install, is mature, stable and under active development. _Chez Scheme_, _Gambit_, _MIT Scheme_ and _PLT Scheme_ are all used extensively in teaching Computer Science courses and hence meet all the aforementioned requirements. _Chicken_, _Bigloo_, _EdScheme_, _OpenScheme_, _Scheme48_, and _SCM_ are quite beginner-friendly too.

I've decided to give Chicken a go, primarily because I find the name amusing, but also as it has POSIX support and provides both an interpreter and compiler. A fair bit of real world development appears to be done with Chicken, so there would be no need to switch implementations if I decided to start building apps in Scheme one day.

###Setting up a Scheme environment in Mac OS X

Installing Chicken is a snap if you have [Mac Ports](http://www.macports.org/) installed - simply run:

```
sudo port install chicken
```

If you don't have Mac Ports installed, the latest release is available from the [Chicken website](http://www.call-with-current-continuation.org/). You'll need to have installed XCode to build Chicken from source.

###Choosing a text editor

If you use TextMate, you'll find the Scheme bundle helpful as it provides syntax hi-lighting and bindings for your Scheme interpreter such as ⌘R for Run Script. To install the bundle, run the following commands in Terminal:

```
mkdir /Library/Application\ Support/TextMate/Bundles/
svn co http://svn.textmate.org/trunk/Bundles/Scheme.tmbundle/
osascript -e 'tell app "TextMate" to reload bundles'
```

Any text editor that you're comfortable with will be fine, but you'll probably find life easier if you select one with some form of syntax hi-lighting and parenthesis matching for LISP/Scheme.

PLT Scheme provides a Scheme IDE called [DrScheme](http://download.plt-scheme.org/drscheme/), which runs on Windows, Linux and OS X. 

Emacs is another popular option in the LISP/Scheme community, and available in many guises. [Aquamacs](http://aquamacs.org/) is a good aqua interpretation for Mac OS X.
