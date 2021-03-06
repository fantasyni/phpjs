---
layout: post
title: "JavaScript array_count_values function"
date: 2011-02-06 12:00:00
comments: true
sharing: true
footer: true
permalink: /phpjs/functions/array_count_values
categories: [ array, functions ]
---
A JavaScript equivalent of PHP's array_count_values
<!-- more -->
{% codeblock array/array_count_values.js lang:js https://raw.github.com/kvz/phpjs/master/functions/array/array_count_values.js raw on github %}
function array_count_values (array) {
    // http://kevin.vanzonneveld.net
    // +   original by: Ates Goral (http://magnetiq.com)
    // + namespaced by: Michael White (http://getsprink.com)
    // +      input by: sankai
    // +   improved by: Kevin van Zonneveld (http://kevin.vanzonneveld.net)
    // +   input by: Shingo
    // +   bugfixed by: Brett Zamir (http://brett-zamir.me)
    // *     example 1: array_count_values([ 3, 5, 3, "foo", "bar", "foo" ]);
    // *     returns 1: {3:2, 5:1, "foo":2, "bar":1}
    // *     example 2: array_count_values({ p1: 3, p2: 5, p3: 3, p4: "foo", p5: "bar", p6: "foo" });
    // *     returns 2: {3:2, 5:1, "foo":2, "bar":1}
    // *     example 3: array_count_values([ true, 4.2, 42, "fubar" ]);
    // *     returns 3: {42:1, "fubar":1}
    var tmp_arr = {},
        key = '',
        t = '';

    var __getType = function (obj) {
        // Objects are php associative arrays.
        var t = typeof obj;
        t = t.toLowerCase();
        if (t === "object") {
            t = "array";
        }
        return t;
    };

    var __countValue = function (value) {
        switch (typeof(value)) {
        case "number":
            if (Math.floor(value) !== value) {
                return;
            }
            // Fall-through
        case "string":
            if (value in this && this.hasOwnProperty(value)) {
                ++this[value];
            } else {
                this[value] = 1;
            }
        }
    };

    t = __getType(array);
    if (t === 'array') {
        for (key in array) {
            if (array.hasOwnProperty(key)) {
                __countValue.call(tmp_arr, array[key]);
            }
        }
    }
    return tmp_arr;
}
{% endcodeblock %}
<ul>
 <li><a href="https://github.com/kvz/phpjs/blob/master/functions/array/array_count_values.js">view on github</a></li>
 <li><a href="https://github.com/kvz/phpjs/edit/master/functions/array/array_count_values.js">edit on github</a></li>
</ul>
