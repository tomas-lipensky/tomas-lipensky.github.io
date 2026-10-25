# WebSphere Application Server

## Interni odkazy

[WAS](was.html)

## Generovani snapu, dumpu atd.

## Prohlizeni logu, snapu, dumpu atd.

Ridi je parametr -Xdump - tzv. dump agent.

#### Snap traces - Snap.*.trc

Obsahuji stopovaci body (tracepoint data) ktera se drzi v stopovacich bugrech. Lokace v profilu, napr. /usr/WebSphere/v7/Profiles/node01

<dl>
java com.ibm.jvm.format.TraceFormat  Snap.20131027.144227.12648526.0004.trc -summary ... prohlizeni Snap.*.trc souboru
java com.ibm.jvm.format.TraceFormat  Snap.20131027.144227.12648526.0004.trc -uservmid 30e41e00 ... podrobne indormace on VMID
</dl>

#### Javadumps - javacore.*.txt

Javadumpy jsou analyzy JVM, obsahujici informace o vlaknech nactenych tridach a heap statistikach. Java parametr -Xdump:java ovlivnuje co se bude dit pri signalech jako napr. SIGQUIT nebo vaznych situacich

<dl>
	kill -3 PID ... vytvori thread dump
	wsadmin prikaz k vyvolani AdminControl.invoke(objName,'dumpThreads')
    IBM Support Assistent - IBM Thead and Monitor Dump Analyzer
</dl>

#### system dumps - core.*.dmp

Java parametr -Xdump:system:events=vmstop,file=my.dmp ovlivnuje vytvareni heap dumpu.

<dl>
	jextract -Xrealtime <core_file>
	jdmpview -Xrealtime -zip <zip file>
	jextract -Xrealtime -nozip <core_file>
	jdmpview -Xrealtime -core <core file>
IBM Support Assistent - IBM Thead and Monitor Dump Analyzer
IBM Support Assistent - IBM Monitoring and Diagnostic Tools for Java - Dump Analyzer
</dl>

#### heap dumps

Obvykle sobory phd. Java parametr -Xdump:none -Xdump:heap:events=vmstop,opts=PHD+CLASSIC

<dl>
	Memory Dump Diagnostic for Java™ (MDD4J) ... na prohlizeni Heap dumpu
	Promenne WASu:
	IBM_HEAPDUMPDIR ... lokace heap dumpu
    IBM_HEAPDUMP_OUTOFMEMORY ... true - zapne generovani heap dumpu pri OutOfMemory problemu
    IBM_HEAPDUMPIBM_HEAP_DUMP ... true - aktivuje produkci heapdumpyu pri volani signalu
    JAVA_DUMP_OPTS ... [podminky](http://publib.boulder.ibm.com/infocenter/realtime/v1r0/topic/com.ibm.rt.doc.10/diag/tools/dumpagents_env.html) za jakych se tvori dumpy

</dl>

#### Console dumps

vystup jde do stdout a stderr. Aktivuje se java parametrem -Xdump:console:events=thrstart+thrstop,range=1..1

#### ffdc
