# Phase 2: Zentrale Mainz Modernisierung

**Zeitraum:** Woche 2 bis 4  
**Status:** Abgeschlossen  
**Fokus:** VPN, DHCP, DNS, Active Directory, Docker, SQL und LDAP-Integration

## Kernziele

- pfSense als zentrales Gateway fuer Admin-Zugriff und VPN aufbauen
- DHCP und DNS auf Windows Server 2025 konsolidieren
- Active Directory `net13.beta` strukturieren und haerten
- Dockerisierte SQL-Umgebung bereitstellen und validieren
- Mailcow an das AD anbinden

## Umgesetzte Bausteine

- pfSense-Routing, statische Routen und WAN/LAN-Zugriff eingerichtet
- OpenVPN mit Zertifikaten und DNS-Routing umgesetzt
- DHCP- und DNS-Infrastruktur auf `192.168.13.10` dokumentiert
- AD mit OUs, Gruppen, User-Import und GPO-Haertung aufgebaut
- Docker-/MySQL-Umgebung fuer `betatrade_db` verifiziert
- Mailcow mit LDAP/LDAPS gegen AD integriert

## Relevante Dokumente

- [00-33 Digitale Kundenakte](../../04_Recourcen_und_Referenzen/00-33_Digitale_Kundenakte.md)
- [00-20 Analyse Abhaengigkeiten Phase 2](../../01-Projekt_Themenfelder/Analysen/00-20_Analyse_Abhaengigkeiten_Phase_2.md)
- [02-04 Connectivity & DHCP Vorbereitung](../../01-Projekt_Themenfelder/Woche_2_Tage/02-04_Woche_2_Tag_4_Connectivity_DHCP_Vorbereitung.md)
- [02-08 VPN Infrastruktur](../../01-Projekt_Themenfelder/Woche_2_Tage/02-08_Woche_2_Tag_5_VPN_Infrastruktur.md)
- [03-01 AD Infrastruktur](../../01-Projekt_Themenfelder/Woche_3_Tage/03-01_Woche_3_Tag_1-2_AD_Infrastruktur.md)
- [04-01 Docker & SQL Infrastruktur](../../01-Projekt_Themenfelder/Woche_4_Tage/04-01_Woche_4_Tag_1_Docker_SQL_Infrastruktur.md)
- [04-02 Mailcow AD Integration](../../01-Projekt_Themenfelder/Woche_4_Tage/04-02_Woche_4_Tag_2_Mailcow_AD_Integration.md)

## Ergebnis von Phase 2

Die fachliche und technische Umsetzung fuer Mainz ist dokumentiert und abgeschlossen. Offene Punkte betreffen vor allem Security-, Monitoring- und Audit-Themen der nachgelagerten Phase 3.
