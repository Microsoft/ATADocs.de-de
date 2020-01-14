---
title: Tutorial zum Setup einer Testumgebung für Azure ATP-Sicherheitswarnungen | Microsoft-Dokumentation
description: In diesem Tutorial richten Sie eine Azure ATP-Testumgebung zum Simulieren von Bedrohungen für die Erkennung durch Azure ATP ein.
ms.service: azure-advanced-threat-protection
ms.topic: tutorial
author: shsagir
ms.author: shsagir
ms.date: 02/28/2019
ms.reviewer: itargoet
ms.openlocfilehash: 8c3238c07c05bf307c91753e6d69b35b376a3c21
ms.sourcegitcommit: 9673eb49729a06d3a25d52c0f43c76ac61b9cf89
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/12/2020
ms.locfileid: "75908512"
---
# <a name="tutorial-setup-an-atp-security-alert-lab"></a>Tutorial: Setup einer ATP-Sicherheitswarnungsumgebung 

 Die Azure ATP-Sicherheitswarnungsumgebung soll die Funktionen von **Azure ATP** zum Identifizieren und Erkennen verdächtiger Aktivitäten und potenzieller Angriffe auf Ihr Netzwerk veranschaulichen. Dieses erste Tutorial einer vierteiligen Reihe führt Sie durch die Erstellung einer Testumgebung für *diskrete* Erkennungen durch Azure ATP. Die Sicherheitswarnungsumgebung konzentriert sich auf *signaturbasierte* Funktionen von Azure ATP. Die Testumgebung enthält keine erweiterten Verhaltenserkennungen auf Machine Learning-, Benutzer- oder Entitätsbasis, da diese Erkennungen eine Lernphase mit echtem Netzwerkverkehr von bis zu 30 Tagen erfordern. Weitere Informationen über jedes Tutorial dieser Reihe finden Sie unter [Tutorialübersicht: ATP-Sicherheitswarnungsumgebung](atp-playbook-lab-overview.md). 


Inhalt des Tutorials: 

> [!div class="checklist"]
> * Einrichten Ihres Testumgebungsservers und Ihrer Computer
> * Konfigurieren von Active Directory mit Benutzern und Gruppen
> * Einrichten und Konfigurieren von Azure ATP
> * Einrichten lokaler Richtlinien für Ihren Server und Ihre Computer
> * Simulieren eines Helpdeskverwaltungsszenarios mithilfe einer geplanten Aufgabe

## <a name="prerequisites"></a>Voraussetzungen

