---
layout: post
title: "JavaScript runkit_method_copy function"
date: 2012-05-17 18:49
comments: true
sharing: true
footer: true
permalink: functions/runkit_method_copy
categories: [ runkit, functions ]
---
A JavaScript equivalent of PHP's runkit_method_copy
<!-- more -->
{% codeblock runkit/runkit_method_copy.js lang:js https://raw.github.com/kvz/phpjs/master/functions/runkit/runkit_method_copy.js raw on github %}
function runkit_method_copy (dClass, dMethod, sClass, sMethod) {
    // http://kevin.vanzonneveld.net
    // +   original by: Brett Zamir (http://brett-zamir.me)
    // *     example 1: runkit_method_copy('newClass', 'newMethod', 'someClass', 'someMethod');
    // *     returns 1: true
/*
    function A(){}
    function C(){}
    C.d = function () {alert('inside d');}
    runkit_method_copy('A', 'b', 'C', 'd');
    A.b(); // 'inside d'
    */
    sMethod = sMethod || dMethod;

    if (typeof dClass === 'string') {
        dClass = this.window[dClass];
    }
    if (typeof sClass === 'string') {
        sClass = this.window[sClass];
    }

    //dClass[dMethod] = sClass[sMethod]; // Copy from static to static method (as per PHP example)
    dClass.prototype[dMethod] = sClass.prototype[sMethod]; // To copy from instance to instance
    return true;
}
{% endcodeblock %}
<ul>
 <li><a href="https://github.com/kvz/phpjs/blob/master/functions/runkit/runkit_method_copy.js">view on github</a></li>
 <li><a href="https://github.com/kvz/phpjs/edit/master/functions/runkit/runkit_method_copy.js">edit on github</a></li>
</ul>
