**Rolle:** IT-Security-Analyst*in bei AlphaTech GmbH **Datum:** 2026-03-26 **Status:** #abgeschlossen

---

## 📋 Aufgabe 1 – Bestehende Richtlinie analysieren

> [!info] Analysierte Richtlinie Datei: `BetaTrade_Incident_Response_Richtlinie.docx` Organisation: BetaTrade AG Analysestand: 2026-03-26

---

### ✅ Was ist bereits vorhanden?

Die Richtlinie deckt folgende Bereiche strukturiert ab:

- **Geltungsbereich** – alle Mitarbeitenden, externe DL, IT- und Sicherheitspersonal; alle IT-Systeme, Netzwerke, Server, Anwendungen
- **Begriffsdefinitionen** – klare Hierarchie: Event → Alert → Incident → False Positive, inkl. Erkennungssysteme und Behandlung
- **Verantwortlichkeiten** – ISB (koordinierend), IT-Administration (operativ-technisch), Mitarbeitende (Meldepflicht), Management (Gesamtverantwortung)
- **Erkennung** – technische Maßnahmen, Log-Analyse/Monitoring, Mitarbeitermeldungen, stufenweise Alert-Bewertung
- **Behandlungsablauf** – 5 Schritte: Eindämmung → Analyse → Beseitigung → Wiederherstellung → Nachbereitung
- **Schweregrad-Klassifikation** – Niedrig / Mittel / Hoch / Kritisch mit Beispielen
- **Dokumentationsanforderungen** – Mindestinhalte für Incident-Dokumentation definiert
- **Eskalationsstufen** – abhängig vom Schweregrad (Niedrig/Mittel intern, Hoch/Kritisch → Management)
- **Schulung & Sensibilisierung** – grundsätzlich gefordert
- **Überprüfung & Konsequenzen** – anlassbezogene Richtlinienprüfung, Sanktionen bei Verstößen

---

### ⚠️ Was ist zu vage oder zu oberflächlich beschrieben?

|Bereich|Problem|Bewertung aus Praxis (Tag 1–3)|
|---|---|---|
|**7.3 Meldewege**|Vollständig leer – keine Kontakte, keine Kanäle, keine Fristen|In der Praxis (Tag 3) wurde der Portscan direkt in Kibana gesehen – kein definierter Meldeweg vorhanden|
|**5.1 Technische Erkennungsmaßnahmen**|Keine konkreten Tools genannt|Tatsächlich im Einsatz: Suricata (IDS) + ELK-Stack (SIEM), OpenVAS/Greenbone (Vulnerability Scanner)|
|**5.2 Log-Analyse**|Keine konkreten Systeme, kein Aufbewahrungszeitraum|Kibana auf `192.168.13.15:5601` mit Suricata-EVE-JSON-Logs – nicht in der Richtlinie erwähnt|
|**6.1 Grundsätzlicher Ablauf**|Keine Zeitvorgaben (Reaktionszeiten, SLAs)|Beim Port-Scan (Tag 3) keine definierten Fristen – wie schnell muss reagiert werden?|
|**6.3 Maßnahmen nach Schweregrad**|Nur allgemeine Aussagen, keine konkreten Handlungsschritte|Z. B. bei EternalBlue (Tag 1, CVSS 9.3): Richtlinie sagt nur „umgehende Behandlung" – kein Playbook|
|**8. Schulung**|Kein Rhythmus, kein Pflichtnachweis, kein Format|—|

---

### ❌ Was fehlt komplett?

- **Konkrete Meldewege und Kontaktdaten** – Sektion 7.3 ist leer (kein Ticket-System, keine E-Mail, kein Telefon)
- **Reaktionszeiten / SLAs** – kein einziger Zeitwert in der gesamten Richtlinie
- **Spezifische Detection-Tools** – Suricata, ELK-Stack und OpenVAS laufen tatsächlich, stehen aber nirgends
- **Playbooks / Runbooks** für bekannte Incident-Typen (Port-Scan, Vulnerability-Fund, Malware)
- **Externe Meldepflichten** – BSI-Meldung, DSGVO Art. 33 (72h-Frist bei Datenschutzverletzung)
- **Beweissicherung / Forensik** – kein einziger Satz dazu
- **Kommunikationsplan** bei kritischen Vorfällen (interne + externe Kommunikation)
- **Recovery-Kriterien** – wann gilt ein System als „clean" und darf zurück in den Betrieb?
- **False-Positive-Prozess** – definiert, dass FPs dokumentiert werden, aber kein Prozess wie genau

