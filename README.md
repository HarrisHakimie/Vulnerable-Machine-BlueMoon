# Vulnerable-Machine-BlueMoon
# BlueMoon 2021 VulnHub Walkthrough

# Objective
- Identify target machine
- Enumerate open services
- Gain initial access
- Escalate privileges to root

- ## Lab Setup
- Attacker: Kali Linux
- Attacker IP : 192.168.56.102
- Target: BlueMoon 2021 (VulnHub)
- Target IP : 192.168.56.105

## Step 1 — Discover Attacker IP

I used ifconfig to know the attacker’s IP.

```bash
ifconfig

```
## Step 2 — Discover Target IP

And then, identify the target machine on the network.

```bash
sudo netdiscover
```
Looking for a new IP that is not my kali machine.

Example result:

192.168.56.105 → target machine

## Step 3 — Port Scanning

I run a full scan to identify open ports and services.

```bash
nmap -sC -sV -Pn -vv 192.168.56.105
```
- Port 22 → SSH
- Port 21 → FTP
- Port 80 → HTTP (Web Server)



