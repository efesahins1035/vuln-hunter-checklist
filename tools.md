# 🛠️ Tools / Araçlar

## Web Application Testing

| Tool | Purpose / Amaç | Link |
|------|----------------|------|
| Burp Suite | Web proxy, scanner | [portswigger.net](https://portswigger.net/burp) |
| OWASP ZAP | Web proxy, scanner (free) | [zaproxy.org](https://www.zaproxy.org/) |
| sqlmap | SQL Injection automation | [sqlmap.org](https://sqlmap.org) |
| ffuf | Web fuzzing | [github.com/ffuf](https://github.com/ffuf/ffuf) |
| gobuster | Directory brute force | [github.com/gobuster](https://github.com/OJ/gobuster) |
| dirb | Directory brute force | Built-in Kali |
| nikto | Web server scanner | [cirt.net/nikto](https://cirt.net/Nikto2) |
| wfuzz | Web fuzzer | [github.com/wfuzz](https://github.com/xmendez/wfuzz) |

## Authentication & Session

| Tool | Purpose / Amaç | Link |
|------|----------------|------|
| Hydra | Brute force | [github.com/hydra](https://github.com/vanhauser-thc/thc-hydra) |
| jwt_tool | JWT testing | [github.com/jwt_tool](https://github.com/ticarpi/jwt_tool) |
| Hashcat | Password cracking | [hashcat.net](https://hashcat.net/hashcat/) |
| John the Ripper | Password cracking | [openwall.com/john](https://www.openwall.com/john/) |

## Network

| Tool | Purpose / Amaç | Link |
|------|----------------|------|
| Nmap | Port scanning | [nmap.org](https://nmap.org) |
| Masscan | Fast port scanning | [github.com/masscan](https://github.com/robertdavidgraham/masscan) |
| Wireshark | Packet analysis | [wireshark.org](https://www.wireshark.org/) |
| Netcat | Network utility | Built-in |
| Responder | LLMNR/NBT-NS poisoning | [github.com/responder](https://github.com/lgandx/Responder) |
| Impacket | Network protocols | [github.com/impacket](https://github.com/SecureAuthCorp/impacket) |

## OSINT

| Tool | Purpose / Amaç | Link |
|------|----------------|------|
| **OSINT Framework** | **Tool collection** | [osintframework.com](https://osintframework.com) |
| theHarvester | Email/subdomain gathering | [github.com/theHarvester](https://github.com/laramies/theHarvester) |
| Shodan | Internet device search | [shodan.io](https://www.shodan.io/) |
| Censys | Internet scan data | [censys.io](https://censys.io/) |
| Maltego | OSINT visualization | [maltego.com](https://www.maltego.com/) |
| Recon-ng | OSINT framework | [github.com/recon-ng](https://github.com/lanmaster53/recon-ng) |
| SpiderFoot | OSINT automation | [spiderfoot.net](https://www.spiderfoot.net/) |

## Subdomain & DNS

| Tool | Purpose / Amaç | Link |
|------|----------------|------|
| Sublist3r | Subdomain enumeration | [github.com/sublist3r](https://github.com/aboul3la/Sublist3r) |
| Amass | Subdomain discovery | [github.com/amass](https://github.com/OWASP/Amass) |
| subfinder | Subdomain discovery | [github.com/subfinder](https://github.com/projectdiscovery/subfinder) |
| dnsrecon | DNS enumeration | [github.com/dnsrecon](https://github.com/darkoperator/dnsrecon) |

## Exploitation

| Tool | Purpose / Amaç | Link |
|------|----------------|------|
| Metasploit | Exploitation framework | [metasploit.com](https://www.metasploit.com/) |
| SearchSploit | Exploit database search | Built-in Kali |
| pwntools | CTF toolkit | [github.com/pwntools](https://github.com/Gallopsled/pwntools) |

## Wordlists

| Wordlist | Purpose / Amaç | Path |
|----------|----------------|------|
| rockyou.txt | Password list | `/usr/share/wordlists/rockyou.txt` |
| SecLists | Everything | [github.com/seclists](https://github.com/danielmiessler/SecLists) |
| dirbuster | Directory lists | `/usr/share/wordlists/dirbuster/` |

---

## 🔧 Quick Install Commands

```bash
# Kali'de hazır gelir, diğerleri için:

# SQLMap
pip install sqlmap

# ffuf
go install github.com/ffuf/ffuf@latest

# gobuster
go install github.com/OJ/gobuster/v3@latest

# jwt_tool
git clone https://github.com/ticarpi/jwt_tool.git
pip install -r jwt_tool/requirements.txt

# theHarvester
pip install theHarvester

# SecLists
git clone https://github.com/danielmiessler/SecLists.git /opt/SecLists
```

---

[← Back to README](../README.md)
