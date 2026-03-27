
# Tag 4 (Woche 4): Monitoring- und Security-Vorbereitung

**Datum:** 13.03.2026  
**Bearbeiter:** Samuel

## Einordnung

Obwohl die eigentliche `Phase 3 Security` noch nicht umgesetzt ist, wurden in Woche 4 bereits konkrete Vorarbeiten sichtbar:

- Sichtung von Host-basierten Alarmen
- Sammlung von Analysehilfen fuer Netzwerkforensik
- Ableitung sinnvoller Monitoring-Use-Cases fuer den spaeteren Security-Betrieb

Damit dient dieser Tag als Bruecke zwischen der abgeschlossenen Infrastrukturmodernisierung und der geplanten Security-Operationalisierung.

## Technische Beobachtungen

### 1. Hostbasierter Netzwerkalarm

![simplewall Warnung fuer ausgehende Python-HTTPS-Verbindung](../../_assets/simplewall_python_https_alert.png)

Im Screenshot wurde eine ausgehende HTTPS-Verbindung eines `python.exe`-Prozesses durch `simplewall` sichtbar. Daraus ergeben sich fuer die spaetere Ueberwachung drei relevante Punkte:

- unbekannte oder unerwartete Prozesskommunikation sollte aktiv sichtbar werden
- Freigabe, Blockierung und Begruendung muessen nachvollziehbar dokumentiert sein
- Host-Alerts sollten mit Firewall- und Server-Logs korreliert werden

### 2. Operative Triage mit Wireshark

![Wireshark Filter Referenz](../../_assets/wireshark_filters_reference.jpg)

Die Filterreferenz ist fuer die Security-Phase praktisch nutzbar, vor allem fuer:

- DNS-Analyse
- DHCP-Fehlerbilder
- TLS-Handshake-Pruefung
- VLAN- und Broadcast-bezogene Paketanalysen

## Abgeleitete Monitoring-Use-Cases

1. Alarm bei neuen ausgehenden Verbindungen administrativer oder unbekannter Prozesse
2. Alarm bei fehlgeschlagenen LDAP- oder VPN-Anmeldungen
3. Regelmaessige Pruefung von DNS-, DHCP- und TLS-bezogenen Auffaelligkeiten
4. Nachvollziehbare Triage mit Paketmitschnitten und Event-Logs

## Dokumentationsbezug

- Phase-3-Konzept: [00-12_Phase_3_Security_Konzept.md](../../02_Phasen/Phase_3_Security/00-12_Phase_3_Security_Konzept.md)
- Incident Response: [00-12a_Incident_Response_Plan.md](../../02_Phasen/Phase_3_Security/00-12a_Incident_Response_Plan.md)
- Firewall-Haertung: [00-21_Analyse_Firewall_Hardening.md](../Analysen/00-21_Analyse_Firewall_Hardening.md)

## Reflexion

Woche 4 endet nicht nur mit Docker-, SQL- und Mail-Themen, sondern liefert bereits belastbare Vorarbeit fuer den spaeteren Security-Betrieb. Besonders wertvoll ist, dass nicht nur Konzepte, sondern erste visuelle Evidenzen fuer Alarmierung und Analyse vorliegen.
