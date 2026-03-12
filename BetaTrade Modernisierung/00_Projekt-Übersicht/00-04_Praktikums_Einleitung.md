# Einleitung zum Praktikumsbericht: IT-Infrastruktur-Modernisierung

## 1. Überblick zum Praktikum
Dieses Dokument dient als Rahmensetzung für die technische Dokumentation der Modernisierungsmaßnahmen bei der **BetaTrade AG**. Das Praktikum wurde bei der **AlphaTech GmbH** absolviert, einem IT-Dienstleister, der auf die Planung und Umsetzung komplexer Netzwerkinfrastrukturen spezialisiert ist.

Im Zeitraum des Praktikums lag der Fokus auf dem Projekt **"BetaTrade Modernisierung (ID 13)"**. Ziel war es, die veraltete Infrastruktur der BetaTrade AG durch moderne, skalierbare und sichere Systeme zu ersetzen.

## 2. Unternehmensvorstellung
### 2.1 Ausbildungsbetrieb: AlphaTech GmbH
Die AlphaTech GmbH agiert als technischer Generalunternehmer für dieses Projekt. Das Unternehmen zeichnet sich durch Expertise in den Bereichen Cisco-Networking, Virtualisierung und IT-Sicherheit aus. Während des Praktikums wurde ich vollständig in das Projekt-Team integriert und übernahm Verantwortung für Teilbereiche der Planung, Konfiguration und Dokumentation.

### 2.2 Der Kunde: BetaTrade AG
Die BetaTrade AG ist ein mittelständisches Unternehmen mit zwei zentralen Standorten:
*   **Kaiserslautern (Neubau):** Ein komplett neuer Standort, der von Grund auf (Greenfield-Ansatz) mit modernster Technik ausgestattet wurde.
*   **Mainz (Bestand):** Ein bestehender Standort, dessen Infrastruktur während des laufenden Betriebs modernisiert und an den neuen Standard angepasst werden musste.

## 3. Projektauftrag und Zielsetzung
Der Kernauftrag bestand in der vollständigen Erneuerung der Netzwerk- und Systemlandschaft. Dabei wurden folgende Schwerpunkte gesetzt:

1.  **Netzwerk-Segmentierung:** Einführung von VLANs zur Trennung von Abteilungen und Diensten (Management, Server, Clients, IoT).
2.  **Routing & Konnektivität:** Implementierung von OSPF für dynamisches Routing zwischen Core-, Distribution- und Access-Layern sowie Standortvernetzung.
3.  **Sicherheit (Hardening):** Einsatz von pfSense-Firewalls mit restriktiven Regelwerken (Least Privilege), VPN-Anbindung für Roadwarrior und Zertifikatsmanagement.
4.  **Zentrale Dienste:** Aufbau einer Windows Server 2025 Umgebung (Active Directory, DNS, DHCP) sowie Linux-basierter Dienste (Mailserver, Webserver, Docker).

## 4. Struktur des Praktikums (Zeitplan)
Das Praktikum wurde in vier thematische Blöcke (Wochen) unterteilt, um eine strukturierte Einarbeitung und Umsetzung zu gewährleisten:

*   **Woche 1: Analyse & Planung:** Bestandsaufnahme, Anforderungsanalyse und Erstellung der logischen Netzpläne in Packet Tracer.
*   **Woche 2: Netzwerkadministration:** Physische und logische Konfiguration der Cisco-Komponenten, Implementierung von DHCP und Basiskonnektivität.
*   **Woche 3: Systemadministration & Security:** Aufbau des Active Directory, VPN-Infrastruktur und Härtung der Firewall-Systeme.
*   **Woche 4: Integration & Übergabe:** Anbindung der Linux-Subsysteme (Mailcow/Docker), Fehlerbehebung (Troubleshooting) und Finalisierung der Dokumentation.

## 5. Methodik der Dokumentation
Ein wesentlicher Bestandteil des Praktikums war die **prozessbegleitende Dokumentation**. Hierfür wurde das Tool **Obsidian** genutzt. Die Vorteile dieser Methodik für den Prüfer sind:
*   **Verknüpfbarkeit:** Technische Abhängigkeiten zwischen Geräten und Protokollen sind durch Bi-Direktionale Links sofort ersichtlich.
*   **Aktualität:** Tagesprotokolle spiegeln den realen Lern- und Umsetzungsfortschritt wider.
*   **Visualisierung:** Komplexe Abläufe wurden mittels Mermaid.js-Diagrammen direkt in den Markdown-Dateien visualisiert.

## 6. Erwartungshaltung des Prüfers
Dieser Bericht enthält neben den rein technischen Konfigurationsauszügen auch Analysen zu getroffenen Design-Entscheidungen. Er soll nachweisen, dass die im Praktikum vermittelten Inhalte nicht nur angewendet, sondern in ihrem systemischen Zusammenhang verstanden wurden.
