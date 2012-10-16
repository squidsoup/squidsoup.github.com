---
layout: post
title: "Tab Completion and ANSI colours in IRB"
description: ""
categories: [ruby]
tags: [ruby, irb, syntax-hilighting]
---
{% include JB/setup %}

To get up and running with wirble:

`sudo gem install wirble`

and then add the following to your ~/.irbrc

    begin
      # load wirble
      require 'wirble'

      # start wirble (with color)
      Wirble.init
      Wirble.colorize
      rescue LoadError => err
      warn "Couldn't load Wirble: #{err}"
    end

Now typing "foo".\[tab\] will give you all the ruby String methods. 

Snazzy!
