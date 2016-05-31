---
title: "Don't mix javascript with jsp, php"
author: An, Hyeong-woo
layout: post
tags:
  - php
  - javascript
  - jsp
---

There is repeated CSS, js on codes I maintain. Naturally I've tried to divide js, CSS from the file. But, IDE alert errors after extract js. Because codes below:

    var url = "http://${pageContext.request.serverName}:${pageContext.request.serverPort}/api/";

`${pageContext.request.serverName}` point domain part on URL in jsp - or IP number. PHP version is below:

    var url = "http://<?= $_SERVER['HTTP_HOST'] ?>/api/";

These codes degrade readability and confuse other developers. Bad. Instead, simply write like below using js.

    var url = location.origin + '/api/';

IE lower than 10 has not `window.location.origin` object, so insert below code before use `origin` object.

<pre>if (!window.location.origin) {
  window.location.origin = window.location.protocol + "//" + window.location.hostname + (window.location.port ? ':' + window.location.port: '');
}</pre>

## Using server-side value on javascript

In case retreive server-side value, can't above method. Suppose you need to `$username` on javascript. You can add `$username` to some location of DOM, and javascript can use it. There is phrase of "Hi, An Hyeong woo!" on somewhere. You can add the value to there. This is also logical. HTML may be below(I'd rather not escape html. Do it if you need).

	<p>
		Hi, 
		<span id="#username" data-username="<?= $username ?>">
			<?= $username ?>
		</span>
	</p>

You can retreive using jQuery.

    var username = $('#username').data('username');

A value like `post_id` can be taken out from somewhere HTML DOM.

    var post_id = $('[name="post_id"]').val();


## JSON using big size server-side data

Big JSON data should be passed to client when draw chart. In this case, the above method has limit. Simply use ajax and codes will be clean.

PHP codes response to ajax are below:

    header('content-type: application/json; charset=utf-8');
    // $data variable setting process is skipped.
    echo json_encode($data);

By the way, server take one more request with above way. And not a case data dynamically change, is there no reason add JSON to page with script tag? Maybe other developers will be confused as call ajax request on static page.

Below code is a compromise. Most javascript code should be divided to other file. Only data JSON is added to page with script tag.

    <script>
    var data = <?= json_encode($data) ?>;
    </script>

Slightly annoying, but other developers can understand easily this code.

You can come across a situation mix more code. That case, you must think deeply to take out a solution using javascript. Again, I added only `var data` variable to `script` tag and rest codes to divided file.


## Conclusion

Except exceptinal case has big JSON data, you can divide javascript from server-side code in most case. You must do so. Any time you think that - it's simple to mix js with jsp or php - it may be wrong. Do not. There must be other solutions.

Purpose is simply getting code readability. Other developers - include you - read your code you write now after some years. They have to understand easily the code. The code seek right now convenience is mostly bad.