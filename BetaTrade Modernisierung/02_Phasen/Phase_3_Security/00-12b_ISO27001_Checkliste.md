# ISO 27001 Checkliste – BetaTrade Modernisierung (Projekt-ID 13)

**Dokument-Typ:** Audit-Vorbereitungs-Checkliste  
**Gültig ab:** Februar 2026  
**Verantwortlich:** Projektassistenz / IT-Leitung BetaTrade AG  
**Ziel:** Sicherstellen, dass die Modernisierungsmaßnahmen wesentliche Anforderungen der ISO/IEC 27001:2022 erfüllen  
**Status:** 🗓️ In Vorbereitung – Phase 3 (Woche 6)

> **INFO:** Scope
> Gilt primär für die IT-Infrastruktur (Netzwerk, Server, Remote-Zugriff, Backup, Monitoring) der Standorte Mainz und Kaiserslautern.

## A.5 – Organisationskontrollen (Auszug relevant)

| Kontrolle | Anforderung (kurz)                             | Umsetzung im Projekt                              | Status     | Nachweis / Verantwortlich | Bemerkung / Offene Punkte                 |
| --------- | ---------------------------------------------- | ------------------------------------------------- | ---------- | ------------------------- | ----------------------------------------- |
| A.5.1     | Informationssicherheitsrichtlinien             | Sicherheitsrichtlinie erstellen (Entwurf Woche 5) | 🟡 Offen   | IT-Leitung                | Muss von GF genehmigt werden              |
| A.5.7     | Threat Intelligence                            | Monitoring + IDS (Phase 3)                        | 🟢 Geplant | Netzwerk-Team             | Feed-Integration (z. B. MISP) prüfen      |
| A.5.23    | Information security for use of cloud services | Cloud-Backup (AWS S3 / Azure?)                    | 🟡 Offen   | Netzwerk-Team             | Vertragsklauseln + Verschlüsselung prüfen |
| A.5.33    | Protection of records                          | Backup-Strategie + WORM-Option                    | 🟢 Geplant | Backup-Verantwortlicher   | 3-2-1-Regel + monatlicher Restore-Test    |

## A.8 – Technische Kontrollen (Kernbereich Projekt)

| Kontrolle | Anforderung (kurz)                                      | Umsetzung im Projekt                          | Status     | Nachweis / Verantwortlich          | Bemerkung / Offene Punkte                  |
|-----------|----------------------------------------------------------|-----------------------------------------------|------------|-------------------------------------|---------------------------------------------|
| A.8.1     | User endpoint devices                                    | 802.1X Port-Security (IT-VLAN)                | 🟢 Geplant | Netzwerk-Team                       | Rollout Woche 2–3                           |
| A.8.9     | Configuration management                                 | Zentrale Config-Backups (Core-Switches)       | 🟢 Geplant | Netzwerk-Team                       | Automatisierung via Ansible?                |
| A.8.16    | Monitoring activities                                    | Zentraler Syslog + IDS-Dashboard              | 🟢 Geplant | Monitoring-Team                     | Alerting per E-Mail/SMS Woche 6             |
| A.8.20    | Networks security                                        | VLAN-Segmentierung + Inter-VLAN-Routing       | ✅ Erledigt (Phase 1) | Netzwerk-Team                       | Dokumentation in [Netzplan Kaiserslautern](Netzplan%20Kaiserslautern.md) |
| A.8.23    | Web filtering                                            | pfSense Content-Filter (optional)             | 🟡 Offen   | IT-Leitung                          | Kunde entscheiden – Datenschutz!            |
| A.8.24    | Use of cryptography                                      | Zertifikatsbasiertes VPN (OpenVPN)            | 🟢 Geplant | Netzwerk-Team                       | Key-Management + Backup Woche 2             |
| A.8.25    | Secure development life cycle                            | Packet Tracer → Staging → Produktion          | ✅ Erledigt (Planung) | Projektassistenz                    | Change-Management-Prozess definieren        |
| A.8.28    | Secure coding                                            | Nicht relevant (keine Eigenentwicklung)       | N/A        | –                                   | –                                           |

## A.9 – Physische & Umgebungskontrollen (kurz)

- A.9.1: Physischer Zutrittsschutz (Serverraum Mainz) → Türschloss + Protokollierung prüfen
- A.9.4: Schutz vor Umwelteinflüssen → USV + Klimatisierung dokumentieren

## Nächste Schritte

- [ ] Mapping aller Projektmaßnahmen → ISO 27001 Controls (Woche 5)
- [ ] Lückenanalyse & Maßnahmenplan erstellen (Woche 6)
- [ ] Internes Pre-Audit durchführen (Ende Phase 3)
- [ ] Dokumentation für externes Audit vorbereiten (PDF-Export aus Obsidian)

> **NOTE:** Wichtig
> ISO 27001:2022 fordert **risikobasierten Ansatz** → siehe [Risiko-Register BetaTrade](Risiko-Register%20BetaTrade.md)

→ Verlinkte Dokumente:  
[Phase_3_Security](Phase_3_Security.md) | [Risiko-Register BetaTrade](Risiko-Register%20BetaTrade.md) | [Masterdokumentation](Masterdokumentation.md)