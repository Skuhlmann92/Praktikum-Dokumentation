---
datum: 2026-02-23
tags:
  - #umsetzung
  - #packet-tracer
  - #troubleshooting
  - #cisco
---
# 📂 Projekt: Labor ID 13 | Themenfeld 2 (Woche 2)

> **ABSTRACT:** Projekt-Überblick
> 
> - **Zeitraum:** Tag 1 - 3
>     
> - **Topologie:** Hierarchisches Design (Core - Distribution - Access)
>     
> - **Hardware:** Cisco 3650 (Core/Distro) & WS-CSwitch-PT (Access)
>     
> - **Routing-Protokoll:** OSPF & Statische Routen
>     

***

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

***

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

***

## 💻 Tag 3: Access-Layer & Endgeräte-Anbindung

**Ziel:** Konfiguration der User-Ports am modularen Switch und Einrichtung von Spanning-Tree Portfast.

### Beispiel: HR-Access (WS-CSwitch-PT)

> **INFO:** Besonderheit Hardware Da es sich um modulare Switches handelt, werden die Ports als `GigabitEthernet X/1` (Slot/Port) angesprochen.

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

# 📝 Testprotokoll & Checkliste | Labor ID 13

> **SUCCESS:** Ziel der Verifizierung Sicherstellen, dass das Routing zwischen den VLANs funktioniert, die DHCP-Zuweisung über die Helper-Adressen stabil läuft und die OSPF-Nachbarschaften aufgebaut sind.

***

## 🔍 Funktionstests (Schritt-für-Schritt)

### 1. Layer 1 & 2 Check (Physikalisch & VLANs)

- [ ] **Link-Status:** Leuchten alle Verbindungen zwischen Core, Distro und Access grün?
    
- [ ] **Trunking:** Zeigt `show interface trunk` auf den Distro-Switches die erlaubten VLANs (10, 20, 30, 110, 120, 130) an?
    
- [ ] **VLAN-Datenbank:** Sind die VLANs auf allen Access-Switches angelegt? (`show vlan brief`)
    

### 2. Layer 3 Check (Routing & OSPF)

- [ ] **OSPF-Neighbor:** Stehen die Adjacencies zum Core?
    
    - Befehl: `show ip ospf neighbor`
        
    - Erwartetes Ergebnis: Status `FULL`.
        
- [ ] **Routing-Tabelle:** Erkennt der Core die Transit-Netze?
    
    - Befehl: `show ip route ospf`
        
- [ ] **Gateway-Erreichbarkeit:** Kann ein PC sein jeweiliges SVI am Distro-Switch pingen? (z.B. HR-PC pingt `10.13.30.1`)
    

### 3. Dienst-Verfügbarkeit (DHCP & Relay)

- [ ] **DHCP-Lease:** Erhalten die PCs in den Abteilungen eine IP aus dem korrekten Bereich?
    
    - _Sales:_ `10.13.10.x`
        
    - _IT:_ `10.13.20.x`
        
    - _HR:_ `10.13.30.x`
        
- [ ] **Helper-Address:** Ist auf den SVIs die IP `192.168.50.100` (Server) hinterlegt?
    
- [ ] **Rückrouten-Check:** Sind die statischen Routen am Core gesetzt? Ohne diese kommen die DHCP-Antworten nicht vom Server zurück zum Client.
    

***

## 🛠️ Wichtige Troubleshooting-Befehle für Obsidian

|Problem|Befehl|Ebene|
|---|---|---|
|**Keine DHCP-IP**|`debug ip dhcp server packet`|Privileged Mode (`#`)|
|**Routing-Fehler**|`show ip route`|Privileged Mode (`#`)|
|**VLAN-Fehler**|`show interfaces status`|Privileged Mode (`#`)|
|**Port-Fehler**|`show interfaces description`|Privileged Mode (`#`)|

In Google Sheets exportieren

***

## 📌 Abschlussergebnis Tag 3

> **INFO:** Status Die Infrastruktur ist für den Datendurchsatz bereit. Die Abteilungen sind logisch getrennt (VLANs), können aber über den Core miteinander kommunizieren. Der nächste Schritt (Woche 3) umfasst die Absicherung durch ACLs und die Konfiguration der Wireless-Infrastruktur.

# ⚠️ Troubleshooting & Fehleranalyse (Lessons Learned)

> **WARNING:** Kritische Fehlerquellen Während der Konfiguration der Labor-ID 13 traten drei Hauptprobleme auf, die aufgrund der spezifischen Hardware (3650er & Generic Switches) und der hierarchischen Struktur entstanden sind.

