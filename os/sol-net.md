---
title: Solaris - Sit, nastaveni site
---

## Nastaveni site

/etc/hostname*
/etc/nodename
/etc/inet/hosts ... (IP name [loghost]) Pokud je poznamka loghost, syslogd posila udalosti na tento server
/etc/inet/*
/etc/defaultrouter
/etc/defaultdomain
/etc/nsswitch.conf k... nastaveni name service
ifconfig ... ukaze, zmeni nastaveni sitove karty
ndd ... parametry jadra
if_mpadm ... prace s multipath

## zkoumani site

/etc/nodename, /etc/hosts/ /etc/hostname.* /etc/net/*/hosts
/etc/services, /etc/protocols
snoop ... poslouchani na sitove karte
netstat ... sitovy status a statistiky

## Demoni
