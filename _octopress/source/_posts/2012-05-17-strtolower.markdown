---
layout: post
title: "JavaScript strtolower function"
date: 2012-05-17 18:49
comments: true
sharing: true
footer: true
permalink: functions/strtolower
categories: [ strings, functions ]
---
A JavaScript equivalent of PHP's strtolower
<!-- more -->
{% codeblock strings/strtolower.js lang:js https://raw.github.com/kvz/phpjs/master/functions/strings/strtolower.js raw on github %}
function strtolower (str) {
    // http://kevin.vanzonneveld.net
    // +   original by: Kevin van Zonneveld (http://kevin.vanzonneveld.net)
    // +   improved by: Onno Marsman
    // *     example 1: strtolower('Kevin van Zonneveld');
    // *     returns 1: 'kevin van zonneveld'
    return (str + '').toLowerCase();
}
{% endcodeblock %}
<ul>
 <li><a href="https://github.com/kvz/phpjs/blob/master/functions/strings/strtolower.js">view on github</a></li>
 <li><a href="https://github.com/kvz/phpjs/edit/master/functions/strings/strtolower.js">edit on github</a></li>
</ul>
