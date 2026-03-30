# 04 02 Risiko Register

# Risiko-Register BetaTrade Modernisierung (Projekt-ID 13)

**Projekt:** IT-Infrastruktur Modernisierung BetaTrade AG  
**Stand:** 20.02.2026 (Ende Planungsphase Themenfeld 1)  
**Verantwortlich:** Projektassistenz AlphaTech GmbH  
**Status:** ✅ Erfasst & priorisiert – laufende Überwachung in Themenfeld 2

> **ABSTRACT:** Zweck dieses Registers
> Systematische Erfassung, Bewertung und Steuerung aller identifizierten Risiken über alle Projektphasen.  
> Aktualisierung: wöchentlich in Themenfeld 2, monatlich danach.

## Risiko-Matrix (Bewertungsskala)

| Wahrscheinlichkeit | Niedrig (1) | Mittel (2) | Hoch (3) |
|--------------------|-------------|------------|----------|
| **Auswirkung**     |             |            |          |
| Niedrig (1)        | 1           | 2          | 3        |
| Mittel (2)         | 2           | 4          | 6        |
| Hoch (3)           | 3           | 6          | 9        |

**Priorität**:  
- 7–9 → **Kritisch** (sofortige Maßnahmen)  
- 4–6 → **Hoch** (innerhalb 1–2 Wochen)  
- 1–3 → **Mittel/Niedrig** (beobachten)

## Risiko-Übersicht

| # | Risiko-Beschreibung                                                                 | Phase betroffen | Wahrscheinlichkeit | Auswirkung | Priorität (Punkte) | Status     | Verantwortlich | Nächste Maßnahme / Deadline |
|---|-------------------------------------------------------------------------------------|-----------------|--------------------|------------|---------------------|------------|----------------|------------------------------|
| 1 | DHCP-Migration führt zu Adresskonflikten oder temporärem Ausfall (z. B. Relay-Fehler) | Phase 1 & 2     | Hoch (3)           | Mittel (2) | Hoch (6)            | 🟡 Offen   | Netzwerk-Team  | Parallelbetrieb + Test-Scope Woche 1 |
| 2 | VPN-Konfiguration (pfSense + Zertifikate) sperrt Admin-Zugriff aus (Lockout)       | Phase 2         | Mittel (2)         | Hoch (3)   | Hoch (6)            | 🟡 Offen   | Netzwerk-Team  | Fallback-Local-Admin + Backup-Strategie Woche 2 |
| 3 | Fehlende / falsche STP-Konfiguration → Broadcast-Sturm / Netz-Ausfall              | Phase 1         | Mittel (2)         | Hoch (3)   | Hoch (6)            | 🟡 Offen   | Netzwerk-Team  | Rapid-PVST + BPDU Guard aktivieren – Test in PT Woche 1 |
| 4 | VoIP-Qualität unzureichend (Jitter, Paketverlust, Latenz)                           | Phase 1         | Mittel (2)         | Mittel (2) | Mittel (4)          | 🟡 Offen   | Netzwerk-Team + Kunde | QoS-Policy + Voice-VLAN-Priorisierung – Klärung Hardware Woche 1 |
| 5 | Zeitverzug bei Zertifikatsausstellung / -Management (externer CA)                   | Phase 2         | Mittel (2)         | Mittel (2) | Mittel (4)          | 🟡 Offen   | Netzwerk-Team  | Frühe Beantragung + interne Test-CA bis Produktion – Woche 2 |
| 6 | Cloud-Backup nicht wiederherstellbar / Restore-Test fehlschlägt                     | Phase 2         | Niedrig (1)        | Hoch (3)   | Mittel (3)          | 🟢 Beobachten | Netzwerk-Team | Monatlicher Restore-Test + 3-2-1-Regel – erster Test Woche 4 |
| 7 | Benutzerakzeptanz-Probleme / Widerstand gegen Umstellung (z. B. neue VPN-Auth)      | Phase 2 & 3     | Mittel (2)         | Mittel (2) | Mittel (4)          | 🟡 Offen   | Projektleitung | Kommunikationsplan + Pilot-Gruppe – Info-Veranstaltung Woche 3 |
| 8 | HSRP-Failover funktioniert nicht (Konfig-Fehler / Hardware-Defekt)                  | Phase 1 & 2     | Niedrig (1)        | Hoch (3)   | Mittel (3)          | 🟢 Beobachten | Netzwerk-Team  | Failover-Test in Packet Tracer + real Woche 2 |

## Top-3 Risiken (Stand 20.02.2026 – höchste Priorität)

> **WARNING:** Kritische Risiken – sofort überwachen
> 1. **DHCP-Migration** (P=6) → Höchstes Risiko durch Live-Betrieb in Mainz  
> 2. **VPN-Lockout** (P=6) → Blockiert gesamte Fernwartung  
> 3. **STP / Broadcast-Sturm** (P=6) → Kann komplette Filiale lahmlegen

## Maßnahmen-Status & Kontrolle

- [x] Risiken in Tag 2 & Tag 5 identifiziert und priorisiert
- [ ] Risiko-Owner für jede Phase zuweisen (Woche 1 Themenfeld 2)
- [ ] Risiko-Tracking-Tabelle in gemeinsames Tool (z. B. Excel / Obsidian-Tabelle / Jira) überführen
- [ ] Wöchentliches Review-Meeting ab Woche 2 (15 min)

> **TIP:** Nächste Schritte
> - Woche 1: Alle Hoch-Prioritäts-Maßnahmen umsetzen (Parallelbetrieb DHCP, STP aktivieren, Fallback-VPN)
> - Woche 2: Erste Tests (Packet Tracer → real) & Update des Registers

→ Verlinkte Dokumente:  
[02_01_Tag_5_Puffer_Reflexion.md](../01-Projekt_Themenfelder/Woche_1_Tage/02_01_Tag_5_Puffer_Reflexion.md) | [04_03_Uebergabe_Protokoll.md](04_03_Uebergabe_Protokoll.md) | [00_01_Masterdokumentation.md](../00_Projekt-Übersicht/00_01_Masterdokumentation.md)

**Letzte Aktualisierung:** 20.02.2026 – Projektassistenz  
**Nächste Überprüfung:** 27.02.2026 (Ende Woche 1 Umsetzung)


