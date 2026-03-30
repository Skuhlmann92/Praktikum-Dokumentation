# 03 03a Incident Response Plan

# Incident Response Plan – BetaTrade AG (Projekt-ID 13)

**Dokument-Typ:** Notfall- & Vorfallmanagement-Vorlage  
**Version:** 1.0 – Entwurf Februar 2026  
**Gültig ab:** Nach Phase 3 (Woche 6)  
**Genehmigung:** IT-Leitung + Geschäftsführung  
**Status:** 🗓️ In Erstellung

> **WARNING:** Zweck
> Schnelle, koordinierte Reaktion auf Sicherheitsvorfälle (z. B. Ransomware, DDoS, unbefugter Zugriff, Datenleck) zur Minimierung von Schaden und Ausfallzeiten.

## 1. Rollen & Verantwortlichkeiten

| Rolle                     | Verantwortlicher (2026) | Aufgaben im Incident-Fall                                      |
|---------------------------|--------------------------|-----------------------------------------------------------------|
| Incident Response Lead    | IT-Leitung              | Gesamtkoordination, Eskalation, Kommunikation GF                |
| Technical Responder       | Netzwerk-Team           | Analyse, Eindämmung, Forensik (Logs, IDS-Alerts)                |
| Communication Lead        | Projektassistenz / GF   | Interne & externe Kommunikation, Behördenmeldung (DSGVO)        |
| Legal & Compliance        | Externer Datenschutzbeauftragter | DSGVO-Meldung, Schadensbegrenzung rechtlich                     |
| Business Owner            | Geschäftsführung        | Entscheidung über Weiterbetrieb / Notfallmaßnahmen              |

## 2. Incident-Kategorien & Prioritäten

| Priorität | Bezeichnung     | Beispiele                                      | Reaktionszeit (Ziel) | Eskalation nach |
|-----------|-----------------|------------------------------------------------|-----------------------|-----------------|
| P1        | Kritisch        | Ransomware, Datenleck Kundendaten, Totalausfall | 15 Min                | Sofort GF       |
| P2        | Hoch            | Unbefugter Zugriff Admin, DDoS, Phishing erfolgreich | 1 Stunde              | Nach 2 h GF     |
| P3        | Mittel          | Fehlkonfiguration, schwache Alerts             | 4 Stunden             | Täglich GF      |
| P4        | Niedrig         | Fehlalarme, geringfügige Anomalien             | 24 Stunden            | Wöchentlich     |

## 3. Incident Response Phasen (NIST-Modell)

1. **Preparation** (Vorbereitung)
   - [ ] Incident-Response-Team benannt
   - [ ] Tools & Zugänge (pfSense Logs, Syslog, IDS-Dashboard)
   - [ ] Backup & Restore getestet
   - [ ] Kommunikationsplan (Telefonliste, Eskalationsmatrix)

2. **Identification** (Erkennung)
   - Quellen: IDS-Alerts, Syslog, Benutzer-Meldungen, Monitoring-Dashboard
   - Erste Bewertung: Ist es echt? Priorität?
   - Hilfsmittel: Wireshark-Filter, pfSense-Logs, Windows Event Viewer, Firewall-/Host-Alerts

3. **Containment** (Eindämmung)
   - Kurzfristig: Isolieren betroffener Systeme (VLAN abschalten, Port shut)
   - Langfristig: Backup wiederherstellen, Passwörter rotieren

4. **Eradication** (Beseitigung)
   - Malware entfernen, Schwachstelle patchen
   - Root-Cause-Analyse (Warum konnte es passieren?)

5. **Recovery** (Wiederherstellung)
   - Systeme schrittweise online bringen
   - Monitoring verstärken (24 h Nachbeobachtung)

6. **Lessons Learned** (Nachbereitung)
   - Post-Incident-Review (innerhalb 7 Tagen)
   - Update Risiko-Register & Kontrollen

## 4. Kommunikationsplan

- **Intern:** Sofort per Teams/SMS an IR-Team
- **GF:** Bei P1/P2 innerhalb 30 Min
- **Kunden:** Bei Datenleck innerhalb 72 h (DSGVO)
- **Behörden:** Meldung an Landesdatenschutzbeauftragten bei relevanten Vorfällen

## 5. Wichtige Kontakte (Beispiel – anpassen!)

- IT-Leitung: +49 6xxx xxx xxx
- GF: +49 6xxx xxx xxx
- Externer Datenschutz: datenschutz@betatrade.de
- Notfall-Hotline Provider (z. B. pfSense-Support): …

## 6. Operative Hilfsmittel fuer die Erkennung

- Wireshark-Filterreferenz: [Wireshark Filters Reference](../../_assets/wireshark_filters_reference.jpg)
- Phase-3-Kontext mit Host-Alert-Beispiel: [03_03_Phase_3_Security_Konzept.md](03_03_Phase_3_Security_Konzept.md)

> **TIP:** Schnell-Checkliste bei Vorfall
> 1. Ruhe bewahren  
> 2. Nichts löschen / ändern (Forensik!)  
> 3. IR-Lead informieren  
> 4. Logs sichern (Export vor Neustart)  
> 5. Systeme isolieren, nicht ausschalten

→ Verlinkte Dokumente:  
[03_03_Phase_3_Security_Konzept.md](03_03_Phase_3_Security_Konzept.md) | [04_02_Risiko_Register.md](../../03_Uebergabe_und_Archiv/04_02_Risiko_Register.md) | [03_03b_ISO27001_Checkliste.md](03_03b_ISO27001_Checkliste.md) | [00_01_Masterdokumentation.md](../../00_Projekt-Übersicht/00_01_Masterdokumentation.md)

**Letzte Aktualisierung:** 20.02.2026  
**Nächste Überprüfung:** Nach Phase 3 Go-Live


