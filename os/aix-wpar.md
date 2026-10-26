---
title: aix-wpar
---

## WPAR - Workload Partition

mkwpar -n wpar1 -N interface=en1 address=10.1.1.81 ... vytvori wpar wpar1 s IP 10.1.1.81 na sitovce en1 a LV pro wpar  
startwpar ... nastartuje wpar  
lswpar ... vypise wpary  
clogin wpar1 .... pripoji se k wparu  
syncwpar ... synchronizuje filesety globalniho prostredi hostitelskeho systemu z hostovanym wparem  
chwpar -R shares_CPU=20 wpar1 ... priradi wparu max. 20% procesoru  
stopwpar ... zastavi wpar  
rmwpar ... snaze wpar
