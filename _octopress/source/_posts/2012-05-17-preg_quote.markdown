---
layout: post
title: "JavaScript preg_quote function"
date: 2012-05-17 18:49
comments: true
sharing: true
footer: true
permalink: functions/preg_quote
categories: [ pcre, functions ]
---
A JavaScript equivalent of PHP's preg_quote
<!-- more -->
{% codeblock pcre/preg_quote.js lang:js https://raw.github.com/kvz/phpjs/master/functions/pcre/preg_quote.js raw on github %}
function preg_quote (str, delimiter) {
    // http://kevin.vanzonneveld.net
    // +   original by: booeyOH
    // +   improved by: Ates Goral (http://magnetiq.com)
    // +   improved by: Kevin van Zonneveld (http://kevin.vanzonneveld.net)
    // +   bugfixed by: Onno Marsman
    // +   improved by: Brett Zamir (http://brett-zamir.me)
    // *     example 1: preg_quote("$40");
    // *     returns 1: '\$40'
    // *     example 2: preg_quote("*RRRING* Hello?");
    // *     returns 2: '\*RRRING\* Hello\?'
    // *     example 3: preg_quote("\\.+*?[^]$(){}=!<>|:");
    // *     returns 3: '\\\.\+\*\?\[\^\]\$\(\)\{\}\=\!\<\>\|\:'
    return (str + '').replace(new RegExp('[.\\\\+*?\\[\\^\\]$(){}=!<>|:\\' + (delimiter || '') + '-]', 'g'), '\\$&');
}
{% endcodeblock %}
<ul>
 <li><a href="https://github.com/kvz/phpjs/blob/master/functions/pcre/preg_quote.js">view on github</a></li>
 <li><a href="https://github.com/kvz/phpjs/edit/master/functions/pcre/preg_quote.js">edit on github</a></li>
</ul>
