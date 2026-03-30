**Name:** Samuel Kuhlmann

**System:** Ubuntu Server (netXX.beta)

**Rolle:** Systemadministrator AlphaTech GmbH

---

## 1. Docker-Grundlagen

### 1.1 Docker-Umgebung erkunden

- **Durchführung:** Zunächst wird ein Docker-Container aus dem Hello-World Image gestartet. Ist dieses Image nicht vorhanden, lädt Docker es automatisch von Docker Hub herunter, sofern es dort vorhanden ist. Da der User momentan noch nicht der docker-Gruppe angehört, muss dies im Terminal mit Admin-Rechten (`sudo`) ausgeführt werden.
    
- **Befehle:**
    
    ```bash
    # Docker-Installation mit einem hello-world Container testen
    sudo docker run hello-world
    
    # Alle vorhandenen Images auflisten
    sudo docker images
    
    # Zeigt nur die laufenden Container an
    sudo docker ps
    
    # Zeigt alle erstellten Container an
    sudo docker ps -a
    ```
    
- **Erklärung:** Der hello-world-Container taucht unter den laufenden Containern nicht auf. Der Grund dafür ist, dass dieser spezielle Container von Docker absichtlich nur gestartet wird, eine Nachricht hinterlässt und sich dann selbst stoppt. Der Exit-Code (0) zeigt dabei an, dass der Container erfolgreich ausgeführt wurde. Um zu sehen, dass er tatsächlich existiert, müssen alle Container aufgelistet werden, nicht nur die laufenden.
    
- **Images vs. Container:** In der objektorientierten Programmierung ist eine Klasse die Blaupause, aus der Objekte (Instanzen) erstellt werden. Bei Docker ist das Prinzip identisch:
    
    - Das **Image** ist wie die Klasse – unveränderlich und wiederverwendbar.
    - Der **Container** ist das daraus erstellte Objekt – eine laufende Instanz des Images.

### 1.2 Container-Verwaltung (Cleanup)

- **Durchführung:** Der Container hat sich bereits nach dem Starten selbst wieder gestoppt. Um den hello-world Docker-Container zu löschen, benötigt man die Container-ID, die bei der Auflistung aller Container angezeigt wird.
    
- **Befehle zum Aufräumen:**
    
    ```bash
    # Container anhand der Container-ID löschen
    sudo docker rm <CONTAINER_ID>
    
    # Prüfen ob Container entfernt wurde
    sudo docker ps -a
    
    # hello-world Image löschen
    sudo docker rmi hello-world
    
    # Erfolg prüfen
    sudo docker images
    ```
    

---

## 2. BetaTrade-Datenbank Setup

### 2.1 Docker Compose

- **Analyse `docker-compose.yml`:** In der `docker-compose.yml` wird der gesamte Datenbankserver (MySQL) konfiguriert. Es wird definiert:
    
    - Welches **Image** verwendet wird
    - **Zugangsdaten** (User, Passwort, Datenbankname)
    - **Netzwerk & Ports** (wie man von außen drauf zugreift)
    - **Datenpersistenz** (dass Daten nicht verloren gehen, wenn der Container stoppt)
    - **Initialisierung** (dass die Datenbank beim ersten Start mit Daten befüllt wird)
- **Start der Datenbank:**
    
    ```bash
    # Wechsel in das richtige Verzeichnis
    cd /home/studentxx/betatrade-database/
    
    # Starten der Kundendatenbank
    sudo docker compose up -d
    
    # Laufende Container anzeigen
    sudo docker ps
    
    # Logs auf Fehler prüfen
    sudo docker logs betatrade-mysql
    ```
    
- **Erwartete Log-Ausgaben:**
    
    - `Creating database betatrade_db` → Datenbank wurde erstellt
        
    - `Creating user admin` → User wurde angelegt
        
    - `Database successfully initialized!` → Initialisierung erfolgreich
        
    - `100 Customers, 100 Accounts, 117 Trades` → Testdaten wurden geladen
        
    - `ready for connections. port: 3306` → Datenbank läuft und ist erreichbar
        
    
    > Die Warnings sind harmlos – Zeitzonen-Dateien und self-signed Zertifikat stören den Betrieb nicht.
    

### 2.2 Verbindung zur Datenbank

