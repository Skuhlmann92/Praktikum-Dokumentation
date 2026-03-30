# 02 04 Tag 1 Docker SQL Infrastruktur



**Datum:** 09.03.2026  
**Bearbeiter:** Samuel 
## 🎯 Tagesziele
- [x] Docker-Umgebung auf Ubuntu-Server verifizieren
- [x] BetaTrade-Kundendatenbank via Docker-Compose bereitstellen
- [x] Business Intelligence Abfragen (SQL) zur Kundenstruktur durchführen
- [x] Backup-Prozess für MySQL-Container validieren

## 👥 Gruppenarbeit
1. **Infrastruktur-Check:** Gemeinsame Durchsicht der `docker-compose.yml` (Mapping von Ports und Volumes).
2. **SQL-Review:** Besprechung der JOIN-Logik für die Verknüpfung von `customers`, `accounts` und `trades`.

## 👤 Einzelarbeit
1. **Container-Management:** Implementierung der Lifecycle-Befehle (Up/Down/Logs).
2. **Datenanalyse:** Erstellung und Test der SQL-Abfragen für die Neukunden-Analyse 2024.
3. **Dokumentation:** Erstellung des Technischen Guides für Docker & SQL (siehe Analysen).

## 📝 Reflexion / Offene Punkte
- Die Container-Lösung bietet eine saubere Trennung von Anwendung und Datenbank.
- Herausforderung: SQL-Dumps müssen automatisiert in den Cloud-Backup-Prozess integriert werden.
- Nächster Schritt: Integration der Datenbank in das Monitoring (Themenfeld 4).
