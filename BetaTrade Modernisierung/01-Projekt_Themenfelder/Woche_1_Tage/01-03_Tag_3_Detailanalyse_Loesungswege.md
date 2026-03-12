---
datum: 2026-02-18
tags:
  - #architektur
  - #entscheidungslog
  - #templates
---
# 📅 Tag 3: Detailanalyse & Lösungswege
**Datum:** 18.02.2026 | **Status:** ✅ Dokumentation abgeschlossen

## 🎯 Tagesziele (PM-3)
- [x] Detailanalyse Phase 1: Kaiserslautern (VLAN/DHCP)
- [x] Detailanalyse Phase 2: Mainz (Roadmap & Abhängigkeiten)
- [x] Entwicklung von Lösungsansätzen für die Geschäftsführung

***

## 🔍 1. Detailanalyse Phase 1 (Kaiserslautern)
Die Anforderung "3 Abteilungen mit Segmentierung" erfordert eine saubere Layer-2-Trennung auf den Switches.

**Was bedeutet das konkret?**
* Jede Abteilung erhält eine eigene Broadcast-Domäne (VLAN).
* Kommunikation zwischen Abteilungen erfolgt ausschließlich über den Core-Switch (Inter-VLAN-Routing).
* Sicherheit: Unbefugte können nicht einfach durch Umstecken des Kabels in ein anderes Netz gelangen.

### 🔢 IP-Adressplan (Vorschlag für Subnetz 13)
| Bereich | VLAN | Netzadresse | Gateway (SVI) | DHCP-Bereich |
| :--- | :---: | :--- | :--- | :--- |
| **Vertrieb** | 10 | 10.13.10.0/24 | 10.13.10.1 | .100 - .200 |
| **IT** | 20 | 10.13.20.0/24 | 10.13.20.1 | .100 - .200 |
| **HR** | 30 | 10.13.30.0/24 | 10.13.30.1 | .100 - .200 |
| **VoIP** | 40 | 10.13.40.0/24 | 10.13.40.1 | .100 - .200 |

***

## 🔍 2. Detailanalyse Phase 2 (Zentrale Mainz)
In Mainz müssen viele Dienste gleichzeitig modernisiert werden. Um Ausfälle zu vermeiden, habe ich folgende Roadmap entwickelt:

**Empfohlene Umsetzungsreihenfolge:**
1. **IP-Konzept & DHCP:** Basis legen.
2. **VPN-Tunnel (pfSense):** Damit wir als AlphaTech sicher von extern arbeiten können.
3. **AD Security Policies:** Sicherheit der Benutzerkonten erhöhen.
4. **Cloud-Backup:** Erst jetzt, da der VPN-Tunnel für den sicheren Datentransfer steht.
5. **LDAP-Mailserver:** Letzter Schritt, nutzt die fertige AD-Struktur.

***

## 💡 3. Lösungsansätze
| Ansatz | Fokus | Technik |
| :--- | :--- | :--- |
| **Lösung A** | Sicherheit | Strikte ACLs, Zertifikats-VPN, 2FA für Admins. |
| **Lösung B** | Verfügbarkeit | HSRP-Redundanz für Gateways, Failover-Internet. |
| **Lösung C** | Kosteneffizienz | Standard-VLANs, Passwort-VPN (nicht empfohlen). |

***

## 🔧 Offene technische Fragen
1. Sind in Kaiserslautern bereits IP-Telefone vorhanden oder müssen Softphones genutzt werden?
2. Hat die pfSense in Mainz genug Kapazität für 25 gleichzeitige VPN-Tunnel?




### Netzwerk-Topologie Kaiserslautern 

![Screenshot 2026-02-20 120200.png](Screenshot%202026-02-20%20120200.png)

# Tag 3: Architektur-Entscheidungen & Vorlagen (Ergänzung)

> **INFO:** Fokus
> Nachvollziehbarkeit technischer Entscheidungen und Vorbereitung standardisierter Dokumente für das Umsetzungsteam.

## 1. Architecture Decision Records (ADRs)
- **Einführung:** Etablierung eines "Entscheidungslogs" im Vault.
- **Beispiel:** Begründung, warum das Subnetz `10.13.x.0/24` gewählt wurde (ausreichend Hosts für die Filialgröße, gute Lesbarkeit durch Mapping von VLAN-ID auf das dritte Oktett).

## 2. Standardisierung von Vorlagen
> **SUCCESS:** Single Source of Truth
> Entwicklung und Bereitstellung von wiederverwendbaren Markdown-Tabellen für IP-Adresspläne und Switch-Port-Belegungen. Das technische Team muss diese in den nächsten Wochen nur noch ausfüllen.

## 3. Kunden-Kommunikation (Offene Punkte)
- Entwurf eines gezielten Fragenkatalogs an die BetaTrade-Geschäftsführung:
  - Wie hoch ist die genaue Anzahl vorhandener IP-Telefone in KL?
  - Reicht die Kapazität der geplanten pfSense für die prognostizierten gleichzeitigen VPN-Tunnel?