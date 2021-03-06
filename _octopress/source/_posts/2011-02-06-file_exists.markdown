---
layout: post
title: "JavaScript file_exists function"
date: 2011-02-06 12:00:00
comments: true
sharing: true
footer: true
permalink: /phpjs/functions/file_exists
categories: [ filesystem, functions ]
---
A JavaScript equivalent of PHP's file_exists
<!-- more -->
{% codeblock filesystem/file_exists.js lang:js https://raw.github.com/kvz/phpjs/master/functions/filesystem/file_exists.js raw on github %}
function file_exists (url) {
    // http://kevin.vanzonneveld.net
    // +   original by: Enrique Gonzalez
    // +      input by: Jani Hartikainen
    // +   improved by: Kevin van Zonneveld (http://kevin.vanzonneveld.net)
    // %        note 1: This function uses XmlHttpRequest and cannot retrieve resource from different domain.
    // %        note 1: Synchronous so may lock up browser, mainly here for study purposes. 
    // *     example 1: file_exists('http://kevin.vanzonneveld.net/pj_test_supportfile_1.htm');
    // *     returns 1: '123'
    var req = this.window.ActiveXObject ? new ActiveXObject("Microsoft.XMLHTTP") : new XMLHttpRequest();
    if (!req) {
        throw new Error('XMLHttpRequest not supported');
    }

    // HEAD Results are usually shorter (faster) than GET
    req.open('HEAD', url, false);
    req.send(null);
    if (req.status == 200) {
        return true;
    }

    return false;
}
{% endcodeblock %}
<ul>
 <li><a href="https://github.com/kvz/phpjs/blob/master/functions/filesystem/file_exists.js">view on github</a></li>
 <li><a href="https://github.com/kvz/phpjs/edit/master/functions/filesystem/file_exists.js">edit on github</a></li>
</ul>
