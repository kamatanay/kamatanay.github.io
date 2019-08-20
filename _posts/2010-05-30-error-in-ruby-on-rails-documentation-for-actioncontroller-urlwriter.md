---
id: 110
title: Error in ruby on rails documentation for ActionController::UrlWriter
date: 2010-05-30T18:25:02+00:00
author: Anay
layout: post
guid: http://anaykamat.com/?p=110
permalink: /2010/05/30/error-in-ruby-on-rails-documentation-for-actioncontroller-urlwriter/
syntaxhighlighter_encoded:
  - "1"
categories:
  - My Thoughts
  - Programming
  - Technologies
tags:
  - rails
  - ruby on rails
---
In Ruby on rails, methods that generate urls from named routes are not globally accessible. For example, you can&#8217;t access them from console (script/console). If you want to use these methods from such places, then the <a href="http://api.rubyonrails.org/classes/ActionController/UrlWriter.html" target="_blank">rails documentation for ActionController::UrlWriter</a> suggests two ways of doing it. According to this documentation, you can:

  1. Include ActionController::UrlWriter in your class
  2. Call the method directly on ActionController::UrlWriter

When I tried it out, only the first method worked. I was able to use methods generated from named routes in console after including ActionController::UrlWriter. However, it was not possible to call those methods on ActionController::UrlWriter. This looks like an issue with documentation to me.

It might be the case that the second method used to work in earlier version of rails. As rails is constantly being developed, some refactoring might have made the second method obsolete. I hope rails community will fix such issues in documentation soon.