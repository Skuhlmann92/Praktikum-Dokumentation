# 02 01 Tag 4 Finalisierung Übergabe


**Datum:** 19.02.2026  
**Rolle:** Planung / Übergabevorbereitung

## Ziel des Tages
Die Umsetzungsvorbereitung für Themenfeld 2 wurde in eine kundentaugliche Form gebracht und die technischen Startparameter für das Netzwerkteam zusammengefasst.

## Durchgeführte Arbeitsschritte
1. VLANs, Namensschema und IP-Logik für Kaiserslautern final zusammengestellt.
2. Packet-Tracer-Ausgangslage auf fehlende VLANs, Routing, STP und Voice-Konfiguration geprüft.
3. Übergabepunkte für die Umsetzung in Mainz und Kaiserslautern dokumentiert.
4. Risiken und offene Fragen für Hardware, VoIP und Management-Zugriff markiert.
5. Struktur für spätere Betriebs- und Abschlussdokumente vorbereitet.

## Lösung der Tagesaufgaben

### Gruppenarbeit

#### 1. Lösungsansätze diskutieren und bewerten
- Die an Tag 3 entwickelten Lösungsansätze wurden verglichen und auf Praxistauglichkeit bewertet.
- Als praktikabelste Variante wurde die Kombination aus klarer VLAN-Segmentierung, zentralen Diensten in Mainz und sicherem Fernzugriff über pfSense/VPN festgelegt.
- Für die Umsetzung wurde priorisiert:
  zuerst Netz- und Zugriffsbasis,
  danach zentrale Dienste,
  danach Integrationen und Security-Erweiterungen.

- Für Themenfeld 2 wurde eine grobe Arbeitslogik vorbereitet:
  Netzwerkgrundlagen und Segmentierung,
  DHCP/DNS,
  VPN,
  danach AD,
  später Docker, SQL und LDAP.
- Die Dokumentationsstruktur wurde so geplant, dass Tagesprotokolle, Analysen, Phasen und Übergabe getrennt, aber nachvollziehbar verbunden sind.
- Das Netzwerk-Team benötigt aus der Planungswoche vor allem:
  VLAN- und IP-Konzept,
  Packet-Tracer-Bestandsaufnahme,
  priorisierte Anforderungen,
  Risiken und offene Fragen.

### Einzelarbeit

#### 1. Übergabe-Dokumentation erstellen
- Die Erkenntnisse der Planungswoche wurden in eine übergabefähige Struktur überführt:
  Projektüberblick,
  Phasenbeschreibung,
  priorisierte Anforderungen,
  empfohlene Lösungsansätze,
  Risiken und offene Punkte.
- Damit ist die Aufgabe des Tages inhaltlich gelöst und für das nachfolgende Umsetzungsteam nutzbar gemacht.

#### 2. Packet-Tracer-Datei sichten
- Die bereitgestellte Packet-Tracer-Ausgangslage wurde fachlich als teilvorkonfiguriert eingeordnet.
- Als noch zu planende bzw. zu prüfende Punkte wurden festgehalten:
  VLAN-Zuordnung,
  Trunking,
  Inter-VLAN-Routing,
  STP-Schutzmechanismen,
  Voice-VLAN bzw. VoIP-Einbindung,
  DHCP-Relay-Konzept.
- Diese Beobachtungen wurden für das Netzwerk-Team dokumentiert.
- Zusätzlich aus der Sichtung abgeleitet:
  `ip routing` muss auf den Core-Switches aktiv sein,
  VTP sollte vorzugsweise im Modus `transparent` betrieben werden,
  bei Voice-VLAN und IP-Telefonen ist das PoE-Budget der Access-Switche zu prüfen.

#### 3. BetaTrade-Organisationsstruktur visualisieren
- Die inhaltliche Struktur für Organigramm und Infrastrukturdiagramm wurde vorbereitet:
  Geschäftsführung,
  IT,
  Filialleitung bzw. Filiale Kaiserslautern,
  getrennte Betrachtung von Mainz und Kaiserslautern.
- Da im Repo kein eigenes finales Organigramm als Datei in Woche 1 abgelegt ist, wurde die Visualisierung inhaltlich in die Übergabevorbereitung übernommen:
  organisatorische Rollen,
  Standorte,
  Netzsegmente und zentrale Systeme sind für eine spätere grafische Umsetzung beschrieben.

##### Organigramm BetaTrade AG

```mermaid
flowchart TD
    GF[Geschäftsführung<br/>BetaTrade AG]
    ITL[IT-Leitung<br/>Mainz]
    FL[Filialleitung<br/>Kaiserslautern]
    ITM[IT-Betrieb / Administration<br/>Mainz]
    V[Vertrieb<br/>Kaiserslautern]
    HR[HR<br/>Kaiserslautern]
    ITK[Lokale IT / Support<br/>Kaiserslautern]

    GF --> ITL
    GF --> FL
    ITL --> ITM
    FL --> V
    FL --> HR
    FL --> ITK
    ITL -. fachliche Abstimmung .- ITK
```

