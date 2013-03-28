JQuery jsonp request bug
==================================================

This bug appears on all jquery versions, including the lastest stable version and the developing version when a jsonp request is done.

Before jsonp request completes, for some reason you need to cancel the request using jqXHR.abort(). The abort function will remove the script tag from the page (used to perform the request), and remove the javascript temporary function (jQuery19107910770212765783_1364346482029), that handles the request.

What happens next is a javascript error, because when the request is issued by the browser, even if you remove the script tag from the page, when the server responds the javascript will be executed and the function is no longer available, because it has been removed by the abort call.

This page reproduces the error using the latest jquery stable version (1.9.1). To see the error occurring, host this page on a web server (iis, apache or a node process) and open your javascript console.

Alternatively you can check this page on jsFiddle: http://jsfiddle.net/XvW4B/

I submitted a patch to jquery, solving this problem, but if you cannot wait for the resolution, check the jquery-fixed.js script.

Hope it helped!
