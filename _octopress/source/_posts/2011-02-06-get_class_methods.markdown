---
layout: post
title: "JavaScript get_class_methods function"
date: 2011-02-06 12:00:00
comments: true
sharing: true
footer: true
permalink: /phpjs/functions/get_class_methods
categories: [ classobj, functions ]
---
A JavaScript equivalent of PHP's get_class_methods
<!-- more -->
{% codeblock classobj/get_class_methods.js lang:js https://raw.github.com/kvz/phpjs/master/functions/classobj/get_class_methods.js raw on github %}
function get_class_methods (name) {
    // http://kevin.vanzonneveld.net
    // +   original by: Brett Zamir (http://brett-zamir.me)
    // *     example 1: function Myclass () {this.privMethod = function (){}}
    // *     example 1: Myclass.classMethod = function () {}
    // *     example 1: Myclass.prototype.myfunc1 = function () {return(true);};
    // *     example 1: Myclass.prototype.myfunc2 = function () {return(true);}
    // *     example 1: get_class_methods('MyClass')
    // *     returns 1: {}
    var constructor, retArr = {},
        method = '';

    if (typeof name === 'function') {
        constructor = name;
    } else if (typeof name === 'string') {
        constructor = this.window[name];
    } else if (typeof name === 'object') {
        constructor = name;
        for (method in constructor.constructor) { // Get class methods of object's constructor
            if (typeof constructor.constructor[method] === 'function') {
                retArr[method] = constructor.constructor[method];
            }
        }
        // return retArr; // Uncomment to behave as "class" is usually defined in JavaScript convention (and see comment below)
    }
    for (method in constructor) {
        if (typeof constructor[method] === 'function') {
            retArr[method] = constructor[method];
        }
    }
    // Comment out this block to behave as "class" is usually defined in JavaScript convention (and see comment above)
    for (method in constructor.prototype) {
        if (typeof constructor.prototype[method] === 'function') {
            retArr[method] = constructor.prototype[method];
        }
    }

    return retArr;
}
{% endcodeblock %}
<ul>
 <li><a href="https://github.com/kvz/phpjs/blob/master/functions/classobj/get_class_methods.js">view on github</a></li>
 <li><a href="https://github.com/kvz/phpjs/edit/master/functions/classobj/get_class_methods.js">edit on github</a></li>
</ul>
