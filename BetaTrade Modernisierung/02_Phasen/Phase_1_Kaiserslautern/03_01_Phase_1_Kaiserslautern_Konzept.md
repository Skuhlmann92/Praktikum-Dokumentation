# 03 01 Phase 1 Kaiserslautern Konzept

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

- [03_01a_Netzplan_Kaiserslautern.md](03_01a_Netzplan_Kaiserslautern.md)
- [03_01b_VLAN_IP_Matrix.md](03_01b_VLAN_IP_Matrix.md)
- [02_01_Tag_1_Onboarding_Analyse.md](../../01-Projekt_Themenfelder/Woche_1_Tage/02_01_Tag_1_Onboarding_Analyse.md)
- [02_01_Tag_2_Projektstruktur_Risikoanalyse.md](../../01-Projekt_Themenfelder/Woche_1_Tage/02_01_Tag_2_Projektstruktur_Risikoanalyse.md)
- [02_01_Tag_3_Detailanalyse_Loesungswege.md](../../01-Projekt_Themenfelder/Woche_1_Tage/02_01_Tag_3_Detailanalyse_Loesungswege.md)
- [02_01_Tag_4_Finalisierung_Übergabe.md](../../01-Projekt_Themenfelder/Woche_1_Tage/02_01_Tag_4_Finalisierung_Übergabe.md)

## Ergebnis von Phase 1

Phase 1 ist keine Live-Umsetzung, sondern die abgeschlossene Planungs- und Vorbereitungsphase fuer Kaiserslautern. Die fachliche Basis fuer VLANs, Adressierung, Routing, DHCP-Relay und Uebergabe an die spaetere Umsetzung ist vorhanden.
