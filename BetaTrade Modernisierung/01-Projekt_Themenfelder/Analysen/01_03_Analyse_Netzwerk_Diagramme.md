# 01 03 Analyse Netzwerk Diagramme

# 📊 Netzwerk-Diagramme (Mermaid Sammlung)

## 0. Importierte Architektur-Skizzen

### Standort- und Rollenuebersicht

![Mainz IT Infrastructure Uebersicht](../../_assets/Screenshot%202026-02-20%20120006.png)

Die Skizze verankert das Projekt fachlich zwischen `Mainz` als Zentrale und `Kaiserslautern` als Regional-Hub. Sie eignet sich als Management-Uebersicht vor den technischen Detaildiagrammen.

### Layer-Topologie Mainz

![Layer-Topologie mit Core, Access und pfSense](../../_assets/Screenshot%202026-02-20%20120200.png)

Die Darstellung passt zur dokumentierten Zielarchitektur mit redundanter Core-Schicht, getrennten Access-Segmenten und Firewall-Uplink zur pfSense.

## 1. Physische & Logische Topologie
```mermaid
graph TD
    subgraph Externe_Admin_Zone
        AdminVM["Ubuntu Admin VM<br/>(10.8.13.2)"]
    end

    subgraph pfSense_Firewall
        WAN_IF["WAN Interface<br/>(10.8.13.1)"]
        FW_Rules{"Firewall Rules<br/>(WAN) & RFC1918 Filter"}
        LAN_IF["LAN Interface<br/>(192.168.13.1)"]
    end

    subgraph Internes_Labor_Netz
        WinSRV["Windows Server 2025<br/>(192.168.13.10)"]
        LinuxSRV["Ubuntu Server<br/>(192.168.13.20)"]
        WinClient["Windows 11 Client<br/>(192.168.13.30)"]
    end

    AdminVM -- "Route: 192.168.13.0/24 via 10.8.13.1" --> WAN_IF
    WAN_IF --> FW_Rules
    FW_Rules -- "PASS (nach Konfiguration)" --> LAN_IF
    LAN_IF --> WinSRV
    LAN_IF --> LinuxSRV
    LAN_IF --> WinClient

    style FW_Rules fill:#f96,stroke:#333,stroke-width:2px
    style AdminVM fill:#dcf,stroke:#333
    style pfSense_Firewall fill:#eee,stroke:#999
```

## 2. DHCP Relay Prozess
```mermaid
graph TD
    subgraph Externe_Admin_Zone ["Externe Admin Zone (WAN)"]
        AdminVM["Ubuntu Admin VM<br/>(10.8.13.2)"]
    end

    subgraph pfSense ["pfSense Firewall & Router"]
        WAN_IF["WAN Interface<br/>(10.8.13.1)"]
        FW_Rules{"Firewall Rules<br/>(WAN PASS ALL)"}
        Relay["<b>DHCP Relay Service</b><br/>Leitet Anfragen an .10 weiter"]
        LAN_IF["LAN Interface<br/>(192.168.13.1)"]
    end

    subgraph Internes_Netz ["Internes Labor Netz (LAN)"]
        WinSRV["<b>Windows Server 2025</b><br/>(192.168.13.10)<br/>DHCP & DNS Server"]
        WinClient["Windows 11 Client<br/>(DHCP-Anfrage)"]
        LinuxSRV["Ubuntu Server<br/>(Statische IP .20)"]
    end

    AdminVM -- "HTTPS / ICMP" --> WAN_IF
    WAN_IF --> FW_Rules --> LAN_IF
    WinClient -- "1. DHCP Discover" --> LAN_IF
    LAN_IF --> Relay
    Relay -- "2. Unicast Forward" --> WinSRV
    WinSRV -- "3. DHCP Offer" --> Relay
    Relay --> WinClient
```