##### Infrastrukturdiagramm Mainz und Kaiserslautern

```mermaid
flowchart LR
    subgraph MZ[Standort Mainz]
        PF[pfSense<br/>Gateway / VPN]
        WIN[Windows Server 2025<br/>AD / DNS / DHCP]
        DOCK[Linux / Docker<br/>SQL / Mail / Apps]
        MCL[Mainz Clients]
        PF --> WIN
        PF --> DOCK
        WIN --> MCL
    end

    subgraph KL[Standort Kaiserslautern]
        CORE[Core / L3-Switching]
        V10[VLAN 10<br/>Vertrieb]
        V20[VLAN 20<br/>IT]
        V30[VLAN 30<br/>HR]
        V40[VLAN 40<br/>VoIP]
        V99[VLAN 99<br/>Management]
        CORE --> V10
        CORE --> V20
        CORE --> V30
        CORE --> V40
        CORE --> V99
    end

    PF <-- Site-to-Site / Admin-Zugriff / zentrale Dienste --> CORE
    WIN -. DHCP / DNS / AD .-> CORE
    DOCK -. spätere Integrationen .-> WIN
```

### Konkrete Übergabepunkte an das Netzwerk-Team
- VLAN-IDs und Namenskonventionen:
  10 Vertrieb, 20 IT, 30 HR, 40 VoIP, 99 Management
- IP-Logik:
  `10.13.X.0/24` mit Zuordnung nach VLAN-ID
- DHCP-Strategie:
  zentrales Service-Modell via DHCP-Relay
- Hardware-Grundannahme:
  Core-/Access-Switching mit späterem Redundanz- und HSRP-Zielbild

### Formale Handover-Checkliste
- [x] VLAN-IDs definiert
- [x] IP-Adressbereiche zugewiesen
- [x] DHCP-Relay-Strategie beschrieben
- [x] Risiken und offene Fragen dokumentiert
- [x] Packet-Tracer-Ausgangslage bewertet

##### Übergabefluss Planung zu Umsetzung

```mermaid
flowchart LR
    P[Planungswoche<br/>Woche 1]
    A[Anforderungen<br/>Risiken<br/>Zielbild]
    U[Übergabe an<br/>Netzwerk-Team]
    N[Netzwerkumsetzung<br/>Woche 2]
    S[Systemdienste / AD<br/>Woche 3]
    I[Integration / Docker / LDAP<br/>Woche 4]

    P --> A --> U --> N --> S --> I
```

### Abschluss des Tages
- Die Lösungsansätze sind bewertet und priorisiert.
- Die Übergabe an das Netzwerk-Team ist fachlich vorbereitet.
- Die Packet-Tracer-Ausgangslage wurde gesichtet und die noch offenen Konfigurationspunkte sind dokumentiert.

## Entscheidung und Begründung
**Ausgangslage:** Das Umsetzungsteam benötigte eine klare Startkonfiguration, damit die technische Arbeit ohne Rückfragen an die Planungswoche anschließen kann.

**Gewählte Option:** Die Übergabe wurde als kompakter technischer Startsatz mit VLAN-/IP-Konzept, offenen Punkten und Prioritäten vorbereitet.

**Warum diese Option:** Dadurch bleibt für den Kunden nachvollziehbar, welche Vorgaben aus der Planungsphase in die spätere Implementierung übernommen wurden.

**Nachweis:** Packet-Tracer-Analyse, Phasenkonzept und Übergabeprotokoll greifen dieselben Eckdaten auf.

## Ergebnis des Tages
- Startparameter für Themenfeld 2 dokumentiert
- typische Konfigurationslücken in der Ausgangslage erkannt
- offene Punkte für Kunde und Technikteam klar benannt
- Übergabefähige Planungsdokumentation erstellt

## Optionale Screenshots
1. Packet-Tracer-Topologie oder Inventaransicht
2. Beispiel für eine erkannte Konfigurationslücke im Simulator

Organigramm, Infrastrukturübersicht und Übergabefluss sind bereits als Mermaid-Grafiken im Dokument enthalten. Ein zusätzlicher Screenshot des Übergabedokuments ist nicht mehr nötig.

## Verweise
- [03_01_Phase_1_Kaiserslautern_Konzept.md](../../02_Phasen/Phase_1_Kaiserslautern/03_01_Phase_1_Kaiserslautern_Konzept.md)
- [01_04_Analyse_Packet_Tracer.md](../Analysen/01_04_Analyse_Packet_Tracer.md)
- [04_03_Uebergabe_Protokoll.md](../../03_Uebergabe_und_Archiv/04_03_Uebergabe_Protokoll.md)


