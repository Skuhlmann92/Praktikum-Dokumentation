# 02 01 Tag 1 Onboarding Analyse


**Datum:** 16.02.2026  
**Rolle:** Projektassistenz / technische Dokumentation

## Ziel des Tages
Am ersten Tag wurde der Projektauftrag eingeordnet, die Ausgangslage des Kunden gesichtet und die Dokumentationsbasis für die folgenden Umsetzungswochen vorbereitet.

## Durchgeführte Arbeitsschritte
1. Kick-off mit Aufgabenabgrenzung zwischen Planung, Umsetzung und Dokumentation durchgeführt.
2. Digitale Kundenakte und vorhandene Ausgangsunterlagen für Kaiserslautern und Mainz gesichtet.
3. Arbeitsumgebung mit Admin-VM, VPN/RDP-Zugang und Obsidian-Vault vorbereitet.
4. Grundstruktur für Projektordner, Tagesprotokolle, Referenzen und Übergabedokumente angelegt.
5. Erste Schwachstellen und Modernisierungsziele aus Kundensicht zusammengefasst.

## Lösung der Tagesaufgaben

### Gruppenarbeit

#### 1. Team-Kick-off und Projektverständnis
- Kick-off via MS Teams als organisatorischer Einstieg des Teams durchgeführt.
- Die digitale Kundenakte der BetaTrade AG gemeinsam ausgewertet und die drei Projektphasen inhaltlich voneinander abgegrenzt.
- Die Rollen von AlphaTech festgelegt:
  Planung und technische Konzeption in Woche 1,
  Umsetzung der Netzwerk- und Systeminfrastruktur in Woche 2 bis 4,
  Vorbereitung bzw. konzeptionelle Erweiterung für Security und Monitoring in Phase 3.
- Die Dokumentationsarbeit für die Woche auf Tagesprotokolle, Phasenbeschreibungen, Risikoerfassung und Übergabeunterlagen verteilt.
- Als Dokumentationstool wurde Obsidian gewählt, weil die Struktur mit Markdown, internen Verweisen und PDF-Export für das Fachgespräch geeignet ist.

#### 2. Netzwerk-Szenarien verstehen
- Die Packet-Tracer-Topologie für Kaiserslautern als Greenfield-Szenario mit drei Abteilungen analysiert.
- Die Mainz-Topologie als Modernisierung einer bestehenden Umgebung mit produktionsnahen Diensten eingeordnet.
- Die Hauptunterschiede festgehalten:
  Kaiserslautern benötigt saubere VLAN- und IP-Planung von Grund auf,
  Mainz benötigt eine risikoarme Migration mit besonderem Fokus auf VPN, DHCP, DNS und spätere AD-/Docker-Integration.
- Zentrale Herausforderung in beiden Szenarien:
  technische Segmentierung und sicherer Fernzugriff müssen früh sauber geplant werden, damit spätere Dienste stabil aufgebaut werden können.

### Einzelarbeit

#### 1. Technische Arbeitsumgebung einrichten
- Dashboard, Admin-VM und bereitgestellte Arbeitsumgebung erfolgreich gesichtet.
- VPN-Konfiguration importiert und Verbindung grundsätzlich verifiziert.
- RDP-Zugriff zur Admin-VM getestet und als Grundlage für die spätere Arbeit dokumentiert.
- Grundfunktionen geprüft:
  Erreichbarkeit der VM,
  Zugriff auf Arbeitsoberfläche,
  Nutzbarkeit für Dokumentation und spätere Infrastrukturaufgaben.
- Potenzielle Störquellen notiert:
  VPN-Lockout-Risiko,
  Abhängigkeit von Fernzugriff,
  Bedarf einer sauberen Zugangs- und Nachweisdokumentation.

