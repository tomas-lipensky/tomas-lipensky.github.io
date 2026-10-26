---
title: Tomas Lipensky - UNIX - Sluzby
---

## [ntp](http://www.akadia.com/services/ntp_synchronize.html)

/usr/sbin/ntpdate -s -b -p 8 -u 129.132.2.21 ... synchronizace casu se serverem
/etc/ntp.conf ... nastaveni serveru ntpd
/etc/rc.d/init.d/ntpd start/stop ... spousteni, zastavovani demona ntpd
ntpq -p ... seznam serveru
ntpdc ... interaktivni prostredi pro prikazy na ntpd
ntpc -c peers  ... seznam klientu
