/
---

# 🔑 Übergabe-Protokoll: Geänderte Passwörter & Logins

**Projekt:** BetaTrade Modernisierung

**Verantwortlich:** AlphaTech IT-Team

**Sicherheitsstufe:** Vertraulich (Nur für Administratoren)

---

## 🏗️ 1. Infrastruktur & Netzwerk (Zentrale Mainz)

_Gehärtete Zugangsdaten für die pfSense-Umgebung und Kern-Dienste._

| Gerät / Dienst        | Benutzername | Geändertes Passwort    | Status           |
| --------------------- | ------------ | ---------------------- | ---------------- |
| **pfSense WebGUI**    | `admin`      | Ug5U3pL]>=rDA5X        | ✅ Geändert       |
| **pfSense Console**   | `root`       | `[Dein_Neues_PW_Hier]` | ✅ Synchron       |
| **pfSense SSH**       | `admin`      | `[Dein_Neues_PW_Hier]` | ✅ Aktiv          |
| **VPN (CA-Key)**      | `Passphrase` | `[CA_Sicherheits_PW]`  | 🔐 Verschlüsselt |
| **Linux Mail-Server** | `root`       | `[Linux_Root_PW]`      | ✅ Geändert       |
|                       |              |                        |                  |

$Password = Read-Host -AsSecureString "Bitte neues Passwort eingeben"
$UserAccount = Get-LocalUser -Name "Administrator"
$UserAccount | Set-LocalUser -Password $Password

---

## 🏢 2. Active Directory & Windows (DC13)

_Administrative Zugänge und Service-Accounts._

|Account-Typ|Benutzername|Passwort / Kennwort|Hinweis|
|---|---|---|---|
|**Domain Admin**|`Administrator`|`[Sicheres_Admin_PW]`|12+ Zeichen|
|**Test-User (IT)**|`d.zimmermann`|`BetaTrade@TQ3b!`|Standard-Initial-PW|
|**Test-User (Corp)**|`a.mueller`|`BetaTrade@TQ3b!`|Standard-Initial-PW|
|**DHCP Service**|`svc_dhcp`|`[Service_Account_PW]`|Läuft auf DC13|

In Google Sheets exportieren

---

## 📡 3. Filiale Kaiserslautern (Packet Tracer)

_Konfigurations-Passwörter für die Hardware vor Ort._

|Gerät|Typ|Passwort (Secret)|Befehl|
|---|---|---|---|
|**Core-Switches**|Console/Enable|`[Cisco_Secret_PW]`|`enable secret`|
|**Dist-Switches**|VTY (Telnet/SSH)|`[VTY_Line_PW]`|`password`|
|**Access Points**|WPA2-PSK (SSID)|`[WLAN_Schlüssel]`|Wireless Config|

In Google Sheets exportieren

---

## 🛡️ 4. Sicherheits-Zusammenfassung (GPO)

_Diese Werte sind systemweit durch die GPO „Password Policy“ erzwungen:_

- **Mindestlänge:** 12 Zeichen
    
- **Ablaufdatum:** 365 Tage (Benutzer wird automatisch zur Änderung aufgefordert)
    
- **Sperre:** 3 Fehlversuche -> 30 Minuten "Cooldown"