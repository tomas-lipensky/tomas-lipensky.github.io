---
title: unix
---

## Unixové prikazy

[unixové prikazy](unix-commands)  
[Sluzby](daemons)  
[Emacs](emacs)  
[awk](awk)  
[VI](vi)  
[C](clib)  
[jq](jq)  
[manpage](manpage)  
[nc](nc) ... netcat, ncat  

## Externi odkazy

[expect](http://oreilly.com/catalog/expect/chapter/ch03.html) - programovani v [TCL](/tcl/), umi poslouchat a posilat odpovedi (mozno uzit pro telnet atd)  
[bash](http://www.gnu.org/s/bash/manual/bash.html)  
[http://kutngedg.homelinux.org/blog/](http://kutngedg.homelinux.org/blog/) ... blogy o AIX, LINUX, HP-UX, Solarix, SQL, Disk Arrarys, ...  
[http://www.g-loaded.eu/2005/11/10/](http://www.g-loaded.eu/2005/11/10/) ... blogy o Linux problemech a jejich reseni  
[http://tldp.org/HOWTO/HOWTO-INDEX/howtos.html](http://tldp.org/HOWTO/HOWTO-INDEX/howtos.html) ... navody na ruzne linux problemu  

## Minimální unix - příkazové ekvivalenty

#### netcat

`(echo > /dev/tcp/google.com/22) >/dev/null 2>&1 && echo "UP" || echo "DOWN"` ... netcat -zv google.com  
cat < /dev/null > /dev/tcp/<hostname or ip>/<port>; echo $? ... to samé  

#### curl/wget

```
exec 3<>/dev/tcp/www.google.com/80
echo -e "GET / HTTP/1.1\r\nhost: http://www.google.com\r\nConnection: close\r\n\r\n" >&3
cat <&3
```
 .... curl, nebo wget  

#### ntp

cat </dev/tcp/time.nist.gov/13 ... ntp server  

#### ps

for i in $(ls /proc/[0-9]*/cmdline ); do echo $i $(cat $i 2>/dev/null) | tr '\0' ' '; echo; done ... ps -ef  
ls /proc/6/tasks ... seznam threadů, jako ps -T -p 6  
echo $[^1]

[^1]:  $(cat /proc/uptime | cut -d. -f1) - ($(cat stat | awk '{ print $22}') / $(cat stat | awk '{ print $22}') )  ... kolik sekund jede proces  
echo $[^2]

[^2]:  $(cat stat | awk '{ print $14}') + $(cat stat | awk '{ print $15}') + $(cat stat | awk '{ print $16}') + $(cat stat | awk '{ print $17}')  ... kolik tiků si vzal proces  
CPU% podíl předchzích  

#### free

cat /proc/meminfo

```
wget ()
{
  IFS=/ read proto z host query <<< "$1"
  exec 3< /dev/tcp/$host/80
  {
    echo GET /$query HTTP/1.1
    echo connection: close
    echo host: $host
    echo
  } >&3
  sed '1,/^$/d' <&3 > $(basename $1)
}

_wget http://www.andreafortuna.org/robots.txt
```

printf "GET / HTTP/1.1\r\nHost: pl-0-eu-central-1.dxwnh.mongodb.net\r\nUser-Agent: linux\r\nAccept: */*\r\n\r\n" | openssl s_client -connect server:port -quiet ... alternativa na curl https  

{ echo -e "GET / HTTP/1.0\r\nHost: www.google.com\r\n\r" >&3; cat <&3 ; } 3<> /dev/tcp/www.google.com/80 ... jako curl  

grep -v "rem_address" /proc/net/tcp  | awk  '{x=strtonum("0x"substr($3,index($3,":")-2,2)); for (i=5; i>0; i-=2) x = x"."strtonum("0x"substr($3,i,2))}{print x":"strtonum("0x"substr($3,index($3,":")+1,4))}' ... jako netstat -anL
