# Lab 1: Network and Service Reconnaissance (Metasploitable 2)

This repository contains my complete report for Lab 1 of the WADF104 course, carried out with Kali Linux against the Metasploitable 2 target machine, on an isolated lab network.

## Content of this repository

The docs folder contains the full report, split in the same order as the original lab document:

* 01: prepare the lab (steps 1 to 3)
* 02: Nmap output vocabulary
* 03: core Nmap scans (steps 4 to 16)
* 04: NSE script enumeration (steps 17 to 22)
* 05: manual check with curl (step 23)
* 06: technology fingerprinting with WhatWeb (steps 24 to 30)
* 07: final service inventory and evidence
* 08: answers to the 14 lab questions
* 09: command cheat sheet and completion checklist

The evidence folder contains the 30 original screenshots taken while doing the lab, each renamed to match the step it belongs to. Every screenshot is embedded and commented on in its matching docs file.

## Target and addresses used

My Kali machine has the address 192.168.119.4/24 on interface eth0.
The Metasploitable 2 machine has the address 192.168.119.3 on interface eth0.
Both machines are on the same isolated network, 192.168.119.0/24.
