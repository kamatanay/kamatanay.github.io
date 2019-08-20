---
id: 49
title: Using JSON in Alfresco WebScripts
date: 2008-05-08T14:44:37+00:00
author: Anay
layout: post
guid: http://anaykamat.com/2008/05/08/using-json-in-alfresco-webscripts/
permalink: /2008/05/08/using-json-in-alfresco-webscripts/
categories:
  - Programming
  - Technologies
---
In my current project, we are using <a href="http://www.alfresco.com/" title="Alfresco" target="_blank">Alfresco</a> for the content repository and all the extra functionalities required are developed using <a href="http://http://wiki.alfresco.com/wiki/Web_Scripts" title="Web scripts" target="_blank">Webscripts</a>. While working on one functionality, I had to serialize javascript objects to JSON and also deserialize it. For doing this, there is a nice <a href="http://wiki.alfresco.com/wiki/Web_Scripts_Examples#JSON_example" title="Javascript code" target="_blank">javascript code</a> on Alfresco Wiki for converting the object to JSON and vice versa. But to use it, you need to make some slight modifications to the code. The original code doesn&#8217;t generate proper JSON code and also has a syntax error in method to obtain the javascript object back from the JSON string. So here is the proper code for handling JSON:

{% highlight javascript linenos %}
/*
   json.js
(modified 2006-09-07): added support for RHINO
(modified 2006-05-02): json.parse, json,stringify added
  USAGE:
  var jsObj = JSON.parse(jsonStr);
  var jsonStr = JSON.stringify(jsObj);
*/
if (!this.json) {
  var json = (function () {
      var m = {
              'b': 'b',
              't': 't',
              'n': 'n',
              'f': 'f',
              'r': 'r',
              '"' : '\"',
              '': ''
          },
          s = {
              array: function (x) {
                  var a = [], b, f, i, l = x.length, v;
                  for (i = 0; i &lt; l; i += 1) {
                      v = x[i];
                      f = s[typeof v];
                      if (f) {
                          v = f(v);
                          if (typeof v == 'string') {
                              a[a.length] = v;
                              b = true;
                          }
                      }
                  }
                  return '['+a.join()+']';
              },
              'boolean': function (x) {
                  return String(x);
              },
              'null': function (x) {
                  return "null";
              },
              number: function (x) {
                  return isFinite(x) ? String(x) : 'null';
              },
              object: function (x) {
                  if (x) {

                      if (x instanceof Array) {
                          return s.array(x);
                      }
                      if (x.hashCode) return s.string(+x.toString());

                      var a = [], b, f, i, v;
                      for (i in x) {
                          v = x[i];
                          f = s[typeof v];
                          if (f) {

                              v = f(v);

                              if (typeof v == 'string') {
                                  a.push(""+s.string(i)+':'+ v+"");
                                  b = true;
                              }
                          }
                      }
                      return '{'+a.join()+'}';
                  }
                  return 'null';
              },
              string: function (x) {
                  if (/["x00-x1f]/.test(x)) {
                      x = x.replace(/([x00-x1f\"])/g, function(a, b) {
                          var c = m[b];
                          if (c) {
                              return c;
                          }
                          c = b.charCodeAt();
                          return 'u00' +
                              Math.floor(c / 16).toString(16) +
                              (c % 16).toString(16);
                      });
                  }
                  return '"' + x + '"';
              }
          };

     return {
        parse: function(s) {
           try {
              return !(/[^,:{}[]0-9.-+Eaeflnr-u nrt]/.test(s.replace(/"(.|[^"])*"/g,""))) && eval('(' + s + ')');
           } catch (e) {
              return false;
           }
        },
        stringify: s.object
     };
  })();
}
{% endhighlight %}

Here is how to use this code to serialize a javascript object:

{% highlight javascript linenos %}
  o={};
	o.name = "Name";
	o.id = 1;
	j = json.stringify(o);
{% endhighlight %}

Also, to obtain the object back from JSON string, you can use following method:

{% highlight javascript %}x = json.parse(j);{% endhighlight %}
