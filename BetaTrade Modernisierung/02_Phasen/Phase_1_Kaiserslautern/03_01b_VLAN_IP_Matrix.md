# 03 01b VLAN IP Matrix

# VLAN & IP-Matrix – Regional-Hub Kaiserslautern (Projekt-ID 13)

**Stand:** 20.02.2026 (Ende Planungsphase)  
**Status:** ✅ Finalisiert & an Netzwerk-Team übergeben  
**Subnetz-Basis:** 10.13.0.0/16 (pro VLAN ein /24-Netz)  
**DHCP-Server:** zentral auf Admin-VM in Mainz (10.8.13.2)  
**DHCP-Relay:** `ip helper-address 10.8.13.2` auf jedem SVI  
**Redundanz:** HSRP zwischen CoreSwitch0 & CoreSwitch1 (virtuelle IP = Gateway)

## VLAN- & IP-Matrix

| VLAN-ID | Name       | Subnetz       | Gateway (SVI / HSRP) | DHCP-Bereich | Nutzung / Bemerkung                                | Priorität | Status    |
| ------- | ---------- | ------------- | -------------------- | ------------ | -------------------------------------------------- | --------- | --------- |
| 10      | Vertrieb   | 10.13.10.0/24 | 10.13.10.1           | .100 – .200  | Sales-Workstations, Notebooks, Drucker             | Hoch      | ✅ Geplant |
| 20      | IT         | 10.13.20.0/24 | 10.13.20.1           | .100 – .200  | Admin-PCs, Server-Zugriff, Management              | Sehr hoch | ✅ Geplant |
| 30      | HR         | 10.13.30.0/24 | 10.13.30.1           | .100 – .200  | Personalabteilung, sensible Personaldaten          | Hoch      | ✅ Geplant |
| 40      | VoIP       | 10.13.40.0/24 | 10.13.40.1           | .100 – .200  | IP-Telefone, VoIP-Server (QoS-Priorisierung)       | Hoch      | ✅ Geplant |
| 99      | Management | 10.13.99.0/24 | 10.13.99.1           | .10 – .50    | Switches, Router, Server-Management, Admin-Zugriff | Sehr hoch | ✅ Geplant |

## Zusätzliche Konfigurations-Empfehlungen

- **Voice-VLAN auf Access-Ports:**  
  `switchport voice vlan 40` + `switchport access vlan X` (X = Data-VLAN)  
  PCs hinter Telefonen durchschleifen (Inline-Power)

- **Port-Security (besonders VLAN 20 IT):**  
  Empfohlen: `switchport port-security maximum 2` + `switchport port-security violation restrict`

- **QoS für VoIP (VLAN 40):**  
  Priorisierung auf Core- & Access-Switches (CoS 5 / DSCP EF)

- **Management-Zugriff (VLAN 99):**  
  Option A: Innerhalb 10.13.99.0/24  
  Option B: Separates Subnetz (z. B. 10.99.99.0/24) – höhere Sicherheit, aber mehr Routing-Aufwand

## Konfigurations-Snippets (Cisco CLI – Beispiele)

### Beispiel Core-Switch (SVI + HSRP + Relay)

```cisco
vlan 10
 name Vertrieb
!
interface Vlan10
 ip address 10.13.10.2 255.255.255.0
 standby 10 ip 10.13.10.1
 standby 10 priority 110
 standby 10 preempt
 ip helper-address 10.8.13.2
!
```
