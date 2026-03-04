# 📑 Übergabe-Protokoll: Planung -> Administration
**Projekt:** BetaTrade Modernisierung | **ID:** 13

## 1. Projektüberblick & Phasen
* **Woche 1:** Planung & Simulation KL (VLANs, DHCP-Relay, VoIP).
* **Woche 2-5:** Umsetzung Mainz (pfSense VPN, Cloud-Backup, AD-Härtung).
* **Woche 6:** Monitoring (IDS) & Compliance (ISO 27001).

## 2. Technische Vorgaben für das Netzwerk-Team
Für die praktische Umsetzung in Themenfeld 2 sind folgende Parameter fixiert:

### VLAN- & IP-Matrix (Regional-Hub KL)
| VLAN | Name | Subnetz | Gateway |
| :--- | :--- | :--- | :--- |
| 10 | Vertrieb | 10.13.10.0/24 | 10.13.10.1 |
| 20 | IT | 10.13.20.0/24 | 10.13.20.1 |
| 30 | HR | 10.13.30.0/24 | 10.13.30.1 |
| 40 | VoIP | 10.13.40.0/24 | 10.13.40.1 |
| 99 | Management | 10.13.99.0/24 | 10.13.99.1 |

### Konfigurations-Details
* **DHCP-Server:** Admin-VM in Mainz (`10.8.13.2`).
* **Relay-Agent:** Muss auf allen SVIs in Kaiserslautern aktiv sein.
* **Redundanz:** Einsatz von HSRP zwischen `CoreSwitch0` und `CoreSwitch1`.

## 3. Empfohlene Lösungsansätze
Wir empfehlen die Nutzung von **802.1X Port-Security** in der IT-Abteilung und eine **pfSense-Instanz** mit OpenVPN für den Remote-Zugriff.

## 4. Bekannte Risiken
* Zeitverzug bei der VPN-Konfiguration durch Zertifikats-Management.
* Mögliche Inkompatibilität der VoIP-Firmware im Packet Tracer.