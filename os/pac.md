---
title: pac
---

[https://findproxyforurl.com/pac-functions/](https://findproxyforurl.com/pac-functions/)

## Funkce

if (shExpMatch(host, "*.local")) ... kdyz je host roven regularnimu vyrazu  
if (dnsDomainIs(host, "google.com") || dnsDomainIs(host, "www.google.com")) ... kdyz je domena jedna z nasledujicich  
if (isInNet(dnsResolve(host), "172.16.0.0", "255.240.0.0")) ... kdyz je cil v nasledujici siti  
if (!isInNet(myIpAddress(), "10.10.1.0", "255.255.255.0")) ... kdyz moje adrese NENI v nasledujici siti  

return "PROXY proxy1.example.com:8080"; ... pouzije se proxy  
else return "DIRECT" ... nepouzije se proxy
