# 03 01a Netzplan Kaiserslautern

### 🖼️ Netzplan & Topologie: BetaTrade AG

**Projekt-ID:** 13 | **Standorte:** Kaiserslautern & Mainz

## 1. 📍 Filiale Kaiserslautern (Regional-Hub)

Die Filiale ist als hierarchisches LAN-Design aufgebaut, um die drei Abteilungen sauber voneinander zu trennen.

### Physische Struktur (Layer 2)

- **Core-Layer:** Zwei Catalyst 3650 Multilayer-Switches (`CoreSwitch0`, `CoreSwitch1`) sorgen für Redundanz und Inter-VLAN-Routing.
    
- **Access-Layer:** Drei dedizierte Switches für die Abteilungen:
    
    - `Sales-AccessSwitch` (VLAN 10)
        
    - `IT-AccessSwitch` (VLAN 20)
        
    - `HR-AccessSwitch` (VLAN 30)
        
- **Uplinks:** Alle Access-Switches sind via **802.1Q Trunks** redundant an beide Core-Switches angebunden.
    

### Logische Segmentierung (VLANs & Subnetze)

|Abteilung|VLAN ID|Subnetz|Gateway (SVI)|
|---|---|---|---|
|**Vertrieb**|10|`10.13.10.0/24`|`10.13.10.1`|
|**IT**|20|`10.13.20.0/24`|`10.13.20.1`|
|**HR**|30|`10.13.30.0/24`|`10.13.30.1`|
|**Management**|99|`10.13.99.0/24`|`10.13.99.1`|

***

## 2. 🏢 Zentrale Mainz (Main Site)

Die Zentrale beherbergt die kritischen Server-Dienste und dient als Ziel für das VPN-Management.

### Zentrale Dienste

- **Domain Controller (AD):** Verwaltung von Benutzern und Gruppenrichtlinien.
    
- **Linux App-Server:** Kundendatenbank (MySQL) und Backup-Services.
    
- **Security Gateway:** pfSense Firewall zur Absicherung des Internetübergangs und zur VPN-Termination.
    

### Vernetzung (S2S VPN)

- **VPN-Tunnel:** Ein verschlüsselter Tunnel verbindet die Zentrale Mainz mit dem Regional-Hub Kaiserslautern.
    
- **DHCP-Relay:** IP-Anfragen aus Kaiserslautern werden über diesen Tunnel zur Admin-VM (`10.8.13.2`) in Mainz weitergeleitet.
    

***

## 3. 🛠️ Dokumentation der Verbindungen

Verwende diesen Block, um deine Screenshots aus dem Packet Tracer zu verknüpfen:

- **Aktuelle Topologie (Screenshot):** `![Kaiserslautern_Topologie_PT.png](Kaiserslautern_Topologie_PT.png)`
    
- **Routing-Tabelle Core-Switch:** `![Routing_Table_Core0.png](Routing_Table_Core0.png)`
