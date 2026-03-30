
**Datum:** 18.02.2026  
**Rolle:** Planung / technische Analyse

## Ziel des Tages
Die technischen Zielbilder für Kaiserslautern und Mainz wurden verdichtet und in eine umsetzbare Reihenfolge gebracht.

## Durchgeführte Arbeitsschritte
1. VLAN- und Adressierungsbedarf für Kaiserslautern auf Abteilungsebene hergeleitet.
2. Zielbild für Mainz mit VPN, Active Directory, DNS, DHCP, Docker und Mail-Integration gegliedert.
3. Umsetzungsreihenfolge für die Kernsysteme fachlich abgestimmt.
4. Mehrere Lösungsansätze für Sicherheit, Verfügbarkeit und Kosten verglichen.
5. Offene technische Fragen für Kunde und Umsetzungsteam gesammelt.

## Lösung der Tagesaufgaben

### Gruppenarbeit

#### 1. Check-in und Erfahrungsaustausch
- Die am Vortag identifizierten Risiken wurden zusammengeführt und auf gemeinsame Schwerpunkte reduziert.
- Besonders häufig bestätigt wurden:
  DHCP-Migration,
  VPN-Zugriffsverlust,
  fehlerhafte Netzsegmentierung,
  VoIP-Qualität,
  Abhängigkeiten bei zentralen Diensten.
- Die Einschätzung der Projektphasen wurde validiert:
  Planung ist kompakt,
  die eigentliche technische Komplexität liegt in der Umsetzung und Integration.

#### 2. Anforderungen priorisieren
- Die Herausforderungen der Kundenakte wurden fachlich priorisiert:
  1. sichere Netzsegmentierung,
  2. stabiler externer Zugriff,
  3. saubere zentrale Dienste,
  4. Verzeichnisdienst und Identitätsmanagement,
  5. Backup und Security-Erweiterungen.
- Diese Reihenfolge wurde als sinnvolle Arbeitsgrundlage für die kommenden Wochen festgelegt.

### Einzelarbeit

#### 1. Detailanalyse Phase 1: Filiale Kaiserslautern
- Die Anforderung `3 Abteilungen mit Segmentierung` wurde konkret als getrennte Broadcast-Domänen für Vertrieb, IT und HR interpretiert.
- Darauf aufbauend wurde ein VLAN-Konzept mit zusätzlichen Infrastruktur-VLANs für Voice und Management vorbereitet.
- Erste IP-Überlegungen wurden am Subnetzprinzip `10.13.X.0/24` ausgerichtet:
  z. B. ein eigenes /24 je VLAN für klare Trennung, einfache Dokumentation und spätere Erweiterbarkeit.
- DHCP-Relay wurde als notwendiger Baustein bewertet, wenn Dienste zentral statt lokal bereitgestellt werden.

##### Konkreter Vorschlag für den IP-Adressplan

| Bereich | VLAN | Netz | Gateway | DHCP-Bereich |
|---|---:|---|---|---|
| Vertrieb | 10 | 10.13.10.0/24 | 10.13.10.1 | 10.13.10.100-200 |
| IT | 20 | 10.13.20.0/24 | 10.13.20.1 | 10.13.20.100-200 |
| HR | 30 | 10.13.30.0/24 | 10.13.30.1 | 10.13.30.100-200 |
| VoIP | 40 | 10.13.40.0/24 | 10.13.40.1 | 10.13.40.100-200 |
| Management | 99 | 10.13.99.0/24 | 10.13.99.1 | statisch / reserviert |

#### 2. Detailanalyse Phase 2: Zentrale Mainz
- Die Aufgaben wurden in fachlich sinnvolle Reihenfolge gebracht:
  1. Konnektivität und Routing,
  2. VPN-Zugang,
  3. DHCP und DNS,
  4. Active Directory,
  5. Docker- und Datenbankdienste,
  6. LDAP-/Mail-Integration,
  7. Backup und nachgelagerte Security-Bausteine.
- Sicherheitsrelevante Abhängigkeiten wurden dokumentiert:
  VPN muss vor Fernwartung stabil sein,
  DNS/DHCP müssen vor AD sauber arbeiten,
  AD muss vor LDAP-Anbindung verfügbar sein,
  Monitoring und Compliance bauen auf einer funktionierenden Infrastruktur auf.

#### 3. Erste Lösungsrichtungen skizzieren
- Für Phase 1 wurden als Lösungsrichtungen definiert:
  VLAN-Trennung pro Fachbereich,
  L3-Routing über Core-Switche,
  zentrales DHCP-Service-Modell mit Relay.
- Für Phase 2 wurden als Lösungsrichtungen definiert:
  pfSense als sicheres Gateway mit VPN,
  Windows Server 2025 für DHCP/DNS/AD,
  Docker für flexible Applikationsdienste,
  LDAP/LDAPS für zentrale Authentisierung.
- Die Ansätze wurden jeweils gegen Kundennutzen, Machbarkeit und Aufwand abgewogen.

##### Zusätzliche offene technische Fragen
- Sind in Kaiserslautern bereits IP-Telefone vorhanden oder wird zunächst mit Softphones geplant?
- Reicht die pfSense-Kapazität in Mainz für die erwarteten gleichzeitigen VPN-Verbindungen und späteren Zusatzverkehr aus?

### Abschluss des Tages
- Die Detailanalyse für beide Phasen ist strukturiert dokumentiert.
- Technische Abhängigkeiten sind festgehalten und können in die Übergabe übernommen werden.
- Die Lösungsansätze sind für Tag 4 diskussions- und übergabefähig vorbereitet.

## Entscheidung und Begründung
**Ausgangslage:** Die Anforderungen des Kunden betrafen gleichzeitig Netzsegmentierung, Fernzugriff, zentrale Dienste und spätere Security-Erweiterungen.

**Gewählte Option:** Es wurde eine Roadmap festgelegt, die zuerst Konnektivität und Basisdienste absichert und darauf aufbauend Verzeichnisdienst, Docker und LDAP-Integration einführt.

**Warum diese Option:** AD, Mail-Integration und Security-Kontrollen sind nur stabil umsetzbar, wenn Routing, VPN, DHCP und DNS bereits sauber funktionieren.

**Nachweis:** Die beschriebenen Phasen- und Tagesprotokolle folgen in den Folgewochen genau dieser Reihenfolge.

## Ergebnis des Tages
- Adress- und VLAN-Konzept für Phase 1 vorbereitet
- technische Reihenfolge für Phase 2 begründet
- Variantenvergleich für die Kundensicht dokumentiert
- offene Rückfragen für die spätere Umsetzung identifiziert

## Optionale Screenshots
1. Packet-Tracer-Topologie oder ein bestätigender Netzplan für Kaiserslautern
2. Falls vorhanden: vorhandene Roadmap-Grafik für Phase 2

Der IP-Adressplan, die Lösungsansätze und die offenen Fragen sind bereits direkt im Dokument enthalten und benötigen keinen separaten Screenshot mehr.

## Verweise
- [03_01_Phase_1_Kaiserslautern_Konzept.md](../../02_Phasen/Phase_1_Kaiserslautern/03_01_Phase_1_Kaiserslautern_Konzept.md)
- [03_02_Phase_2_Mainz_Konzept.md](../../02_Phasen/Phase_2_Mainz/03_02_Phase_2_Mainz_Konzept.md)

