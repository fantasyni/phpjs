---
layout: post
title: "JavaScript escapeshellarg function"
date: 2011-02-06 12:00:00
comments: true
sharing: true
footer: true
permalink: /phpjs/functions/escapeshellarg
categories: [ exec, functions ]
---
A JavaScript equivalent of PHP's escapeshellarg
<!-- more -->
{% codeblock exec/escapeshellarg.js lang:js https://raw.github.com/kvz/phpjs/master/functions/exec/escapeshellarg.js raw on github %}
function escapeshellarg (arg) {
    // http://kevin.vanzonneveld.net
    // +   original by: Felix Geisendoerfer (http://www.debuggable.com/felix)
    // +   improved by: Brett Zamir (http://brett-zamir.me)
    // *     example 1: escapeshellarg("kevin's birthday");
    // *     returns 1: "'kevin\'s birthday'"
    var ret = '';

    ret = arg.replace(/[^\\]'/g, function (m, i, s) {
        return m.slice(0, 1) + '\\\'';
    });

    return "'" + ret + "'";
}
{% endcodeblock %}
<ul>
 <li><a href="https://github.com/kvz/phpjs/blob/master/functions/exec/escapeshellarg.js">view on github</a></li>
 <li><a href="https://github.com/kvz/phpjs/edit/master/functions/exec/escapeshellarg.js">edit on github</a></li>
</ul>
