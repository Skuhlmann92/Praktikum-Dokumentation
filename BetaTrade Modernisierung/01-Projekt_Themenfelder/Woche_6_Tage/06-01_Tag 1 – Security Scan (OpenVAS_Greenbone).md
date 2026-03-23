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

# 🧾 Abschluss Doku (fertig einfügen)

## 🔹 Security Scan durchgeführt  
  
Ein erster Vulnerability Scan wurde mit OpenVAS durchgeführt.  
  
### Konfiguration  
Target: 192.168.13.0/24    
Scan: Full and fast    
Scanner: OpenVAS Default    
  
### Durchführung  
Startzeit: 14:30    
Scan erfolgreich abgeschlossen    
  
### Ergebnis  
Mehrere Schwachstellen identifiziert, darunter kritische und hohe Risiken.  
  
### Analyse  
Die TOP 5 Schwachstellen wurden nach CVSS priorisiert.  
  
### Bewertung  
Kritische Schwachstellen betreffen insbesondere:  
- veraltete Software  
- unsichere Protokolle  
- schwache Authentifizierung  
  
### Fazit  
Die BetaTrade-Infrastruktur weist mehrere sicherheitsrelevante Schwachstellen auf, die priorisiert behoben werden müssen.

---

# 🔥 Merksatz für Prüfung

Non-Credentialed = Außenangriff  
Credentialed = Innenanalyse