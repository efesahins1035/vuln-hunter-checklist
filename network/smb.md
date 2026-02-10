# 📂 SMB Enumeration (Port 139/445)

## 🇹🇷 Türkçe

### Kontrol Listesi

| # | Test | Açıklama | Durum |
|---|------|----------|-------|
| 1 | Null Session | Şifresiz giriş | ⬜ |
| 2 | Share Listing | Paylaşılan klasörler | ⬜ |
| 3 | User Enumeration | Kullanıcı listesi (RID cycling) | ⬜ |
| 4 | Vulnerability Check | EternalBlue (MS17-010) vb. | ⬜ |
| 5 | Password Spraying | Zayıf şifre denemesi | ⬜ |

### Araçlar & Komutlar

**SMBClient:**
```bash
# List shares (Null session)
smbclient -L //target_ip -N

# Connect to share
smbclient //target_ip/share -N
```

**CrackMapExec (Swiss Army Knife):**
```bash
# Bilgi toplama
crackmapexec smb target_ip

# Paylaşımları listele
crackmapexec smb target_ip --shares -u '' -p ''

# Null session testi
crackmapexec smb target_ip -u 'guest' -p '' 

# Password Spraying
crackmapexec smb target_ip -u users.txt -p 'Password123!'
```

**Enum4Linux:**
```bash
enum4linux -a target_ip
```

**Nmap Scriptleri:**
```bash
nmap --script smb-enum-shares,smb-enum-users target_ip
nmap --script smb-vuln* -p 445 target_ip
```

### EternalBlue (MS17-010)

Eğer Nmap "VULNERABLE" derse:
1. Metasploit aç
2. `use exploit/windows/smb/ms17_010_eternalblue`
3. Ayarları yap ve `exploit`

---

## 🇬🇧 English

### Checklist

| # | Test | Description | Status |
|---|------|-------------|--------|
| 1 | Null Session | Anonymous access | ⬜ |
| 2 | List Shares | Find files | ⬜ |
| 3 | Enum Users | Get usernames | ⬜ |
| 4 | Check Vulns | MS17-010 check | ⬜ |

### Essential Commands

```bash
# Quick check
crackmapexec smb <ip>

# List shares
smbclient -L //<ip> -N

# Full enumeration
enum4linux -a <ip>
```

### Tips

1.  **Check permissions:** Look for READ/WRITE access.
2.  **Look for sensitive files:** `web.config`, `password.txt`, `backup`.

---

[← Back to README](../README.md)
