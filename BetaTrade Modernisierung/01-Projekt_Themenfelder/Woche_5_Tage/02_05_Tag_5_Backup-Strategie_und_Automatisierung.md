# 🛠️ 💾 Backup-Strategie & Automatisierung

---

# 🎯 Ziel

- Kritische Daten identifizieren
    
- Backup-Strategie definieren
    
- Datenbank-Backup einrichten
    
- PostgreSQL Dump erstellen
    
- Disaster-Recovery-Plan erstellen
    
- Disaster-Szenario simulieren und Wiederherstellung testen
    

---

# 🔹 Aufgabe 1: Kritische Daten identifizieren

---

## 📊 Übersicht

|Datentyp|Speicherort|Priorität|Backup-Häufigkeit|
|---|---|---|---|
|Kundendatenbank|/home/student13/betatrade-database/|🔴 Hoch|täglich|
|Active Directory|Windows Server (NTDS.dit)|🔴 Hoch|täglich|
|Netzwerk-Config (pfSense)|Firewall (XML Export)|🔴 Hoch|wöchentlich|
|Benutzerdaten|/home/student13/|🟡 Mittel|täglich|
|Logs|/var/log/|🟢 Niedrig|optional|

---

## 🧠 Begründung

- Datenbank = geschäftskritisch
    
- AD = Benutzer + Authentifizierung
    
- pfSense = komplette Netzwerkkonfiguration
    

👉 Verlust = Systemausfall

---

# 🔹 Aufgabe 2: Datenbank-Backup einrichten

---

# 🧠 Wichtiger Punkt

👉 Restic kann **keine Datenbanken direkt sichern**

👉 deshalb:

1. Dump erstellen
    
2. Dump-Datei sichern
    

➡️ Standard Vorgehen

---

# 🔧 Schritt 1: Verzeichnis prüfen

```bash
cd /home/student13/betatrade-database/
ls
```

---

# 🔧 Schritt 2: PostgreSQL Dump erstellen

👉 Container prüfen:

```bash
docker ps
```

---

👉 Dump erstellen:

```bash
docker-compose exec postgres pg_dump -U trader betatrade > betatrade-backup.sql
```

---

## 🧠 Erklärung

- `docker-compose exec postgres` → im Container ausführen
    
- `pg_dump` → Datenbank exportieren
    
- `-U trader` → Benutzer
    
- `betatrade` → Datenbankname
    
- `>` → Ausgabe in Datei
    

👉 PostgreSQL Dumps sind notwendig für konsistente Backups

---

# 🔍 Schritt 3: Dump prüfen

```bash
ls -lh
```

👉 Beispiel:

```text
betatrade-backup.sql  25MB
```

---

# 🔧 Schritt 4: Backup Plan in Backrest erstellen

---

## Einstellungen:

```text
Name: BetaTrade-Database
Pfad: /backup/home/student13/betatrade-database/
Schedule: disabled
Retention: 7 daily
```

---

# 🔧 Schritt 5: Backup durchführen

👉 Backrest:

```text
Backup Now
```

---


# 🔍 Schritt 6: Backup prüfen

👉 MinIO öffnen  
👉 Bucket prüfen

---


# 📊 Ergebnis

|Kriterium|Ergebnis|
|---|---|
|Dump erstellt|✔|
|Backup erfolgreich|✔|
|Datei vorhanden|✔|

---

# ⚠️ Wichtige Erkenntnisse

- Datenbank darf **nicht einfach kopiert werden**
    
- immer Dump verwenden
    
- sonst Inkonsistenz möglich
    

---

# 🧠 Best Practice

👉 Kombination:

```text
pg_dump → Datei → Restic Backup
```

---

# 🧾 Fazit

Die Datenbank wurde erfolgreich:

- exportiert (pg_dump)
    
- gesichert (Backrest)
    
- in S3 gespeichert
    

👉 System ist backupfähig

---

# 🔹 Aufgabe 3: Disaster-Recovery-Plan erstellen

---

## 🧠 Prioritäten-Reihenfolge

Bei BetaTrade wurde die Wiederherstellung in folgender Reihenfolge geplant:

1. **Kundendatenbank** – geschäftskritisch, ohne Datenbank funktionieren zentrale Abläufe nicht
2. **Anwendungsdienste / Docker-Services** – nach Datenwiederherstellung müssen Container neu gestartet werden
3. **Benutzer- und Infrastrukturkomponenten** – Active Directory, Netzwerkdienste, weitere Systemkomponenten
4. **Abschließende Funktionskontrolle** – Prüfen ob die Umgebung wieder vollständig arbeitsfähig ist

---

## 👥 Verantwortlichkeiten

|Bereich|Aufgabe|
|---|---|
|Systemadministration|Wiederherstellung der Linux-Umgebung und Backups|
|Datenbank / Applikation|Rücksicherung der BetaTrade-Daten und Start der Container|
|Netzwerk / Infrastruktur|Kontrolle der Erreichbarkeit und Konnektivität|
|Dokumentation|Protokollierung aller Schritte und Zeiten|

---

## 🔑 Benötigte Zugangsdaten und Informationen

- Zugang zur Backrest Web-Oberfläche
- Zugriff auf das Restore-Verzeichnis
- Zugriff auf den Linux-Server
- Kenntnisse über den Speicherort der BetaTrade-Daten
- Zugriff auf die Docker-Umgebung
- Pfade und Befehle zur Wiederherstellung

Wichtige Pfade:

```text
/home/student13/betatrade-database/
/restore/
```

---

