# 05 01 Cisco Cheatsheet

### 🟢 1. Grundlegende Navigation & Hilfe

| Befehl                | Beschreibung                                         |
| --------------------- | ---------------------------------------------------- |
| `enable`              | Wechsel in den privilegierten Modus (Admin).         |
| `configure terminal`  | Wechsel in den globalen Konfigurationsmodus.         |
| `exit` / `end`        | Eine Ebene zurück / Zurück zum Start.                |
| `?`                   | Zeigt alle verfügbaren Befehle im aktuellen Kontext. |
| `show running-config` | Zeigt die aktuelle Konfiguration im RAM.             |
| `write memory`        | Speichert die Config dauerhaft (NVRAM).              |

In Google Sheets exportieren

***

### 🔵 2. VLAN & Access-Port Konfiguration

Wichtig für die Abteilungs-Switches (Sales, IT, HR).

Code-Snippet

```
# VLAN erstellen
vlan 10
 name Vertrieb
exit

# Ports einem VLAN zuweisen
interface range GigabitEthernet1/0/1-10
 switchport mode access
 switchport access vlan 10
 no shutdown
```

***

### 🟡 3. Trunking (Verbindung zwischen Switches)

Wichtig für die Verbindung vom Core-Switch zu den Abteilungen.

Code-Snippet

```
interface GigabitEthernet1/1/1
 # Nur bei Multilayer-Switches (z.B. 3650) nötig:
 switchport trunk encapsulation dot1q 
 
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,99
```

***

### 🔴 4. Inter-VLAN Routing (Core-Switch)

Damit die Abteilungen miteinander kommunizieren können.

Code-Snippet

```
ip routing  # Aktiviert Layer-3 Funktionen

# SVI (Gateway) für VLAN 10
interface vlan 10
 ip address 10.13.10.1 255.255.255.0
 no shutdown
```

***

### 🟣 5. DHCP-Relay (ip helper)

Leitet DHCP-Anfragen an deine Admin-VM (`10.8.13.2`) weiter.

Code-Snippet

```
interface vlan 10
 ip helper-address 10.8.13.2
interface vlan 20
 ip helper-address 10.8.13.2
interface vlan 30
 ip helper-address 10.8.13.2
```

***

### 🔍 6. Diagnose & Troubleshooting

Diese Befehle nutzt du zur Verifizierung für deine Doku:

| Befehl                    | Was es prüft                                           |
| ------------------------- | ------------------------------------------------------ |
| `show vlan brief`         | Welche Ports sind in welchem VLAN?                     |
| `show ip interface brief` | Sind die IPs vergeben und die Ports "up"?              |
| `show interfaces trunk`   | Stehen die Trunk-Verbindungen?                         |
| `show ip route`           | Funktioniert das Routing zwischen den Subnetzen?       |
| `show cdp neighbors`      | Welche anderen Cisco-Geräte sind direkt angeschlossen? |
|                           |                                                        |

In Google Sheets exportieren
