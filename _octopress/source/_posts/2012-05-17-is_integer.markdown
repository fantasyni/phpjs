---
layout: post
title: "JavaScript is_integer function"
date: 2012-05-17 18:49
comments: true
sharing: true
footer: true
permalink: functions/is_integer
categories: [ var, functions ]
---
A JavaScript equivalent of PHP's is_integer
<!-- more -->
{% codeblock var/is_integer.js lang:js https://raw.github.com/kvz/phpjs/master/functions/var/is_integer.js raw on github %}
function is_integer (mixed_var) {
    // http://kevin.vanzonneveld.net
    // +   original by: Paulo Freitas
    //  -   depends on: is_int
    // %        note 1: 1.0 is simplified to 1 before it can be accessed by the function, this makes
    // %        note 1: it different from the PHP implementation. We can't fix this unfortunately.
    // *     example 1: is_integer(186.31);
    // *     returns 1: false
    // *     example 2: is_integer(12);
    // *     returns 2: true
    return this.is_int(mixed_var);
}
{% endcodeblock %}
<ul>
 <li><a href="https://github.com/kvz/phpjs/blob/master/functions/var/is_integer.js">view on github</a></li>
 <li><a href="https://github.com/kvz/phpjs/edit/master/functions/var/is_integer.js">edit on github</a></li>
</ul>
