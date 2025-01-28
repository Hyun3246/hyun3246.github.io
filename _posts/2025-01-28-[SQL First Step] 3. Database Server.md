---
title:  "[SQL First Step] 3. Database Server"
excerpt: "Client/Server Model, CGI"

categories:
  - Data Science & ML
tags:
  - [Database]

use_math: true
toc: true
toc_sticky: true

date: 2025-01-28
last_modified_at: 2025-01-28

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/SQL First Step.png
---
# Client/Server Model
RDBMS runs as a client/server model. <span style="color:#F5F5F7">Client can send 'request' to server and server returns 'response' to the request</span>.
<br/>
<figure style="display:block; text-align:center;">
<img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/SQL First Step/Client Server model.png"
    style="width: 40%; height: auto; margin:10px">
</figure>
<br/>

The following is an example of client/server model of web system. A client sends a request about web page reading, and a web server returns HTML file.
<br/>
<figure style="display:block; text-align:center;">
<img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/SQL First Step/Web system client Server example.png"
    style="width: 40%; height: auto; margin:10px">
</figure>
<br/>

In RDBMS, <span style="color:#F5F5F7">user authorization</span> step is added before request. As RDBMS can limit access to DB according to the users, a client should pass through authorization (e.g. ID and PW) first. After the authorization, a client can send a request.
<br/>
<figure style="display:block; text-align:center;">
<img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/SQL First Step/RDBMS user authorization step.png"
    style="width: 40%; height: auto; margin:10px">
</figure>
<br/>


## Structure of Web Application
If the webpage is only composed of static HTML, a web server is enough. However, to generate HTML dynamically, we need control program. In web server, there is an extension for dynamic contents called <span style="color:#F5F5F7">CGI</span>. The following is a structure of using CGI in web.
<br/>
<figure style="display:block; text-align:center;">
<img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/SQL First Step/Structure of using CGI in web.png"
    style="width: 40%; height: auto; margin:10px">
</figure>
<br/>

In database field, <span style="color:#F5F5F7">CGI becomes a client for database</span>. Focus on the right part of the image below. After authorization to access, CGI delivers SQL requests to DB and DB returns responses to CGI.
<br/>
<figure style="display:block; text-align:center;">
<img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/SQL First Step/Structure of using CGI in DB.png"
    style="width: 40%; height: auto; margin:10px">
</figure>
<br/>

## MySQL
In MySQL, a client and a server runs in the same computer. As we still need network connection, client pass through network and access to server, which is called 'loop back' access.
<br/>
<figure style="display:block; text-align:center;">
<img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/SQL First Step/Loop back of MySQL.png"
    style="width: 40%; height: auto; margin:10px">
</figure>
<br/>

<br/>
<br/>

*All images, except those with separate source indications, are excerpted from lecture materials.*