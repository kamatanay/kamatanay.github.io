---
id: 54
title: Be careful while using ‘replaceAll’ and ‘replaceFirst’ methods of String class in Java
date: 2008-10-27T07:55:50+00:00
author: Anay
layout: post
guid: http://anaykamat.com/?p=54
permalink: '/2008/10/27/be-careful-while-using-%e2%80%98replaceall%e2%80%99-and-%e2%80%98replacefirst%e2%80%99-methods-of-string-class-in-java/'
categories:
  - Programming
  - Tips
tags:
  - Java
  - regular expression
  - replace
  - replaceAll
  - replaceFirst
  - String
---
Most of the time, while trying to replace a substring in a given string, either all its occurrences or just the first one, java programmers tend to use ‘replaceAll’ and ‘replaceFirst’ methods provided by String class in Java. Java programmers like to use these methods to replace substrings as compared to ‘replace’ method of String class because of different reasons like:

  1. ‘replaceAll’ and ‘replaceFirst’ methods use regular expressions instead of character sequence. It is pre-assumed most of the time that using these methods will allow us to replace a given pattern in future, instead of just replacing a substring.
  2. ‘replaceAll’ and ‘replaceFirst’ methods are named such that they clarify the intent of their execution.

However, while using these methods, we need to be very careful while providing the string value which would replace a given substring or a pattern. Let’s understand why with the following example:

Run the following java code:

{% highlight java linenos %}
public class StringReplace {

  public static void main(String[] args){
    String stringValue = "test1 test2 test1 test3";
    String replaceValue = "test";
    stringValue = stringValue.replaceAll("test1", replaceValue);
    System.out.print(stringValue);
  }

}
{% endhighlight %}

This code works properly. But now try running the same code by changing the value of variable ‘replaceValue’ as:

{% highlight java %}String replaceValue = "$100";{% endhighlight %}

This would result in an exception of type ‘IndexOutOfBoundException’. This is because the ‘$’ symbol is used to identify a group from the regular expression which is the first parameter of ‘replaceAll’ or ‘replaceFirst’ method. We can solve this problem by:

  1. Using ‘replace’ method: This would be the good choice if you want to replace a string literal and not a pattern.
  2. Escaping ‘$’ symbol: If you need to a use regular expression, and your pattern has no groups identified, then you can escape any group identification symbols from your replace string as shown below:

<p style="text-align: center;">
{% highlight java  %}String replaceValue = java.util.regex.Matcher.quoteReplacement("$100");{% endhighlight %}
</p>
