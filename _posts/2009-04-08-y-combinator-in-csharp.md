---
id: 58
title: 'Y-Combinator in C#'
date: 2009-04-08T14:19:26+00:00
author: Anay
layout: post
guid: http://anaykamat.com/?p=58
permalink: /2009/04/08/y-combinator-in-csharp/
syntaxhighlighter_encoded:
  - "1"
categories:
  - Programming
  - Technologies
tags:
  - .net
  - functional programming
---
For last few days, I was trying to use lambda feature of C# to implement Y-Combinator. After few trial and errors, I was able to implement it in C# 3.5. I&#8217;m currently posting the code here and in my next blog, I&#8217;ll explain how I derived it.
<!-- more -->
In this code, Y-Combinator function, is used to implement anonymous recursive-factorial function called &#8216;factorial&#8217;.

{% highlight csharp linenos %}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace YCombinator
{
    class Program
    {
        delegate Func RecursiveFunction(RecursiveFunction f);

        static void Main(string[] args)
        {

            Func, Func>, Func> Y = (f) =>
            {
                RecursiveFunction function = (h) =>
                {
                    return (x) =>
                    {
                        return f(h(h))(x);
                    };
                };
                return function(function);
            };

            Func factorial = Y(function=>
            {
                return x =>
                {
                    return x == 0 ? 1 : x * function(x - 1);
                };
            });
            Console.WriteLine(factorial(5));
            Console.ReadLine();
        }
    }
}
{% endhighlight %}