- **Login-Befehl:**
    
    ```bash
    sudo docker exec -it betatrade-mysql mysql -uadmin -pbetatrade betatrade_db
    ```
    
    - `docker exec -it` → Befehl im laufenden Container ausführen
        
    - `betatrade-mysql` → Name des Containers
        
    - `mysql -uadmin -pbetatrade betatrade_db` → MySQL mit User `admin` und Passwort `betatrade` öffnen
        
    
    > An der letzten Zeile `mysql>` kann man sehen, dass die Verbindung und der Login erfolgreich war.
    

---

## 3. Datenbank-Erkundung & SQL-Struktur

### 3.1 Tabellen-Struktur (DESCRIBE)

- **Alle Tabellen anzeigen:**
    
    ```sql
    SHOW TABLES;
    ```
    
    Es gibt 3 Tabellen in der Kundendatenbank: `accounts`, `customers`, `trades`.
    
- **Struktur der Tabellen anzeigen:**
    
    ```sql
    DESCRIBE customers;
    DESCRIBE accounts;
    DESCRIBE trades;
    ```
    

|Tabelle|Zweck|
|---|---|
|`customers`|Stammdaten der Kunden (Name, Email, Reg-Datum)|
|`accounts`|Kontoinformationen, verknüpft mit customer_id|
|`trades`|Transaktionsdaten, verknüpft mit account_id|

- **Detaillierte Tabellenstruktur:**
    
    **customers – Kundentabelle:**
    
    - `customer_id` → eindeutige ID (Primary Key, auto_increment)
    - `first_name`, `last_name`, `email`, `phone` → Kontaktdaten
    - `registration_date` → Registrierungsdatum
    - `status` → nur `active` oder `inactive` möglich (enum)
    
    **accounts – Kontotabelle:**
    
    - `account_id` → eindeutige ID (Primary Key)
    - `customer_id` → Fremdschlüssel → Verbindung zu `customers`
    - `account_type` → nur `Standard`, `Premium` oder `VIP` möglich (enum)
    - `balance` → Kontostand mit 2 Dezimalstellen
    
    **trades – Handelstabelle:**
    
    - `trade_id` → eindeutige ID (Primary Key)
    - `account_id` → Fremdschlüssel → Verbindung zu `accounts`
    - `trade_type` → nur `BUY` oder `SELL` möglich (enum)
    - `profit_loss` → Gewinn/Verlust des Trades

### 3.2 Beispieldaten anzeigen

```sql
-- Die ersten 10 Kunden anzeigen
SELECT * FROM customers LIMIT 10;

-- Die ersten 10 Konten anzeigen
SELECT * FROM accounts LIMIT 10;

-- Die ersten 10 Trades anzeigen
SELECT * FROM trades LIMIT 10;

-- Die Gesamtzahl der Kunden anzeigen
SELECT COUNT(*) FROM customers;

-- Die Gesamtzahl der Trades anzeigen
SELECT COUNT(*) FROM trades;
```

---

## 4. Daten-Abfragen (Queries)

### 4.1 Filtern & Suchen (WHERE)

```sql
-- Alle aktiven Kunden anzeigen
SELECT * FROM customers WHERE status = 'active';

-- Alle inaktiven Kunden
SELECT * FROM customers WHERE status = 'inactive';

-- Kunden mit @betatrade-test.de E-Mail
SELECT * FROM customers WHERE email LIKE '%@betatrade-test.de';

-- Kunde Michael Becker
SELECT * FROM customers WHERE first_name = 'Michael' AND last_name = 'Becker';
```

- `WHERE` → filtert Zeilen nach Bedingung
- `LIKE '%...'` → `%` ist ein Platzhalter für beliebige Zeichen davor
- `AND` → beide Bedingungen müssen erfüllt sein

### 4.2 Nach Datum filtern

```sql
-- Kunden die sich 2024 registriert haben
SELECT * FROM customers WHERE YEAR(registration_date) = 2024;

-- Kunden die sich vor 2023 registriert haben
SELECT * FROM customers WHERE YEAR(registration_date) < 2023;

-- Kunden die sich im Januar 2024 registriert haben
SELECT * FROM customers WHERE YEAR(registration_date) = 2024 AND MONTH(registration_date) = 1;
```

