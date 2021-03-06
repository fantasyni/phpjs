---
layout: post
title: "JavaScript stream_get_line function"
date: 2012-05-17 18:49
comments: true
sharing: true
footer: true
permalink: functions/stream_get_line
categories: [ stream, functions ]
---
A JavaScript equivalent of PHP's stream_get_line
<!-- more -->
{% codeblock stream/stream_get_line.js lang:js https://raw.github.com/kvz/phpjs/master/functions/stream/stream_get_line.js raw on github %}
function stream_get_line (handle, length, ending) {
    // http://kevin.vanzonneveld.net
    // +   original by: Brett Zamir (http://brett-zamir.me)
    // *     example 1: fopen('http://kevin.vanzonneveld.net/pj_test_supportfile_1.htm', 'r');
    // *     example 1: stream_get_line(handle, 2);
    // *     returns 1: '<'
    var start = 0,
        fullline = '';

    if (!this.php_js || !this.php_js.resourceData || !this.php_js.resourceDataPointer || length !== undefined && !length) {
        return false;
    }

    start = this.php_js.resourceDataPointer[handle.id];

    if (start === undefined || !this.php_js.resourceData[handle.id][start]) {
        return false; // Resource was already closed or already reached the end of the file
    }

    // Fix: Should we also test for /\r\n?|\n/?
    fullline = this.php_js.resourceData[handle.id].slice(start, this.php_js.resourceData[handle.id].indexOf(ending, start) + 1);
    if (fullline === '') {
        fullline = this.php_js.resourceData[handle.id].slice(start); // Get to rest of the file
    }

    length = (length === undefined || fullline.length < length) ? fullline.length : Math.floor(length / 2) || 1; // two bytes per character (or surrogate), but ensure at least one
    this.php_js.resourceDataPointer[handle.id] += length;
    return this.php_js.resourceData[handle.id].substr(start, length - (fullline && ending && ending.length ? ending.length : 0));
}
{% endcodeblock %}
<ul>
 <li><a href="https://github.com/kvz/phpjs/blob/master/functions/stream/stream_get_line.js">view on github</a></li>
 <li><a href="https://github.com/kvz/phpjs/edit/master/functions/stream/stream_get_line.js">edit on github</a></li>
</ul>
