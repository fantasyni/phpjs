---
layout: post
title: "JavaScript similar_text function"
date: 2011-02-06 12:00:00
comments: true
sharing: true
footer: true
permalink: /phpjs/functions/similar_text
categories: [ strings, functions ]
---
A JavaScript equivalent of PHP's similar_text
<!-- more -->
{% codeblock strings/similar_text.js lang:js https://raw.github.com/kvz/phpjs/master/functions/strings/similar_text.js raw on github %}
function similar_text (first, second) {
    // http://kevin.vanzonneveld.net
    // +   original by: Rafał Kukawski (http://blog.kukawski.pl)
    // +   bugfixed by: Chris McMacken
    // *     example 1: similar_text('Hello World!', 'Hello phpjs!');
    // *     returns 1: 7
    // *     example 2: similar_text('Hello World!', null);
    // *     returns 2: 0
    if (first === null || second === null || typeof first === 'undefined' || typeof second === 'undefined') {
        return 0;
    }

    first += '';
    second += '';

    var pos1 = 0,
        pos2 = 0,
        max = 0,
        firstLength = first.length,
        secondLength = second.length,
        p, q, l, sum;

    max = 0;

    for (p = 0; p < firstLength; p++) {
        for (q = 0; q < secondLength; q++) {
            for (l = 0;
            (p + l < firstLength) && (q + l < secondLength) && (first.charAt(p + l) === second.charAt(q + l)); l++);
            if (l > max) {
                max = l;
                pos1 = p;
                pos2 = q;
            }
        }
    }

    sum = max;

    if (sum) {
        if (pos1 && pos2) {
            sum += this.similar_text(first.substr(0, pos2), second.substr(0, pos2));
        }

        if ((pos1 + max < firstLength) && (pos2 + max < secondLength)) {
            sum += this.similar_text(first.substr(pos1 + max, firstLength - pos1 - max), second.substr(pos2 + max, secondLength - pos2 - max));
        }
    }

    return sum;
}
{% endcodeblock %}
<ul>
 <li><a href="https://github.com/kvz/phpjs/blob/master/functions/strings/similar_text.js">view on github</a></li>
 <li><a href="https://github.com/kvz/phpjs/edit/master/functions/strings/similar_text.js">edit on github</a></li>
</ul>
