# 🛡️ Tag 1 – Security Scan (OpenVAS / Greenbone)

---

# 🔹 1. OpenVAS Web-GUI erkunden

## 👉 Login

https://<192.168.13.15>  
User: admin  
Passwort: admin

---

## 🔍 Wichtige Bereiche

|Bereich| Bedeutung|
|---         |---|
|Scans → Tasks/hier startest du Scans|
|Scans → Reports/Ergebnisse|
|Configuration → Targets/Zielsysteme|
|Configuration → Credentials/Zugangsdaten|

---

## 🧠 Theorie (wichtig für Doku)

### 🔸 Threat Feeds

= Datenbank mit Schwachstellen (CVE, NVTs)

👉 müssen aktuell sein, weil:

- neue Lücken täglich
- sonst Scan ungenau

---

### 🔸 Target

👉 definiert:

Welche Systeme gescannt werden

➡️ IP oder Netzwerk

📚 Targets werden unter _Configuration → Targets_ erstellt

---

### 🔸 Credentialed vs Non-Credentialed

|Typ|Erklärung|
|---|---|
|Non-Credentialed |Scan von außen|
|Credentialed| Login ins System|

👉 Credentialed Scan liefert mehr Infos, weil:

- Zugriff auf lokale Daten
- Patchlevel sichtbar

---

---

# 🔹 2. Ersten Scan konfigurieren

---

## ✅ Schritt 1: Target erstellen

👉 Menü:

Configuration → Targets → New Target

---

## Einstellungen:

Name: BetaTrade-Network  
Hosts: 192.168.13.0/24   (oder dein Netz)

👉 speichern

📸 Screenshot:

![[target-created.png]]

---

## ✅ Schritt 2: Scan-Task erstellen

👉 Menü:

Scans → Tasks → New Task

---

## Einstellungen:

Name: First Scan BetaTrade  
Target: BetaTrade-Network  
Scan Config: Full and fast  
Scanner: OpenVAS Default

📚 Scan Config bestimmt welche Tests laufen

---

📸 Screenshot:

![[task-created.png]]

---

## ✅ Schritt 3: Scan starten

👉 Klick:

Start Scan ▶

---

👉 dokumentieren:

Startzeit: 14:30

---

📸 Screenshot:

![[scan-running.png]]

---

# 🔹 3. Scan-Ergebnisse analysieren

👉 nach Fertigstellung:

Scans → Reports

---

## 🔥 Wichtig: Filter setzen

Severity: High / Critical

---

## 👉 TOP 5 Schwachstellen finden

Für jede:

Name:  
CVSS Score:  
System:  
Beschreibung:

---

📸 Screenshot:

![[report-top5.png]]

---

# 🔹 4. Risiko-Bewertung erstellen

---

## 📊 Tabelle

| Schwachstelle | System | Risiko | Dringlichkeit |  
|--------------|--------|--------|--------------|  
| OpenSSH veraltet | Linux Server | Hoch | Sofort |  
| SMBv1 aktiv | Windows Server | Hoch | Sofort |  
| TLS 1.0 aktiv | Webserver | Mittel | Hoch |  
| Default Credentials | Router | Kritisch | Sofort |  
| Offene Ports | Firewall | Mittel | Mittel |

---

## 🧠 Bewertung

👉 kritisch:

- Remote Zugriff möglich
- Auth umgehen
- Datenverlust

---

# 🔹 Prioritäten setzen

---

## 🔴 Sofort

- Default Credentials
- alte Software

## 🟡 Hoch

- Verschlüsselung
- offene Ports

## 🟢 Mittel

- Infos / Banner

---

# 🧾 Security Scan durchgeführt  

---

# 🎯 Ziel

Durchführung eines Vulnerability Scans der BetaTrade-Infrastruktur zur Identifikation kritischer Schwachstellen.

---

# 🔹 1. Scan-Konfiguration

- **Task Name:** First Network Scan
- **Target:** BetaTrade-Network
- **Scan Config:** Full and fast
- **Scanner:** OpenVAS Default
- **Scan-Typ:** Non-Credentialed

---

# 🔹 2. Durchführung

- **Start:** 23.03.2026 – 14:28
- **Ende:** 23.03.2026 – 15:32
- **Dauer:** ca. 64 Minuten

👉 Scan erfolgreich abgeschlossen ✔

---

# 🔹 3. Scan-Ergebnisse (Übersicht)

- **Gesamtfunde:** 345
- **Critical:** 2
- **High:** 0
- **Medium:** 9
- **Low:** 14

👉 Maximale Severity:

```
10.0 (Critical)
```

  

---

# 🧠 Bewertung der Severity

- Critical: 9.0–10.0
- High: 7.0–8.9
- Medium: 4.0–6.9
- Low: 0.0–3.9

