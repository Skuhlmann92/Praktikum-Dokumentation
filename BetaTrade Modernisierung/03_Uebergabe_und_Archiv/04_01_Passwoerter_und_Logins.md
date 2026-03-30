
***

# 🔑 Übergabe-Protokoll: Geänderte Passwörter & Logins

**Projekt:** BetaTrade Modernisierung

**Verantwortlich:** AlphaTech IT-Team

**Sicherheitsstufe:** Vertraulich (Nur für Administratoren)

***

## 🏗️ 1. Infrastruktur & Netzwerk (Zentrale Mainz)

_Gehärtete Zugangsdaten für die pfSense-Umgebung und Kern-Dienste._

| Gerät / Dienst                                                                 | Benutzername                                                                   | Geändertes Passwort | Status     |
| ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ | ------------------- | ---------- |
| **pfSense WebGUI**                                                             | `admin`                                                                        | Ug5U3pL]>=rDA5X     | ✅ Geändert |
| **Linux Mail-Server**                                                          | `root`                                                                         | Ug5U3pL]>=rDA5X     | ✅ Geändert |
| windows dc                                                                     | Student                                                                        | qwerasdfxycv        | ✅ Geändert |
| [rene@mindrefined.de](mailto:rene@mindrefined.de "mailto:rene@mindrefined.de") | [rene@mindrefined.de](mailto:rene@mindrefined.de "mailto:rene@mindrefined.de") |                     |            |
|                                                                                |                                                                                | Ug5U3pL]>=rDA5X     |            |
**E-Mail Adresse:** student.samuel@mindrefined.de

**Username Dashboard:** student.samuel@mindrefined.de

**Password Dashboard**: N8yvJ8Y6gD$p

**Interne ID Netzwerk:** 13
Ug5U3pL]>=rDA5X
***

## 🏢 2. Active Directory & Windows (DC13)

_Administrative Zugänge und Service-Accounts._

| Account-Typ          | Benutzername    | Passwort / Kennwort    | Hinweis             |
| -------------------- | --------------- | ---------------------- | ------------------- |
| **Domain Admin**     | `Administrator` | `[Sicheres_Admin_PW]`  | 12+ Zeichen         |
| **Test-User (IT)**   | `d.zimmermann`  | `BetaTrade@TQ3b!`      | Standard-Initial-PW |
| **Test-User (Corp)** | `a.mueller`     | `BetaTrade@TQ3b!`      | Standard-Initial-PW |
| **DHCP Service**     | `svc_dhcp`      | `[Service_Account_PW]` | Läuft auf DC13      |

In Google Sheets exportieren

***

## 📡 3. Filiale Kaiserslautern (Packet Tracer)

_Konfigurations-Passwörter für die Hardware vor Ort._

|Gerät|Typ|Passwort (Secret)|Befehl|
|---|---|---|---|
|**Core-Switches**|Console/Enable|`[Cisco_Secret_PW]`|`enable secret`|
|**Dist-Switches**|VTY (Telnet/SSH)|`[VTY_Line_PW]`|`password`|
|**Access Points**|WPA2-PSK (SSID)|`[WLAN_Schlüssel]`|Wireless Config|

In Google Sheets exportieren

***

## 🛡️ 4. Sicherheits-Zusammenfassung (GPO)

_Diese Werte sind systemweit durch die GPO „Password Policy“ erzwungen:_

- **Mindestlänge:** 12 Zeichen
    
- **Ablaufdatum:** 365 Tage (Benutzer wird automatisch zur Änderung aufgefordert)
    
- **Sperre:** 3 Fehlversuche -> 30 Minuten "Cooldown"