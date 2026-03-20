#  Troubleshooting & VPN/MTU Analyse

## 📅 Datum

19.03.2026

## 👤 Rolle

Support / Administrator – BetaTrade GmbH

---

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

📸 Screenshot einfügen:

```
![[ping-test.png]]
```

👉 Bilder können in Obsidian einfach per Drag & Drop eingefügt werden und erscheinen als `![[datei.png]]` ()

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

📸 Screenshot einfügen:

```
![[mtu-test.png]]
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

📸 Screenshot:

```
![[netplan-config.png]]
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

📸 Screenshot:

```
![[windows-mtu.png]]
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

📸 Screenshot:

```
![[pfsense-mss.png]]
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

📸 Screenshot:

```
![[vpn-error.png]]
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

📸 Screenshot:

```
![[vpn-config.png]]
```

---

# ✅ 7. Verifikation

## Tests:

- SSH stabil ✔
    
- RDP stabil ✔
    
- VPN stabil ✔
    
- kein Timeout ✔
    

---

📸 Screenshot:

```
![[final-test.png]]
```

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

---

# 📌 Obsidian Tipps

## Screenshot einfügen:

```
![[bild.png]]
```

## Überschriften:

```
# Titel
## Abschnitt
```

## Codeblöcke:

```
sudo ip a
```

👉 Codeblöcke werden mit ``` erstellt ()

---

# ✅ Abschluss

✔ Problem identifiziert  
✔ Ursache behoben  
✔ System stabil  
✔ Dokumentation vollständig