# 🔐 Vulnerability Hunter Checklist
### CTF & Bug Bounty Quick Reference Guide

<div align="center">

![Security](https://img.shields.io/badge/Security-Checklist-red?style=for-the-badge&logo=hackthebox&logoColor=white)
![CTF](https://img.shields.io/badge/CTF-Ready-green?style=for-the-badge&logo=tryhackme&logoColor=white)

**[🇹🇷 Türkçe](#-türkçe) | [🇬🇧 English](#-english)**

</div>

---

# 🇹🇷 Türkçe

## 🎯 Neden Bu Projeyi Yaptık?

CTF yarışmalarında ve bug bounty avcılığında hız önemlidir. Her seferinde "şimdi ne deneyecektim?" diye düşünmek yerine, hızlı bir referans kaynağına ihtiyaç duyduk.

Bu checklist:
- ✅ Senaryoya göre organize edilmiş (login sayfası, file upload, vb.)
- ✅ Kopyala-yapıştır komutlar içeriyor
- ✅ Türkçe ve İngilizce destekli
- ✅ Sürekli güncelleniyor

## 📂 Yapı

| Kategori | Açıklama | Link |
|----------|----------|------|
| 🌐 **Web** | Web uygulama zafiyetleri | [web/](./web/) |
| 🔌 **Network** | Ağ tabanlı saldırılar | [network/](./network/) |
| 🔍 **OSINT** | Açık kaynak istihbarat | [osint/](./osint/) |
| 🛠️ **Tools** | Araç listesi | [tools.md](./tools.md) |

### Web Kategorisi
- [Login Sayfası](./web/login.md) - SQL Injection, Brute Force, Default Creds
- [File Upload](./web/file-upload.md) - Extension Bypass, Magic Bytes
- [XSS](./web/xss.md) - Reflected, Stored, DOM-based
- [SQL Injection](./web/sqli.md) - Union, Blind, Error-based
- [XXE](./web/xxe.md) - XML External Entity Injection
- [SSRF](./web/ssrf.md) - Server-Side Request Forgery
- [LFI/RFI](./web/lfi-rfi.md) - Local/Remote File Inclusion

### Network Kategorisi
- [Port Scanning](./network/port-scanning.md) - Nmap, Masscan
- [SMB](./network/smb.md) - Enumeration, Attacks
- [SSH](./network/ssh.md) - Brute Force, Key Attacks

### OSINT Kategorisi
- [Reconnaissance](./osint/recon.md) - Subdomain, Email, Social Media

## 🚀 Nasıl Kullanılır?

1. Hedef sistemi belirle
2. İlgili kategoriye git
3. Checklist'i takip et
4. Komutları kopyala-yapıştır

## ⚠️ Yasal Uyarı

Bu araç sadece **eğitim amaçlıdır**. Yalnızca izin verilen sistemlerde kullanın. Yetkisiz erişim suçtur.

---

# 🇬🇧 English

## 🎯 Why We Built This?

Speed matters in CTF competitions and bug bounty hunting. Instead of thinking "what should I try now?", we needed a quick reference guide.

This checklist:
- ✅ Organized by scenario (login page, file upload, etc.)
- ✅ Contains copy-paste commands
- ✅ Supports Turkish and English
- ✅ Continuously updated

## 📂 Structure

| Category | Description | Link |
|----------|-------------|------|
| 🌐 **Web** | Web application vulnerabilities | [web/](./web/) |
| 🔌 **Network** | Network-based attacks | [network/](./network/) |
| 🔍 **OSINT** | Open Source Intelligence | [osint/](./osint/) |
| 🛠️ **Tools** | Tool list | [tools.md](./tools.md) |

### Web Category
- [Login Page](./web/login.md) - SQL Injection, Brute Force, Default Creds
- [File Upload](./web/file-upload.md) - Extension Bypass, Magic Bytes
- [XSS](./web/xss.md) - Reflected, Stored, DOM-based
- [SQL Injection](./web/sqli.md) - Union, Blind, Error-based
- [XXE](./web/xxe.md) - XML External Entity Injection
- [SSRF](./web/ssrf.md) - Server-Side Request Forgery
- [LFI/RFI](./web/lfi-rfi.md) - Local/Remote File Inclusion

### Network Category
- [Port Scanning](./network/port-scanning.md) - Nmap, Masscan
- [SMB](./network/smb.md) - Enumeration, Attacks
- [SSH](./network/ssh.md) - Brute Force, Key Attacks

### OSINT Category
- [Reconnaissance](./osint/recon.md) - Subdomain, Email, Social Media

## 🚀 How to Use?

1. Identify target system
2. Go to relevant category
3. Follow the checklist
4. Copy-paste commands

## ⚠️ Legal Disclaimer

This tool is for **educational purposes only**. Use only on authorized systems. Unauthorized access is a crime.

---

<div align="center">

**Made with ❤️ by [Efe Şahin](https://github.com/efesahins1035) & Atlas-01**

⭐ Star this repo if you find it useful!

</div>
