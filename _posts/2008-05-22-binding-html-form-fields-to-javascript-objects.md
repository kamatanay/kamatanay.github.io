---
id: 50
title: Binding HTML Form Fields To Javascript Objects
date: 2008-05-22T15:42:58+00:00
author: Anay
layout: post
guid: http://anaykamat.com/?p=50
permalink: /2008/05/22/binding-html-form-fields-to-javascript-objects/
categories:
  - Programming
tags:
  - .net
  - 'C#'
  - data bindings
  - databindings
  - forms
  - javascript
---
Consider that I have a object called &#8216;person&#8217; with a property called &#8216;Name&#8217; which returns me the name of a particular person. I want to assign this object property to a form element such that:

  1. The form element will display the value of object property (In our case, the value of person.Name)
  2. If I change the value in form, then it should automatically get assigned to the object property

In C#, it could be done by using the following piece of code:

{% highlight csharp %}nameTextBox.DataBindings.Add("Text", person, "Name");{% endhighlight %}

I really like the way DataBinding works and would really like have something like this when I&#8217;m working on web applications to bind a object property to input elements in HTML forms. So I decided to write a small javascript that would allow me to bind object properties to form elements. For example, I wanted to write something like this:

{% highlight html %}<input type="text" object="person" property="firstName" />{% endhighlight %}

Thanks to the power of Javascript and prototype library, I was able to use data binding in html forms using code:

{% highlight javascript linenos %}
function initializeFormBinding()
{
	var formElements = document.getElementsByTagName('input');
	$A(formElements).each(function(formElement)
				{
					Element.extend(formElement);
					initializeFormElement(formElement);
				});
}

function initializeFormElement(formElement)
{
	if (!(formElementHasObjectAttribute(formElement) &amp;&amp; formElementHasPropertyAttribute(formElement)))
		return;
	var objectName = getAttributeValue(formElement,'object');
	var propertyName = getAttributeValue(formElement,'property');
	window.eval('formElement.value = '+objectName+'.'+propertyName);
	window.eval('formElement.onchange=function(){ '+objectName+'.'+propertyName+' = formElement.value; }');
}

function formElementHasObjectAttribute(formElement)
{
	return getAttributeValue(formElement,'object')!=null;
}

function formElementHasPropertyAttribute(formElement)
{
	return getAttributeValue(formElement,'property')!=null;
}

function getAttributeValue(element, attributeName)
{
	return element.readAttribute(attributeName);
}
{% endhighlight %}

Lets see how to use this: First, create a javascript object. For example:

{% highlight javascript linenos %}
var person = {};
person.firstName = '';
person.lastName = '';
person.age = '';
person.country = '';
{% endhighlight %}

After that call initializeFormBinding() function using onLoad attribute of body tag. For example:

{% highlight html  %}<body onLoad="javascript:initializeFormBinding();">{% endhighlight %}

Now, in each of your input elements, put the name of the object in &#8216;object&#8217; attribute and name of property in &#8216;property&#8217; attribute as follows:

{% highlight html linenos %}
<form>
First Name:
<input type="text" object="person" property="firstName" /><br>
Last Name:
<input type="text" object="person" property="lastName" /><br>
Age:
<input type="text" object="person" property="age" /><br>
Country:
<input type="text" object="person" property="country" /><br>
</form>
{% endhighlight %}

Thats it&#8230;. If you initialize properties of person object, you would see those values in respective form elements. On the other hand, if you modify the value in a particular input element then it would get reflected in the corresponding object property. Anybody is free to use this code in their applications.

[Download a small example application.](/wp-content/uploads/JavascriptDataBinding.zip "Application example").
