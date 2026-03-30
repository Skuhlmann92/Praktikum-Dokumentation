# Praktikumsdokumentation: BetaTrade Modernisierung

## Titelblatt

### Modernisierung der IT-Infrastruktur

**Projekt:** BetaTrade Modernisierung (ID 13)  
**Kunde:** BetaTrade AG  
**Einsatzort:** Kaiserslautern / Mainz

### Erstellt von

**Samuel Kuhlmann**  
Cybersecurity Weiterbildung

### Praktikumsbetrieb

**AlphaTech GmbH**  
Technischer Generalunternehmer  
[Straße, PLZ Ort]

## Projektdaten

- **Projekt-ID:** 13
- **Projektname:** BetaTrade Modernisierung
- **Zeitraum:** 16.02.2026 bis 27.03.2026
- **Ansprechpartner AlphaTech:** [Name des Betreuers]
- **Ansprechpartner BetaTrade:** [IT-Leiter Kunde]

## Sperrvermerk

Der vorliegende Praktikumsbericht enthaelt vertrauliche Informationen ueber die IT-Infrastruktur, Sicherheitskonfigurationen und Netzwerk-Topologien der **BetaTrade AG** sowie interne Prozesse der **AlphaTech GmbH**.

Die Inhalte dieser Dokumentation sind ausschliesslich fuer Pruefungszwecke bestimmt. Eine Weitergabe des Berichts oder von Auszuegen daraus an Dritte, die Veroeffentlichung oder Vervielfaeltigung ist ohne ausdrueckliche schriftliche Genehmigung der AlphaTech GmbH und der BetaTrade AG nicht gestattet.

Nach Abschluss des Pruefungsverfahrens sind digitale Kopien sicher zu loeschen bzw. physische Exemplare auf Verlangen zurueckzugeben oder datenschutzgerecht zu vernichten.

### Freigabe
Reichshof, den 27.03.26
_________________________  
**Ort, Datum**
![[IMG_0877.jpeg|254]]
_________________________  
**Unterschrift (Praktikant)**

## Einleitung zum Praktikumsbericht

### Ueberblick zum Praktikum

Dieses Dokument dient als Rahmensetzung fuer die technische Dokumentation der Modernisierungsmassnahmen bei der **BetaTrade AG**. Das Praktikum wurde bei der **AlphaTech GmbH** absolviert, einem IT-Dienstleister, der auf die Planung und Umsetzung komplexer Netzwerkinfrastrukturen spezialisiert ist.

Im Zeitraum des Praktikums lag der Fokus auf dem Projekt **BetaTrade Modernisierung (ID 13)**. Ziel war es, die veraltete Infrastruktur der BetaTrade AG durch moderne, skalierbare und sichere Systeme zu ersetzen.

### Unternehmensvorstellung

#### Ausbildungsbetrieb: AlphaTech GmbH

Die AlphaTech GmbH agiert als technischer Generalunternehmer fuer dieses Projekt. Das Unternehmen zeichnet sich durch Expertise in den Bereichen Cisco-Networking, Virtualisierung und IT-Sicherheit aus. Waehrend des Praktikums wurde ich vollstaendig in das Projektteam integriert und uebernahm Verantwortung fuer Teilbereiche der Planung, Konfiguration und Dokumentation.

#### Kunde: BetaTrade AG

Die BetaTrade AG ist ein mittelstaendisches Unternehmen mit zwei zentralen Standorten:

- **Kaiserslautern (Neubau):** Ein komplett neuer Standort, der von Grund auf mit moderner Technik ausgestattet wurde.
- **Mainz (Bestand):** Ein bestehender Standort, dessen Infrastruktur waehrend des laufenden Betriebs modernisiert und an den neuen Standard angepasst wurde.

### Projektauftrag und Zielsetzung

Der Kernauftrag bestand in der vollstaendigen Erneuerung der Netzwerk- und Systemlandschaft. Dabei wurden folgende Schwerpunkte gesetzt:

1. **Netzwerk-Segmentierung:** Einfuehrung von VLANs zur Trennung von Abteilungen und Diensten.
2. **Routing und Konnektivitaet:** Umsetzung der Standort- und Netzverbindung mit Routing, Firewall und VPN.
3. **Sicherheit und Hardening:** Einsatz restriktiver Firewall-Regeln, Roadwarrior-VPN und Zertifikatsmanagement.
4. **Zentrale Dienste:** Aufbau einer Windows Server 2025 Umgebung mit Active Directory, DNS und DHCP sowie Linux-basierter Dienste wie Docker, Mailcow und Datenbanksystemen.

### Struktur des Praktikums

Das Praktikum wurde in mehrere thematische Arbeitsbloecke gegliedert:

- **Woche 1:** Analyse, Planung und Dokumentationsstruktur
- **Woche 2:** Netzwerkadministration und Basiskonnektivitaet
- **Woche 3:** Systemadministration, Active Directory und Firewall-Haertung
- **Woche 4:** Integration, Troubleshooting und Uebergabevorbereitung
- **Woche 5:** Betriebserweiterung, Freescout und Backup
- **Woche 6:** Security Operations, Scanning, SIEM/IDS und Richtlinien

### Methodik der Dokumentation

Ein wesentlicher Bestandteil des Praktikums war die prozessbegleitende Dokumentation in **Obsidian**. Diese Struktur erlaubt:

- **Verknuepfbarkeit:** Technische Abhaengigkeiten zwischen Systemen und Themenfeldern bleiben direkt nachvollziehbar.
- **Aktualitaet:** Tagesprotokolle spiegeln den realen Lern- und Umsetzungsfortschritt wider.
- **Visualisierung:** Netzplaene, Mermaid-Diagramme und technische Guides ergaenzen die operative Dokumentation.

### Erwartungshaltung des Pruefers

Dieser Bericht enthaelt neben technischen Konfigurationsauszuegen auch Analysen zu getroffenen Designentscheidungen. Er soll nachweisen, dass die im Praktikum vermittelten Inhalte nicht nur umgesetzt, sondern in ihrem systemischen Zusammenhang verstanden wurden.