#### 2. Projektdokumentation strukturieren
- Projektordner `BetaTrade Modernisierung` als zentrale Arbeitsablage angelegt.
- Startlogik für Projektübersicht, Tagesprotokolle, Phasen, Übergabe und Referenzen definiert.
- Damit wurde sichergestellt, dass spätere Konfigurationsschritte, Screenshots und Entscheidungen nachvollziehbar einsortiert werden können.
- Die Toolentscheidung wurde methodisch begründet:
  Obsidian erfüllt Offline-Nutzung, lokale Datenhaltung, Markdown-Basis und PDF-Export für die Abgabe am besten.
- Für die spätere Ablage wurde zusätzlich ein konsistenter Metadaten- und Strukturansatz vorbereitet, damit Tagesprotokolle, Analysen und Übergabeunterlagen einheitlich gepflegt werden können.

#### 3. Erste Anforderungsanalyse durchführen
- Kritische Probleme aus der Kundenakte priorisiert:
  fehlende Segmentierung in Kaiserslautern,
  unsicherer externer Zugriff in Mainz,
  fehlendes Backup-Konzept,
  unklare serviceorientierte Struktur für spätere Kernsysteme.
- Erste Prioritätenliste erstellt:
  1. Netzsegmentierung und Adresskonzept,
  2. sicherer Fernzugriff per VPN,
  3. zentrale Dienste wie DHCP und DNS,
  4. darauf aufbauend AD, Docker und Mail-Integration.
- Obsidian wurde dabei bewusst gegen typische Cloud-Werkzeuge abgegrenzt, weil lokale Datenhaltung und spätere Exportfähigkeit im Projektkontext wichtiger als Kollaborationskomfort waren.

### Abschluss des Tages
- Das technische Setup wurde als arbeitsfähig eingeordnet.
- Die erste Anforderungsanalyse wurde gespeichert und als Grundlage für Tag 2 vorbereitet.
- Ein kurzes Statusupdate ans Team ist fachlich vorbereitet:
  Dokumentationsstruktur steht,
  Arbeitszugang funktioniert,
  die ersten Kernprobleme des Kunden sind identifiziert.
- Rückfragen für das nächste Check-in wurden abgeleitet:
  genaue Rollenverteilung,
  Umfang von Phase 1,
  zeitliche Abhängigkeit zwischen VPN, DHCP/DNS und späterer Serverintegration.

## Entscheidung und Begründung
**Ausgangslage:** Die Unterlagen enthielten technische Informationen zu zwei Standorten, aber noch keine einheitliche Arbeitsstruktur für Nachweise und Projektdokumentation.

**Gewählte Option:** Die Dokumentation wurde von Beginn an in einer klar gegliederten Vault-Struktur mit Tagesprotokollen, Phasen, Referenzen und Übergabeunterlagen aufgebaut.

**Warum diese Option:** So lassen sich spätere Konfigurationsschritte, Entscheidungen und Nachweise taggenau ablegen und für den Kunden nachvollziehbar wiederfinden.

**Nachweis:** Projektstruktur, erste Projektübersicht und die gesichteten Kundenunterlagen bilden die Grundlage für alle Folgeprotokolle.

## Ergebnis des Tages
- Projektauftrag und Rollentrennung verstanden
- Unterschiede zwischen Neubau Kaiserslautern und Bestandsstandort Mainz dokumentiert
- Dokumentationsumgebung funktionsfähig aufgebaut
- Erste Risiken und Modernisierungsschwerpunkte identifiziert

## Optionale Screenshots
1. Geöffnete digitale Kundenakte als Nachweis für die Ausgangsanalyse
2. Erfolgreicher Zugriff auf die Admin-VM oder die vorbereitete Arbeitsumgebung

Die Projektstruktur und der Phasenüberblick sind im Text bereits ausreichend beschrieben und benötigen keinen zusätzlichen Screenshot mehr.

## Verweise
- [05_04_Digitale_Kundenakte.md](../../04_Recourcen_und_Referenzen/05_04_Digitale_Kundenakte.md)
- [00_01_Masterdokumentation.md](../../00_Projekt-Übersicht/00_01_Masterdokumentation.md)


