
---

# 📑 Labor-Dokumentation: Tag 4-6 – DHCP-Infrastruktur & Migration

**Projekt:** pfSense-Infrastruktur Modernisierung Zentrale Mainz **Auftraggeber:** BetaTrade AG **Techniker:** AlphaTech / Student 13 **Status:** 🟢 DHCP-Migration abgeschlossen

---

## 🗺️ Netzwerk-Planfigur (Mermaid)

Diese Grafik visualisiert den aktuellen Stand nach der DHCP-Implementierung und zeigt den Weg des DHCP-Relays.


---

## 🛠️ Konfigurations-Details

### 1. Windows Server 2025 (DHCP-Rolle)

Die DHCP-Server-Rolle wurde installiert, um die zentrale IP-Verwaltung der BetaTrade AG zu realisieren.

- **Scope-Name:** Labor_Netz_13.
    
- **IP-Range:** 192.168.13.100 bis 192.168.13.130.
    
- **Adresskapazität:** Deckt die geforderten 31 Host-Adressen ab.
    
- **Option 003 (Gateway):** 192.168.13.1 (pfSense).
    
- **Option 006 (DNS):** 192.168.13.10 (Lokaler Server).
    

### 2. pfSense (DHCP-Relay)

Um den Windows Server als zentrale Instanz zu nutzen, wurden die Dienste auf der pfSense angepasst.

- **DHCP-Server:** Deaktiviert auf dem LAN-Interface.
    
- **DHCP-Relay:** Aktiviert; alle LAN-Anfragen werden per Unicast an 192.168.13.10 weitergeleitet.
    

---

## 📊 IP-Adressplan & Migrations-Strategie

Gemäß der "Best Practice" Analyse wurden kritische Infrastruktur-Komponenten statisch belassen, während Endgeräte migriert wurden.

|Host|Typ|IP-Adresse|Strategie|
|---|---|---|---|
|**pfSense**|Gateway|192.168.13.1|**Statisch** (Infrastruktur-Kern)|
|**WinSRV 2025**|Server|192.168.13.10|**Statisch** (Dienstleister für DHCP/DNS)|
|**Security SRV**|Server|192.168.13.15|**DHCP-Reservierung**|
|**Ubuntu Server**|Server|192.168.13.20|**DHCP-Reservierung** (Identifier: MAC)|
|**Win 11 Client**|Client|192.168.13.1xx|**Dynamisch** (Pool .100-.130)|

In Google Sheets exportieren

---

## 🔍 Wichtige technische Hinweise

> [!IMPORTANT] Linux-Migration Für den Ubuntu Server wurde in der Netplan-Konfiguration `dhcp-identifier: mac` gesetzt. Ohne diese Einstellung schlagen MAC-basierte Reservierungen im Windows DHCP fehl.

> [!TIP] Konnektivitäts-Test Der Zugang von der Admin-VM erfolgt über die statische Route 192.168.13.0/24 via 10.8.13.3. Dieser Zugriff muss während der gesamten Migration aufrechterhalten werden, um den Administrations-Zugang nicht zu verlieren.

---

## 📋 Nächste Aufgaben (Vorschau)

- [ ] **DNS-Zonen:** Erstellung der Forward-Lookup-Zonen `net13.beta` und `betatrade.beta`.
    
- [ ] **Reverse-Lookup:** Erstellung der PTR-Records für den gewählten Adressbereich.
    
- [ ] **VPN:** Vorbereitung der OpenVPN-Implementierung mit Zertifikaten.