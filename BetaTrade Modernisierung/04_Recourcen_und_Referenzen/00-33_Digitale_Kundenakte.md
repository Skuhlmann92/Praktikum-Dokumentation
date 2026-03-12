# 📄 Digitale Kundenakte: BetaTrade AG

**Branche:** Mittelständischer Aktien- und Wertpapierhandel **Größe:** ca. 25 Mitarbeiter **Standorte:** Zentrale Mainz, neue Filiale Kaiserslautern (Regional-Hub)

***

## 🏗️ Ist-Zustand (Zentrale Mainz)

Die IT-Infrastruktur in Mainz dient als Basis und wird im Laufe des Projekts modernisiert.

- **Server:**
    
    - Windows Server: Active Directory, DNS, Dateiserver.
        
    - Linux App-Server: Kundendatenbank (MySQL), Backup, Container.
        
    - Gateway: pfSense (Firewall, Routing, VPN).
        
- **Schwachstellen:**
    
    - Externer Zugriff nur durch Passwort gesichert (unsicher).
        
    - Keine interne Segmentierung zwischen Abteilungen.
        
    - Fehlendes externes Backup-Konzept.
        

***

## 📍 Projektphase 1: Regional-Hub Kaiserslautern

Die Filiale in Kaiserslautern ist größer geplant als ursprünglich vorgesehen und erfordert ein eigenständiges Netzwerkdesign.

**Anforderungen:**

1. **3-Abteilungen-Architektur:** Strikte Trennung via VLANs.
    
2. **VLAN-Planung (ID 13):**
    
    - VLAN 10: Vertrieb
        
    - VLAN 20: IT
        
    - VLAN 30: HR
        
3. **Dienste:**
    
    - Implementierung DHCP-Server & DHCP-Relay zur Zentrale.
        
    - Abteilungsübergreifende VoIP-Telefonie.
        
4. **Status:** Packet Tracer Datei ist weitestgehend vorkonfiguriert, Planung der Segmentierung und IP-Adressen fehlt noch.
    

***

## 🏢 Projektphase 2: Modernisierung Zentrale

- **Netzwerk:** IP-Konzept Optimierung & DHCP-Automatisierung.
    
- **Sicherheit:** VPN-Tunnel für sichere Fernwartung (Ersatz der reinen Passwort-Auth).
    
- **Backup:** Integration eines bereits beauftragten Cloud-Storage-Service.
    

***

## 🛡️ Projektphase 3: Security & Monitoring

- **Überwachung:** IDS (Intrusion Detection System) und Alerting-Dashboard.
    
- **Compliance:** Anpassung der Richtlinien nach **ISO 27001**.
    
- **Prozesse:** Incident Response Plan & Schwachstellen-Management.
    

***

## 👥 Ansprechpartner

- **IT-Leitung:** Herr Weber
    
- **Geschäftsführung:** Herr Schmidt (Budget & Entscheidungen)
    
- **Filialleitung KL:** Herr Müller
    

***

### 💡 Notiz für die Dokumentation (Tag 1)

> "Die Analyse der Kundenakte zeigt, dass die Priorität auf der Segmentierung der neuen Filiale und der Absicherung des externen Zugriffs liegt. Das IP-Konzept für Kaiserslautern (VLAN 10, 20, 30) muss konsistent zum Gesamtnetz (Subnetz 13) geplant werden."