# Part 9: Command Cheat Sheet

| Purpose | Command |
|---|---|
| Host discovery | nmap -sn 192.168.119.0/24 |
| Default scan | nmap 192.168.119.3 |
| Versions | nmap -sV 192.168.119.3 |
| Maximum version intensity | nmap -sV --version-intensity 9 192.168.119.3 |
| OS detection | sudo nmap -O 192.168.119.3 |
| Aggressive scan | sudo nmap -A 192.168.119.3 |
| Full TCP scan | sudo nmap -p- 192.168.119.3 |
| Full TCP scan with versions | sudo nmap -p- -sV 192.168.119.3 |
| Faster timing | sudo nmap -p- -T4 192.168.119.3 |
| Selected ports | nmap -p 21,22,23,25,80,139,445 192.168.119.3 |
| Port range | sudo nmap -p 1-1024 192.168.119.3 |
| UDP scan | sudo nmap -sU 192.168.119.3 |
| Top UDP ports with versions | sudo nmap -sU --top-ports 20 -sV 192.168.119.3 |
| Default scripts | nmap -sC -sV 192.168.119.3 |
| HTTP title | nmap -p 80 --script http-title 192.168.119.3 |
| HTTP headers | nmap -p 80 --script http-headers 192.168.119.3 |
| SMB protocols | nmap -p 139,445 --script smb-protocols 192.168.119.3 |
| SSH host keys | nmap -p 22 --script ssh-hostkey 192.168.119.3 |
| FTP banner | nmap -p 21 -sV --script banner 192.168.119.3 |
| curl headers | curl -I http://192.168.119.3 |
| WhatWeb basic | whatweb http://192.168.119.3 |
| WhatWeb verbose | whatweb -v http://192.168.119.3 |
| WhatWeb level 1 | whatweb -a 1 http://192.168.119.3 |
| WhatWeb level 3 | whatweb -a 3 http://192.168.119.3 |
| WhatWeb level 4 | whatweb -a 4 http://192.168.119.3 |
| WhatWeb follow redirects | whatweb --follow-redirect=always http://192.168.119.3 |
| WhatWeb save output | whatweb -v http://192.168.119.3 > whatweb-results.txt |

# Part 10: Completion Checklist

I used only the authorised target, 192.168.119.3, for every command in this lab.
I completed every required Nmap scan type from Steps 4 to 16.
I can explain each important option in my own words in Part 8.
I completed the safe NSE enumeration in Steps 17 to 22.
I compared the WhatWeb aggression levels in Steps 26 to 28.
I built the final service inventory in Part 7 from my Step 11 scan.
I answered all 14 questions in my own words based on my own results.
