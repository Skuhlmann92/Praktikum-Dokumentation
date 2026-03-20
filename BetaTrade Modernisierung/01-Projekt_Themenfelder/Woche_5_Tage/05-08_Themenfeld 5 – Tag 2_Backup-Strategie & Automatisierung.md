# 🛠️ 💾 Backup-Strategie & Automatisierung

---

# 🎯 Ziel

- Kritische Daten identifizieren
    
- Backup-Strategie definieren
    
- Datenbank-Backup einrichten
    
- PostgreSQL Dump erstellen
    

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

📸 Screenshot einfügen:  
Ordnerstruktur Datenbank

```markdown
![[database-folder.png]]
```

---

# 🔹 Aufgabe 2: Datenbank-Backup einrichten

---

# 🧠 Wichtiger Punkt

👉 Restic kann **keine Datenbanken direkt sichern**

👉 deshalb:

1. Dump erstellen
    
2. Dump-Datei sichern
    

➡️ Standard Vorgehen (turn0search1)

---

# 🔧 Schritt 1: Verzeichnis prüfen

```bash
cd /home/student13/betatrade-database/
ls
```

---

📸 Screenshot einfügen:

```markdown
![[database-files.png]]
```

---

# 🔧 Schritt 2: PostgreSQL Dump erstellen

👉 Container prüfen:

```bash
docker ps
```

---

📸 Screenshot einfügen:

```markdown
![[docker-ps.png]]
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
    

👉 PostgreSQL Dumps sind notwendig für konsistente Backups (turn0search10)

---

📸 Screenshot einfügen:

```markdown
![[pg-dump.png]]
```

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

📸 Screenshot einfügen:

```markdown
![[dump-file.png]]
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

📸 Screenshot einfügen:

```markdown
![[backup-plan-db.png]]
```

---

# 🔧 Schritt 5: Backup durchführen

👉 Backrest:

```text
Backup Now
```

---

📸 Screenshot einfügen:

```markdown
![[backup-db-run.png]]
```

---

# 🔍 Schritt 6: Backup prüfen

👉 MinIO öffnen  
👉 Bucket prüfen

---

📸 Screenshot einfügen:

```markdown
![[minio-db.png]]
```

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
    
- sonst Inkonsistenz möglich (turn0search10)
    

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

# ✅ Ergebnis

✔ Datenbank gesichert  
✔ Backup-Plan erstellt  
✔ Grundlage für Automatisierung gelegt

---