---

### 🔍 Vergleich mit Erfahrungen Tag 1–3

| Tag       | Erfahrung                                                                                                 | Deckt die Richtlinie das ab?                                                              |
| --------- | --------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| **Tag 1** | OpenVAS-Scan → EternalBlue (CVSS 9.3) auf `10.10.148.71` gefunden                                         | Teilweise: Schweregrad „Kritisch" wäre passend, aber kein Playbook für Vulnerability-Fund |
| **Tag 2** | ELK-Stack / Suricata aufgesetzt, Baseline erhoben (~1.358 Events/min, 0 Packet Drops)                     | Nein: Richtlinie nennt keine konkreten Tools, keine Baseline-Anforderung                  |
| **Tag 3** | Live-Portscan `nmap -sV 192.168.13.1` durchgeführt → 2.000 Events/min in Kibana, Suricata-Alert ausgelöst | Teilweise: Event→Alert→Incident-Prozess stimmt, aber kein Meldeweg, keine Zeitvorgabe     |
| **Tag 2** | 5 Alerts analysiert (APT User-Agent, Truncated Packets, NCSI) – alle False Positives                      | Schwach: FP-Prozess nur als Satz erwähnt, kein konkretes Vorgehen                         |

> [!note] Fazit Richtlinienanalyse Die Richtlinie ist ein solides konzeptionelles Grundgerüst, scheitert aber in der Praxis an fehlenden Detailangaben. Ein Security-Analyst, der heute (Tag 3) einen Port-Scan erkennt, findet in der Richtlinie **keine Antwort** auf die Fragen: Wo melde ich das? Bis wann? Mit welchem Tool dokumentiere ich? Was genau tue ich als nächstes?

---

## 🛠️ Aufgabe 2 – Richtlinie konkretisieren und erweitern

### Ergänzung 1: Konkrete Detection-Systeme (zu Sektion 5.1)

**Problem:** Richtlinie beschreibt Erkennungsmaßnahmen abstrakt ohne konkrete Tools.

**Vorschlag für Ergänzung in Sektion 5.1:**

```
5.1 Eingesetzte Erkennungssysteme bei BetaTrade AG (konkret):

- Suricata (NIDS/NIPS)
  - Echtzeit-Netzwerkanalyse auf Interface ens19
  - Alert-Generierung via Regel-Signaturen (EVE-JSON-Format)
  - Überwachte Protokolle: TCP/UDP/DNS/HTTP/TLS/SSH/Flow

- ELK-Stack (SIEM)
  - Kibana Dashboard: http://192.168.13.15:5601
  - Elasticsearch als zentrale Log-Datenbank
  - Filebeat als Log-Shipper von Suricata → Elasticsearch
  - Zuständig für: Log-Speicherung, Visualisierung, Alert-Übersicht

- OpenVAS / Greenbone (Vulnerability Scanner)
  - Regelmäßige Schwachstellen-Scans des internen Netzes (192.168.13.0/24)
  - Non-credentialed und credentialed Scan-Modi
  - Ergebnisse nach CVSS-Score klassifiziert

- Überwachte Log-Quellen:
  - Suricata EVE-JSON (Netzwerk-Events und Alerts)
  - System-Logs der Hosts 192.168.13.10, .15, .20
  - DNS-Queries (Port 53/UDP)
  - Authentifizierungsereignisse (SSH Port 22, RDP Port 3389)
```

---

### Ergänzung 2: Reaktionszeiten / SLAs (neue Sektion 6.0)

**Problem:** Keine einzige Zeitangabe in der gesamten Richtlinie.

**Vorschlag für neue Sektion 6.0:**

