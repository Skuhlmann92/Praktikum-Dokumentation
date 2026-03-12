---
datum: 2026-03-10
tags:
  - #systemadministration
  - #active-directory
  - #mailserver
  - #tagesprotokoll
status: done
---

# Tag 2 (Woche 4): Windows-Linux Integration (Mailserver)

**Datum:** 10.03.2026  
**Bearbeiter:** Samuel (via AI-Assistent)  
**Status:** ✅ Erledigt

## 🎯 Tagesziele
- [x] Mailcow-Container-Stack bereitstellen & analysieren
- [x] Interne DNS-Weiterleitung (Unbound) auf AD-Domaincontroller konfigurieren
- [x] LDAP-Anbindung von Mailcow an das Active Directory umsetzen
- [x] Authentifizierungstests mit AD-Benutzern durchführen

## 👥 Gruppenarbeit
1. **Infrastruktur-Abstimmung:** Festlegung des Service-Accounts für den LDAP-Bind im Windows-Team.
2. **DNS-Troubleshooting:** Behebung eines Auflösungsfehlers (beta.local wurde intern nicht korrekt auf den DC geroutet).

## 👤 Einzelarbeit
1. **Konfiguration:** Anpassung der `unbound.conf` und Neustart des Containers.
2. **AD-Integration:** Einrichtung des LDAP Identity Providers im Mailcow-Admin-Panel.
3. **Validierung:** Erfolgreiche Anmeldung am SOGo Webmail mit Test-Usern aus den OUs `HR` und `IT`.

## 📸 Dokumentation & Screenshots

![Pasted image 20260309160937.png](Pasted%20image%2020260309160937.png)
- **Screenshot 1:** Status der Mailcow-Container in Docker (`docker ps`).  
  `![mailcow_status.png](mailcow_status.png)`
- **Screenshot 2:** LDAP-Konfigurationsmaske (Test Connection erfolgreich).  
  `![mailcow_ldap_success.png](mailcow_ldap_success.png)`
- **Screenshot 3:** Erfolgreicher SOGo-Login eines AD-Benutzers.  
  `![sogo_login_success.png](sogo_login_success.png)`

## 📝 Reflexion / Offene Punkte
- Die Integration vereinfacht die Benutzerverwaltung erheblich (Single Source of Truth im AD).
- **Lessons Learned:** Bei LDAP über Port 636 muss das Zertifikat des DCs im Mailcow-Container bekannt sein (oder "Ignore SSL Errors" temporär aktiv).
- Nächster Schritt: Einrichtung der Backup-Strategie für das gesamte Mail-System.
