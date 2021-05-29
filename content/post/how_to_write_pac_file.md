---
title: "How to write proxy PAC file"
date: 2021-05-29T14:34:30+08:00
categories:
  - "computer"
tags:
  - "proxy pac"

---

# Overview

Proxy Auto-Configuration (PAC) is a method used by Web browsers to select a proxy for a given URL. The method for choosing a proxy is written as a JavaScript function contained in a PAC file. This file can be hosted locally or on a network. Browsers can be configured to use the file manually.

# How PAC Files Work

1. Direct all traffic through the first proxy. If it is unreachable, use the second proxy. If both are unavailable go direct:
```js

function FindProxyForURL(url, host) {
   return "PROXY proxy1.my.com:8080; PROXY
   proxy2.my.com:8080; DIRECT"; }
```
2. Direct HTTP traffic as in the first example, but send all HTTPS traffic direct:
```js
function FindProxyForURL(url, host) {
   if (url.substring(0,6)=="https:") return 
   "DIRECT"; else return "PROXY
   proxy1.my.com:8080; PROXY
   proxy2.my.com:8080; DIRECT"; }
```
3. Direct all traffic as in the first example, but send traffic for a given domain direct:
```js

function FindProxyForURL(url, host) {
   if (host=="my.com") return "DIRECT"; else
   return "PROXY proxy1.my.com:8080; PROXY
   proxy2.my.com:8080; DIRECT"; }
```
4. If the client computer is on the specified internal network, go through the proxy. Otherwise go direct:
```js

function FindProxyForURL(url, host) {
   if (isInNet(myIPaddress(), "192.168.1.0",
   "255.255.255.0")) return "PROXY
   proxy1.my.com:8080; PROXY 
   proxy2.my.com:8080; DIRECT"; else return
   "DIRECT"; }
```
# Example PAC File
```js

function FindProxyForURL(url, host) {
// Web sites you wish to go to direct and not through the Web Scanning Services. This 
list would include internally hosted Web sites, intranets, and so on
if (shExpMatch(url,"*.somecompany.co.uk*") ||
   shExpMatch(url,"*.example.com*") ||
   shExpMatch(url,"*.anotherexample.com*"))
{ return "DIRECT"; }
// Internal IP address ranges that you need to be able to go to directly
else if(isInNet(host, "xxx.xxx.xxx.xxx",
   "255.255.0.0") ||
isInNet(host, "xxx.xxx.xxx.xxx",
   "255.255.0.0") ||
isInNet (host, "xxx.xxx.xxx.xxx",
   "255.255.0.0"))
{ return "DIRECT"; }
// Send all other HTTP HTTPS and FTP traffic to Web Services
else { return
"PROXY proxy.example1.com:8080"; } }

```

# Configuring Google Chrome to Use a PAC File

1. Open Google Chrome, open the Chrome menu, then click Settings. The Settings window appears.

2. Click Show advanced settings.... The Show advanced settings... window appears.

3. Go to Network and click Change proxy settings.... The Internet Properties window appears.

4. Click LAN settings. The Local Area Network (LAN) Settings window appears.

5. Select Use automatic configuration script and paste the PAC file URL that you copied in step 2. 

6. Click OK to save the configuration.


The reference contains details info https://developer.mozilla.org/en-US/docs/Web/HTTP/Proxy_servers_and_tunneling/Proxy_Auto-Configuration_PAC_file#description
