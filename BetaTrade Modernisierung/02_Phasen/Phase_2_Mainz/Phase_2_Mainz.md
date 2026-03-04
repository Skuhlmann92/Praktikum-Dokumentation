# 🏢 Phase 2: Zentrale Mainz Modernisierung
**Zeitraum:** Woche 2 - 5 | **Status:** 📅 Geplant

## 🎯 Hauptziele
* **VPN-Termination:** Einrichtung eines pfSense-Gateways für sichere Fernwartung.
* **Zentrale Dienste:** Optimierung von DHCP, DNS und Active Directory (AD).
* **Backup-Strategie:** Integration von Cloud-Storage für die Datensicherung.
* **Identity Management:** LDAP-Integration für den Mailserver.

## 🔒 Security-Fokus
* VPN-Zugang für Dienstleister (Weg von reiner Passwort-Auth).
* AD Security Policies & Gruppenrichtlinien.

## 📑 Relevante Dokumente
* [[Digitale_Kundenakte]]
* [[VPN_Konfigurationsguide]]

---
## 📝 Planungs-Notizen
Die Modernisierung in Mainz ist zeitintensiv (3,5 Wochen), da hier Live-Dienste (Datenbanken) migriert und gesichert werden müssen.

# 🏢 Phase 2: Zentrale Mainz Modernisierung
**Status:** 📅 Geplant (Woche 2 - 5,5)
**Fokus:** Server-Infrastruktur, VPN & Cloud

## 🎯 Kernziele
- [ ] **VPN-Gateway:** Migration von Passwort-Auth zu Zertifikats-basiertem VPN (pfSense).
- [ ] **Active Directory:** Optimierung der Group Policies (GPOs) und Security-Level.
- [ ] **Mailserver:** Integration von LDAP für die Benutzerauthentifizierung.
- [ ] **Cloud-Backup:** Automatisierte Sicherung der Kundendatenbank (MySQL).

## 🔒 Sicherheits-Fokus
- Fernwartungszugang für AlphaTech absichern.
- Trennung von Management- und Produktivnetz.

## 🔗 Ressourcen
* [[Digitale_Kundenakte|Zusammenfassung Digitale Kundenakte]]
* [[Thema1_Tag_3|Analyse der Abhängigkeiten (Phase 2)]]

---
> [!WARNING] Herausforderung
> Phase 2 ist mit 3,5 Wochen die zeitintensivste Phase. Die Abhängigkeiten zwischen AD, DNS und dem Backup-System müssen strikt eingehalten werden.