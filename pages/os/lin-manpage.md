.TH PILOTAGE 1 LOCAL
.SH NAME
pilotage - checks and print the status of monitored processes, FS's and URLs on stdout
.SH SYNOPSIS
.B pilotage
.B [
.I -v | -h | -f | -q | -a XXX | -m XXX | -d XXX
.B "]
.SH AVAILABILITY
UNIX platforms: Linux, AIX, HP-UX, Solaris
.SH DESCRIPTION
pilotage makes a test of all processes, file systems and URL's defined in the configuration files of the monitoring tools: BMC Patrol, DM Unix, IBM Tivoli Monitoring v.5 and IBM Tivoli Monitoirng v.6. It can also work with maintenance flag on ITMv5 and ITMv6.
.SH OPTIONS
If there are on options, it will make check of all defined configuration files and check the points defined in the config files. It prints the status of defined points (processes, file systems and URLs) on the standard output.
.TP 5
1.f
forces to run pilotage on the different platforms than Linux, AIX, HP-UX and Solaris
.TP
1.h
help message - short description and list of options
.TP
1.v
version of the tool
.TP
1.q
quite mode - it shows only alerts - processes, FSs and URLs, which doesn't work
.TP
1.m CH12345678
Defines the maintenance for the ticket CH12345678
.TP
1.a CH12345678
activates maintenance flag for the ticket CH12345678
.TP
1.d CH12345678
deactivates maintenance flag for the ticket CH12345678
.SH AUTHOR
Tomas Lipensky