- `YEAR()` → extrahiert das Jahr aus einem Datum
- `MONTH()` → extrahiert den Monat aus einem Datum
- `<` → kleiner als (vor 2023 = Jahr kleiner als 2023)

### 4.3 Trades filtern

```sql
-- Alle Trades für AAPL
SELECT * FROM trades WHERE instrument = 'AAPL';

-- Alle Trades für BTC/USD
SELECT * FROM trades WHERE instrument = 'BTC/USD';

-- Alle BUY Trades
SELECT * FROM trades WHERE trade_type = 'BUY';

-- Alle Trades mit profit_loss > 500
SELECT * FROM trades WHERE profit_loss > 500;
```

- `=` → exakter Vergleich, genauer Instrumentenname ist bekannt
- `>` → größer als

### 4.2 Aggregation & Gruppierung

```sql
-- Gesamtgewinn (SUM)
SELECT SUM(profit_loss) FROM trades;

-- Durchschnittlicher Kontostand
SELECT AVG(balance) FROM accounts;

-- Trades pro Instrument
SELECT instrument, COUNT(*) FROM trades GROUP BY instrument;

-- Trades pro trade_type (BUY/SELL)
SELECT trade_type, COUNT(*) FROM trades GROUP BY trade_type;

-- Kunden gruppiert nach Status
SELECT status, COUNT(*) FROM customers GROUP BY status;
```

---

## 5. Sortierung

```sql
-- Kunden sortiert nach last_name A-Z
SELECT * FROM customers ORDER BY last_name ASC;

-- Kunden sortiert nach registration_date (neueste zuerst)
SELECT * FROM customers ORDER BY registration_date DESC;

-- Trades sortiert nach profit_loss (höchster Gewinn zuerst)
SELECT * FROM trades ORDER BY profit_loss DESC;
```

- `ORDER BY` → sortiert die Ergebnisse
- `ASC` → aufsteigend (A-Z, kleinste zuerst) – ist Standard, kann weggelassen werden
- `DESC` → absteigend (Z-A, größte zuerst)

---

## 6. Relationale Verknüpfungen (JOINs)

### 6.1 Beziehungen verstehen

Die Tabellen sind wie folgt verbunden:

- `customers` → `accounts` (über `customer_id`)
- `accounts` → `trades` (über `account_id`)

**Warum drei Tabellen statt einer großen?** Das Prinzip heißt **Normalisierung**. Eine große Tabelle hätte folgende Probleme:

- Ein Kunde mit 10 Trades → seine Adresse/Email wird 10x gespeichert (Redundanz)
- Ändert sich die Email, müsste man sie 10x ändern (Fehleranfälligkeit)
- Gelöschte Trades würden Kundendaten mitlöschen (Datenverlust)

Drei getrennte Tabellen lösen das – jede Information wird nur einmal gespeichert und über Fremdschlüssel verknüpft.

### 6.2 Einfacher JOIN

```sql
-- Kundennamen mit ihren Kontonummern
SELECT c.first_name, c.last_name, a.account_number
FROM customers c
JOIN accounts a ON c.customer_id = a.customer_id;

-- Kundennamen mit ihrem Kontotyp
SELECT c.first_name, c.last_name, a.account_type
FROM customers c
JOIN accounts a ON c.customer_id = a.customer_id;

-- Kundennamen mit ihrem Kontostand
SELECT c.first_name, c.last_name, a.balance
FROM customers c
JOIN accounts a ON c.customer_id = a.customer_id;
```

**JOIN-Typen:**

- `INNER JOIN` (kurz `JOIN`) → nur Zeilen, die in beiden Tabellen einen Match haben
- `LEFT JOIN` → alle Zeilen der linken Tabelle, auch ohne Match rechts
- `RIGHT JOIN` → alle Zeilen der rechten Tabelle, auch ohne Match links

> In diesem Fall wurde immer `INNER JOIN` verwendet, da jeder Account einem Kunden zugeordnet ist.

---

## 7. Geschäftsfragen beantworten (Business Questions)

### 7.1 Neukunden-Analyse

**Frage:** Wie viele Neukunden hat BetaTrade seit dem 1. Januar 2024 gewonnen?

**Antwort:** BetaTrade hat seit dem 01.01.2024 25 Kunden dazugewonnen.

