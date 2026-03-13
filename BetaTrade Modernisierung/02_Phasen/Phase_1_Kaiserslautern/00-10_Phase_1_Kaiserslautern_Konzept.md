# Phase 1: Regional-Hub Kaiserslautern

**Zeitraum:** Woche 1  
**Status:** Abgeschlossen (Planungs- und Zielbildphase)  
**Fokus:** Segmentierung, Routing, DHCP-Relay, VoIP und technische Uebergabe an die Umsetzung

## Kernziele

- VLAN-Struktur fuer Vertrieb, IT, HR, VoIP und Management definieren
- Adressschema `10.13.X.0/24` festlegen
- Inter-VLAN-Routing ueber L3-Switches planen
- DHCP-Relay und zentrales Service-Modell dokumentieren
- Anforderungen fuer VoIP, QoS und HSRP-Redundanz vorbereiten

## Technischer Zielzustand

- Zwei Catalyst-3650-Switche als Core/L3-Ebene
- Mehrere Access-Switche fuer Abteilungsanschluesse
- Trunk-Uplinks zwischen Access- und Core-Ebene
- DHCP-Relay im Zielbild fuer die zentralen Dienste
- Voice-VLAN fuer Telefonie und QoS-Priorisierung

## Relevante Dokumente

- [00-10a Netzplan Kaiserslautern](00-10a_Netzplan_Kaiserslautern.md)
- [00-10b VLAN & IP Matrix](00-10b_VLAN_IP_Matrix.md)
- [01-01 Tag 1 Onboarding & Analyse](../../01-Projekt_Themenfelder/Woche_1_Tage/01-01_Tag_1_Onboarding_Analyse.md)
- [01-02 Tag 2 Projektstruktur & Risikoanalyse](../../01-Projekt_Themenfelder/Woche_1_Tage/01-02_Tag_2_Projektstruktur_Risikoanalyse.md)
- [01-03 Tag 3 Detailanalyse & Loesungswege](../../01-Projekt_Themenfelder/Woche_1_Tage/01-03_Tag_3_Detailanalyse_Loesungswege.md)
- [01-04 Tag 4 Finalisierung & Uebergabe](../../01-Projekt_Themenfelder/Woche_1_Tage/01-04_Tag_4_Finalisierung_Uebergabe.md)

## Ergebnis von Phase 1

Phase 1 ist keine Live-Umsetzung, sondern die abgeschlossene Planungs- und Vorbereitungsphase fuer Kaiserslautern. Die fachliche Basis fuer VLANs, Adressierung, Routing, DHCP-Relay und Uebergabe an die spaetere Umsetzung ist vorhanden.