### 1. Die "Encapsulation"-Hürde (Layer-3-Switches)

**Problem:** Der Befehl `switchport mode trunk` wurde vom HR-Distro-Switch (3650) mit einer Fehlermeldung abgelehnt. **Ursache:** Multilayer-Switches wie der 3650 unterstützen theoretisch mehrere Trunking-Protokolle (ISL und Dot1q). Solange das Protokoll nicht feststeht, verweigert der Switch den Trunk-Modus. **Lösung:** - Manuelle Zuweisung über: `switchport trunk encapsulation dot1q`.

- _Hinweis:_ Bei einigen Modellen im Packet Tracer wird dies automatisch gesetzt; wenn der Befehl als "Invalid" markiert wird, ist Dot1q bereits der einzige unterstützte Standard.
    

### 2. Adressierungs-Fehler am modularen Access-Switch

**Problem:** Der Befehl `interface range FastEthernet0/1 - 24` schlug fehl. **Ursache:** Du hast den **Generic Switch (WS-CSwitch-PT)** verwendet. Im Gegensatz zu fest verbauten Switches (wie dem 2960) ist dieser modular. Jeder Port sitzt in einem eigenen Slot. **Lösung:** - Die Ports müssen über die Slot-Logik angesprochen werden: `GigabitEthernet0/1`, `1/1`, `2/1` etc.

- In der Dokumentation wurde daher die Aufzählung mit Kommas verwendet: `interface range G0/1, G1/1, G2/1...`.
    

### 3. DHCP-Relay & Statische Rückrouten

**Problem:** PCs erhielten keine IP-Adresse vom DHCP-Server, obwohl `ip helper-address` auf den Distro-Switches korrekt konfiguriert war. **Ursache:** Der DHCP-Server sendet die Antwort an das Gateway der Abteilung (z.B. `10.13.30.1`). Der Core-Switch kannte jedoch keinen Weg zurück in dieses Subnetz, da er nur die Transit-Netze (`10.0.x.x`) in seiner Routing-Tabelle hatte. **Lösung:** - Konfiguration von statischen Routen auf dem **Core-Switch**, die auf die jeweiligen Distribution-Switches zeigen: `ip route 10.13.30.0 255.255.255.0 10.0.2.1`.

### 4. Routed Interfaces vs. Switchports

**Problem:** Eine IP-Adresse konnte nicht auf einem physischen Port des 3650 vergeben werden. **Ursache:** Alle Ports am 3650 starten standardmäßig als Layer-2-Ports (Switchports). **Lösung:** - Der Port muss erst mit dem Befehl `no switchport` in den Layer-3-Modus (Routed Port) versetzt werden, bevor eine IP-Adresse akzeptiert wird.


# Troubleshooting


## 1. Cisco 3650 Interface Bug
- **Problem:** Bei der Konfiguration des HR-DistroSwitches schlug der Befehl `interface range GigabitEthernet1/0/1 - 2` fehl. 
- **Fehlermeldung:** `% Interface range command failed`
- **Ursache:** Bekannter Bug/Besonderheit in der Hardware-Emulation des Cisco 3650 im Packet Tracer, wenn Ports einen fehlerhaften Status haben.
- **Lösung:** > [!success] Workaround
  > Ports virtuell "geresettet" und auf den `range`-Befehl verzichtet. Die Konfiguration wurde stattdessen schrittweise und einzeln auf die funktionierenden Ports angewandt.

## 2. Physische vs. Logische Port-Diskrepanz
- **Problem:** Switch-Ports (z. B. auf HR-Distro und Core1) zeigten in der CLI den Status `up/up` an, bauten aber keine funktionierende Verbindung auf.
- **Analyse:** Die visuelle Überprüfung und der Befehl `show cdp neighbors detail` zeigten, dass die Kabel im Simulator physisch falsch gesteckt waren (z. B. `Gig1/0/1` statt `Gig1/0/3`).
- **Lösung:** Physische Verkabelung im Simulator an die CLI-Konfiguration angepasst.

## 3. OSPF & Routing-Fehler
- **Problem:** DHCP- und Ping-Anfragen aus HR- und Sales-VLANs erreichten das IT-Netz nicht.
- **Ursache:** Fehlende Rückroute.
- **Lösung:** 1. Statische Default-Route auf dem IT-DistroSwitch gesetzt: `ip route 0.0.0.0 0.0.0.0 10.0.30.6`
  2. Fehlende Netze (z. B. `10.0.30.0`) nachträglich in den OSPF-Prozess aufgenommen.