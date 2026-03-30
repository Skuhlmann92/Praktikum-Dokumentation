# 02 05 Tag 3 Troubleshooting VPN MTU Analyse

## 📅 Datum 19.03.2026

# 🎯 Ziel

- Problem analysieren und beheben
    
- Ursache identifizieren
    
- System stabilisieren
    
- Dokumentation aller Schritte
    

---

# 🧠 Ausgangssituation

**Problembeschreibung:**

- SSH und RDP Verbindungen brechen ab
    
- Webseiten laden teilweise nicht
    
- VPN instabil
    
- Ping funktioniert weiterhin
    

---

# 🧩 1. Information sammeln

## 🔍 Beobachtungen

- SSH Verbindung:
    
    - Idle stabil
        
    - bei Nutzung → Abbruch
        
- RDP:
    
    - bricht ebenfalls ab
        
- Ping:
    
    - stabil
        

---

# 🧠 2. Hypothesen

Mögliche Ursachen:

- Firewall Problem ❌
    
- Routing Problem ❌
    
- **MTU / Paketgröße Problem ✔**
    

---

# 🧪 3. Tests

## 🔹 Test 1: Ping mit DF Flag

```
ping -M do -s 1472 192.168.13.10
```

## 🔍 Ergebnis:

```
message too long, mtu=1380
```

---

## 🧠 Analyse

👉 Netzwerk erlaubt nur:

```
MTU = 1380
```

👉 Standard wäre:

```
MTU = 1500
```

➡️ Ursache: Paketfragmentierung / MTU Blackhole

---

# 🛠️ 4. Behebung

---

## 🔧 Linux Server Fix

```
sudo ip link set dev eth0 mtu 1380
```

### dauerhaft:

```
sudo nano /etc/netplan/50-cloud-init.yaml
```

### Anpassung:

```
mtu: 1380
```

```
sudo netplan apply
```
---

## 🔧 Windows Server Fix

```
netsh interface ipv4 show subinterfaces
```

```
netsh interface ipv4 set subinterface "Ethernet" mtu=1380 store=persistent
```

---

## 🔧 pfSense MSS Clamping

Pfad:

```
Firewall → Rules → LAN → Advanced
```

Wert:

```
Maximum MSS = 1340
```

---

# 🌐 5. VPN Analyse

## 🔍 Problem

VPN verbunden aber:

- kein Traffic
    
- Timeout
    
- FRAG Fehler
    

---

## 🔍 Logs

```
FRAG_IN error: FRAG_TEST not implemented
Inactivity timeout
```

---

# 🧠 Ursache

👉 Inkonsistente Fragmentierung

- Client nutzt Fragmentierung
    
- Server nicht
    

---

# 🛠️ 6. VPN Fix

## ❌ entfernt:

```
fragment 1300
mssfix 1380
```

## ✅ gesetzt:

```
tun-mtu 1380
mssfix 1340
keepalive 10 60
```

---

# ✅ 7. Verifikation

## Tests:

- SSH stabil ✔
    
- RDP stabil ✔
    
- VPN stabil ✔
    
- kein Timeout ✔
    

---

# 📊 8. Fehleranalyse

|Problem|Ursache|Lösung|
|---|---|---|
|SSH Abbruch|MTU zu hoch|MTU angepasst|
|RDP Abbruch|Paketverlust|MSS gesetzt|
|VPN Timeout|Fragmentierung|Config korrigiert|

---

# 🧾 9. Lessons Learned

- Ping reicht nicht zur Diagnose
    
- MTU Probleme zeigen sich nur bei Last
    
- VPN fügt zusätzlichen Overhead hinzu
    
- MSS Clamping ist Best Practice
    

---

# 💡 Fazit

Das Problem wurde verursacht durch:

👉 **MTU Blackhole + falsche VPN Fragmentierung**

Durch:

- MTU Anpassung
    
- MSS Clamping
    
- VPN Config Fix
    

konnte das System vollständig stabilisiert werden.
