---
title: aix-errpt
---

ref code B181e436:
it means that HMC lost communication with the server intermitantly

Client failed to send its heartbeat message within the stipulated time
On systems with a redundant service processor, SRC B181E62F, B181E436, or B181B0B6 may be reported during
the installation of firmware level causing a serviceable event to be logged.  The error is caused by
a disruption of the communications, or process contention, between the service processors, during the
firmware installation process.  If any of these SRCs  are reported during the firmware installation
process they will be resolved when the firmware installation is complete and the serviceable events can
be ignored.

if you can communicate with hmc , we can close this ticket
