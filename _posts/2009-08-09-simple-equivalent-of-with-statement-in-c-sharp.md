---
id: 84
title: 'Simple equivalent of &#8220;With&#8221; statement in C#'
date: 2009-08-09T16:06:29+00:00
author: Anay
layout: post
guid: http://anaykamat.com/?p=84
permalink: /2009/08/09/simple-equivalent-of-with-statement-in-c-sharp/
syntaxhighlighter_encoded:
  - "1"
categories:
  - Programming
  - Tips
tags:
  - .net
  - 'C#'
  - DSL
  - lambdas
---
Consider the following class in C#
<!-- more -->
{% highlight csharp linenos %}
public class Person
	{
		private string name;
		private int age;

		public string Name{
			get {return name;}
			set { name = value; }
		}

		public int Age{
			get {return age;}
			set { age = value; }
		}
	}
{% endhighlight %}

If I want to set the value of Name and Age property on the instance of Person class, I&#8217;ll need to refer to that instance for every property I need to set in the code. For example:

{% highlight csharp linenos %}
var person = new Person();
person.Name = "Super Man";
person.Age = 30;
{% endhighlight %}

It would have been great if C# had an equivalent of VB&#8217;s &#8220;With..End&#8221; statement, where we could refer to the instance of Person class only once and then refer to properties only.

Today, I came across this post &#8220;<a href="http://blog.bittercoder.com/PermaLink,guid,d1831805-dbf7-4b74-a6fd-2e9ed437c3d9.aspx" target="_blank">mucking about with hashes&#8230;</a>&#8220;, which shows how C# lambdas could be used as hashes. Using this concept, I implemented a simple extension method that simulates the behavior of VB&#8217;s &#8220;With..End&#8221; statement to some extent.

Here is the code for extension method:

{% highlight csharp linenos %}
public static class MetaExtensions
	{
		public static void Set(this object obj,params Func<string,object>[] hash){
				foreach(Func<string,object> member in hash){
					var propertyName = member.Method.GetParameters()[0].Name;
					var propertyValue = member(string.Empty);
					obj.GetType()
						.GetProperty(propertyName)
							.SetValue(obj,propertyValue,null);
				};
		}
	}
{% endhighlight %}

Using this extension method, we can set the value of properties on instance of Person class as follows:

{% highlight csharp linenos %}
var person = new Person();
person.Set(
	Name => "Super Man",
	Age => 30
);
{% endhighlight %}

Isn&#8217;t that cool?
