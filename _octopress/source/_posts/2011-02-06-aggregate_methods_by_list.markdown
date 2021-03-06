---
layout: post
title: "JavaScript aggregate_methods_by_list function"
date: 2011-02-06 12:00:00
comments: true
sharing: true
footer: true
permalink: /phpjs/functions/aggregate_methods_by_list
categories: [ objaggregation, functions ]
---
A JavaScript equivalent of PHP's aggregate_methods_by_list
<!-- more -->
{% codeblock objaggregation/aggregate_methods_by_list.js lang:js https://raw.github.com/kvz/phpjs/master/functions/objaggregation/aggregate_methods_by_list.js raw on github %}
function aggregate_methods_by_list (obj, class_name, properties_list, exclude) {
    // http://kevin.vanzonneveld.net
    // +   original by: Brett Zamir (http://brett-zamir.me)
    // %          note 1: We can't copy privileged methods, as those require instantiation (with potential side-effects when called)
    // %          note 1: We've chosen not to assign to or create a prototype object on the destination object even if the original object had the methods on its prototype
    // *     example 1: var A = function () {};
    // *     example 1: A.prototype.method = function () {};
    // *     example 1: var b = {};
    // *     example 1: aggregate_methods_by_list(b, 'A', ['method'], false);
    // *     returns 1: undefined

    var p = '',
        i = 0,
        record = {},
        pos = -1;
    var indexOf = function (value) {
        for (var i = 0, length = this.length; i < length; i++) {
            if (this[i] === value) {
                return i;
            }
        }
        return -1;
    };

    if (typeof class_name === 'string') { // PHP behavior
        class_name = this.window[class_name];
    }

    // BEGIN REDUNDANT
    this.php_js = this.php_js || {};
    this.php_js.aggregateKeys = this.php_js.aggregateKeys || [];
    this.php_js.aggregateRecords = this.php_js.aggregateRecords || []; // Needed to allow deaggregate() and aggregate_info()
    this.php_js.aggregateClasses = this.php_js.aggregateClasses || [];
    var getFuncName = function (fn) {
        var name = (/\W*function\s+([\w\$]+)\s*\(/).exec(fn);
        if (!name) {
            return '(Anonymous)';
        }
        return name[1];
    };
    // END REDUNDANT
    this.php_js.aggregateClasses.push(getFuncName(class_name));

    if (!properties_list.indexOf) {
        properties_list.indexOf = indexOf;
    }

    if (exclude) {
        for (p in class_name) {
            if (!(p in obj) && typeof class_name[p] === 'function' && p[0] !== '_' && properties_list.indexOf(p) === -1) { // Static (non-private) class methods
                obj[p] = class_name[p];
                record[p] = class_name[p];
            }
        }
        for (p in class_name.prototype) {
            if (!(p in obj) && typeof class_name.prototype[p] === 'function' && p[0] !== '_' && properties_list.indexOf(p) === -1) { // Prototype (non-private) instance methods
                obj[p] = class_name.prototype[p];
                record[p] = class_name.prototype[p];
            }
        }
    } else {
        for (i = 0; i < properties_list.length; i++) {
            p = properties_list[i];
            if (!(p in obj) && p in class_name && p[0] !== '_' && typeof class_name.prototype[p] === 'function') { // Static (non-private) class methods
                obj[p] = class_name[p];
                record[p] = class_name[p];
            } else if (!(p in obj) && p in class_name.prototype && p[0] !== '_' && typeof class_name.prototype[p] === 'function') { // Prototype (non-private) instance methods
                obj[p] = class_name.prototype[p];
                record[p] = class_name.prototype[p];
            }
        }
    }
    if (!this.php_js.aggregateKeys.indexOf) {
        this.php_js.aggregateKeys.indexOf = indexOf;
    }
    pos = this.php_js.aggregateKeys.indexOf(obj);
    if (pos !== -1) {
        this.php_js.aggregateRecords[pos].push(record);
        this.php_js.aggregateClasses[pos].push(getFuncName(class_name));
    } else {
        this.php_js.aggregateKeys.push(obj);
        this.php_js.aggregateRecords.push([record]);
        this.php_js.aggregateClasses[0] = [];
        this.php_js.aggregateClasses[0].push(getFuncName(class_name));
    }
}
{% endcodeblock %}
<ul>
 <li><a href="https://github.com/kvz/phpjs/blob/master/functions/objaggregation/aggregate_methods_by_list.js">view on github</a></li>
 <li><a href="https://github.com/kvz/phpjs/edit/master/functions/objaggregation/aggregate_methods_by_list.js">edit on github</a></li>
</ul>
