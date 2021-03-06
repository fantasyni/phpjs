---
layout: post
title: "JavaScript array_change_key_case function"
date: 2011-12-29 12:00:00
comments: true
sharing: true
footer: true
permalink: /phpjs/functions/array_change_key_case
categories: [ array, functions ]
---
A JavaScript equivalent of PHP's array_change_key_case
<!-- more -->
{% codeblock array/array_change_key_case.js lang:js https://raw.github.com/kvz/phpjs/master/functions/array/array_change_key_case.js raw on github %}
function array_change_key_case (array, cs) {
    // http://kevin.vanzonneveld.net
    // +   original by: Ates Goral (http://magnetiq.com)
    // +   improved by: marrtins
    // +      improved by: Brett Zamir (http://brett-zamir.me)
    // *     example 1: array_change_key_case(42);
    // *     returns 1: false
    // *     example 2: array_change_key_case([ 3, 5 ]);
    // *     returns 2: {0: 3, 1: 5}
    // *     example 3: array_change_key_case({ FuBaR: 42 });
    // *     returns 3: {"fubar": 42}
    // *     example 4: array_change_key_case({ FuBaR: 42 }, 'CASE_LOWER');
    // *     returns 4: {"fubar": 42}
    // *     example 5: array_change_key_case({ FuBaR: 42 }, 'CASE_UPPER');
    // *     returns 5: {"FUBAR": 42}
    // *     example 6: array_change_key_case({ FuBaR: 42 }, 2);
    // *     returns 6: {"FUBAR": 42}
    var case_fn, key, tmp_ar = {};

    if (Object.prototype.toString.call(array) === '[object Array]') {
        return array;
    }
    if (array && typeof array === 'object' && array.change_key_case) { // Duck-type check for our own array()-created PHPJS_Array
        return array.change_key_case(cs);
    }
    if (array && typeof array === 'object' ) {
        case_fn = (!cs || cs === 'CASE_LOWER') ? 'toLowerCase' : 'toUpperCase';
        for (key in array) {
            tmp_ar[key[case_fn]()] = array[key];
        }
        return tmp_ar;
    }
    return false;
}
{% endcodeblock %}
<ul>
 <li><a href="https://github.com/kvz/phpjs/blob/master/functions/array/array_change_key_case.js">view on github</a></li>
 <li><a href="https://github.com/kvz/phpjs/edit/master/functions/array/array_change_key_case.js">edit on github</a></li>
</ul>
