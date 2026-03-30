# 01 01 Analyse Abhaengigkeiten Phase 2

# Analyse der Abhängigkeiten (Phase 2: Zentrale Mainz)

**Datum:** 18.02.2026  
**Status:** ✅ Ergänzung zur Detailanalyse Tag 3  
**Ziel:** Klare Darstellung der Reihenfolge, Abhängigkeiten und kritischer Pfade in Phase 2

> **ABSTRACT:** Warum diese Analyse?
> Phase 2 ist die aufwendigste und risikoreichste Phase (Live-Migration, VPN, AD-Optimierung, Backup).  
> Viele Aufgaben haben starke Abhängigkeiten → Fehlreihenfolge kann zu Ausfällen, Lockouts oder Zeitverzügen führen.

## Hauptziele Phase 2 (Zusammenfassung)

- IP-Migration & Subnetz-Anpassung
- Active Directory Integration & Security Policies (GPOs)
- VPN-Termination (pfSense + Zertifikats-Auth)
- Cloud-Backup (MySQL Kundendatenbank)
- LDAP-Integration Mailserver
- Optimierung DHCP/DNS (zentral auf Admin-VM)

## Abhaengigkeits-Graph

![Phase-2 Roadmap und kritische Abhaengigkeiten](../../_assets/phase2_dependency_roadmap.png)

Die Grafik zeigt die kritischen Pfade der Mainzer Umsetzung in verdichteter Form:

- `IP Migration` und `Subnet DHCP Relay Configuration` bilden die technische Basis fuer die spaetere Zentralisierung.
- `AD Integration`, `GPO Configuration` und `LDAP/SSO path` haengen direkt an der sauberen Netz- und DNS-Erreichbarkeit.
- `VPN Setup`, `pfSense Certificate Configuration` und `Certificate Management` sichern den administrativen Fernzugriff ab.
- `Cloud Backup`, `Backup Jobs` und `Restore Test` laufen parallel, muessen aber vor dem eigentlichen Go-Live belastbar nachgewiesen sein.
- `LDAP Integration`, `Mailserver Connection` und `SSO Setup` liegen spaet im Ablauf und profitieren von bereits verifizierten Zertifikaten, DNS und AD.
