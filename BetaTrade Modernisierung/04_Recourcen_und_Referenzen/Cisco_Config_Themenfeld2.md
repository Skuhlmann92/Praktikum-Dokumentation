# 📂 Projekt: Labor ID 13 | Themenfeld 2 (Woche 2)

> [!abstract] Projekt-Überblick
> 
> - **Zeitraum:** Tag 1 - 3
>     
> - **Topologie:** Hierarchisches Design (Core - Distribution - Access)
>     
> - **Hardware:** Cisco 3650 (Core/Distro) & WS-CSwitch-PT (Access)
>     
> - **Routing-Protokoll:** OSPF & Statische Routen
>     

---

## 🏗️ Tag 1: Core-Ebene & Transit-Routing

**Ziel:** Aufbau des Netzwerkrückgrats und Konfiguration der Punkt-zu-Punkt-Verbindungen.

### Core-Switch (3650)

Der Core agiert als reiner Layer-3-Knoten. Hier werden die Abteilungen über separate Transit-Netze angebunden.

Bash

```
enable
configure terminal
ip routing

! --- Routed Interfaces zu den Distro-Switches ---
interface GigabitEthernet1/0/2
 description Link-to-Sales
 no switchport
 ip address 10.0.0.2 255.255.255.252
exit

interface GigabitEthernet1/0/3
 description Link-to-IT
 no switchport
 ip address 10.0.1.2 255.255.255.252
exit

interface GigabitEthernet1/0/4
 description Link-to-HR
 no switchport
 ip address 10.0.2.2 255.255.255.252
exit

! --- Dynamisches Routing ---
router ospf 1
 network 10.0.0.0 0.0.255.255 area 0
exit

! --- Statische Rückrouten (WICHTIG für DHCP-Relay) ---
ip route 10.13.10.0 255.255.255.0 10.0.0.1   # Sales Data
ip route 10.13.20.0 255.255.255.0 10.0.1.1   # IT Data
ip route 10.13.30.0 255.255.255.0 10.0.2.1   # HR Data
write
```

---

## ⚡ Tag 2: Distribution-Layer & VLAN-Gateways

**Ziel:** Konfiguration der SVIs (Gateways) und Aktivierung des DHCP-Relay-Agents (`ip helper`).

### Beispiel: HR-Distribution (3650)

Bash

```
enable
configure terminal
ip routing

! --- VLAN Definitionen ---
vlan 30
 name HR-Data
vlan 130
 name HR-Voice
exit

! --- Gateways (SVI) ---
interface vlan 30
 ip address 10.13.30.1 255.255.255.0
 ip helper-address 192.168.50.100
 no shutdown
exit

interface vlan 130
 ip address 192.168.40.129 255.255.255.192
 ip helper-address 192.168.50.100
 no shutdown
exit

! --- Downlinks (Trunk) ---
interface range GigabitEthernet1/0/1 - 2
 switchport
 switchport mode trunk
 no shutdown
exit

! --- Uplink (Routed) ---
interface GigabitEthernet1/0/3
 no switchport
 ip address 10.0.2.1 255.255.255.252
exit
```

---

## 💻 Tag 3: Access-Layer & Endgeräte-Anbindung

**Ziel:** Konfiguration der User-Ports am modularen Switch und Einrichtung von Spanning-Tree Portfast.

### Beispiel: HR-Access (WS-CSwitch-PT)

> [!info] Besonderheit Hardware Da es sich um modulare Switches handelt, werden die Ports als `GigabitEthernet X/1` (Slot/Port) angesprochen.

Bash

```
enable
configure terminal

vlan 30
vlan 130
exit

! --- Endgeräte Konfiguration ---
interface range GigabitEthernet0/1, GigabitEthernet1/1, GigabitEthernet2/1, GigabitEthernet3/1, GigabitEthernet4/1, GigabitEthernet5/1
 switchport mode access
 switchport access vlan 30
 switchport voice vlan 130
 spanning-tree portfast
exit

! --- Uplink zum Distro ---
interface range GigabitEthernet8/1, GigabitEthernet9/1
 switchport mode trunk
 no shutdown
exit
write
```
