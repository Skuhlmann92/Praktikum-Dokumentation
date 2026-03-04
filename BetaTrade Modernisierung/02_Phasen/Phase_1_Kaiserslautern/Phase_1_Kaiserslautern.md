# 📍 Phase 1: Regional-Hub Kaiserslautern
**Zeitraum:** Woche 1 | **Status:** 🔄 In Bearbeitung

## 🎯 Hauptziele
* **Netzwerk-Segmentierung:** Einrichtung von 3 VLANs (Vertrieb, IT, HR).
* **IP-Adresskonzept:** Strukturierte Vergabe im Subnetz `10.13.X.X`.
* **Connectivity:** DHCP-Relay Konfiguration zur zentralen Admin-VM.
* **Telefonie:** Implementierung einer abteilungsübergreifenden VoIP-Lösung.

## 🏗️ Infrastruktur-Details
* **Hardware:** 2x Core-Switches (L3), 3x Access-Switches.
* **Gateways:** SVIs auf den Core-Switches mit HSRP-Redundanz.
* **Services:** DHCP via Relay-Agent (`10.8.13.2`).

## 📑 Verknüpfte Berichte
* [[2026-02-16_Tag_1]] - Initiales Setup & VLAN-Basis.
* [[2026-02-17_Tag_2]] - GANTT & Risikoanalyse.

---
## 🛠️ Technischer Nachweis (CLI)
> [!TIP] Wichtigster Befehl dieser Phase
> `ip helper-address 10.8.13.2` auf den VLAN-Interfaces.

# 📍 Phase 1: Regional-Hub Kaiserslautern
**Status:** 🔄 In Arbeit (Woche 1)
**Fokus:** LAN-Infrastruktur, Segmentierung & Dienste

## 🎯 Kernziele
- [ ] **VLAN-Struktur:** Aufbau der Netze für Vertrieb (10), IT (20) und HR (30).
- [ ] **IP-Adresskonzept:** Implementierung des Schemas `10.13.X.0/24`.
- [ ] **Routing:** Inter-VLAN Routing auf den Core-Switches aktivieren.
- [ ] **DHCP-Relay:** Weiterleitung der Anfragen an die Admin-VM (`10.8.13.2`).
- [ ] **VoIP:** Einrichtung der IP-Telefonie für alle Abteilungen.

## 🏗️ Topologie-Details
* **Core-Layer:** 2x Catalyst 3650 (Redundant).
* **Access-Layer:** 3x Switches (Sales, IT, HR).
* **Uplinks:** 802.1Q Trunks zwischen allen Switchen.

## 🔗 Relevante Berichte
* [[2026-02-16_Tag_1|Tag 1: Initiales VLAN-Setup & Troubleshooting]]
* [[2026-02-17_Tag_2|Tag 2: GANTT-Planung & Meilensteine]]

---
> [!INFO] Status-Quo
> Die physische Verkabelung im Packet Tracer steht. Aktueller Fokus liegt auf der korrekten Trunk-Konfiguration und dem IP-Helper.