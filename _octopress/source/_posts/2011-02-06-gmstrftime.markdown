---
layout: post
title: "JavaScript gmstrftime function"
date: 2011-02-06 12:00:00
comments: true
sharing: true
footer: true
permalink: /phpjs/functions/gmstrftime
categories: [ datetime, functions ]
---
A JavaScript equivalent of PHP's gmstrftime
<!-- more -->
{% codeblock datetime/gmstrftime.js lang:js https://raw.github.com/kvz/phpjs/master/functions/datetime/gmstrftime.js raw on github %}
function gmstrftime (format, timestamp) {
    // http://kevin.vanzonneveld.net
    // +   original by: Brett Zamir (http://brett-zamir.me)
    // +   input by: Alex
    // +   bugfixed by: Brett Zamir (http://brett-zamir.me)
    // -    depends on: strftime
    // *     example 1: gmstrftime("%A", 1062462400);
    // *     returns 1: 'Tuesday'
    var dt = ((typeof(timestamp) == 'undefined') ? new Date() : // Not provided
    (typeof(timestamp) == 'object') ? new Date(timestamp) : // Javascript Date()
    new Date(timestamp * 1000) // UNIX timestamp (auto-convert to int)
    );
    timestamp = Date.parse(dt.toUTCString().slice(0, -4)) / 1000;
    return this.strftime(format, timestamp);
}
{% endcodeblock %}
<ul>
 <li><a href="https://github.com/kvz/phpjs/blob/master/functions/datetime/gmstrftime.js">view on github</a></li>
 <li><a href="https://github.com/kvz/phpjs/edit/master/functions/datetime/gmstrftime.js">edit on github</a></li>
</ul>
