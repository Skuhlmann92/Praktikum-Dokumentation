## 🛠️ Tag 1 – Cloud-Backup Setup (S3 + Backrest)

---

## 📅 Datum

19.03.2026

## 👤 Rolle

Cloud-Administrator – AlphaTech GmbH

## 🏢 Kunde

BetaTrade AG

---

# 🎯 Ziel des Tages

- S3 Storage einrichten
    
- Backup-System implementieren
    
- Linux & Windows sichern
    
- Restore testen
    

---

# 🧠 Theorie

## 📦 S3-Buckets

S3 ist ein **Objektspeicher**, keine klassische Ordnerstruktur.  
Daten werden als Objekte gespeichert.

👉 Wichtig:

- kein echtes Filesystem
    
- hohe Skalierbarkeit
    
- ideal für Backups
    
---

## ⚡ Backup-Verhalten

👉 Erstes Backup:

- Full Backup
    
- dauert lange
    

👉 Weitere Backups:

- inkrementell
    
- nur Änderungen
    

➡️ dadurch deutlich schneller ()

---

## 🐢 Restore Verzögerung

- S3 hat keine echte Ordnerstruktur
    
- Backrest muss Index laden
    

👉 deshalb:

- Snapshot Browser braucht 1–3 Minuten
    

---

# 🧪 Praxis

---

# 🔹 Aufgabe 1: S3 Zugriff

## 🔧 Login MinIO

```
User: adminuser  
Passwort: MR_Stuxx@net13  
```

---

## 🪣 Bucket erstellt

```
backups-student13
```

---

# 🔹 Aufgabe 2: Backrest Linux

## 🔧 Docker Start

```
docker run -d \
 --name backrest \
 --restart unless-stopped \
 -p 9898:9898 \
 -e BACKREST_PORT=9898 \
 -e BACKREST_DATA=/data \
 -v /:/backup:ro \
 -v /restore:/restore:rw \
 garethgeorge/backrest:latest
```

---

## 🌐 Web UI

```
http://<linux-ip>:9898
```
---

# 🔹 Aufgabe 3: Backrest Windows

## 🔧 Installation

- Setup ausgeführt
    
- Service gestartet
    

---
# 🔹 Aufgabe 4: Repository

---

## 🐧 Linux Repo

```
s3:https://training13.s3.mindrefined.de/backups-student13/linux-server
```

---

## 🪟 Windows Repo

```
s3:https://training13.s3.mindrefined.de/backups-student13/windows-server
```

---

## ⚠️ Fehler & Lösung

### ❌ Fehler

```
bucket not valid
```

👉 Ursache:

- falscher Bucketname
    

✔ Lösung:

- Bucket korrekt erstellt
    

---

# 🔹 Aufgabe 5: Backup Plan

---

## 🐧 Linux

```
/backup/home/student13/test-backup
```

---

## 🪟 Windows

```
C:\Backup
```

---

# 🔹 Aufgabe 6: Backup Test

---

## 📂 Testdaten

```
touch test1.txt test2.txt test3.txt
```

---

## ▶ Backup gestartet

- Button: Backup Now
    

---

## 📊 Ergebnis

- Backup erfolgreich
    
- Daten im S3 Bucket sichtbar
    
---

# 🔹 Aufgabe 7: Restore Test

---

## 🧪 Linux

```
rm test1.txt
```

Restore → `/restore/`

---

## 🪟 Windows

- Datei gelöscht
    
- Restore to path
    

---

# ⏱️ Dokumentation

|Aktion|Dauer|
|---|---|
|Backup|~30–40 Sekunden|
|Restore|~1–3 Minuten|


---

# 🧠 Lessons Learned

- S3 ist kein klassisches Filesystem
    
- erstes Backup ist immer Full
    
- inkrementelle Backups sparen Zeit
    
- richtige Pfade sind entscheidend
    

---

# 💡 Fazit

Die Cloud-Backup-Infrastruktur wurde erfolgreich eingerichtet.

👉 Beide Server sichern zuverlässig in die Cloud  
👉 Restore funktioniert vollständig

---

# 📌 Bonus

pfSense Backup exportiert:

```
Diagnostics → Backup & Restore
```

---
