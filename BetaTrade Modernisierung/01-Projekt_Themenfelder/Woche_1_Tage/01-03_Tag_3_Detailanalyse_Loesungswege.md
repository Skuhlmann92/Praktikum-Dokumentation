---
datum: 2026-02-18
tags:
  - #architektur
  - #vlan
  - #entscheidungen
---
# Tag 3: Detailanalyse und Loesungswege

**Datum:** 18.02.2026  
**Rolle:** Planung / technische Analyse

## Ziel des Tages
Die technischen Zielbilder fuer Kaiserslautern und Mainz wurden verdichtet und in eine umsetzbare Reihenfolge gebracht.

## Durchgefuehrte Arbeitsschritte
1. VLAN- und Adressierungsbedarf fuer Kaiserslautern auf Abteilungsebene hergeleitet.
2. Zielbild fuer Mainz mit VPN, Active Directory, DNS, DHCP, Docker und Mail-Integration gegliedert.
3. Umsetzungsreihenfolge fuer die Kernsysteme fachlich abgestimmt.
4. Mehrere Loesungsansaetze fuer Sicherheit, Verfuegbarkeit und Kosten verglichen.
5. Offene technische Fragen fuer Kunde und Umsetzungsteam gesammelt.

## Entscheidung und Begruendung
**Ausgangslage:** Die Anforderungen des Kunden betrafen gleichzeitig Netzsegmentierung, Fernzugriff, zentrale Dienste und spaetere Security-Erweiterungen.

**Gewaehlte Option:** Es wurde eine Roadmap festgelegt, die zuerst Konnektivitaet und Basisdienste absichert und darauf aufbauend Verzeichnisdienst, Docker und LDAP-Integration einfuehrt.

**Warum diese Option:** AD, Mail-Integration und Security-Kontrollen sind nur stabil umsetzbar, wenn Routing, VPN, DHCP und DNS bereits sauber funktionieren.

**Nachweis:** Die beschriebenen Phasen- und Tagesprotokolle folgen in den Folgewochen genau dieser Reihenfolge.

## Ergebnis des Tages
- Adress- und VLAN-Konzept fuer Phase 1 vorbereitet
- technische Reihenfolge fuer Phase 2 begruendet
- Variantenvergleich fuer die Kundensicht dokumentiert
- offene Rueckfragen fuer die spaetere Umsetzung identifiziert

## Screenshot-Hinweise
1. Adress- oder VLAN-Plan fuer Kaiserslautern
2. Diagramm zur Roadmap fuer Mainz
3. Vergleichstabelle der Loesungsansaetze
4. Liste der offenen Punkte oder Freigabefragen

## Verweise
- [00-10_Phase_1_Kaiserslautern_Konzept.md](../../02_Phasen/Phase_1_Kaiserslautern/00-10_Phase_1_Kaiserslautern_Konzept.md)
- [00-11_Phase_2_Mainz_Konzept.md](../../02_Phasen/Phase_2_Mainz/00-11_Phase_2_Mainz_Konzept.md)
- [00-27_Learnings_und_Entscheidungen.md](../Analysen/00-27_Learnings_und_Entscheidungen.md)
