# 📑 Dokumentation: Implementierung der L3-Netzwerkinfrastruktur

## 1. Projektübersicht

Im Rahmen der Modernisierung der Zentrale Mainz habe ich die Netzwerk-Infrastruktur von einer statischen Adressierung auf ein dynamisches, hierarchisches Routing-Modell umgestellt. Der Fokus lag auf der Implementierung von Layer-3-Kommunikation zwischen Core- und Distribution-Ebene sowie der zentralen DHCP-Bereitstellung.

## 2. Core-Layer Konfiguration (CoreSwitch0 & CoreSwitch1)

Um eine effiziente Kommunikation zwischen den Abteilungen zu gewährleisten, habe ich die Core-Switches als zentrale Routing-Instanzen konfiguriert.

### Umgesetzte Maßnahmen:

- **Aktivierung des IP-Routings:** Grundvoraussetzung für die Inter-VLAN-Kommunikation.
    
- **Routed Ports:** Die Uplinks zu den Distribution-Switches wurden mit `no switchport` von Layer-2 auf Layer-3 umgestellt, um Punkt-zu-Punkt-Verbindungen (Transit-Netze) zu etablieren.
    
- **Statisches Routing:** Implementierung von Routen für die Zielnetze (HR, Sales, IT) und das Server-Segment.
    

### Beispiel-Konfiguration (CoreSwitch1):

Plaintext

```
interface GigabitEthernet1/0/4
 no switchport
 ip address 10.0.30.5 255.255.255.252
!
ip route 192.168.50.0 255.255.255.0 10.0.30.6
ip route 10.13.10.0 255.255.255.0 10.0.10.6
```

## 3. Distribution-Layer & DHCP-Relay

Die Distribution-Switches fungieren als Standard-Gateways für die jeweiligen Abteilungen. Da der DHCP-Server zentral im IT-Segment steht, habe ich DHCP-Relay-Agenten implementiert.

### Umgesetzte Maßnahmen:

- **SVI-Konfiguration:** Einrichtung der VLAN-Interfaces (VLAN 10, 20, 30) als Default-Gateways.
    
- **DHCP-Helper:** Konfiguration der `ip helper-address`, um DHCP-Broadcasts als Unicasts zum Windows-Server (192.168.50.100) weiterzuleiten.
    

### Konfiguration am Beispiel HR-Distro:

Plaintext

```
interface Vlan 10
 ip address 10.13.10.1 255.255.255.0
 ip helper-address 192.168.50.100
```

## 4. IT-Segment & Server-Anbindung

Das IT-Segment wurde so strukturiert, dass sowohl die IT-Arbeitsplätze als auch die zentralen Dienste (DHCP/DNS) erreichbar sind.

### Umgesetzte Maßnahmen:

- **Trunking:** Konfiguration von EtherChannel/Trunks zum IT-Access-Switch zur Redundanz und Bandbreitenerhöhung.
    
- **Rückrouten:** Einrichtung einer Default-Route (`0.0.0.0/0`) auf dem IT-DistroSwitch in Richtung Core, um sicherzustellen, dass Server-Antworten den Core erreichen.
    

## 5. Verifizierung & Testing

Zur Validierung der Konfiguration wurden folgende Tests erfolgreich durchgeführt:

1. **ICMP-Check:** Pings vom Core-Switch zum IT-Gateway (192.168.50.1) und zum DHCP-Server (192.168.50.100) verliefen erfolgreich.
    
2. **DHCP-Migration:** Workstations in HR und Sales erhielten nach Umstellung auf DHCP erfolgreich IP-Adressen aus dem korrekten Scope (z.B. `10.13.10.x`).
    
3. **Routing-Tabelle:** Verifizierung der `show ip route` Einträge auf allen Layer-3-Komponenten zur Bestätigung der Pfadredundanz.