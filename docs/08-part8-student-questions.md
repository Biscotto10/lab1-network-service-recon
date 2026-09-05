# Part 8: Student Questions

## 1. What is reconnaissance?

Reconnaissance is the first step I take before doing anything else on a target. It means collecting information about a system without changing it and without trying to break into it: which hosts are alive, which ports are open, what software is running behind them, and what versions those services are. In this lab, this is exactly what I did with Nmap, curl and WhatWeb. I never logged into anything or sent anything harmful, I only observed. Every finding, the IP address of Metasploitable 2, the 30 open ports, the versions of vsftpd, OpenSSH, Apache and the rest, counts as reconnaissance because it is purely information gathering.

## 2. What is the difference between host discovery and port scanning?

Host discovery answers the question of which machines on a network are actually alive, without checking what they run. That is what my nmap -sn 192.168.119.0/24 command did in Step 4, it simply told me which of the 256 possible addresses on my subnet responded (192.168.119.1, .2, .3 and .4). Port scanning happens after that, on one specific host I already know is alive, and it tells me which ports on that host are open, closed or filtered. Everything from Step 5 onward is port scanning, done specifically against 192.168.119.3 once I had already identified it as my target.

## 3. Explain open, closed and filtered.

Based on my own results, open means a real service answered. All 23 ports found in Step 5, and later all 30 in Step 10, showed as open because something was really listening there. Closed means the host answered but nothing is running on that port, and my scans reported 977 closed ports in Step 5 and 65505 closed in Step 10, meaning Metasploitable 2 itself told Nmap that nothing was there. Filtered means Nmap got no usable answer at all. I did not see much of this on the TCP side since there is no firewall between Kali and Metasploitable 2, but I did see the related open or filtered state on my UDP scan in Step 15, where ports like 68 and 69 came back as open or filtered because Nmap could not tell if they were genuinely open or simply silent.

## 4. What does -sV do?

-sV is the version detection option. Without it, Step 5 only gave me a port number and a guessed service name. As soon as I added -sV in Step 6, Nmap connected to each port and read what it actually returned, which is how I learned things like vsftpd 2.3.4 on port 21, OpenSSH 4.7p1 Debian 8ubuntu1 on port 22, and Apache httpd 2.2.8 (Ubuntu) DAV/2 on port 80. It turns a simple port list into a real inventory of the software running on the target.

## 5. What does -O do?

-O tries to guess the operating system of the target based on how its network stack behaves. When I ran sudo nmap -O in Step 8, it told me the target was running Linux 2.6.X, more precisely somewhere between kernel 2.6.9 and 2.6.33, with a network distance of 1 hop. It needed sudo because guessing the operating system requires sending raw packets, which normal users are not allowed to do.

## 6. Explain what -A combines and why it is noisier.

-A combines OS detection, version detection, the default script scan and a traceroute all in one command. When I ran sudo nmap -A in Step 9, I got a lot more information in a single scan than in Steps 6 and 8 separately, for example the anonymous FTP login check on port 21, the SSH host keys on port 22, and the expired SSL certificate on port 25. It is called noisier because doing all of this means sending a lot more packets to the target than a plain scan, so it is easier to notice on a network, not because it actually damages anything.

## 7. What does -p- mean?

-p- tells Nmap to check every port from 1 to 65535 instead of only the default set of common ports. This mattered a lot in my case. Step 5, the default scan, found 23 open ports, but Step 10 with -p- found 30, seven more: distccd on 3632, a second irc service on 6697, a Ruby service on 8787, and four unnamed high ports. Those extra services would have been completely missed if I had only relied on the default scan.

## 8. Why can UDP scans take longer?

UDP does not have a handshake like TCP, so Nmap cannot simply confirm a port is open the way it can with TCP's SYN and ACK exchange. It has to send a probe and wait to see if anything comes back, and if nothing comes back it cannot be sure if the port is open and silent or filtered by something. I experienced this directly. My full UDP scan in Step 15 took 1088 seconds, over 18 minutes, to check all UDP ports, while the equivalent full TCP scan in Step 10 only took about 73 seconds. That difference is huge, and it explains why Step 16 used the top 20 most common UDP ports instead of scanning all of them, which brought the time down to about 111 seconds.

## 9. What does -sC do?

-sC runs Nmap's default set of scripts against whatever ports are open. In Step 17, this is what let me see the ftp-anon result showing anonymous FTP login is allowed, the ssh-hostkey fingerprints, and details about the outdated SSL ciphers on port 25, all without me having to run each script separately.

## 10. What information did the HTTP title/headers scripts reveal?

The http-title script in Step 18 simply told me the page title, Metasploitable2 - Linux, which already told me a lot about what I was dealing with. The http-headers script in Step 19 gave me more, the Apache/2.2.8 (Ubuntu) DAV/2 server header and an X-Powered-By header showing PHP/5.2.4-2ubuntu5.10. I later confirmed this exact same information manually with curl -I in Step 23, so I know these headers are genuine and not a scanning mistake.

## 11. What did SMB/SSH/FTP enumeration add?

The SMB script in Step 20 told me the server only supports the NT LM 0.12 dialect, which is SMBv1, and Nmap itself labelled this as dangerous in the output. The SSH script in Step 21 gave me the exact host key fingerprints, a 1024 bit DSA key and a 2048 bit RSA key, which lets me identify the server without ever logging in. The FTP banner script in Step 22 returned 220 (vsFTPd 2.3.4), which matches exactly what -sV already found in Step 6, so this gave me a second independent confirmation of the same finding rather than brand new information, and that confirmation still matters because it increases my confidence in the result.

## 12. What is the difference between Nmap service detection and WhatWeb?

Nmap's -sV works at the level of any network service, on any port and any protocol, which is why it could identify FTP, SSH, SMTP, MySQL and everything else on this target. WhatWeb only looks at the web service running over HTTP, but goes into more depth about it specifically. On my results, both tools agree on the Apache version, but WhatWeb went further and also showed me the PHP version, the page title, and a WebDAV flag, none of which the plain -sV scan reported on its own. So Nmap gave me the full map of every service on the machine, while WhatWeb zoomed in on the one website running on port 80 and described it in more detail.

## 13. How did WhatWeb levels 1, 3 and 4 differ?

In my results, level 1 in Step 26 gave exactly the same output as the basic default scan in Step 24, so the lightest setting barely changed anything. Level 3 in Step 27 added one small extra detail, an additional PHP match showing PHP[5, 5.2.4-2ubuntu5.10] instead of just the version number alone. Level 4 in Step 28 went further and detected an extra plugin called Matomo that was not present at the lower levels. I am not convinced this detection is correct, since Metasploitable 2 is an old vulnerable machine and I found no other evidence anywhere in this lab that it runs Matomo, so this looks like the more aggressive mode matching something too loosely. This showed me that higher aggression levels can surface more information, but that information is not always reliable and should be checked against other evidence before I trust it.

## 14. Why must aggressive scanning/fingerprinting remain inside the authorised lab?

These scans send a large number of probes to the target, and outside of a lab like this one, doing that against a system I do not own or do not have permission to test would be illegal, regardless of my intentions. On top of the legal side, some of what I ran, like the full UDP scan that took over 18 minutes, uses a real amount of the target's resources and network bandwidth, which could cause problems on a live system. Metasploitable 2 is built specifically to be scanned and tested safely inside an isolated network, which is exactly why I only ever pointed these commands at 192.168.119.3 and nowhere else.
