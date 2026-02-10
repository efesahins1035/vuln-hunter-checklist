# 🔑 SSH Enumeration (Port 22)

## 🇹🇷 Türkçe

### Kontrol Listesi

| # | Test | Açıklama | Durum |
|---|------|----------|-------|
| 1 | Banner Grabbing | Versiyon/OS bilgisi | ⬜ |
| 2 | Weak Algorithms | Zayıf şifreleme algoritmaları | ⬜ |
| 3 | User Enumeration | Timing saldırısı ile kullanıcı tespiti | ⬜ |
| 4 | Brute Force | Şifre deneme | ⬜ |
| 5 | Key Permissions | Private key izinleri (local) | ⬜ |

### Komutlar

**Banner Grabbing:**
```bash
nc -v target_ip 22
# Çıktı: SSH-2.0-OpenSSH_7.2p2 Ubuntu-4ubuntu2.10
# Searchsploit ile versiyonu arat
```

**Brute Force (Hydra):**
```bash
hydra -l root -P /usr/share/wordlists/rockyou.txt target_ip ssh
hydra -L users.txt -P pass.txt target_ip ssh -t 4
```

**Audit (Zayıf Config):**
```bash
# ssh-audit tool
ssh-audit target_ip
```

**SSH Key İzinleri (Local):**
Eğer bir private key (`id_rsa`) bulursan:
```bash
chmod 600 id_rsa
ssh -i id_rsa user@target_ip
```

---

## 🇬🇧 English

### Checklist

| # | Test | Description | Status |
|---|------|-------------|--------|
| 1 | Banner | Version info | ⬜ |
| 2 | Brute Force | Guess credentials | ⬜ |
| 3 | Keys | Found keys usage | ⬜ |
| 4 | Audit | Weak config | ⬜ |

### Commands

```bash
# Connect with key
chmod 600 key.pem
ssh -i key.pem user@host

# Brute force
hydra -l user -P pass.txt host ssh
```

### Tips

1.  **Don't brute force aggressively:** Use `-t 4` to avoid lockout.
2.  **Look for keys:** Search for `id_rsa`, `.pub`, `authorized_keys`.

---

[← Back to README](../README.md)
