# 🌐 Network & IP Testing Guide (Nmap)

This repository provides a **practical guide for network reconnaissance and IP testing** using **Nmap**, commonly performed during **Network VAPT and internal assessments**.

---

## ⚠️ Disclaimer

This guide is intended strictly for **educational and authorized security testing purposes**.  
Run these commands **only on networks and systems you own or have explicit permission to test**.

---

## 🧪 Prerequisites

- Nmap installed on the system
- Network access to the target subnet
- Basic understanding of networking concepts

---

## 🔍 Step 1 — Identify Alive Hosts

Scan the subnet to discover **active (alive) hosts**:

```bash
nmap -sn 192.168.1.0/24 -oA alive
```

### What this does:
- Performs a ping scan
- Identifies live hosts only
- Saves output in all formats (`.nmap`, `.gnmap`, `.xml`)

---

## 📄 Step 2 — Extract Alive IP Addresses

Extract IP addresses of hosts that are **up** and save them for further scanning:

```bash
grep "Up" alive.gnmap | cut -d " " -f 2 > alive_ips.txt
```

### Output:
- `alive_ips.txt` will contain a list of active IPs
- Used as input for deeper scans

---

## 🔐 Step 3 — TCP Scan (Service, Script & OS Detection)

Perform a detailed TCP scan on the alive hosts:

```bash
nmap -sV -sC -O -iL ip.txt -oA tcpscan1
```

### Scan details:
- `-sV` → Service version detection  
- `-sC` → Default NSE scripts  
- `-O` → OS detection  
- `-iL` → Input list of IPs  
- `-oA` → Output in all formats  

---

## 📡 Step 4 — UDP Scan (Top Ports)

Scan the **top 100 UDP ports** on the target hosts:

```bash
nmap -sU -sV --top-ports 100 -iL ip.txt -oA udp1
```

### Scan details:
- `-sU` → UDP scan  
- `-sV` → Service version detection  
- `--top-ports 100` → Scans most common UDP ports  

---

## 📡 Step 5 — Convert .xml file to .html

```
xsltproc output.xml > output.html
```

## 📚 Use Cases

- Network VAPT
- Internal network assessment
- Asset discovery
- Service enumeration
- OS and protocol identification

---

## 📝 Notes

- UDP scans are slower than TCP scans
- Firewall rules may affect scan accuracy
- Always validate critical findings manually
- Combine results with vulnerability scanners for deeper analysis

---

## 📜 License

This guide is intended for **educational and authorized security testing purposes only**.
