# Part 7: Evidence and Reporting

## Evidence Checklist

Target identification and ping: Steps 1 to 3, screenshots in evidence/step01 to step03.
Host discovery result: Step 4, evidence/step04_host_discovery.png.
Default Nmap result: Step 5, evidence/step05_default_scan.png.
Version detection result: Steps 6 and 7, evidence/step06_service_version.png and evidence/step07_version_intensity9.png.
OS and aggressive scan results: Steps 8 and 9, evidence/step08_os_detection.png and evidence/step09_aggressive_scan.png.
Full TCP scan evidence: Steps 10, 11 and 12, evidence/step10 to step12.
UDP scan evidence: Steps 15 and 16, evidence/step15_udp_scan.png and evidence/step16_udp_top20_sV.png.
NSE enumeration results: Steps 17 to 22, evidence/step17 to step22.
WhatWeb comparison: Steps 24, 26, 27 and 28, evidence/step24 to step28.
Saved WhatWeb file: Step 30, evidence/step30_whatweb_save.png.

## Final Service Inventory

This table is built directly from my Step 11 scan, sudo nmap -p- -sV 192.168.119.3, which is the most complete scan I ran in this lab.

| Port | Protocol | State | Service | Version | Source |
|------|----------|-------|---------|---------|--------|
| 21 | tcp | open | ftp | vsftpd 2.3.4 | Step 11, confirmed by Step 22 banner |
| 22 | tcp | open | ssh | OpenSSH 4.7p1 Debian 8ubuntu1 | Step 11, confirmed by Step 21 host keys |
| 23 | tcp | open | telnet | Linux telnetd | Step 11 |
| 25 | tcp | open | smtp | Postfix smtpd | Step 11 |
| 53 | tcp | open | domain | ISC BIND 9.4.2 | Step 11, confirmed by Step 17 dns-nsid |
| 80 | tcp | open | http | Apache httpd 2.2.8 (Ubuntu) DAV/2 | Step 11, confirmed by Step 19 and Step 23 |
| 111 | tcp | open | rpcbind | 2 (RPC 100000) | Step 11 |
| 139 | tcp | open | netbios-ssn | Samba smbd 3.X to 4.X | Step 11, confirmed by Step 20 |
| 445 | tcp | open | netbios-ssn | Samba smbd 3.X to 4.X | Step 11, confirmed by Step 20 |
| 512 | tcp | open | exec | netkit-rsh rexecd | Step 11 |
| 513 | tcp | open | login | (no banner) | Step 11 |
| 514 | tcp | open | shell | tcpwrapped | Step 11 |
| 1099 | tcp | open | rmiregistry | GNU Classpath grmiregistry | Step 11 |
| 1524 | tcp | open | bindshell | Metasploitable root shell | Step 11 |
| 2049 | tcp | open | nfs | 2 to 4 (RPC 100003) | Step 11 |
| 2121 | tcp | open | ftp | ProFTPD 1.3.1 | Step 11 |
| 3306 | tcp | open | mysql | MySQL 5.0.51a-3ubuntu5 | Step 11 |
| 3632 | tcp | open | distccd | distccd v1 (GNU 4.2.4) | Step 11, first seen in Step 10 |
| 5432 | tcp | open | postgresql | PostgreSQL DB 8.3.0 to 8.3.7 | Step 11 |
| 5900 | tcp | open | vnc | VNC protocol 3.3 | Step 11 |
| 6000 | tcp | open | X11 | access denied | Step 11 |
| 6667 | tcp | open | irc | UnrealIRCd | Step 11 |
| 6697 | tcp | open | irc | UnrealIRCd | Step 11, first seen in Step 10 |
| 8009 | tcp | open | ajp13 | Apache Jserv Protocol v1.3 | Step 11 |
| 8180 | tcp | open | http | Apache Tomcat/Coyote JSP engine 1.1 | Step 11 |
| 8787 | tcp | open | drb | Ruby DRb RMI, Ruby 1.8, path /usr/lib/ruby/1.8/drb | Step 11, first seen in Step 10 |
| 49173 | tcp | open | mountd | 1 to 3 (RPC 100005) | Step 11, first seen in Step 10 |
| 51767 | tcp | open | status | 1 (RPC 100024) | Step 11, first seen in Step 10 |
| 51966 | tcp | open | nlockmgr | 1 to 4 (RPC 100021) | Step 11, first seen in Step 10 |
| 54203 | tcp | open | java-rmi | GNU Classpath grmiregistry | Step 11, first seen in Step 10 |

On top of this TCP list, my UDP scans in Steps 15 and 16 also found port 53 (domain, ISC BIND 9.4.2), port 111 (rpcbind), port 137 (netbios-ns), port 138 (netbios-dgm, open|filtered), port 2049 (nfs), port 49152 (status), and ports 68 and 69 (dhcpc and tftp, both open|filtered).

Overall, this machine exposes 30 open TCP ports and at least 8 relevant UDP ports, which is an unusually large attack surface for a single host, and this is consistent with Metasploitable 2 being deliberately built as an insecure practice target.
