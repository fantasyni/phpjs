---
layout: post
title: "JavaScript strncasecmp function"
date: 2011-02-06 12:00:00
comments: true
sharing: true
footer: true
permalink: /phpjs/functions/strncasecmp
categories: [ strings, functions ]
---
A JavaScript equivalent of PHP's strncasecmp
<!-- more -->
{% codeblock strings/strncasecmp.js lang:js https://raw.github.com/kvz/phpjs/master/functions/strings/strncasecmp.js raw on github %}
function strncasecmp (argStr1, argStr2, len) {
    // http://kevin.vanzonneveld.net
    // +   original by: Saulo Vallory
    // +      input by: Nate
    // +   bugfixed by: Onno Marsman
    // %          note: Returns < 0 if str1 is less than str2 ; > 0 if str1 is greater than str2 , and 0 if they are equal.
    // *     example 1: strncasecmp('Price 12.9', 'Price 12.15', 2);
    // *     returns 1: 0
    // *     example 2: strncasecmp('Price 12.09', 'Price 12.15', 10);
    // *     returns 2: -1
    // *     example 3: strncasecmp('Price 12.90', 'Price 12.15', 30);
    // *     returns 3: 8
    // *     example 4: strncasecmp('Version 12.9', 'Version 12.15', 20);
    // *     returns 4: 8
    // *     example 5: strncasecmp('Version 12.15', 'Version 12.9', 20);
    // *     returns 5: -8
    var diff, i = 0;
    var str1 = (argStr1 + '').toLowerCase().substr(0, len);
    var str2 = (argStr2 + '').toLowerCase().substr(0, len);

    if (str1.length !== str2.length) {
        if (str1.length < str2.length) {
            len = str1.length;
            if (str2.substr(0, str1.length) == str1) {
                return str1.length - str2.length; // return the difference of chars
            }
        } else {
            len = str2.length;
            // str1 is longer than str2
            if (str1.substr(0, str2.length) == str2) {
                return str1.length - str2.length; // return the difference of chars
            }
        }
    } else {
        // Avoids trying to get a char that does not exist
        len = str1.length;
    }

    for (diff = 0, i = 0; i < len; i++) {
        diff = str1.charCodeAt(i) - str2.charCodeAt(i);
        if (diff !== 0) {
            return diff;
        }
    }

    return 0;
}
{% endcodeblock %}
<ul>
 <li><a href="https://github.com/kvz/phpjs/blob/master/functions/strings/strncasecmp.js">view on github</a></li>
 <li><a href="https://github.com/kvz/phpjs/edit/master/functions/strings/strncasecmp.js">edit on github</a></li>
</ul>
