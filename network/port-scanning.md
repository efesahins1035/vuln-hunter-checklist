# 🔌 Port Scanning

## 🇹🇷 Türkçe

### Kontrol Listesi

| # | Test | Açıklama | Durum |
|---|------|----------|-------|
| 1 | TCP SYN Scan | Hızlı, gizli tarama | ⬜ |
| 2 | Service Version | Versiyon tespiti | ⬜ |
| 3 | UDP Scan | UDP portları | ⬜ |
| 4 | Script Scan | NSE scriptleri ile zafiyet | ⬜ |
| 5 | Full Port | Tüm 65535 port | ⬜ |

### Nmap Komutları

```bash
# Hızlı tarama (İlk 1000 port)
nmap target.com

# Detaylı tarama (Versiyon, Script, OS) - Favori!
nmap -sC -sV -oA scan_result target.com

# Tüm portlar (Yavaş ama kapsamlı)
nmap -p- -T4 target.com

# UDP Tarama (Kritik servisler için: DNS, SNMP, NTP)
nmap -sU --top-ports 100 target.com

# Belirli Scriptler
nmap --script "vuln" target.com
nmap --script "http-*" target.com
```

### Masscan (Çok Hızlı)

```bash
# Tüm interneti tarar! (Dikkatli kullan)
masscan -p80,443,8080 192.168.1.0/24 --rate=1000
```

### Netcat

```bash
# Port açık mı kontrolü
nc -zv target.com 80 443

# Banner grabbing
nc -v target.com 22
```

---

## 🇬🇧 English

### Checklist

| # | Test | Description | Status |
|---|------|-------------|--------|
| 1 | TCP SYN Scan | Fast check | ⬜ |
| 2 | Service Version | Identify software | ⬜ |
| 3 | UDP Scan | Check UDP services | ⬜ |
| 4 | Script Scan | Vuln detection | ⬜ |
| 5 | All Ports | Full scan | ⬜ |

### Best Nmap Flags

- `-sC`: Default scripts
- `-sV`: Version detection
- `-oA <name>`: Output all formats
- `-p-`: Scan all ports
- `-Pn`: No ping (assume up)

### Tips

1.  **UDP takes time:** Scan top UDP ports only unless necessary.
2.  **Firewalls:** Use `-Pn` if host seems down. Fragment packets `-f`.

---

[← Back to README](../README.md)
