---
title: "How does HTTP and HTTPS Proxies Work "
date: 2020-08-18T13:34:29+08:00
categories:
  - "computer"
---

HTTP proxy gets a plain-text request and [in most but not all cases] sends a different HTTP request to the remote server, then returns information to the client.
The specific flow of the HTTP proxy server is as follows.
![http_proxy](https://milestone-of-se.nesuke.com/wp-content/uploads/2018/05/en-proxy-1.png)

HTTPS proxy is a relayer, which receives special HTTP request (CONNECT verb) and builds an opaque tunnel to the destination server (which is not necessarily even an HTTPS server). Then the client sends SSL/TLS request to the server and they continue with SSL handshake and then with HTTPS (if requested).

Proxy connection of https communication.

![https_proxy](https://milestone-of-se.nesuke.com/wp-content/uploads/2018/05/en-proxy-2.png)
