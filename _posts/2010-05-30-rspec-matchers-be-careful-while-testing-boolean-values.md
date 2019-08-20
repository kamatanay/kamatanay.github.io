---
id: 105
title: 'RSpec Matchers: Be careful while testing boolean values'
date: 2010-05-30T14:19:55+00:00
author: Anay
layout: post
guid: http://anaykamat.com/?p=105
permalink: /2010/05/30/rspec-matchers-be-careful-while-testing-boolean-values/
syntaxhighlighter_encoded:
  - "1"
categories:
  - Programming
  - Technologies
  - Tips
tags:
  - rspec
  - ruby
  - ruby on rails
  - unit tests
---
While testing methods that return boolean values in ruby (the ones that end in &#8216;?&#8217;), try to avoid following matchers:

{% highlight ruby %}
method_returning_true?.should be_true
{% endhighlight %}

or

{% highlight ruby %}
method_returning_false?.should be_false
{% endhighlight %}

This is because, &#8216;be\_true&#8217; and &#8216;be\_false&#8217; matchers considers &#8216;nil&#8217; to be false and anything other than &#8216;nil&#8217; to be true. When we write methods in ruby which end with question mark (&#8216;?&#8217;), intent is that the method will return boolean value. To ensure that our tests will always reflect the intent of code, use following to assert boolean values instead of using &#8216;be\_true&#8217; or &#8216;be\_false&#8217; matchers:

{% highlight ruby %}
method_returning_true?.should == true
{% endhighlight %}

or

{% highlight ruby %}
method_returning_false?.should == false
{% endhighlight %}
