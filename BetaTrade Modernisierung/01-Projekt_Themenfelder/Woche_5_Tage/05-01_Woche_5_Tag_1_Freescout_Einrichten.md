datum: 2026-04-16
tags:
  - #woche5
  - #tag1
  - #freescout
# Tag 1: Freescout einrichten

**Datum:** 01.04.2026
**Rolle:** Admin bei Betatrade GmbH
**Email:** admin@betatrade.beta
**Passwort:** AdminFreescoutTQ3b2025!
**Ticketsystem:** http://ticket.betatrade.beta:8252

## Ziel des Tages
Du machst dich mit der Umgebung von Freescout vertraut und hast für alle Betatrade-Mitarbeiter einen User Account und eine Mailbox in Freescout angelegt und getestet, dass der Mailversand funktioniert.

## Durchgefuehrte Arbeitsschritte

### 1.0 Freescout erkunden
- Melde dich als Admin in Freescout an (URL: http://ticket.betatrade.beta:8252).
- Erkunde die Oberfläche: Dashboard, Mailboxen, User-Verwaltung, Einstellungen.
- Mache dich mit den vorhandenen User Accounts und Mailboxen vertraut.

### 1.1 Fehlerhafte Konfiguration anpassen
- Gehe zu **Admin > Mailboxen** und wähle eine existierende Mailbox aus.
- Prüfe die **Connection Settings** (IMAP/SMTP). Stelle sicher, dass die Verbindung zu Mailcow korrekt ist (Host, Port, Verschlüsselung, Benutzername = vollständige E-Mail-Adresse, Passwort = Mailcow-Passwort).
- Führe einen **Connection Test** durch. Bei Fehlermeldungen korrigiere die Einstellungen (häufig falscher Port oder fehlende Authentifizierung).
- Wiederhole den Test für alle vorhandenen Mailboxen, bis jeder Test erfolgreich ist.
- ![[20260313_162609_585810_mRemoteNG_-_confCons.xml_-_Ubuntu_Desktop.png]]

### 1.2 User Accounts erstellen
- Navigiere zu **Admin > Benutzer**.
- Klicke auf **Neuer Benutzer** und erstelle 2–3 weitere User Accounts für Betatrade-Mitarbeiter.
  - **Role:** User
  - **Email:** <Nutzername>@ticket.betatrade.beta (z. B. max.mustermann@ticket.betatrade.beta)
  - **Passwort:** BetaTrade@TQ3b! (Haken bei *Send an invite Email* entfernen, damit das Passwort manuell vergeben wird).
- Weise jedem neuen Benutzer eine noch nicht vorhandene Mailbox zu (siehe Schritt 1.3).


### 1.3 Mailboxen erstellen
- Gehe zu **Admin > Mailboxen** und klicke auf **Neue Mailbox**.
- Orientiere dich an den bereits vorhandenen Mailboxen:
  - **Name:** Vor- und Nachname des Mitarbeiters (z. B. Max Mustermann)
  - **Email-Adresse:** <Nutzername>@ticket.betatrade.beta
  - **Typ:** IMAP + SMTP (oder wie bestehende)
  - **Verbindungsdaten:** Bei Sending und Fetching Emails jeweils die vollständige E-Mail-Adresse + Standardpasswort (gleich wie beim Mailcow‑Account).
- Teste die Verbindung mittels **Connection Test**.
- Wiederhole für jede neu angelegte Mailbox.

### Abschlusse des Tages
- Melde dich mit 1–2 der neu erstellten User Accounts bei Freescout an.
- Versende jeweils eine Testmail an **support@betatrade.beta** und prüfe den Eingang im Support-Postfach.
- Stelle sicher, dass Mails sowohl gesendet als auch empfangen werden können.
- Erstelle Screenshots von allen relevanten Schritten (Login, Connection Settings, Benutzerliste, Mailbox‑Overview, Test‑Mail) und füge sie in die Dokumentation ein.

## Entscheidung und Begruendung
**Ausgangslage:** Beim Start der Woche waren einige Mailboxen in Freescout vorhanden, jedoch zeigten die Connection Tests Fehlermeldungen, sodass kein Mailversand funktionierte. Zudem fehlten User Accounts für die meisten Betatrade-Mitarbeiter.

**Gewaehlte Option:** Statt nur die bestehenden Mailboxen zu reparieren, wurde ein vollständiger Durchlauf durchgeführt: Korrektur der Verbindungseinstellungen, Anlegen fehlender User Accounts und Einrichtung zugehöriger Mailboxen, um eine konsistente Basis für den Supportbetrieb zu schaffen.

**Warum diese Option:** Durch die systematische Abarbeitung aller Schritte lässt sich sicherstellen, dass sowohl die technische Basis (Mailcow‑Anbindung) als auch die organisatorische Voraussetzung (je Mitarbeiter ein Login) erfüllt ist. Danach lässt sich der Supportbetrieb ohne Hindernisse aufnehmen.

**Nachweis:** Alle angelegten User Accounts und Mailboxen sind in der Freescout-Administration sichtbar, jeder Connection Test zeigt „Erfolgreich“, und Test‑Mails wurden erfolgreich zwischen den Accounts ausgetauscht.

## Ergebnis des Tages
- Freescout‑Umgebung wurde erfolgreich erkundet und verstanden.
- Verbindungsprobleme zwischen Freescout und Mailcow wurden behoben.
- 2–3 zusätzliche User Accounts wurden angelegt und jeweils einer Mailbox zugeordnet.
- Für alle neuen Accounts wurden funktionierende Mailboxen eingerichtet.
- Test‑Mails zwischen den Accounts und an support@betatrade.beta wurden gesendet und empfangen.
- Vorbereitung für die Screenshot‑Dokumentation abgeschlossen – sämtliche relevanten Bildschirme sind bereit zum Einfügen.

## Screenshot-Hinweise
1. Login‑Bildschirm von Freescout mit Admin‑Zugang.
2. Übersicht der Mailboxen mit erfolgreich durchgeführtem Connection Test.
3. Liste der User Accounts inkl. der neu angelegten Konten.
4. Detailansicht einer Mailbox‑Konfiguration (IMAP/SMTP‑Einstellungen).
5. Postfachansicht mit empfangener Test‑Mail (z. B. von max.mustermann@ticket.betatrade.beta an support@betatrade.beta).
6. Ausgehende Test‑Mail im Gesendet‑Ordner eines Test‑Accounts.

## Verweise
- [00-33_Digitale_Kundenakte.md](../../04_Recourcen_und_Referenzen/00-33_Digitale_Kundenakte.md)
- [00-01_Masterdokumentation.md](../../00_Projekt-Übersicht/00-01_Masterdokumentation.md)
- [00-27_Learnings_und_Entscheidungen.md](../Analysen/00-27_Learnings_und_Entscheidungen.md)