```sql
-- Alle Kunden seit 01.01.2024
SELECT * FROM customers WHERE registration_date >= '2024-01-01';

-- Anzahl zählen
SELECT COUNT(*) FROM customers WHERE registration_date >= '2024-01-01';

-- Namen und Registrierungsdaten sortiert nach Datum
SELECT first_name, last_name, registration_date
FROM customers
WHERE registration_date >= '2024-01-01'
ORDER BY registration_date ASC;
```

### 7.2 Trading-Aktivitätsanalyse

**Frage:** Welcher Kunde war im März 2024 am aktivsten?

```sql
-- Schritt 1: Alle Trades im März 2024 finden
SELECT * FROM trades
WHERE YEAR(trade_date) = 2024 AND MONTH(trade_date) = 3;

-- Schritt 2: Trades pro account_id im März 2024 zählen
SELECT account_id, COUNT(*) as trade_count
FROM trades
WHERE YEAR(trade_date) = 2024 AND MONTH(trade_date) = 3
GROUP BY account_id
ORDER BY trade_count DESC;

-- Schritt 3: Kundeninformationen mit JOIN hinzufügen (komplexe Analyse)
SELECT c.first_name, c.last_name, COUNT(t.trade_id) as trade_count
FROM customers c
JOIN accounts a ON c.customer_id = a.customer_id
JOIN trades t ON a.account_id = t.account_id
WHERE YEAR(t.trade_date) = 2024 AND MONTH(t.trade_date) = 3
GROUP BY c.customer_id, c.first_name, c.last_name
ORDER BY trade_count DESC LIMIT 1;
```

---

## 8. Datensicherheit & Bereinigung

### 8.1 Test-Benutzer identifizieren

```sql
-- Alle Kunden mit betatrade-test.de E-Mails finden
SELECT * FROM customers WHERE email LIKE '%betatrade-test.de%';

-- Alle inaktiven Kunden finden
SELECT * FROM customers WHERE status = 'inactive';

-- Anzahl der Test-Konten dokumentieren
SELECT COUNT(*) FROM customers WHERE email LIKE '%betatrade-test.de%';
```

### 8.2 Datenbank-Backup (Dump)

```bash
# MySQL-Client verlassen
exit

# Backup vom Host-System aus erstellen
docker exec betatrade-mysql mysqldump -uadmin -pbetatrade betatrade_db > backup_day3.sql

# Prüfen ob die Backup-Datei erstellt wurde
ls -lh backup_day3.sql
```

### 8.3 Test-Daten löschen

```bash
# Erneut mit der Datenbank verbinden
sudo docker exec -it betatrade-mysql mysql -uadmin -pbetatrade betatrade_db
```

```sql
-- Zuerst den Test-User zur Überprüfung selektieren
SELECT * FROM customers WHERE email = 'test.user1@betatrade-test.de';

-- Test-User löschen
DELETE FROM customers WHERE email = 'test.user1@betatrade-test.de';

-- Löschung durch Zählen der Gesamtkunden überprüfen
SELECT COUNT(*) FROM customers;
```

---

## 9. Bonus-Aufgaben

### Bonus 1: Komplexe Filterung

```sql
-- Kunden die sich 2024 registriert haben UND ein VIP-Konto haben
SELECT c.first_name, c.last_name, a.account_type
FROM customers c
JOIN accounts a ON c.customer_id = a.customer_id
WHERE YEAR(c.registration_date) = 2024 AND a.account_type = 'VIP';
-- Ergebnis: Es gibt keinen Kunden mit diesen Anforderungen.

-- Trades im März 2024 mit Gewinn > 200
SELECT * FROM trades
WHERE YEAR(trade_date) = 2024 AND MONTH(trade_date) = 3
AND profit_loss > 200;

-- Top 5 profitabelsten Trades aller Zeiten
SELECT * FROM trades ORDER BY profit_loss DESC LIMIT 5;
```

### Bonus 2: Erweiterte Aggregation

