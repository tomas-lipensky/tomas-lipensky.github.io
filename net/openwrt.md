# OpenWRD

## Typy routru a firmware

### WRT54GL

- Stahnout a nahrat image [Kamikaze](http://downloads.openwrrt.org/kamikaze/8.09.2/brcm-2.4): openwrt-54h-squashfs.bin (jadro 2.4, umoznuje menit parametry nvram)
- pripojit se na router: telnet 192.168.1.1
- nvram set boot_wait=on
- nvram set boot_time=10
- nvram commit &amp;&amp; reboot
- Stahnout a nahrat image [Backfire](http://downloads.openwrrt.org/backfire/10.03/brcm47xx): openwrt-54h-squashfs.bin (jadro 2.6)
- resetnout router, treba vytazenim napajeni a pocat 5 sekund
- nabidnout na stazeni image pres tftp: tftp -i 192.168.1.1 PUT openwrt-54h-squashfs.bin
- pripojit se na router: telnet 192.168.1.1
