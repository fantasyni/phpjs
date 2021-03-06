---
layout: post
title: "JavaScript runkit_method_add function"
date: 2011-02-06 12:00:00
comments: true
sharing: true
footer: true
permalink: /phpjs/functions/runkit_method_add
categories: [ runkit, functions ]
---
A JavaScript equivalent of PHP's runkit_method_add
<!-- more -->
{% codeblock runkit/runkit_method_add.js lang:js https://raw.github.com/kvz/phpjs/master/functions/runkit/runkit_method_add.js raw on github %}
function runkit_method_add (classname, methodname, args, code, flags) {
    // http://kevin.vanzonneveld.net
    // +   original by: Brett Zamir (http://brett-zamir.me)
    // *     example 1: function a (){}
    // *     example 1: runkit_method_add ('a', 'b', 'a,b', 'return a+b');
    // *     returns 1: true
    var func, argmnts = [];

    switch (flags) {
    case 'RUNKIT_ACC_PROTECTED':
        throw 'Protected not supported';
    case 'RUNKIT_ACC_PRIVATE':
        throw 'Private not supported';
    case 'RUNKIT_ACC_PUBLIC':
    default:
        break;
    }

    argmnts = args.split(/,\s*/);

    if (typeof classname === 'string') {
        classname = this.window[classname];
    }

    // Could use the following to add as a static method to the class
    //        func = Function.apply(null, argmnts.concat(code));
    //            classname[methodname] = func;
    func = Function.apply(null, argmnts.concat(code));
    classname.prototype[methodname] = func;
    return true;
}
{% endcodeblock %}
<ul>
 <li><a href="https://github.com/kvz/phpjs/blob/master/functions/runkit/runkit_method_add.js">view on github</a></li>
 <li><a href="https://github.com/kvz/phpjs/edit/master/functions/runkit/runkit_method_add.js">edit on github</a></li>
</ul>