|Schweregrad|Erstreaktion (Meldung)|Eindämmung|Management-Info|Beispiel aus Praxis|
|---|---|---|---|---|
|**Niedrig**|< 24h|< 72h|nicht erforderlich|TCP Timestamps aktiv (CVSS 2.6)|
|**Mittel**|< 4h|< 24h|bei Bedarf|RDP schwache Cipher (CVSS 4.3)|
|**Hoch**|< 1h|< 4h|< 1h|RPC-Enumeration lsass.exe (CVSS 5.0)|
|**Kritisch**|< 15 Min|sofort|sofort|EternalBlue CVSS 9.3 → RCE möglich|

> [!tip] Begründung aus Praxis Beim Port-Scan (Tag 3) stieg die Event-Rate innerhalb von Sekunden auf 2.000 Events/min. Ohne definierte Reaktionszeit ist unklar, ob 5 Minuten oder 2 Stunden akzeptabel sind.

---

### Ergänzung 3: Konkrete Meldewege (Sektion 7.3 – derzeit leer)

**Problem:** Sektion 7.3 enthält keinen einzigen konkreten Kontakt oder Kanal.

**Vorschlag zur Befüllung von Sektion 7.3:**

```
7.3 Meldewege BetaTrade AG

Erstmeldung durch Mitarbeitende:
  → Kanal: Freescout Mail Ticket System
  → Erreichbarkeit: Mo–Fr 08:00–18:00

Meldung an IT-Administration:
  → E-Mail: [it-admin@betatrade.ag] ← NOCH ZU BEFÜLLEN
  → Telefon: [intern XXXX] ← NOCH ZU BEFÜLLEN

Meldung an ISB:
  → E-Mail: [security@betatrade.ag] ← NOCH ZU BEFÜLLEN
  → Bei Schweregrad HOCH oder KRITISCH: auch telefonisch
  → Rufbereitschaft: [Ja/Nein – NOCH ZU KLÄREN]

Eskalation an Management:
  → Bei Schweregrad HOCH: innerhalb 1h
  → Bei Schweregrad KRITISCH: sofort, auch außerhalb Bürozeiten

Externe Meldepflichten:
  → BSI (KRITIS): bei kritischen Vorfällen
  → Datenschutzbehörde: bei DSGVO-relevantem Datenverlust (72h-Frist, Art. 33 DSGVO)
```

---

### Ergänzung 4: Beweissicherung (neue Sektion 6.1a – fehlt komplett)

**Problem:** Kein einziger Satz zu Forensik/Beweissicherung in der Richtlinie.

**Vorschlag für neue Sektion 6.1a:**

```
6.1a Beweissicherung (NEU)

Vor Einleitung destruktiver Gegenmaßnahmen müssen Beweise gesichert werden:

Technische Maßnahmen:
  - Log-Export aus Kibana/Elasticsearch (mit exakten Timestamps)
  - Suricata EVE-JSON sichern (Pfad: /var/log/suricata/eve.json)
  - Netzwerk-Capture (PCAP) falls Angriff noch aktiv: tcpdump -i ens19
  - Screenshots der Kibana-Dashboard-Ansicht (Event-Rate, Alerts)
  - Memory Dump bei Malware-Verdacht (vor Neustart!)

Grundsatz:
  Kein Neustart, kein Löschen, keine Konfigurationsänderung am 
  betroffenen System vor Beweissicherung – außer zur unmittelbaren 
  Schadensbegrenzung bei aktivem Angriff.

Aufbewahrung: Logs mindestens 90 Tage (DSGVO/Nachweispflicht).
```

---

### Ergänzung 5: False-Positive-Prozess (zu Sektion 5.4)

**Problem:** FPs werden laut Richtlinie „dokumentiert", aber kein konkreter Prozess.

**Aus Praxis Tag 2:** 5 von 5 analysierten Alerts waren False Positives (APT User-Agent, Truncated Packets, NCSI). Ohne strukturierten FP-Prozess entsteht Alert-Fatigue.

**Vorschlag:**

