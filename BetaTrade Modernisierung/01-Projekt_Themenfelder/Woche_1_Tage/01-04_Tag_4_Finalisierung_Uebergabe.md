---
datum: 2026-02-19
tags:
  - #visualisierung
  - #handover
  - #roadmap
---
## Tag 4: Finalisierung & Übergabe-Vorbereitung

**Datum:** 19.02.2026  
**Status:** ✅ Dokumentation abgeschlossen | ✅ Visualisierung abgeschlossen

### Tagesziele (PM-4)

- [x] Lösungsansätze finalisieren und bewerten (Entscheidung für Lösung A gefallen)
- [x] Arbeitsplanung für die kommenden Wochen (Themenfeld 2 strukturiert)
- [x] Übergabe-Dokumentation erstellen (Finaler Entwurf)
- [x] Packet Tracer Datei (KL) sichten & detailliert analysieren
- [x] Organisationsstruktur visualisieren (Organigramm integriert)

***

## 1. Arbeitsplanung Netzwerkadministration (Update)

Das Netzwerk-Team erhält von uns folgendes **finales Paket** für die Umsetzung in Themenfeld 2:

- **VLAN-IDs & Namen:**  
  10 – Vertrieb  
  20 – IT  
  30 – HR  
  40 – VoIP  
  99 – Management

- **IP-Adressbereiche:** 10.13.X.0/24 (X = VLAN-ID)

- **DHCP-Strategie:** Zentrales Management über Admin-VM (10.8.13.2) via Relay-Agent auf allen SVIs

- **Hardware-Set:**  
  2× Catalyst 3650 (Core – Stacking + HSRP-Redundanz geplant)  
  3× Catalyst 2960 (Access)  
  1× pfSense (Mainz – VPN-Termination)
![Screenshot 2026-02-20 120006.png](../../_assets/Screenshot%202026-02-20%20120006.png)
***

## 2. Finale Übergabe-Dokumentation (Struktur)

### Projektüberblick
Modernisierung der BetaTrade-Infrastruktur. Kernstück ist der Ausbau Kaiserslauterns zum Regional-Hub mit Hochverfügbarkeits-Ansatz (HSRP, redundante Trunks).

### Priorisierte Anforderungen & Erkenntnisse

1. **Sicherheit**  
   Isolation der Abteilungen durch VLANs. Port-Security (802.1X) auf Access-Switches für IT-Bereich zwingend erforderlich.

2. **Konnektivität**  
   S2S-VPN (Site-to-Site) zwischen Mainz und KL. Zertifikatsbasierte Authentifizierung statt Passwort.

3. **Dienste**  
   DHCP-Relay muss auf den Core-Switches für alle Client-VLANs aktiv sein (`ip helper-address 10.8.13.2`).

→ Detaillierte Uebergabe: [00-42 Uebergabe-Protokoll](../../03_Uebergabe_und_Archiv/00-42_Uebergabe_Protokoll.md)

### Ausgearbeitete Lösung (A – Security-Fokus)
Wir implementieren **Lösung A**. Diese beinhaltet:

- VLAN-Segmentierung + Inter-VLAN-Routing nur über Core
- 802.1X Port-Security (IT-VLAN)
- pfSense OpenVPN mit Zertifikaten
- HSRP-Redundanz zwischen beiden Core-Switches
- QoS für VoIP (VLAN 40 priorisieren)
- Vorbereitung für IDS/IPS in Phase 3

***

## 3. Detaillierte Analyse Packet Tracer (Kaiserslautern_initial.pkt)

**Inventar-Check:**  
Die physische Topologie entspricht dem hierarchischen Design (Core → Distribution → Access).  
Neu: Es sind bereits IP-Telefone und PCs an den Access-Switches angeschlossen, jedoch ohne Link-Licht (Ports teilweise noch im `shutdown`).

**Konfigurations-Lücken (zu erledigen in TF-2):**

- **VTP/VLANs:** Noch keine VLAN-Datenbanken vorhanden. Empfehlung: VTP-Modus `transparent` nutzen.
- **STP (Spanning Tree):** Aufgrund redundanter Anbindung → `Rapid-PVST` konfigurieren, um Loops zu verhindern.
- **Layer 3:** Core-Switches laufen aktuell nur Layer 2. Erster Schritt: `ip routing` aktivieren.
- **VoIP:** Telefone benötigen Voice-VLAN (40) + PoE. Leistungsbilanz der Switches prüfen (PoE-Budget).

**Offene Fragen aus PT-Analyse:**

- Management-VLAN 99: Separates Subnetz außerhalb 10.13.X.X sinnvoll?
- Voice-VLAN: Inline-Power + Data-VLAN durchschleifen (PC hinter Telefon) korrekt unterstützt?


### Proof of Concept (Packet Tracer Lab)
Zur Validierung wurde eine initiale Konfiguration im Packet Tracer erstellt.

**VLAN-Datenbank (Switch):**
```cisco
vlan 10
 name SALES
vlan 20
 name IT
vlan 30
 name HR
vlan 40
 name VOIP
```

**OSPF-Routing (Core):**
```cisco
router ospf 1
 network 10.13.0.0 0.0.255.255 area 0
 passive-interface Vlan10
 passive-interface Vlan20
 passive-interface Vlan30
```
> **Ergebnis:** Pings zwischen VLAN 10 und VLAN 20 sind erfolgreich. DHCP-Relay wurde vorbereitet (`ip helper-address`).

***

## 4. Organisationsstruktur (Organigramm-Erkenntnisse)

Das Organigramm wurde erstellt und zeigt die strikte Trennung:

- **Zentrale Mainz:** Management & Kern-Server (AD, DB, pfSense).
    
- **Regional-Hub KL:** Operatives Geschäft (Vertrieb, HR) mit lokaler IT-Präsenz.
    
- **Infrastruktur-Diagramm:** Ein zweites Diagramm wurde erstellt, das die logische Zuordnung der Server in Mainz zu den neuen VLANs in KL visualisiert. ![Screenshot 2026-02-20 120542.png](../../_assets/Screenshot%202026-02-20%20120542.png)
***

## 5. Offene Fragen & Risikomanagement (Update Tag 4)

- **Risiko (VoIP VLAN 40):** PCs hinter Telefonen → korrekte Voice-VLAN-Zuweisung prüfen (Packet Tracer Test)
- **Risiko (Hardware/IOS):** Catalyst 3650 benötigen passendes IOS für Inter-VLAN-Routing + HSRP
- **Frage an Technik/Kunde:** Management-Zugriff (VLAN 99) → separates Subnetz (z. B. 10.99.99.0/24) oder innerhalb 10.13.99.0/24 belassen?

→ Verlinkte Dokumente:  
[00-42 Uebergabe-Protokoll](../../03_Uebergabe_und_Archiv/00-42_Uebergabe_Protokoll.md) | [00-41 Risiko-Register](../../03_Uebergabe_und_Archiv/00-41_Risiko_Register.md) | [00-10 Phase 1 Kaiserslautern Konzept](../../02_Phasen/Phase_1_Kaiserslautern/00-10_Phase_1_Kaiserslautern_Konzept.md)

**Letzte Aktualisierung:** 19.02.2026 – Projektassistenz  
**Nächster Schritt:** Übergabe-Meeting Themenfeld 2 (KW 8)
