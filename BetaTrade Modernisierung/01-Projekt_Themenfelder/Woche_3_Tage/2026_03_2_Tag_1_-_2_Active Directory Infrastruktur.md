
---

# 📑 Projektdokumentation: Active Directory Infrastruktur BetaTrade

**Erstellt von:** Systemadministrator (AlphaTech GmbH)

**Datum:** 02. März 2026

**System-Umgebung:** Windows Server 2022 (Hostname: **DC13**)

**Domäne:** `net13.beta`

---

## 1. Projektübersicht & Analyse

Ziel war die vollständige Automatisierung der Benutzerverwaltung und die Implementierung einer sicheren Zugriffssteuerung für die BetaTrade AG basierend auf einer CSV-Mitarbeiterliste.

### 1.1 Analyse der Quelldaten (`BetaTrade_Mitarbeiterliste.csv`)

Die Datei enthält 20 Datensätze mit den Feldern: `Vorname, Nachname, Benutzername, Email, Abteilung, Position, Telefon`.

- **Besonderheit:** Die Abteilung ist im Format `Hauptabteilung-Unterabteilung` angegeben (z.B. `Corporate-HR`).
    
- **Strategie:** Die Hauptabteilung dient als Name für die **OU** (Organizational Unit) und die zugehörige **Security Group**.
    

---

## 2. Phase 1: Automatisierte Benutzeranlage

Statt einer manuellen Anlage wurde ein PowerShell-Skript verwendet, um Fehlerquellen zu minimieren.

### 2.1 Das PowerShell-Skript (Core-Logik)

Ich habe das Skript so konzipiert, dass es fehlende Gruppen automatisch erstellt und User direkt zuweist.

PowerShell

```
# Import-Modul und Pfaddefinition
Import-Module ActiveDirectory
$csvPath = "C:\Users\Student\Desktop\CSV Dateien\BetaTrade_Mitarbeiterliste_net13.csv"
$defaultPassword = ConvertTo-SecureString "BetaTrade@TQ3b!" -AsPlainText -Force

# Verarbeitung der CSV
$users = Import-Csv $csvPath -Delimiter ","

foreach ($row in $users) {
    # Extraktion der Haupt-OU (z.B. IT aus IT-Support)
    $mainDept = $row.Abteilung.Split("-")[0]
    $ouPath = "OU=$mainDept,DC=net13,DC=beta"
    $groupName = "$mainDept-User"

    # 1. Sicherstellen, dass die Gruppe existiert
    if (-not (Get-ADGroup -Filter "Name -eq '$groupName'")) {
        New-ADGroup -Name $groupName -GroupCategory Security -GroupScope Global -Path $ouPath
    }

    # 2. Benutzer anlegen
    $userParams = @{
        SamAccountName = $row.Benutzername
        UserPrincipalName = "$($row.Benutzername)@net13.beta"
        Name = "$($row.Vorname) $($row.Nachname)"
        GivenName = $row.Vorname
        Surname = $row.Nachname
        EmailAddress = $row.Email
        Path = $ouPath
        AccountPassword = $defaultPassword
        Enabled = $true
        ChangePasswordAtLogon = $false # Für RDP-Test deaktiviert
    }
    
    if (-not (Get-ADUser -Filter "SamAccountName -eq '$($row.Benutzername)'")) {
        New-ADUser @userParams
        Write-Host "User $($row.Benutzername) erstellt." -ForegroundColor Green
    }

    # 3. Gruppenmitgliedschaft zuweisen
    Add-ADGroupMember -Identity $groupName -Members $row.Benutzername
}
```

---

## 3. Phase 2: Fileserver & Berechtigungsmatrix

Für die Zusammenarbeit wurden zentrale Verzeichnisse auf `C:\BetaTrade` eingerichtet.

### 3.1 Verzeichnisstruktur

Die Ordner wurden analog zur Abteilungsstruktur erstellt:

- `C:\BetaTrade\Corporate` (Unterordner: HR, Finance)
    
- `C:\BetaTrade\IT` (Unterordner: Security, Support)
    
- `C:\BetaTrade\Marketing` (Unterordner: Digital, Events)
    

### 3.2 Berechtigungskonzept (RBAC)

Ich habe die Vererbung (Inheritance) unterbrochen, um den Zugriff strikt zu trennen.

- **Admins:** Full Control.
    
- **Abteilungsgruppe (z.B. IT-User):** Modify-Rechte auf ihren eigenen Ordner.
    
- **Andere Gruppen:** Kein Zugriff (Access Denied).
    

---

## 4. Phase 3: Gruppenrichtlinien (GPOs)

Zur Absicherung der Domäne wurden drei zentrale Richtlinien in der `Group Policy Management Console` (GPMC) konfiguriert.

### 3.1 Passwort-Sicherheit (Default Domain Policy)

- **Mindestlänge:** 12 Zeichen.
    
- **Maximales Alter:** 365 Tage (12 Monate).
    
- **Komplexität:** Deaktiviert (gemäß Kundenwunsch).
    

### 3.2 Account Lockout (Brute-Force Schutz)

- **Sperrung nach:** 3 Fehlversuchen.
    
- **Dauer:** 30 Minuten.
    

### 3.3 Drive Mapping (Benutzerkomfort)

Ein Netzlaufwerk wurde über die `User Configuration -> Preferences` zugewiesen:

- **Pfad:** `\\DC13\IT_Data$`
    
- **Laufwerksbuchstabe:** `I:`
    
- **Filterung:** Über **Item-Level Targeting** wurde das Laufwerk nur Mitgliedern der Gruppe `IT-User` zugewiesen.
    

---

## 5. Phase 4: Validierung & Troubleshooting

### 5.1 Durchgeführte Tests

1. **Login-Test:** Erfolgreiche Anmeldung mit `d.zimmermann`.
    
2. **GPO-Check:** `gpresult /r` zeigt die korrekte Anwendung der `GPO_DriveMapping`.
    
3. **Sicherheits-Check:** Versuchter Zugriff von `a.mueller` (Corporate) auf den IT-Ordner wurde erfolgreich vom System blockiert.
    

### 5.2 Troubleshooting: RDP-Zugriff am Domain Controller

**Problem:** Test-User erhielten beim Login die Meldung: _"The connection was denied because the user account is not authorized..."_ **Lösung:** Da auf einem Domain Controller standardmäßig nur Admins RDP-Rechte haben, wurden die Gruppen `IT-User` etc. in der **Default Domain Controllers Policy** unter `User Rights Assignment -> Allow log on through Remote Desktop Services` hinzugefügt.

---

## 6. Abschluss & Lessons Learned

Das Projekt wurde erfolgreich abgeschlossen. Alle 20 Mitarbeiter haben Zugriff auf ihre spezifischen Ressourcen.

- **Optimierungspotenzial:** Für zukünftige Projekte sollte das Skript eine Logging-Funktion in eine Textdatei enthalten, um Fehler bei der Anlage (z.B. Duplikate) besser nachverfolgen zu können.
    
- **Sicherheitshinweis:** Die Deaktivierung der Passwort-Komplexität sollte langfristig kritisch hinterfragt und ggf. revidiert werden.
    

---

### 📋 Übergabe-Checkliste

- [x] OUs und Gruppen in AD vorhanden?
    
- [x] Benutzer passend zur CSV importiert?
    
- [x] NTFS-Berechtigungen auf C:\BetaTrade gesetzt?
    
- [x] GPOs verknüpft und mit `gpupdate /force` getestet?
    
- [x] Netzlaufwerke erscheinen automatisch?