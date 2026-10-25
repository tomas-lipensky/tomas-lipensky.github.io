# Solaris - ostatni prikazy

mt ... (magnetic tape) ovladani pasky
ufsdump ... zalohovani fs

/usr/openv/netbackup/bin/bpps -a ... jede Netbackup?
/usr/local/bin/netbackup/sauv_monitor ... report za 24 hodin
/usr/openv/netbackup/bin/admincmd/bpdbjobs -report ... report za 3 dny
bperror -U -problems -hoursago 24
bpmedia -ev WH128D
vmquery -m WH128D
format
usermod
bpgetmedia -p SCRATCH | awk '{print $1}'
bpadm
vmchange ... hybani s paskama
vmchange -res -m PSA198 -mt dlt -rt none -rc1 0 -rc2 0 ... eject tape PSA198
