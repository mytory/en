---
title: changing register_globals=On when PHP runtime
author: Ahn, Hyeong-woo
layout: post
categories:
  - Web Server
tags:
  - php
  - tip
---
I set `register_globals=``Off` on localhost. That must be expected.

But, when maintain some site, there is situation need to set `resister_globals=On`.

To solve this problem, you can use below code. Of course, I do not recommend. This is totally expedient.

<pre>extract($_REQUEST);</pre>

You know, `extract()` function take out variables from array using key. `$_REQUEST` is array has `$_GET` values and `$_POST` values. If you set above code in first file that all files includes, you can produce same effect as fixing `register_globals` to `On` in `php.ini`.

Again, I absolutely do not recommend. This code should be used only when unavoidable. At the end of the work the code should be deleted.

But You probably will forget. At least, write as follow:

<pre>if($_SERVER['REMOTE_ADDR'] == 127.0.0.1){
  extract($_REQUEST);
}</pre>

end.