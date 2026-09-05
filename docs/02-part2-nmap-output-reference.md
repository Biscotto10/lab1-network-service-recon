# Part 2: Understand Nmap Output

Before going further, here is the vocabulary I needed to understand every result in this lab.

| Field or State | What it means |
|---|---|
| PORT | The port number and protocol, for example 22/tcp. |
| open | A real service is accepting connections on that port. |
| closed | The host answered but nothing is listening on that specific port. |
| filtered | Nmap could not tell the real state because something is blocking the probe or its response. |
| SERVICE | Nmap's guess of what usually runs on that port number. |
| VERSION | The actual product and version Nmap identified, only shown when I use -sV. |

I used this table throughout the lab to interpret every scan result, and I refer back to it in my answers in Part 8.
