# Arbeitsprotokoll: SSH-Troubleshooting & VPN-Optimierung

**Datum:** 2026-03-09 **Projekt:** Stabilisierung der Administrations-Infrastruktur **Status:** ✅ Optimiert

---

## 6. Fehlerbehebung: SSH Host Key Verification

Beim ersten SSH-Verbindungsaufbau zum internen Ubuntu-Server (`192.168.13.20`) trat eine Sicherheitswarnung auf (Host Identification Changed).

### 6.1 Ursache

Die IP-Adresse wurde in der Vergangenheit bereits mit einem anderen SSH-Schlüssel in der Datei `known_hosts` der Admin-VM verknüpft (z.B. durch eine Neuinstallation des Zielsystems).

### 6.2 Lösung

Der veraltete Schlüssel wurde manuell aus dem Cache entfernt:

- **Befehl:** `ssh-keygen -f '/home/student13/.ssh/known_hosts' -R '192.168.13.20'`
    
- **Ergebnis:** Beim nächsten Login konnte der neue Fingerprint mit `yes` dauerhaft akzeptiert werden.
    

---

## 7. Behebung von SSH-Verbindungsabbrüchen (Freezes)

Es wurde festgestellt, dass SSH-Sitzungen über den VPN-Tunnel sporadisch einfrieren, insbesondere bei Inaktivität oder hoher Textausgabe.

### 7.1 Analyse der VPN-Konfiguration

Die Untersuchung der `pfSense-UDP4-1194-admin-vpn-config.ovpn` und der pfSense-Systemkonfiguration ergab Optimierungspotenzial bei MTU-Werten und State-Timeouts.

### 7.2 Implementierte Maßnahmen (Client-Seite)

Um die Verbindung stabil zu halten, wurden folgende Parameter angepasst:

- **Keepalive-Signale:** SSH wird nun mit einem Intervall gestartet, das die Firewall-States aktiv hält.
    
    - **Befehl:** `ssh -o ServerAliveInterval=60 student13@192.168.13.20`
        
- **MTU-Anpassung:** In der `.ovpn`-Datei wurde der MSS-Fix ergänzt, um Paketfragmentierung zu verhindern.
    
    - **Eintrag:** `mssfix 1360`
        

### 7.3 Systemweite Optimierung (pfSense)

In den pfSense-Systemeinstellungen wurden folgende Änderungen vorgenommen:

- **Firewall Optimization:** Umstellung von `Normal` auf `Conservative` (System > Advanced > Firewall & NAT). Dies verlängert die Haltezeit von inaktiven UDP-Verbindungen.
    
- **Hardware Offloading:** Deaktivierung von Hardware-Prüfsummen-Berechnungen, um Instabilitäten in der virtuellen Umgebung zu vermeiden (System > Advanced > Networking).
    

---

## 8. VPN-Management (Workflows)

Für den effizienten Umgang mit der VPN-Verbindung wurden Routinen zum sauberen Beenden der Sitzung etabliert.

### 8.1 Beenden der Verbindung

Da OpenVPN im Hintergrund (Daemon-Modus) gestartet wird, erfolgt das Stoppen über die Prozesssteuerung:

- **Befehl:** `sudo killall openvpn`
    
- **Kontrolle:** `ip a | grep tun0` (Verifizierung, dass das Interface entfernt wurde).
    

### 8.2 Erstellung eines Stop-Skripts (`stop_vpn.sh`)

Bash

```
#!/bin/bash
echo "Beende VPN-Verbindung..."
sudo killall openvpn
echo "Route zum internen Netz wird entfernt."
```

- **Rechte:** `chmod +x /home/student13/Downloads/stop_vpn.sh`
    

---

## Zusammenfassung der Infrastruktur-Parameter

|Komponente|Konfiguration / IP|
|---|---|
|**Admin-VM (VPN IP)**|`10.8.13.2`|
|**VPN-Gateway**|`10.8.13.1`|
|**Ziel-Server (LAN)**|`192.168.13.20`|
|**Optimierung**|`Conservative States`, `mssfix 1360`|