# 🔹 Aufgabe 4: „Datacenter Failure"-Szenario simulieren

---

## ⏱️ Zeitdokumentation

Zu Beginn der Simulation wird die Startzeit des Vorfalls notiert, um die Recovery-Dauer mit dem geplanten RTO vergleichen zu können:

```text
Start der Störung:        Uhrzeit dokumentieren
Beginn der Wiederherstellung: Uhrzeit dokumentieren
Ende nach Funktionstest:  Uhrzeit dokumentieren
```

---

## 🔧 Schritt 1: BetaTrade-Datenbank stoppen

```bash
cd /home/student13/betatrade-database/
docker-compose stop
```

## 🧠 Erklärung

👉 Mit diesem Befehl werden die BetaTrade-Container gestoppt, damit während der Wiederherstellung keine laufenden Prozesse auf die Daten zugreifen.

---

## 🔧 Schritt 2: Datenverlust simulieren

```bash
mv docker-compose.yml /tmp/docker-compose.yml.backup
```

## 🧠 Erklärung

👉 Durch das Umbenennen der `docker-compose.yml` ist die ursprüngliche Startkonfiguration nicht mehr direkt verfügbar.  
👉 Damit wird ein realistisches Störungsszenario nachgebildet, bei dem ein zentraler Bestandteil der Anwendung fehlt.

---

# 🔹 Aufgabe 5: Service-Recovery durchführen

---

## 🔧 Schritt 1: Backrest Web-Oberfläche öffnen

```text
http://192.168.13.20:9898
```

👉 Passendes Backup für die BetaTrade-Datenbank auswählen.

---

## 🔧 Schritt 2: Letzten Snapshot auswählen

👉 Worauf zu achten ist:

- Status des Backups: **erfolgreich**
- korrekter Backup-Plan
- aktueller Sicherungszeitpunkt

---

## 🔧 Schritt 3: Restore-Ziel festlegen

👉 Wiederherstellung in das vorgesehene Restore-Verzeichnis:

```text
/restore/
```

👉 Das Restore-Verzeichnis dient als Zwischenablage – Daten werden zuerst geprüft, dann zurückkopiert.

---

## 🔧 Schritt 4: Wiederhergestellte Dateien zurückkopieren

```bash
cp /restore/home/student13/betatrade-database/* /home/student13/betatrade-database/
```

## 🧠 Erklärung

👉 Die wiederhergestellten Dateien werden aus dem Restore-Verzeichnis in das produktive Verzeichnis zurückgespielt.

---

## 🔧 Schritt 5: Services erneut starten

```bash
cd /home/student13/betatrade-database/
docker-compose up -d
```

## 🧠 Erklärung

👉 Die Container werden im Hintergrund wieder gestartet.

---

## 🔍 Schritt 6: Funktionstest durchführen

```bash
docker ps
```

👉 Prüfen ob:

- alle Container laufen
- die Anwendung erreichbar ist
- die Datenbank antwortet
- alle wichtigen Dateien wieder vorhanden sind

---

# 📊 Recovery-Zeiten auswerten

| Phase                     | Start | Ende  | Dauer     |
| ------------------------- | ----- | ----- | --------- |
| Ausfall erkannt           | 10:00 | 10:02 | 2min      |
| Backup identifiziert      | 10:02 | 10:05 | 3min      |
| Restore gestartet         | 10:05 | 10:10 | 5min      |
| Dateien kopiert           | 10:10 | 10:13 | 3min      |
| Services gestartet        | 10:13 | 10:16 | 3min      |
| Funktionstest erfolgreich | 10:16 | 10:20 | 4min      |
| **Gesamt**                | 10:00 | 10:20 | **20min** |

---

# 📊 Vergleich mit RTO und RPO

| Ziel                    | Geplant   | Erreicht | Ergebnis |
| ----------------------- | --------- | -------- | -------- |
| RTO (max. Ausfallzeit)  | 2 Stunden | 20min    | ✔ / ✔    |
| RPO (max. Datenverlust) | 1 Stunde  | 20min    | ✔ / ✔    |

---

# ⚠️ Lessons Learned

## ✅ Was gut funktioniert hat

- Backup war vorhanden und nutzbar
- Wiederherstellung konnte strukturiert durchgeführt werden
- Rücksicherung in das Zielverzeichnis war nachvollziehbar
- Services ließen sich nach dem Restore wieder starten

## ⏳ Was länger gedauert hat als erwartet

- Identifizieren des richtigen Backups kann Zeit kosten
- Manuelles Zurückkopieren der Dateien ist fehleranfällig
- Wenn Pfade nicht dokumentiert sind, verlängert sich die Wiederherstellung

## 🔧 Was beim nächsten Mal verbessert werden sollte

- Recovery-Schritte noch genauer dokumentieren
- Checkliste für den Wiederanlauf vorbereiten
- Wiederherstellung regelmäßig testen
- Restore-Prozess möglichst standardisieren
- Kritische Befehle zentral dokumentieren
- Backups zusätzlich auf Konsistenz prüfen
- Zeitmessung bei jedem Testlauf mitführen

---

# ⚠️ Fallstricke und Lösungen

|Problem|Lösung|
|---|---|
|Falscher Snapshot gewählt|Backup-Zeitpunkt genau prüfen|
|Restore im falschen Verzeichnis|Pfade vor Start kontrollieren|
|Dateien unvollständig kopiert|Inhalt des Restore-Ordners prüfen|
|Dienste starten nicht korrekt|`docker ps` und Logs kontrollieren|
|Zeitdokumentation fehlt|Jeden Schritt sofort protokollieren|


---