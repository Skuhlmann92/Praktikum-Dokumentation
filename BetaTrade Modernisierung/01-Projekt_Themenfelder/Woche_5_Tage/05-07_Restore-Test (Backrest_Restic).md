# 🔄 Restore-Test (Backrest / Restic)

---

## 🎯 Ziel

- Überprüfung der Backup-Integrität
    
- Wiederherstellung einer einzelnen Datei
    
- Dokumentation von Dauer und Ablauf
    

👉 Restic stellt Daten aus einem Snapshot in ein Zielverzeichnis wieder her ([Debian Manpages](https://manpages.debian.org/bookworm/restic/restic-restore.1.en.html?utm_source=chatgpt.com "restic-restore(1) — restic — Debian bookworm — Debian Manpages"))

---

# 🧪 1. Linux Restore

---

## 🔹 1.1 Testdatei identifizieren

```bash
cd /home/student13/test-backup
ls
```

👉 ausgewählte Datei:

```text
test2.txt
```

---
Dateiliste vor Löschung
![[Pasted image 20260320104155.png]]
---

## 🔹 1.2 Datei löschen

```bash
rm test2.txt
```

```bash
ls
```

👉 Datei ist entfernt

![[Pasted image 20260320111614.png]]
---

## 🔹 1.3 Restore starten (Backrest GUI)

👉 Schritte:

1. Backrest öffnen
    
2. Repository auswählen
    
3. Snapshots öffnen
    
4. letzten Snapshot auswählen
    
5. Datei `test2.txt` suchen
    
6. **Restore to path** klicken
    

---

Snapshot Browser
![[Pasted image 20260320111718.png]]
---

## 🔹 1.4 Zielpfad setzen

```text
/restore/
```

👉 Restore starten

---
Restore Dialog
![[Pasted image 20260320112000.png]]
---

## 🔹 1.5 Restore prüfen

```bash
sudo ls /restore/home/student13/test-backup/
```

👉 Datei wieder vorhanden

---  
Restore Ergebnis

![[Pasted image 20260320112249.png]]

---

## 🔹 1.6 Datei zurückkopieren

```bash
sudo cp /restore/home/student13/test-backup/test2.txt /home/student13/test-backup/
```

---  
Datei wieder im Originalordner
![[Pasted image 20260320113249.png]]

---

# 🧪 2. Windows Restore

---

## 🔹 2.1 Datei löschen

👉 Pfad:

```text
C:\Backup
```

👉 Datei `test2.txt` löschen

---


Windows Datei gelöscht
![[Pasted image 20260320114436.png]]

---

## 🔹 2.2 Backrest öffnen

👉 Browser:

```text
http://localhost:9897
```

---

## 🔹 2.3 Restore durchführen

👉 Schritte:

1. Snapshot öffnen
    
2. Datei auswählen
    
3. **Restore to path** klicken
    
4. Ziel:
    

```text
C:\Backup
```

---

Windows Restore
![[Pasted image 20260320115118.png]]

---

## 🔹 2.4 Ergebnis prüfen

👉 Datei wieder vorhanden

---
Windows Restore Ergebnis
![[Pasted image 20260320115304.png]]

---
## 🔹 2.5 Datei per Konsole zurückkopieren (Windows)

Nach dem erfolgreichen Restore wurde die Datei zusätzlich per Kommandozeile in das ursprüngliche Verzeichnis kopiert.

---

### 🔧 Befehl

```cmd
copy C:\restore\Backup\test2.txt C:\Backup\
```

---

### 🧠 Erklärung

- `copy` kopiert Dateien in Windows
    
- erster Pfad = Quelle (Restore-Verzeichnis)
    
- zweiter Pfad = Ziel (Originalverzeichnis)
    

---
CMD mit Copy-Befehl
Datei im Zielverzeichnis
![[Pasted image 20260320115509.png]]

---

### 🔍 Überprüfung

```cmd
dir C:\Backup
```

👉 Datei ist wieder vorhanden:

```text
test2.txt
```

---

### 📌 Ergebnis

Die Datei wurde erfolgreich:

- aus dem Backup wiederhergestellt
    
- per Konsole kopiert
    
- im Originalverzeichnis verifiziert
    

--- 
# ⏱️ 3. Zeitmessung

|Aktion|Zeit|
|---|---|
|Restore Start|14:10|
|Restore Ende|14:12|
|Dauer|~2 Minuten|

---

# 📊 4. Bewertung

|Kriterium|Ergebnis|
|---|---|
|Datei gefunden|✔|
|Restore erfolgreich|✔|
|Dauer akzeptabel|✔|
|Bedienung einfach|✔|

---

# ⚠️ Besonderheiten

- Snapshot Browser benötigt 1–3 Minuten Ladezeit
    
- Ursache: S3 lädt Index und Dateistruktur verzögert
    
- kein klassisches Dateisystem
    

---

# 🧠 Technischer Hintergrund

👉 Restic arbeitet mit Snapshots:

- Snapshot = Zustand eines Systems
    
- Daten werden daraus extrahiert (restore) ([Creative Projects](https://creativeprojects.github.io/resticprofile/reference/profile/restore/index.html?utm_source=chatgpt.com "restore :: resticprofile"))
    

👉 Restore erfolgt immer in ein Zielverzeichnis:

```text
--target /restore
```

([Ralphs Blog](https://golb.hplar.ch/2020/04/backup-restic.html?utm_source=chatgpt.com "Backup with restic"))

---

# 🧾 Fazit

Der Restore-Test war erfolgreich:

- Datei konnte wiederhergestellt werden
    
- Backup ist funktional
    
- System ist einsatzbereit
    

👉 Backup-System gilt als validiert

---

# ✅ Ergebnis

✔ Restore funktioniert  
✔ Daten vollständig  
✔ Backup zuverlässig

---