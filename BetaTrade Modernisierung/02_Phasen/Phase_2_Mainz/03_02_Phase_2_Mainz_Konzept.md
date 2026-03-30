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

- [05_04_Digitale_Kundenakte.md](../../04_Recourcen_und_Referenzen/05_04_Digitale_Kundenakte.md)
- [01_01_Analyse_Abhaengigkeiten_Phase_2.md](../../01-Projekt_Themenfelder/Analysen/01_01_Analyse_Abhaengigkeiten_Phase_2.md)
- [02_02_Tag_4_Connectivity_DHCP_Vorbereitung.md](../../01-Projekt_Themenfelder/Woche_2_Tage/02_02_Tag_4_Connectivity_DHCP_Vorbereitung.md)
- [02_02_Tag_5_VPN_Infrastruktur.md](../../01-Projekt_Themenfelder/Woche_2_Tage/02_02_Tag_5_VPN_Infrastruktur.md)
- [02_03_Tag_1-2_AD_Infrastruktur.md](../../01-Projekt_Themenfelder/Woche_3_Tage/02_03_Tag_1-2_AD_Infrastruktur.md)
- [02_04_Tag_1_Docker_SQL_Infrastruktur.md](../../01-Projekt_Themenfelder/Woche_4_Tage/02_04_Tag_1_Docker_SQL_Infrastruktur.md)
- [02_04_Tag_2_Mailcow_AD_Integration.md](../../01-Projekt_Themenfelder/Woche_4_Tage/02_04_Tag_2_Mailcow_AD_Integration.md)

## Ergebnis von Phase 2

Die fachliche und technische Umsetzung fuer Mainz ist dokumentiert und abgeschlossen. Offene Punkte betreffen vor allem Security-, Monitoring- und Audit-Themen der nachgelagerten Phase 3.