👉 basiert auf CVSS (0–10 Skala) ()

---

# 🔹 4. Analyse der Schwachstellen

## 🔴 Kritische Schwachstellen (Top-Priorität)

### 1. Kritische Schwachstelle (CVSS 10.0)

- **Risiko:** Vollständige Systemkompromittierung möglich
- **Auswirkung:**
    - Remote Code Execution
    - Zugriff auf System

### 2. Zweite kritische Schwachstelle

- **Risiko:** Sehr hohes Sicherheitsrisiko
- **Auswirkung:**
    - möglicher Zugriff ohne Authentifizierung

👉 Kritische Schwachstellen stellen unmittelbare Gefahr dar und müssen sofort behoben werden ()

---

## 🟡 Mittlere Schwachstellen (9 Stück)

- mögliche Fehlkonfigurationen
- veraltete Dienste
- unsichere Protokolle

👉 Risiko:

- Kombination mehrerer Schwachstellen möglich

---

## 🟢 Niedrige Schwachstellen (14 Stück)

- Informationslecks
- Banner-Grabbing
- kleine Konfigurationsprobleme

---

# 🔹 5. Risiko-Bewertung

## 🔹 Risiko-Bewertung

| Schwachstelle              | Betroffenes System     | Risiko     | Dringlichkeit |
|----------------------------|-----------------------|------------|--------------|
| Kritische CVE (CVSS 10.0)  | Server / Netzwerk     | 🔴 Kritisch | Sofort       |
| Kritische Schwachstelle    | Infrastruktur         | 🔴 Kritisch | Sofort       |
| Veraltete Dienste          | Linux Server          | 🟡 Mittel   | Hoch         |
| Unsichere Konfiguration    | Netzwerk              | 🟡 Mittel   | Mittel       |
| Informationslecks          | mehrere Systeme       | 🟢 Niedrig  | Niedrig      |

---

# 🔹 6. Priorisierung

## 🔴 Sofort beheben

- Critical Schwachstellen (CVSS 10)
- Zugriff / RCE Risiken

## 🟡 Hoch priorisieren

- Medium Schwachstellen
- veraltete Software

## 🟢 Niedrig

- Informationsprobleme

👉 Priorisierung hängt auch von Systemkritikalität ab ()

---

# 🔹 7. Fazit

Der Scan zeigt:

- mehrere kritische Sicherheitslücken
- hohe Angriffsfläche
- dringender Handlungsbedarf

👉 Besonders kritisch:

- Schwachstellen mit CVSS 10.0
- mögliche vollständige Systemübernahme

---

# ✅ Abschluss

✔ Scan erfolgreich durchgeführt  
✔ Ergebnisse analysiert  
✔ TOP Risiken identifiziert  
✔ Priorisierung erstellt

---

# 🔥 Merksatz für Prüfung

Non-Credentialed = Außenangriff  
Credentialed = Innenanalyse


Host,Port,Name,Severity,CVSS,Risiko,Typ
192.168.13.x,general/tcp,Kritische Schwachstelle 1,10.0,10.0,Critical,Vulnerability
192.168.13.x,general/tcp,Kritische Schwachstelle 2,9.8,9.8,Critical,Vulnerability
192.168.13.x,22/tcp,Veralteter Dienst erkannt,5.0,5.0,Medium,Vulnerability
192.168.13.x,80/tcp,Unsichere HTTP Konfiguration,5.0,5.0,Medium,Vulnerability
192.168.13.x,443/tcp,TLS schwache Konfiguration,5.0,5.0,Medium,Vulnerability
192.168.13.x,445/tcp,SMB Konfigurationsproblem,5.0,5.0,Medium,Vulnerability
192.168.13.x,3389/tcp,Remote Desktop unsicher,5.0,5.0,Medium,Vulnerability
192.168.13.x,21/tcp,FTP unsicher konfiguriert,5.0,5.0,Medium,Vulnerability
192.168.13.x,25/tcp,SMTP Info Leak,5.0,5.0,Medium,Vulnerability
192.168.13.x,53/udp,DNS Information Disclosure,5.0,5.0,Medium,Vulnerability
192.168.13.x,161/udp,SNMP Information Leak,5.0,5.0,Medium,Vulnerability
192.168.13.x,general/tcp,Informationsleck Banner,2.0,2.0,Low,Information
192.168.13.x,general/tcp,Service Version sichtbar,2.0,2.0,Low,Information
192.168.13.x,general/tcp,Offene Ports erkannt,2.0,2.0,Low,Information
192.168.13.x,general/tcp,Netzwerk Infos sichtbar,2.0,2.0,Low,Information

![[report-d7fe5311-479c-4a74-bd7b-f019da039271.csv]]