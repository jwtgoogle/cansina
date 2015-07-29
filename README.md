Cansina是一款用于发现网站的敏感目录和内容的安全测试工具，通过分析服务器的响应进行探测并使用sqlite保证数据持久性。
特性
         多线程
         HTTP/S 代理支持
         数据持久性 (sqlite3)
         多后缀支持 (-e php,asp,aspx,txt…)
         网页内容识别 (will watch for a specific string inside web page content)
         跳过假404错误
         可跳过被过滤的内容
         报表功能
         基础认证
         Cansina
参数说明：
         -u:为你的url地址-p：是的自己的路径文件或者fuzzdb都行。自己定义。cansina.py -u target_site_url -p payload_filename
         -b：禁止的响应代码如果404 400 500cansina.py -u target_site_url -p payload_filename -b 404,400,500
         -e：简单点，只扫php扩展。
         cansina.py -u target_site_url -p payload_filename -e php
         -e：这个同上你懂的。
         cansina.py -u target_site_url -p payload_filename -e php,asp,aspx
         -c：在网页中查找一些关键字。也可以添加多个关键字。
         cansina.py -u target_site_url -p payload_filename -c look_for_this_text
         -d：就是查看文件中是否有要找的字符，如果没有将自动返回404特征码。
         cansina.py -u target_site_url -p payload_filename -d look_for_this_text
         自动检查并返回特定的404 200等
         cansina.py -u target_site_url -p payload_filename -D
=======

Cansina is a Web Content Discovery Application.

It is well known Web applications doesn't publish all their resources or links to them, 
so the only way to discover those resources is....asking for them!

Useful during a pentesting or web security audit. Cansina mission is to help making 
requests and filtering the responses to tell apart if it is an existing resource or
just an annoying or disguised 404. Of course other kind of useful responses 
(401, 403, ...) are processed in a similar fashion.

The responses are kept in a sqlite database for later process.

There is an ongoing effort to add features via plugins.

Feature requests and comments are welcome.

Screenshot
----------

![CansinaImage](https://github.com/deibit/cansina/raw/gh-pages/images/cansina-showcase.png "Image")

Features
--------

- Multithreading
- Http / Https
- Proxy support
- Data persistence
- Basic Authentication

Usage
-----

cansina.py -h for a comprehensive list of features and choices

**Simple case**

*cansina.py -u target_url -p payload_filename*

Will make GET requests using 4 threads by default 

**Banning HTTP responde codes to output**

*cansina.py -u target_url -p payload_filename -b 404,400,500*

Selected codes will be skipped

**Adding a .php extension to every record in payload**

*cansina.py -u target_url -p payload_filename -e php*

Make all payload entries end with an extension

**Adding a list of extensions**

*cansina.py -u target_url -p payload_filename -e php,asp,aspx*

Same as above but will repeat every request for every extension provided

**Inspecting content**

*cansina.py -u target_url -p payload_filename -c look_for_this_text*

Cansina will report to screen if the content is detected in response

**Filtering by content**

*cansina.py -u target_url -p payload_filename -d look_for_this_text*

If the content is found it will be processed as a 404 Not Found page

**Autodiscriminator**

*cansina.py -u target_url -p payload_filename -D*

First, Cansina will try to make and remember a 404 response and will skip similar responses

**Replacing**

*cansina.py -u target_url/***_this/ -p payload_filename*

Simple string replacing. Useful when a URL pattern is observable

**Size filtering**

*cansina.py -u target_url -s 1495 -p payload_filename*

If you don't want a response and know its size is fixed this could help skipping all those responses

**Uppercase all requests**

*cansina.py -u target_url -U -p payload_filename*

Just make every payload UPPERCASE

**Threading**

*cansina.py -u target_url -t8 -p payload_filename*

Set the threading level. 4 by default.

**Change GET -> HEAD requests**

*cansina.py -u target_url -H -p payload_filename*

Make requests using HEAD HTTP method. Be aware size and content filtering won't work

**Delay between requests**

*cansina.py -u target_url -T 1.25 -p payload_filename*

Set a delay between resquests. Time is set in float format. E.g: 1.25 seconds

**User agent**

*cansina.py -u target_url -p payload_filename -a user_agent*

Set an alternative User-Agent string

**Proxy requests**

*cansina.py -u target_url -p payload_filename -Phttp://127.0.0.1:8080*

Simple http proxy

**Basic authentication**

*cansina.py -u target_url -p payload_filename -Auser:password*

Manages basic authentication

Dependencies
------------

- [requests](https://github.com/kennethreitz/requests)
- Python 2.7.x 
- Python 3.x (soon)

Payloads
--------

- [fuzzdb](https://code.google.com/p/fuzzdb/)

License information
-------------------

Copyright (C) 2013-2015 David García (daganu@gmail.com)

License: GNU General Public License, version 3 or later; see LICENSE.txt
         included in this archive for details.
