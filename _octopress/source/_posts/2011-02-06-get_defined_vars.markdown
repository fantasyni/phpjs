---
layout: post
title: "JavaScript get_defined_vars function"
date: 2011-02-06 12:00:00
comments: true
sharing: true
footer: true
permalink: /phpjs/functions/get_defined_vars
categories: [ var, functions ]
---
A JavaScript equivalent of PHP's get_defined_vars
<!-- more -->
{% codeblock var/get_defined_vars.js lang:js https://raw.github.com/kvz/phpjs/master/functions/var/get_defined_vars.js raw on github %}
function get_defined_vars () {
    // http://kevin.vanzonneveld.net
    // +   original by: Brett Zamir (http://brett-zamir.me)
    // +   bugfixed by: Brett Zamir (http://brett-zamir.me)
    // %        note 1: Test case 1: If get_defined_vars can find itself in the defined vars, it worked :)
    // *     example 1: function test_in_array(array, p_val) {for(var i = 0, l = array.length; i < l; i++) {if(array[i] == p_val) return true;} return false;}
    // *     example 1: funcs = get_defined_vars();
    // *     example 1: found = test_in_array(funcs, 'get_defined_vars');
    // *     results 1: found == true
    var i = '',
        arr = [],
        already = {};

    for (i in this.window) {
        try {
            if (typeof this.window[i] === 'object') {
                for (var j in this.window[i]) {
                    if (this.window[j] && !already[j]) {
                        already[j] = 1;
                        arr.push(j);
                    }
                }
            } else if (!already[i]) {
                already[i] = 1;
                arr.push(i);
            }
        } catch (e) { // Problems accessing some properties in FF (e.g., sessionStorage)
            if (!already[i]) {
                already[i] = 1;
                arr.push(i);
            }
        }
    }

    return arr;
}
{% endcodeblock %}
<ul>
 <li><a href="https://github.com/kvz/phpjs/blob/master/functions/var/get_defined_vars.js">view on github</a></li>
 <li><a href="https://github.com/kvz/phpjs/edit/master/functions/var/get_defined_vars.js">edit on github</a></li>
</ul>