```sql
-- Gesamtgewinn/-verlust pro Kunde (2 JOINs)
SELECT c.first_name, c.last_name, SUM(t.profit_loss) as gesamt
FROM customers c
JOIN accounts a ON c.customer_id = a.customer_id
JOIN trades t ON a.account_id = t.account_id
GROUP BY c.customer_id, c.first_name, c.last_name
ORDER BY gesamt DESC;

-- Kunden mit mehr als 10 Trades insgesamt
SELECT c.first_name, c.last_name, COUNT(t.trade_id) as trade_count
FROM customers c
JOIN accounts a ON c.customer_id = a.customer_id
JOIN trades t ON a.account_id = t.account_id
GROUP BY c.customer_id, c.first_name, c.last_name
HAVING trade_count > 10;

-- Durchschnittlichen Trade-Gewinn pro Instrument berechnen
SELECT instrument, AVG(profit_loss) as durchschnitt
FROM trades
GROUP BY instrument
ORDER BY durchschnitt DESC;
```

---

## 10. Reflexion

### Docker-Referenz

|Befehl|Beschreibung|
|---|---|
|`docker run <image>`|Container aus Image erstellen und starten|
|`docker ps`|Laufende Container anzeigen|
|`docker ps -a`|Alle Container anzeigen|
|`docker images`|Alle Images anzeigen|
|`docker rm <id>`|Container löschen|
|`docker rmi <image>`|Image löschen|
|`docker logs <name>`|Container-Logs anzeigen|
|`docker exec -it <name> <befehl>`|Befehl in laufendem Container ausführen|
|`docker compose up -d`|Container per docker-compose starten|
|`docker compose down`|Container per docker-compose stoppen|

**Docker Compose:** Ohne docker-compose müsste man jeden Container manuell mit langen `docker run` Befehlen starten, inklusive aller Parameter wie Ports, Volumes, Netzwerke und Umgebungsvariablen. Docker Compose fasst all das in einer einzigen `docker-compose.yml` Datei zusammen. Mit nur einem Befehl (`docker compose up -d`) wird die gesamte Umgebung gestartet – reproduzierbar und fehlerfrei.

```bash
# Status prüfen
sudo docker ps

# Logs anzeigen
sudo docker logs betatrade-mysql
```

### SQL-Referenz

```sql
-- Alle Daten einer Tabelle abrufen
SELECT * FROM tabelle;

-- Bestimmte Spalten abrufen
SELECT spalte1, spalte2 FROM tabelle;

-- Filtern
SELECT * FROM tabelle WHERE bedingung;

-- Sortieren
SELECT * FROM tabelle ORDER BY spalte ASC/DESC;

-- Begrenzen
SELECT * FROM tabelle LIMIT 10;

-- Zählen
SELECT COUNT(*) FROM tabelle;

-- Aggregation
SELECT SUM(spalte), AVG(spalte), MIN(spalte), MAX(spalte) FROM tabelle;

-- Gruppieren
SELECT spalte, COUNT(*) FROM tabelle GROUP BY spalte;

-- Tabellen verbinden
SELECT * FROM tabelle1 JOIN tabelle2 ON tabelle1.id = tabelle2.id;
```

**Unterschied zwischen WHERE, GROUP BY und HAVING:**

- `WHERE` → filtert einzelne Zeilen **vor** der Gruppierung
- `GROUP BY` → fasst Zeilen mit gleichem Wert zusammen
- `HAVING` → filtert Gruppen **nach** der Gruppierung (wie WHERE, aber für Gruppen)

```sql
-- Beispiel: WHERE filtert zuerst, dann wird gruppiert, HAVING filtert die Gruppen
SELECT status, COUNT(*)
FROM customers
WHERE registration_date >= '2024-01-01'  -- erst filtern
GROUP BY status                           -- dann gruppieren
HAVING COUNT(*) > 5;                      -- dann Gruppen filtern
```

### Wichtigste Erkenntnisse

- **Docker:** Docker Compose ist deutlich effizienter als manuelle `docker run` Befehle, da die gesamte Konfiguration (Netzwerk, Volumes) versionierbar in einer Datei liegt.
    
- **SQL:** Die größte Herausforderung war der **Triple-JOIN** (Customers → Accounts → Trades). Die Lösung war der schrittweise Aufbau: erst Trades finden, dann nach `account_id` gruppieren, dann Kundendaten per JOIN hinzufügen. Wichtig ist, immer die Fremdschlüssel (`customer_id`, `account_id`) als Brücke zu nutzen.
    
- **Sicherheit:** Vor jedem `DELETE` sollte immer ein `SELECT` mit derselben Bedingung ausgeführt werden, um sicherzustellen, dass man nicht die falschen Zeilen löscht.
    

---