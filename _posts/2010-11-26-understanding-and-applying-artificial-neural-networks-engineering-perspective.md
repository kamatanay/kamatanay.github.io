---
id: 127
title: 'Understanding and Applying Artificial Neural Networks : Engineering Perspective'
date: 2010-11-26T07:57:02+00:00
author: Anay
layout: post
guid: http://anaykamat.com/?p=127
permalink: /2010/11/26/understanding-and-applying-artificial-neural-networks-engineering-perspective/
categories:
  - Engineering
  - Programming
  - Technologies
tags:
  - ann
  - artificial neural networks
  - engineering perspective
  - jruby
  - ruby
---
Lasts week (15th November to 19th November), <a href="http://www.nitttrbhopal.org/index.php?option=com_content&view=article&id=237:goa-extension-centre&catid=52:articles&Itemid=261" target="_blank">NITTTR</a> (National Institute of Technical Teachers Training and Research) had organized a course on Artificial Neural Networks at [Government College Of Engineering &#8211; Farmagudi, Goa](http://www.gec.ac.in/). I was appointed as course faculty for this event.

Personally, I do not believe in concept of teaching. Humans are smart and intelligent animals and as such, they are capable of learning new things themselves based on their experience and observations. Thus, rather than providing a training, I preferred sharing my experience and knowledge on ANN with the members attending the course.

Considering the fact that this event was organized for staff of engineering colleges, the &#8220;Joint &#8211; Discussion&#8221; was titled, &#8220;**Engineering Solutions With Artificial Intelligence Using A System Popularized As Artificial Neural Networks**&#8220;.

Generally, we discuss Artificial Neural Networks either in theoretical perspective or in terms of purely scientific applications. However, the world of practical engineering is always different from theoretical or purely scientific perspective. The same applies to applications of ANN in perspective of modern digital engineering.

In this joint discussion, we spent first two days trying to understand the concept of artificial neural networks. To understand it practically, demonstrations were provided using the examples developed in JRuby. The code written for this purpose is now available on GitHub (The link is provided at the end of this post).

For next two days, all the participants were allowed to experiment with the JRuby code. Participants could play around with different training sets while modifying variables like learning rate, momentum, activation functions, number of hidden layers, number of neurons in hidden layers etc. They could also experiment with performing the same training using backpropagation algorithm and genetic algorithm. This helped them in understanding the challenges faced by engineers in practically implementing the solutions using ANN.

On the last day (Friday 19th, November 2010), we concluded the joint discussion by determining the capabilities and limitations of ANN based on the experience and knowledge obtained by participants in four days. At the end, a demo of <a href="http://userscripts.org/scripts/review/38736" target="_blank">OCR written in Javascript</a> was given by Tejas Vernekar.

During the joint discussion, some of the alternative non-neural solutions for few problems were discussed as well. A ruby equivalent of spell checker (which uses statistical language processing) originally developed in python was also demonstrated. The ruby equivalent code is available in the code in GitHub Repository.

In case you are interested in JRuby code used during the joint discussion, you can download it from <a href="https://github.com/kamatanay/JRuby-Neural-Networks" target="_blank">this GitHub repository</a>.