# ssh-config

```
# HTTP-proxy for all servers
Host *
  ProxyCommand corkscrew http-proxy.example.com 8080 %h %p ~/.ssh/proxyauth
# in ~/.ssh/proxyauth is stored userID and passwd (userID:passwd)

## Another http-proxy solution
Host *.com
  ProxyCommand connect -H proxy.local.net:8080 %h %p

Host Home
  User whyDoYouWantToKnow
  Port 8322
  ProxyCommand connect -S socks.local.net %h %p
#Socks proxy
  HostName harisund.com

Host Office
  User UberConfidential
  Port 22
  HostName machine.whereIwork.com
  
```