1. [Ein Testumgebungs-Domänencontroller und zwei Testumgebungs-Arbeitsstationen](#servers-and-computers).
   - Fahren Sie fort, und [aktualisieren Sie Active Directory (AD) mit Benutzern](#bkmk_hydrate).
1. Eine [Azure ATP](install-atp-step1.md)-Instanz, die mit [AD verbunden ist](install-atp-step2.md).
1. [Laden Sie die neueste Version des Azure ATP-Sensors](install-atp-step3.md) auf den Domänencontroller Ihrer Testumgebung herunter, und [installieren](install-atp-step4.md) Sie sie.
1. Vertrautheit mit [Arbeitsstationen mit privilegiertem Zugriff](https://docs.microsoft.com/windows-server/identity/securing-privileged-access/privileged-access-workstations) und [SAMR-Richtlinie](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).

## <a name="recommendations"></a>Empfehlungen

Sie sollten die Setupanweisungen für die Testumgebung genau einhalten. Je mehr Ihre Testumgebung dem vorgeschlagenen Testumgebungssetup entspricht, desto einfacher können Sie die Azure ATP-Testverfahren befolgen. Nachdem das Testumgebungssetup abgeschlossen ist, können Sie Aktionen mit den vorgeschlagenen Hackererforschungstools ausführen und die Azure ATP-Erkennungen dieser Aktionen überprüfen.

Ihr abgeschlossenes Testumgebungssetup sollte dem folgenden Diagramm so ähnlich wie möglich sein:

![Azure ATP-Testumgebungssetup](media/playbook-atp-setup-lab.png)

### <a name="servers-and-computers"></a>Server und Computer

Diese Tabelle enthält ausführliche Informationen zu den Computern und den erforderlichen Konfigurationen. IP-Adressen werden nur zu Referenzzwecken bereitgestellt, damit Sie Sachverhalte leicht nachvollziehen können.

In den Beispielen dieses Tutorials lautet der Gesamtstruktur-NetBIOS-Name **CONTOSO.AZURE**.

|  FQDN | Betriebssystem | IP | Zweck |
|------|-------|---------|--------------|
| ContosoDC.contoso.azure | Windows Server 2012 R2 | 10.0.24.4 | Lokal installierter Domänencontroller mit Azure ATP-Sensor |
| VictimPC.contoso.azure | Windows 10 | 10.0.24.5 |PC des Opfers |
| AdminPC.contoso.azure | Windows 10  | 10.0.24.6 | PC des Domänenadministrators (auch als „Sichere Administratorarbeitsstation“ oder „Privilegierte Administratorarbeitsstation“ bezeichnet) |

### <a name="active-directory-users-and-groups"></a>Active Directory-Benutzer und -Gruppen

In dieser Testumgebung gibt es drei Hauptbenutzer und ein Dienstkonto. Das Dienstkonto ist für Azure ATP bestimmt und wird sowohl für Zwecke der LDAP-Synchronisierung als auch SAMR verwendet.

Es gibt eine „Helpdesk“-Sicherheitsgruppe (SG), der Ron HelpDesk angehört. Diese SG simuliert den Helpdesk. Dieser SG ist ein Gruppenrichtlinienobjekt zugeordnet, das unseren Helpdesk-Mitgliedern lokale Administratorrechte auf den entsprechenden Computern gewährt. Dieses Setup wird verwendet, um ein realistisches Verwaltungsmodell in einer Produktionsumgebung zu simulieren.

| Vollständiger Name    | SAMAccount |Zweck|
|--------------|------------|--------------------------------------------------------------------------------------------------|
| Jeff Leatherman  | JeffL  | Bald Opfer eines unglaublich effektiven Phishingangriffs  |
| Ron HelpDesk  | RonHD  |Ron ist der Ansprechpartner im IT-Team von Contoso. RonHD ist Mitglied der Sicherheitsgruppe „Helpdesk“. |
| Samira Abbasi | SamiraA  | Bei Contoso ist diese Benutzerin unsere Domänenadministratorin. |
| Azure ATP-Dienst | AATPService | Azure ATP-Dienstkonto |

## <a name="azure-atp-base-lab-environment"></a>Azure ATP-Basistestumgebung

Um die Basistestumgebung zu konfigurieren, fügen wir Active Directory Benutzer und Gruppen hinzu, bearbeiten eine SAM-Richtlinie und eine sensible Gruppe in Azure ATP.

### <a name="bkmk_hydrate"></a> Aktualisieren von Active Directory-Benutzern auf ContosoDC

Um die Testumgebung zu vereinfachen, haben wir den Vorgang so automatisiert, dass fiktive Benutzer und Gruppen in Active Directory erstellt werden. Dieses Skript wird als Voraussetzung für dieses Tutorial ausgeführt. Sie können das Skript verwenden oder ändern, um die Active Directory-Umgebung ihrer Testumgebung zu aktualisieren. Wenn Sie kein Skript verwenden möchten, können Sie dies manuell tun.

Führen Sie als Domänenadministrator auf ContosoDC Folgendes aus, um unsere Active Directory-Benutzer zu aktualisieren:

``` PowerShell

# Store the user passwords as variables
$SamiraASecurePass = ConvertTo-SecureString -String 'NinjaCat123' -AsPlainText -Force
$ronHdSecurePass = ConvertTo-SecureString -String 'FightingTiger$' -AsPlainText -Force
$jefflSecurePass = ConvertTo-SecureString -String 'Password$fun' -AsPlainText -Force
$AATPService = ConvertTo-SecureString -String 'Password123!@#' -AsPlainText -Force

# Create new AD user SamiraA and add her to the domain admins group
New-ADUser -Name SamiraA -DisplayName "Samira Abbasi" -PasswordNeverExpires $true -AccountPassword $samiraASecurePass -Enabled $true
Add-ADGroupMember -Identity "Domain Admins" -Members SamiraA

# Create new AD user RonHD, create new Helpdesk SG, add RonHD to the Helpdesk SG
New-ADUser -Name RonHD -DisplayName "Ron Helpdesk" -PasswordNeverExpires $true -AccountPassword $ronHdSecurePass -Enabled $true
New-ADGroup -Name Helpdesk -GroupScope Global -GroupCategory Security
Add-ADGroupMember -Identity "Helpdesk" -Members "RonHD"

# Create new AD user JeffL
New-ADUser -Name JeffL -DisplayName "Jeff Leatherman" -PasswordNeverExpires $true -AccountPassword $jefflSecurePass -Enabled $true

# Take note of the "AATPService" user below which will be our service account for Azure ATP.
# Create new AD user Azure ATP Service

New-ADUser -Name AatpService -DisplayName "Azure ATP/ATA Service" -PasswordNeverExpires $true -AccountPassword $AATPService -Enabled $true

```

### <a name="configure-sam-r-capabilities-from-contosodc"></a>Konfigurieren von SAM-R-Funktionen von ContosoDC

Damit der Azure ATP-Dienst ordnungsgemäß die SAM-R-Enumeration ausführen und Lateral-Movement-Pfade erstellen kann, müssen Sie die SAM-Richtlinie bearbeiten.

1. Sie finden Ihre SAM-Richtlinie unter: **Richtlinien \> Windows-Einstellungen \> Sicherheitseinstellungen \> Lokale Richtlinien \>Sicherheitsoptionen\> „Netzwerkzugriff: Clients einschränken, die Remoteaufrufe an SAM ausführen dürfen“** .

    ![Ändern Sie die Gruppenrichtlinie, damit Azure ATP Lateral-Movement-Pfad-Funktionen nutzen kann.](media/playbook-labsetup-localgrouppolicies3.png)

2. Fügen Sie das Azure ATP-Dienstkonto, AATPService, der Liste von zulässigen Konten hinzu, die diese Aktion auf Ihren modernen Windows-Systemen durchführen können.

    ![Hinzufügen des Diensts](./media/samr-add-service.png)

### <a name="add-sensitive-group-to-azure-atp"></a>Hinzufügen von sensiblen Gruppen zu Azure ATP

Wenn Sie die „Helpdesk“-Sicherheitsgruppe als **sensible Gruppe** hinzufügen, können Sie die Lateral-Movement-Graph-Funktion von Azure ATP verwenden. Das Markieren hoch sensibler Benutzer und Gruppen, die nicht unbedingt Domänenadministratoren sind, jedoch über Berechtigungen für zahlreiche Ressourcen verfügen, ist eine bewährte Methode.

1. Klicken Sie im Azure ATP-Portal in der Menüleiste auf das Zahnrad **Konfiguration**.

2. Klicken Sie unter **Erkennung** auf **Entitätstag**.

    ![Azure ATP-Entitätstags](media/entity-tags.png)

3. Geben Sie im Abschnitt **Sensibel** den Namen „Helpdesk“ für **Sensible Gruppen** ein, und klicken Sie anschließend auf das Zeichen **+** , um diese hinzuzufügen.

    ![Markieren Sie den „Helpdesk“ als sensible Azure ATP-Gruppe, um Lateral-Movement-Diagramme und Berichte für diese privilegierte Gruppe zu aktivieren.](media/playbook-labsetup-helpdesksensitivegroup.png)

4. Klicken Sie auf **Speichern**.

### <a name="azure-atp-lab-base-setup-checklist"></a>Checkliste zur grundlegenden Einrichtung der Azure ATP-Testumgebung

An diesem Punkt sollten Sie über ein Azure ATP-Basistestumgebung verfügen. Azure ATP sollte zur Verwendung bereit und die Benutzer sollten bereitgestellt sein. Überprüfen Sie die Checkliste, um sicherzustellen, dass die Basistestumgebung vollständig ist.  

| Schritt    | Aktion | Status |
|--------------|------------|------------------|
| 1  | Azure ATP-Sensor auf ContosoDC installiert (erforderlicher Schritt)| - [ ] |
| 2  | Benutzer und Gruppen in Active Directory erstellt  | - [ ] |
| 3  | Azure ATP-Dienstkontoberechtigungen für SAMR ordnungsgemäß konfiguriert | - [ ] |
| 4  | Helpdesk-Sicherheitsgruppe als **sensible Gruppe** in Azure ATP hinzugefügt| - [ ] |

## <a name="set-up-the-lab-workstations"></a>Einrichten der Testumgebungs-Arbeitsstationen

Sobald Sie sich vergewissert haben, dass Ihre Azure ATP-Basistestumgebung eingerichtet ist, können Sie die Arbeitsstationskonfiguration in Vorbereitung auf die nächsten drei Tutorials in dieser Reihe beginnen. Wir aktivieren unseren VictimPC und AdminPC, um diese Testumgebung zu aktivieren.

### <a name="victimpc-local-policies"></a>Lokale VictimPC-Richtlinien

Der nächste Schritt für Ihre Testumgebung ist das Vervollständigen der Einrichtung der lokalen Richtlinie. Für **VictimPC** sind sowohl JeffL als auch die Helpdesk-Sicherheitsgruppe Mitglied der lokalen Gruppe „Administrators“. Wie bei vielen Organisationen ist JeffL ein Administrator auf seinem eigenen Gerät, **VictimPC**.

Richten Sie als lokaler Administrator Richtlinien durch Ausführen des automatischen PowerShell-Skripts ein:

``` PowerShell
# Add JeffL to local Administrators group on VictimPC
Add-LocalGroupMember -Group "Administrators" -Member "Contoso\JeffL"
# Add Helpdesk to local Administrators group on VictimPC
Add-LocalGroupMember -Group "Administrators" -Member "Contoso\Helpdesk"
```

Überprüfen Sie die Gruppe „Administrators“ auf **VictimPC**, sodass Sie sicher sind, dass sie mindestens „Helpdesk“ und JeffL als Mitglieder hat:

![„Helpdesk“ und JeffL sollten in der lokalen Administratorengruppe für VictimPC sein.](media/playbook-labsetup-localgrouppolicies2.png)

### <a name="helpdesk-simulation"></a> Simulieren von Helpdesksupport auf VictimPC

Um ein funktionierendes und verwaltetes Netzwerk zu simulieren, erstellen Sie auf **VictimPC** eine geplante Aufgabe zur Ausführung des Prozesses „cmd.exe“ als **RonHD**.

1. Öffnen Sie auf VictimPC ein **PowerShell-Konsolenfenster mit erhöhten Rechten**, und führen Sie den folgenden Befehl aus:

    ``` PowerShell
    $action = New-ScheduledTaskAction -Execute 'cmd.exe'
    $trigger = New-ScheduledTaskTrigger -AtLogOn
    $runAs = 'Contoso\RonHD'
    $ronHHDPass = 'FightingTiger$'
    Register-ScheduledTask -TaskName "RonHD Cmd.exe - AATP SA Playbook" -Trigger $trigger -User $runAs -Password $ronHHDPass -Action $action
    ```

2. Melden Sie sich beim Computer als **JeffL** an. Der Prozess „cmd.exe“ wird im Kontext von RonHD nach der Anmeldung gestartet und simuliert die Verwaltung des Computers durch Helpdesk.

### <a name="turn-off-antivirus-on-victimpc"></a>Deaktivieren von Virenschutzprogrammen auf VictimPC

Deaktivieren Sie für Testzwecke alle Virenschutzprogramme in der Testumgebung. Dadurch wird sichergestellt, dass wir uns während dieser Übungen auf Azure ATP konzentrieren können und nicht auf Techniken zur Virenabwehr.

Einige der Tools im nächsten Abschnitt können Sie erst herunterladen, wenn Sie Virenschutzprogramme deaktivieren. Außerdem müssen Sie die Tools nach dem Deaktivieren von Virenschutzprogrammen erneut herunterladen, wenn Virenschutzprogramme aktiviert sind, nachdem die Angriffstools bereitgestellt wurden.

### <a name="stage-common-hacker-tools"></a>Bereitstellen allgemeiner Hackertools

> [!WARNING]
> Die folgenden Tools sind nur für Forschungszwecke vorgesehen. Microsoft ist **nicht** Besitzer dieser Tools und kann für deren Verhalten nicht garantieren. Diese Tools sollten **nur** in einer Testumgebung ausgeführt werden.

Um die Azure ATP-Sicherheitswarnungs-Playbooks ausführen zu können, sind die folgenden Tools erforderlich.

| Tool | URL |
|----|-----|
| Mimikatz | [GitHub – Mimikatz](https://github.com/gentilkiwi/mimikatz) |
| PowerSploit | [GitHub – PowerSploit](https://github.com/PowerShellMafia/PowerSploit) |
| PsExec | [Microsoft-Dokumentation](https://docs.microsoft.com/sysinternals/downloads/psexec) |
| NetSess | [JoeWare-Tools](https://www.joeware.net/freetools) |

Wir danken den Autoren dieser Forschungstools, dass sie der Community ermöglichen, Cyberrisiken und deren Auswirkungen besser zu verstehen.

### <a name="adminpc-local-policies"></a>Lokale Richtlinien für AdminPC

Für **AdminPC** muss **Helpdesk** der lokalen Gruppe „Administrators“ hinzugefügt werden. Entfernen Sie dann „Domänenadministratoren“ aus der lokalen Gruppe „Administrators“. Dieser Schritt stellt sicher, dass Samira, eine Domänenadministratorin, kein Administrator von AdminPC ist. Dies ist eine bewährte Methode für sichere Anmeldeinformationen. Führen Sie diesen Schritt manuell aus, oder verwenden Sie das bereitgestellte PowerShell-Skript.

1. Fügen Sie **Helpdesk** zu **AdminPC** hinzu, und *entfernen* Sie „Domänenadministratoren“ durch Ausführen des folgenden PowerShell-Skripts aus der lokalen Administratorgruppe:

    ``` PowerShell
   # Add Helpdesk to local Administrators group
   Add-LocalGroupMember -Group "Administrators" -Member "Contoso\Helpdesk"
   # Remove Domain Admins from local Administrators group
   Remove-LocalGroupMember -Group "Administrators" -Member "Domain Admins"

   ```

2. Nach der Ausführung des Skripts befindet sich **Helpdesk** in der lokalen Liste **Administratoren** > **Mitglieder** von **AdminPC**.
![„Helpdesk“ in der lokalen Administratorengruppe für AdminPC](media/playbook-labsetup-localgrouppolicies1.png)

### <a name="simulate-domain-activities-from-adminpc"></a>Simulieren von Domänenaktivitäten von AdminPC

Simulierte Domänenaktivitäten sind von SamiraA erforderlich. Dieser Schritt kann manuell ausgeführt werden, oder verwenden Sie das bereitgestellte PowerShell-Skript. Das PowerShell-Skript greift alle 5 Minuten auf den Domänencontroller zu, und so wird Netzwerkaktivität als Samira simuliert.

Führen Sie als **SamiraA** das folgende Skript in einer PowerShell-Eingabeaufforderung in AdminPC aus:

```PowerShell

while ($true)
{
    Invoke-Expression "dir \\ContosoDC\c$"
    Start-Sleep -Seconds 300
}

```

### <a name="workstation-setup-checklist"></a>Checkliste für das Arbeitsstationssetup

Überprüfen Sie die Checkliste, um sicherzustellen, dass das Arbeitsstationssetup vollständig ist.

| Schritt    | Aktion | Status |
|--------------|------------|------------------|
| 1  | Fügen Sie JeffL und Helpdesk als lokale Administratoren auf VictimPC hinzu. | - [ ] |
| 2  | Erstellen Sie geplante Aufgaben, die als RonHD auf VictimPC ausgeführt werden. | - [ ] |
| 3  | Deaktivieren Sie Virenschutzprogramme auf VictimPC. | - [ ] |
| 4  | Stellen Sie Hackertools auf VictimPC bereit.| - [ ] |
| 5  | Hinzufügen von „Helpdesk“ zur lokalen Gruppe „Administrators“ von AdminPC und Entfernen von Domänenadministratoren daraus| - [ ] |
| 6  | Führen Sie das PowerShell-Skript als Samira aus, um Domänenaktivitäten zu simulieren. | - [ ] |

## <a name="mission-accomplished"></a>Mission erfüllt!

Ihre Azure ATP-Testumgebung ist jetzt einsatzbereit. Bei der Auswahl der in dieser Einrichtung verwendeten Methoden wurde berücksichtigt, dass Ressourcen (von *etwas* oder *jemandem*) verwaltet werden müssen, und die Verwaltung lokale Administratorrechte erfordert. Es gibt andere Möglichkeiten, einen Verwaltungsworkflow in der Testumgebung zu simulieren:

- Protokollieren des ein- und ausgehenden Datenverkehrs von VictimPC mit dem Konto von RonHD
- Hinzufügen einer anderen Version einer geplanten Aufgabe
- Eine RDP-Sitzung
- Ausführen von „runas“ in der Befehlszeile

 Wählen Sie für optimale Ergebnisse eine Simulationsmethode, die Sie in Ihrer Testumgebung durchgängig automatisieren können.


## <a name="next-steps"></a>Nächste Schritte

Testen Sie Ihre Azure ATP-Testumgebung mithilfe der Azure ATP-Sicherheitswarnungsplaybooks für die einzelnen Phasen der Cyberangriffsabwehr-Kette beginnend mit der Reconnaissancephase.  

> [!div class="nextstepaction"]
> [Playbook zu Azure ATP-Reconnaissance](atp-playbook-reconnaissance.md)


## <a name="join-the-community"></a>Beitritt zur Community

Haben Sie weitere Fragen, oder möchten Sie mit anderen über Azure ATP und damit verbundene Sicherheitsaspekte diskutieren? Treten Sie noch heute der [Azure ATP-Community](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) bei!

