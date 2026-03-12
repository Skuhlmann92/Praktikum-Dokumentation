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

## Abhängigkeits-Graph ![Screenshot 2026-02-20 121823 1.png](Screenshot%202026-02-20%20121823%201.png)