```
FP-Dokumentation enthält mindestens:
  - Alert-ID / Signature-ID (SID)
  - Grund für FP-Einordnung
  - Empfehlung: Regel supprimieren / Threshold anpassen / Whitelist

Beispiele aus BetaTrade-Praxis:
  - ET INFO GNU/Linux APT User-Agent → whitelist de.archive.ubuntu.com
  - SURICATA AF-PACKET truncated packet → snaplen auf 65535 erhöhen
  - ET INFO Microsoft Connection Test → whitelist NCSI-IPs
```

---

## 📝 Aufgabe 3 – Incident Report

> [!info] Dokumentierter Vorfall Port-Scan-Simulation vom 25. März 2026 (Tag 3 der Woche)

---

### INCIDENT REPORT – BetaTrade AG

**Report-ID:** IR-2026-001 **Erstellt von:** IT-Security-Analyst*in (Praktikum) – AlphaTech GmbH **Erstellungsdatum:** 2026-03-26

---

#### 1. Vorfallsübersicht

|Feld|Wert|
|---|---|
|**Vorfallstyp**|Netzwerk-Port-Scan (Reconnaissance / SCAN)|
|**Schweregrad**|Mittel (simuliert) / in Realproduktion: Hoch|
|**Status**|Geschlossen (Simulation)|
|**Erkennungszeitpunkt**|2026-03-25, ca. 10:51 Uhr|
|**Bestätigungszeitpunkt**|2026-03-25, ca. 10:52 Uhr (sofort in Kibana sichtbar)|
|**Abschlusszeitpunkt**|2026-03-25, Übungsende|

---

#### 2. Erkennung

|Feld|Wert|
|---|---|
|**Erkennungsquelle**|Suricata IDS → ELK-Stack (Kibana Dashboard)|
|**Alert-Kategorie**|SCAN (Reconnaissance / attempted-recon)|
|**Alert-Beschreibung**|Massive Zunahme der Event-Rate durch SYN-Pakete auf mehrere Ports sequenziell|
|**Erkannt durch**|IT-Security-Analyst*in via Kibana Suricata-Dashboard|

**Beobachtung in Kibana:**

```
Baseline vor Scan:  ~30 Events/Minute  (Normalzustand Tag 3)
Während Scan:       ~2.000 Events/Minute  (+6.567% Anstieg)
Event-Typen:        flow, alert (SCAN-Klasse)
```

**Ausgeführter Scan-Befehl (Angreifer-Perspektive):**

```bash
nmap -sV 192.168.13.1
```

**Passende Suricata-Erkennungsregel (Community-Standard):**

```
alert tcp any any -> $HOME_NET any (
  msg:"Possible Port Scan Detected";
  flags:S;
  threshold:type threshold, track by_src, count 5, seconds 10;
  sid:9000003; rev:3;
)
```

Regel greift auf: SYN-Flag im TCP-Header, mehr als 5 Verbindungsversuche / 10 Sekunden von derselben Quell-IP.

---

#### 3. Betroffene Systeme und Daten

|System|IP / Hostname|Betroffenheit|
|---|---|---|
|Internes Netzwerk-Gateway|192.168.13.1|Scan-Ziel (alle Ports gescannt)|
|Suricata-Sensor / Kibana-Host|192.168.13.15|Alert erzeugt, nicht angegriffen|
|Interne Hosts|192.168.13.10, .20|Indirekt betroffen (Scan-Traffic im Segment)|

**Betroffene Daten:**

- Keine personenbezogenen Daten betroffen (Simulation)
- Keine Datentransmission / kein Datenabfluss festgestellt
- Reines Reconnaissance-Event (Aufklärungsphase)

---

#### 4. Analyse und Ursache

**Angriffsmuster:**

```
nmap -sV sendet SYN-Pakete an alle Ports sequenziell.
Suricata registriert den massiven Anstieg von TCP-SYN-Paketen
von einer einzigen Source-IP innerhalb weniger Sekunden.
Event-Rate: 30 → 2.000 Events/Minute (anomal).
Alert-Klasse: SCAN (classtype: attempted-recon)
```

**Zeitlicher Ablauf (Timeline):**

