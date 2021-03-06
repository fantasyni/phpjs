---
layout: post
title: "JavaScript quoted_printable_decode function"
date: 2012-05-17 18:49
comments: true
sharing: true
footer: true
permalink: functions/quoted_printable_decode
categories: [ strings, functions ]
---
A JavaScript equivalent of PHP's quoted_printable_decode
<!-- more -->
{% codeblock strings/quoted_printable_decode.js lang:js https://raw.github.com/kvz/phpjs/master/functions/strings/quoted_printable_decode.js raw on github %}
function quoted_printable_decode (str) {
    // http://kevin.vanzonneveld.net
    // +   original by: Ole Vrijenhoek
    // +   bugfixed by: Brett Zamir (http://brett-zamir.me)
    // +   reimplemented by: Theriault
    // +   improved by: Brett Zamir (http://brett-zamir.me)
    // +   bugfixed by: Theriault
    // *     example 1: quoted_printable_decode('a=3Db=3Dc');
    // *     returns 1: 'a=b=c'
    // *     example 2: quoted_printable_decode('abc  =20\r\n123  =20\r\n');
    // *     returns 2: 'abc   \r\n123   \r\n'
    // *     example 3: quoted_printable_decode('012345678901234567890123456789012345678901234567890123456789012345678901234=\r\n56789');
    // *     returns 3: '01234567890123456789012345678901234567890123456789012345678901234567890123456789'
    // *    example 4: quoted_printable_decode("Lorem ipsum dolor sit amet=23, consectetur adipisicing elit");
    // *    returns 4: Lorem ipsum dolor sit amet#, consectetur adipisicing elit
    // Removes softline breaks
    var RFC2045Decode1 = /=\r\n/gm,
        // Decodes all equal signs followed by two hex digits
        RFC2045Decode2IN = /=([0-9A-F]{2})/gim,
        // the RFC states against decoding lower case encodings, but following apparent PHP behavior
        // RFC2045Decode2IN = /=([0-9A-F]{2})/gm,
        RFC2045Decode2OUT = function (sMatch, sHex) {
            return String.fromCharCode(parseInt(sHex, 16));
        };
    return str.replace(RFC2045Decode1, '').replace(RFC2045Decode2IN, RFC2045Decode2OUT);
}
{% endcodeblock %}
<ul>
 <li><a href="https://github.com/kvz/phpjs/blob/master/functions/strings/quoted_printable_decode.js">view on github</a></li>
 <li><a href="https://github.com/kvz/phpjs/edit/master/functions/strings/quoted_printable_decode.js">edit on github</a></li>
</ul>
