---
layout: post
title: "JavaScript create_function function"
date: 2012-05-17 18:49
comments: true
sharing: true
footer: true
permalink: functions/create_function
categories: [ funchand, functions ]
---
A JavaScript equivalent of PHP's create_function
<!-- more -->
{% codeblock funchand/create_function.js lang:js https://raw.github.com/kvz/phpjs/master/functions/funchand/create_function.js raw on github %}
function create_function (args, code) {
    // http://kevin.vanzonneveld.net
    // +   original by: Johnny Mast (http://www.phpvrouwen.nl)
    // +   reimplemented by: Brett Zamir (http://brett-zamir.me)
    // *     example 1: f = create_function('a, b', "return (a + b);");
    // *     example 1: f(1, 2);
    // *     returns 1: 3
    try {
        return Function.apply(null, args.split(',').concat(code));
    } catch (e) {
        return false;
    }
}
{% endcodeblock %}
<ul>
 <li><a href="https://github.com/kvz/phpjs/blob/master/functions/funchand/create_function.js">view on github</a></li>
 <li><a href="https://github.com/kvz/phpjs/edit/master/functions/funchand/create_function.js">edit on github</a></li>
</ul>