|Zeitpunkt|Ereignis|
|---|---|
|~10:50 Uhr|Baseline-Check in Kibana: 30 Events/min, normaler Zustand|
|~10:51 Uhr|`nmap -sV 192.168.13.1` gestartet vom Security-Server|
|~10:51 Uhr|Event-Rate springt auf ~2.000 Events/min in Kibana|
|~10:52 Uhr|Suricata SCAN-Alert ausgelöst, im Dashboard sichtbar|
|~10:52 Uhr|Analyst bestätigt Incident (kein False Positive – Simulation bekannt)|
|Übungsende|Vorfall als Simulation dokumentiert, Analyse abgeschlossen|

**Risikobewertung (wenn real):**

Ein Port-Scan ist typischerweise die Vorbereitungsphase eines Angriffs (Reconnaissance). Im Kontext der Woche besonders relevant: Auf `10.10.148.71` wurde in Tag 1 via OpenVAS **MS17-010 / EternalBlue (CVSS 9.3)** gefunden. Ein realer Angreifer würde nach dem Port-Scan genau diese offenen Ports (445/tcp SMB, 3389/tcp RDP) als nächstes gezielt angreifen.

---

#### 5. Getroffene Maßnahmen

**Im Rahmen der Simulation:**

- Scan in Kibana beobachtet und dokumentiert
- Alert-Kategorie korrekt als SCAN (Reconnaissance) eingeordnet
- Suricata-Erkennungsregel analysiert und verstanden
- Kein produktiver Schaden entstanden

**Empfohlene Maßnahmen bei realem Vorfall:**

- Quell-IP des Scanners sofort in Firewall sperren
- Betroffenes Segment auf weitere verdächtige Aktivität überwachen (Post-Scan-Aktivität?)
- Prüfen: Hatte die Quell-IP Erfolg? Offene Ports identifiziert?
- Wenn interne IP: Kompromittierung des internen Hosts prüfen
- Log-Sicherung aus Kibana/Elasticsearch für Beweissicherung

---

#### 6. Wiederherstellung

|Feld|Wert|
|---|---|
|**Systemzustand**|Nicht beeinträchtigt (Simulation)|
|**Normalbetrieb**|Durchgehend aufrechterhalten|
|**Nachkontrolle**|Baseline-Rate nach Scan wieder auf ~30 Events/min bestätigt|

---

#### 7. Nachbereitung und Lessons Learned

**Was hat funktioniert:**

- Suricata hat den Scan sofort und zuverlässig erkannt
- Kibana-Dashboard machte die Anomalie visuell sofort sichtbar (Event-Rate-Sprung)
- Die Event → Alert → Incident-Hierarchie aus der Richtlinie war in der Praxis korrekt anwendbar

**Was die Richtlinie NICHT abgedeckt hat:**

- Kein definierter Meldeweg: Wohin hätte ich den Alert gemeldet?
- Keine Zeitvorgabe: Wie schnell muss ich reagieren?
- Kein Playbook für „Port-Scan erkannt": Was sind die nächsten konkreten Schritte?
- Keine Beweissicherungsanweisung: Log-Export vor Gegenmaßnahmen?

**Verbesserungsmaßnahmen:**

- [ ] Reaktionszeiten-Tabelle in Richtlinie aufnehmen (siehe Ergänzung 2)
- [ ] Meldeweg Sektion 7.3 konkret befüllen
- [ ] Port-Scan-Playbook erstellen
- [ ] Suricata-Threshold für Port-Scan-Regel kalibrieren (aktuell: 5 SYN/10s)
- [ ] snaplen auf 65535 erhöhen (behebt Truncated-Packet-Alerts aus Tag 2)

---

#### 8. Abschließende Bewertung

|Feld|Wert|
|---|---|
|**Endgültige Einstufung**|Incident (simuliert) / kein False Positive|
|**Schweregrad**|Mittel (Simulation) → Hoch (reale Umgebung mit bekannten Schwachstellen)|
|**Folgeaktionen erforderlich**|Ja: Richtlinienergänzungen, Playbook Port-Scan|
|**Besonderheit**|Kontext zu Tag 1: EternalBlue auf Port 445 gefunden → Portscan wäre direkter Angriffsvorläufer|
