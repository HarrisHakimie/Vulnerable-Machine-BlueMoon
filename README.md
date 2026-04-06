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
## Example Findings:
- Port 22 → SSH
- Port 21 → FTP
- Port 80 → HTTP (Web Server)

## Step 4 — Web Enumeration
I used gobuster to perform brute-forcing command to discover hidden paths on a web server.

```bash
gobuster dir --url http://ip -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 25 -x .txt, .php, .bak, .zip, .html
```
These are the directories that has been succesfully identified.
- /service-status
- /hiddent_text
- Accessing the root URL at http://192.168.56.102/hidden_text that led to a maintenance notice which stating, "Maintenance!Sorry For Delay.We will recover soon. Thank You ...
- There is something off with the Thank You and after clicking it, I discovered a QR code.
- Decoding the QR code revealed a FTP credentials for user and password.
  
- ```bash
  user : user ftp passsword : fttp@ssword 
  ```
## Step 5 — FTP Access

## Connecting to FTP

I attempted to connect to the FTP service on the target machine:
```bash
  ftp 192.168.56.105
 ```
## Enumerating Files
Once inside the FTP server, I listed the available files:
```bash
ls
```
The following files were found:
```bash
information.txt
p_lists.txt
```
These files looked interesting and potentially contained useful information such as credentials or hints.

