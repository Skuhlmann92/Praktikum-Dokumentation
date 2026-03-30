# 📑 Übergabe-Protokoll: Planung -> Administration -> Betrieb
**Projekt:** BetaTrade Modernisierung | **ID:** 13

## 1. Projekt-Status (Stand 12.03.2026)
* **Woche 1 (Planung):** ✅ Abgeschlossen.
* **Woche 2-4 (Umsetzung):** ✅ Abgeschlossen (Netzwerk, AD, Docker, SQL, LDAP).
* **Woche 5+ (Abschluss):** 🗓️ Übergabe an Phase 3 (Security-Audit & Monitoring).

## 2. Implementierte Infrastruktur (Zusammenfassung)

### Netzwerk (Kaiserslautern & Mainz)
* **VLAN-Segmentierung:** Vollständig umgesetzt (10, 20, 30, 40, 99).
* **L3-Routing:** OSPF-Routing zwischen Standorten aktiv.
* **VPN-Konnektivität:** pfSense S2S-VPN mit Zertifikats-Authentifizierung stabil.
* **DHCP/DNS:** Zentrales Management via Windows Server 2025 (`192.168.13.10`).

### Systeme & Applikationen
* **Active Directory:** `net13.beta` Domäne mit GPO-Härtung (RDP-Einschränkung, Firewall).
* **Docker-Services:** `betatrade-db` (MySQL/MariaDB) in versionierter Umgebung aktiv.
* **Mail-Integration:** Mailcow via LDAPS (Port 636) an AD angebunden.
* **Troubleshooting:** SSH-Optimierung (Keep-Alive, Host-Key Fixes) durchgeführt.

## 3. Übergabepunkte für Phase 3 (Security)
* **Firewall-Regeln:** pfSense-Regeln basieren auf "Least Privilege" (Aliase für Admin-Zugriff).
* **LDAP-Verschlüsselung:** LDAPS ist zwingend; "Ignore TLS" in Mailcow nur für Test-Phase (Self-Signed).
* **Backups:** MySQL-Dumps werden via Cron/Script erstellt (`backup_day3.sql`).

## 4. Offene Dokumentation & Referenzen
* [00_01_Masterdokumentation.md](../00_Projekt-Übersicht/00_01_Masterdokumentation.md)
* [04_02_Risiko_Register.md](04_02_Risiko_Register.md)
* [04_01_Passwoerter_und_Logins.md](04_01_Passwoerter_und_Logins.md)

> **HINWEIS:** Alle technischen Passwoerter wurden in [04_01_Passwoerter_und_Logins.md](04_01_Passwoerter_und_Logins.md) dokumentiert. Die Infrastruktur ist fuer das finale Security-Audit vorbereitet.


