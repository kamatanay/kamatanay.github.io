---
id: 53
title: Taking a close look at inheritance and closures in Javascript
date: 2008-06-30T10:03:24+00:00
author: Anay
layout: post
guid: http://anaykamat.com/?p=53
permalink: /2008/06/30/taking-a-close-look-at-inheritance-and-closures-in-javascript/
categories:
  - Programming
tags:
  - closures
  - inheritance
  - javascript
---
Let’s play with inheritance and closures in Javascript. Take a look at the following javascript code:
<!-- more -->
{% highlight javascript linenos %}
function BaseClass(){
	var id=200;
	this.Id=function(){
		return id;
	}
}

function ChildClass(){
	var id=500;
}

ChildClass.prototype = new BaseClass();
var childObject=new ChildClass();
{% endhighlight %}

In Javascript, inheritance is achieved using prototype. When we try to access any member on Javascript object, it first tries to search for the member within that object. If the member is found, then its accessed otherwise it tries to search for that member in its prototype object.

We make BaseClass the parent class of ChildClass with the following instruction:

{% highlight javascript %}ChildClass.prototype = new BaseClass();{% endhighlight %}

Notice that ChildClass does not have a method called ‘Id’. When we make a call to method ‘Id’ on childObject, it will see that ChildClass does not have ‘Id’ method and so will take it from its prototype object which is nothing but the object of BaseClass.

Based on this knowledge, what do you think will be the output of the following instruction?

{% highlight javascript %}childObject.Id(){% endhighlight %}

If you think it should be 500, then you are wrong. The correct answer is 200. This happens due to what is known as Closures. According to a <a title="Javascript Closure Tutorial" href="http://www.javascriptkit.com/javatutors/closures.shtml" target="_blank">tutorial on javascript closures</a> by Morris Johns:

> &#8220;a closure is the local variables for a function &#8211; kept alive after the function has returned&#8221;

To understand how this works in our case, let’s try to understand how javascript actually executes a call to the method ‘Id’ on childObject.

As childObject does not have a method called ‘Id’, it takes that method from its prototype and then executes it. You can imagine that Javascript performs the following steps to execute a call to the method ‘Id’ on childObject.

{% highlight javascript %}childObject.Id = ChildClass.prototype.Id;
childObject.Id();{% endhighlight %}

But does its mean that in Javascript, it’s not possible to override the values from base class/object at all? Well, It is possible by making a small change to our code. Javascript has a keyword called ‘this’. The ‘this’ keyword points to the object in which the method being called is present. For more information on ‘this’ keyword, refer to the article ‘<a title="this keyword tutorial" href="http://www.quirksmode.org/js/this.html" target="_blank">The this keyword</a>’.

In our current code, we are defining a variable using keyword ‘var’ which makes it local to the function in which it is defined. Due to this, closure comes into picture and call to the method ‘Id’ always prints the value from the BaseClass. To solve this problem, we need to refer to the variable ‘id’ using ‘this’ keyword. This will tell our method to use the value from the object in which the method has been placed. In this way, when the method is placed in ChildClass object, it will print the value of ‘id’ from ChildClass and not from BaseClass. Thus, the modified code which allows overriding is given below:

{% highlight javascript linenos %}
function BaseClass(){
	this.id=200;
	this.Id=function(){
		return this.id;
	}
}

function ChildClass(){
	this.id=500;
}

ChildClass.prototype = new BaseClass();
var childObject=new ChildClass();
{% endhighlight %}
