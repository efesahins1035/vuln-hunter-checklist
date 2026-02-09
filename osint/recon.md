# 🔍 OSINT Reconnaissance

## 🇹🇷 Türkçe

### Kontrol Listesi

| # | Test | Açıklama | Durum |
|---|------|----------|-------|
| 1 | Subdomain Enumeration | Alt domain keşfi | ⬜ |
| 2 | Email Harvesting | Email toplama | ⬜ |
| 3 | Social Media | Sosyal medya araştırması | ⬜ |
| 4 | Google Dorking | Gelişmiş Google araması | ⬜ |
| 5 | WHOIS | Domain bilgileri | ⬜ |
| 6 | DNS Records | DNS kayıtları | ⬜ |
| 7 | Wayback Machine | Eski site versiyonları | ⬜ |
| 8 | GitHub Recon | Kod deposu araştırması | ⬜ |

### 🌐 OSINT Framework

Tüm OSINT araçları için kapsamlı kaynak:
**[https://osintframework.com](https://osintframework.com)**

### Google Dorks

```
# Subdomain bulma
site:*.target.com

# Hassas dosyalar
site:target.com filetype:pdf
site:target.com filetype:doc
site:target.com filetype:xls
site:target.com filetype:sql
site:target.com filetype:log
site:target.com filetype:bak

# Login sayfaları
site:target.com inurl:login
site:target.com inurl:admin
site:target.com intitle:"login"

# Hata mesajları
site:target.com "error" "warning"
site:target.com "mysql" "error"
site:target.com "sql syntax"

# API keys / credentials
site:target.com "api_key"
site:target.com "password"
site:target.com "secret"
site:github.com "target.com" password
site:pastebin.com "target.com"
```

### Subdomain Enumeration

```bash
# Sublist3r
python3 sublist3r.py -d target.com

# Amass (pasif)
amass enum -passive -d target.com

# Amass (aktif)
amass enum -active -d target.com

# subfinder
subfinder -d target.com

# crt.sh (certificate transparency)
curl -s "https://crt.sh/?q=%25.target.com&output=json" | jq -r '.[].name_value' | sort -u

# Brute force
ffuf -w /opt/SecLists/Discovery/DNS/subdomains-top1million-5000.txt -u http://FUZZ.target.com -H "Host: FUZZ.target.com"
```

### Email Harvesting

```bash
# theHarvester
theHarvester -d target.com -b google,bing,linkedin

# hunter.io (web)
# https://hunter.io

# phonebook.cz (web)
# https://phonebook.cz
```

### DNS Enumeration

```bash
# DNS kayıtları
dig target.com ANY
dig target.com MX
dig target.com NS
dig target.com TXT

# Zone transfer (nadir çalışır)
dig axfr @ns1.target.com target.com

# dnsrecon
dnsrecon -d target.com -t std

# Reverse DNS
dig -x IP_ADDRESS
```

### WHOIS

```bash
# WHOIS sorgusu
whois target.com

# Web alternatifleri:
# https://who.is
# https://whois.domaintools.com
```

### GitHub Recon

```bash
# GitHub'da arama
# https://github.com/search?q=target.com

# Aranacaklar:
- "target.com" password
- "target.com" api_key
- "target.com" secret
- "target.com" credentials
- org:targetcompany password
```

### Wayback Machine

```bash
# Web arayüzü
# https://web.archive.org

# API ile URL'leri çek
curl -s "https://web.archive.org/cdx/search/cdx?url=*.target.com/*&output=text&fl=original&collapse=urlkey" | sort -u
```

### Shodan

```bash
# Shodan CLI
shodan search hostname:target.com

# Web arayüzü
# https://shodan.io

# Arama örnekleri:
hostname:target.com
org:"Target Company"
ssl.cert.subject.CN:target.com
```

---

## 🇬🇧 English

### Checklist

| # | Test | Description | Status |
|---|------|-------------|--------|
| 1 | Subdomain Enumeration | Subdomain discovery | ⬜ |
| 2 | Email Harvesting | Collect emails | ⬜ |
| 3 | Social Media | Social media research | ⬜ |
| 4 | Google Dorking | Advanced Google search | ⬜ |
| 5 | WHOIS | Domain information | ⬜ |
| 6 | DNS Records | DNS records | ⬜ |
| 7 | Wayback Machine | Old site versions | ⬜ |
| 8 | GitHub Recon | Code repository research | ⬜ |

### 🌐 OSINT Framework

Comprehensive resource for all OSINT tools:
**[https://osintframework.com](https://osintframework.com)**

### Quick Commands

```bash
# Subdomain enumeration
subfinder -d target.com

# Email harvesting
theHarvester -d target.com -b google,bing

# Certificate transparency
curl -s "https://crt.sh/?q=%25.target.com&output=json" | jq -r '.[].name_value' | sort -u
```

---

[← Back to README](../README.md)
