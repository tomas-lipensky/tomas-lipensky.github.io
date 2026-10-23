# Solaris - ostatni prikazy

mt ... (magnetic tape) ovladani pasky<br />
ufsdump ... zalohovani fs<br />
<br />
/usr/openv/netbackup/bin/bpps -a ... jede Netbackup?<br />
/usr/local/bin/netbackup/sauv_monitor ... report za 24 hodin<br />
/usr/openv/netbackup/bin/admincmd/bpdbjobs -report ... report za 3 dny<br />
bperror -U -problems -hoursago 24<br />
bpmedia -ev WH128D<br />
vmquery -m WH128D<br />
format<br />
usermod<br />
bpgetmedia -p SCRATCH | awk '{print $1}'<br />
bpadm<br />
vmchange ... hybani s paskama<br />
vmchange -res -m PSA198 -mt dlt -rt none -rc1 0 -rc2 0 ... eject tape PSA198<br />
