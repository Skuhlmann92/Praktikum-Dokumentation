# Packet Tracer Analyse – Kaiserslautern_initial.pkt

**Datum der Sichtung:** 19.02.2026 (Tag 4)  
**Datei:** Kaiserslautern_initial.pkt  
**Status:** ✅ Analysiert – Lücken dokumentiert

### Inventar-Check

- Topologie: Hierarchisch (Core → Access) – entspricht Plan
- Vorhanden: 2× Core (3650), 3× Access (2960), IP-Telefone & PCs angeschlossen
- Auffällig: Viele Ports im `shutdown` → keine Link-Lichter

### Konfigurations-Lücken (Priorität für TF-2)

1. **VLANs & VTP**  
   - Keine VLANs definiert  
   - Empfehlung: `vtp mode transparent` + manuelle VLAN-Erstellung

2. **Spanning Tree**  
   - Kein STP aktiv → bei redundanten Links droht Loop  
   - Muss: `spanning-tree mode rapid-pvst`

3. **Layer-3-Fähigkeit**  
   - Core-Switches nur L2 → `ip routing` fehlt  
   - SVIs (z. B. `interface vlan 10`, `ip address 10.13.10.1 255.255.255.0`)

4. **DHCP-Relay**  
   - `ip helper-address 10.8.13.2` auf allen VLAN-SVIs fehlt

5. **VoIP / Voice-VLAN**  
   - VLAN 40 muss als Voice-VLAN konfiguriert werden  
   - `switchport voice vlan 40` auf Access-Ports  
   - PoE-Budget prüfen (C2960 hat oft Limit)

6. **Sicherheit**  
   - Port-Security / 802.1X noch nicht vorhanden  
   - Empfehlung: Erst nach VLANs & Routing

### Offene Fragen

- Management-VLAN 99: 10.13.99.0/24 oder separates Subnetz?
- PoE-Budget ausreichend für alle Telefone + PCs?
- IOS-Version der 3650 unterstützt HSRP + Rapid-PVST?

→ Nächster Schritt: Alle Lücken in TF-2 schließen & Test-Konfiguration erstellen  
→ Verlinkung: [[2026-02-19_Tag_4]] | [[Phase_1_Kaiserslautern]]