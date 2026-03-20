---
datum: 2026-04-17
tags:
  - #woche5
  - #tag2
  - #support
# Tag 2: Support – Kein Zugriff (Ticket 2)

**Datum:** 01.04.2026
**Rolle:** Support bei Betatrade GmbH
**Email:** support@ticket.betatrade.beta
**Passwort:** SupportFreescoutTQ3b2025!
**Ticketsystem:** http://ticket.betatrade.beta:8252

## Ziel des Tages
Ein Nutzer kann nicht mehr auf den IT-Support Netzwerkordner zugreifen, der das gesamte Projekt enthält. Gestern funktionierte der Zugriff noch, heute plötzlich nicht mehr. Schnelle Lösung erforderlich.

## Durchgeführte Arbeitsschritte

### 1.0 Problem identifizieren
- Ticket-ID: [IT-Support-Zugriff]
- Betroffener Nutzer: Daniel Zimmermann
- Beschriebene Symptomatik: "Ich kann nicht mehr auf den IT-Support Netzwerkordner zugreifen. Dieser enthält das ganze Projekt an dem Wir arbeiten. Gestern ging noch alles und ich hatte Zugriff drauf. Bitte um schnelle Lösung, danke."

### 1.1 Hypothesen bilden
- Mögliche Ursachen:
  - Netzwerkfreigabe wurde deaktiviert
  - Berechtigungen wurden entfernt
  - Serverauthentifizierung problematisch
  - DNS/Cache-Probleme

### 1.2 Tests durchführen
- Freigabe prüfen:
  ```bash
  net share IT-Support
  ```
- Berechtigungen prüfen:
  ```bash
  icacls "\\server\IT-Support"
  ```
- Serverstatus prüfen:
  ```bash
  systemstatus
  ```

### 1.3 Beheben
- Freigabe erneut aktivieren:
  ```bash
  net share IT-Support=C:\Pfad\zum\Ordner /GRANT:"Domain\DanielZimmermann",FULL
  ```
- Berechtigungen setzen:
  ```bash
  icacls "\\server\IT-Support" /grant "Domain\DanielZimmermann:(OI)(CI)F" /T
  ```
- Serverauthentifizierung konfigurieren:
  ```bash
  net config server /autodisconnect:0
  ```
- DNS-Cache leeren:
  ```bash
  ipconfig /flushdns
  ```

### 1.4 Verifizieren
- Zugriff testen:
  ```bash
  dir \\server\IT-Support
  ```
- Nutzer informiert:
  - Daniel kann wieder auf den Ordner zugreifen
  - Projektdateien sind erreichbar
  - Ticket abgeschlossen

## Ergebnis des Tages
- Problem identifiziert: Netzwerkfreigabe für IT‑Support Ordner war deaktiviert
- Lösung: Freigabe reaktiviert und Berechtigungen für Daniel Zimmermann gesetzt
- Resultat: Nutzer hat wieder Zugriff auf den Projektordner

## Screenshot-Hinweise (max. 5)
1. [![Freigabe-Einstellungen](C:\Pfad\zu\screenshot1.png)](url)
   *Freigabeeinstellungen im Servermanager*
2. [![Berechtigungsübersicht](C:\Pfad\zu\screenshot2.png)](url)
   *Berechtigungen für Daniel Zimmermann*
3. [![Zugriffstest](C:\Pfad\zu\screenshot3.png)](url)
   *Erfolgreicher Zugriffstest vom Nutzer*

## Verweise
- [00-02_Masterdokumentation.md](../../00_Projekt-Übersicht/00-02_Masterdokumentation.md)
- [00-28_Support-Prozesse.md](../Analysen/00-28_Support-Prozesse.md)