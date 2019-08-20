---
id: 76
title: Fixing SyntaxHighligher plugin in WordPress Blass2 theme
date: 2009-08-06T15:47:15+00:00
author: Anay
layout: post
guid: http://anaykamat.com/?p=76
permalink: /2009/08/06/fixing-syntaxhighligher-plugin-in-wordpress-blass2-theme/
syntaxhighlighter_encoded:
  - "1"
categories:
  - Tips
tags:
  - php
  - wordpress
---
Yesterday I installed and activated Blass2 theme for this blog. I liked this theme as it was very simple and free from any extra graphics. After installing the theme, I discovered that &#8220;<a href="http://www.viper007bond.com/wordpress-plugins/syntaxhighlighter/" target="_blank">SyntaxHighlighter Evolved</a>&#8221; plugin which I use to display code segments, was not working. I searched for other themes which are similar to blass2 and can run syntaxhighlighter plugin, but couldn&#8217;t find anything better. Finally, this is how I fixed it.
<!-- more -->
To fix it, I had to edit &#8216;footer.php&#8217; of Blass2 theme using inbuilt theme editor of WordPress (Appearance > Editor). The original &#8216;footer.php&#8217; looked like this:

{% highlight php %}
<div id="footer">

 <p>&copy; <?php echo date("Y")?> <!-- Please leave this line intact --><?php if (is_home()) : ?><?php bloginfo('name'); ?> | Theme <a href="http://1000ff.de/wordpress-theme-blass-english-version/">Blass</a> by <a href="http://1000ff.de/">1000ff</a><?php else : ?>Theme Blass by 1000ff<?php endif; ?> | Powered by <a href="http://wordpress.org/">WordPress</a></p>

</div>
{% endhighlight %}

To fix the plugin, you need to add a call to &#8216;wp_footer&#8217; function in &#8216;footer.php&#8217;.

{% highlight php %}
<div id="footer">

 <p>&copy; <?php echo date("Y")?> <!-- Please leave this line intact --><?php if (is_home()) : ?><?php bloginfo('name'); ?> | Theme <a href="http://1000ff.de/wordpress-theme-blass-english-version/">Blass</a> by <a href="http://1000ff.de/">1000ff</a><?php else : ?>Theme Blass by 1000ff<?php endif; ?> | Powered by <a href="http://wordpress.org/">WordPress</a></p>
<?php wp_footer() ?>
</div>
{% endhighlight %}

After making this change, syntaxhighlighter plugin started working again.
