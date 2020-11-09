---
title: Tutorial zur Einrichtung eines Labs für Microsoft Defender for Identity-Sicherheitswarnungen
description: In diesem Tutorial richten Sie ein Microsoft Defender for Identity-Testlab ein, um Bedrohungen zu simulieren, die von Microsoft Defender for Identity erkannt werden sollen.
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 8adbc288f2512b6322797931b8fcb2a17649e8a4
ms.sourcegitcommit: 8cb9839a67fce42921f7a24564fddf15e503bdea
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93278613"
---
# <a name="tutorial-setup-a-product-long-security-alert-lab"></a>Tutorial: Einrichten eines Labs für [!INCLUDE [Product long](includes/product-long.md)]-Sicherheitswarnungen

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Das Lab zu [!INCLUDE [Product long](includes/product-long.md)]-Sicherheitswarnungen soll die Funktionen von **[!INCLUDE [Product short](includes/product-short.md)]** zum Identifizieren und Erkennen verdächtiger Aktivitäten und potenzieller Angriffe auf Ihr Netzwerk veranschaulichen. Dieses erste Tutorial einer vierteiligen Reihe führt Sie durch die Erstellung einer Labumgebung für *diskrete* Erkennungen durch [!INCLUDE [Product short](includes/product-short.md)]. In diesem Lab für Sicherheitswarnungen geht es primär um die *signaturbasierten* Funktionen von [!INCLUDE [Product short](includes/product-short.md)]. Die Testumgebung enthält keine erweiterten Verhaltenserkennungen auf Machine Learning-, Benutzer- oder Entitätsbasis, da diese Erkennungen eine Lernphase mit echtem Netzwerkverkehr von bis zu 30 Tagen erfordern. Weitere Informationen zu den einzelnen Tutorials dieser Reihe finden Sie unter [Tutorialübersicht: [!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnungsumgebung](playbook-lab-overview.md).

In diesem Lernprogramm führen Sie folgende Schritte aus:

> [!div class="checklist"]
>
> - Einrichten Ihres Testumgebungsservers und Ihrer Computer
> - Konfigurieren von Active Directory mit Benutzern und Gruppen
> - Einrichten und Konfigurieren von [!INCLUDE [Product short](includes/product-short.md)]
> - Einrichten lokaler Richtlinien für Ihren Server und Ihre Computer
> - Simulieren eines Helpdeskverwaltungsszenarios mithilfe einer geplanten Aufgabe

## <a name="prerequisites"></a>Voraussetzungen

1. [Ein Testumgebungs-Domänencontroller und zwei Testumgebungs-Arbeitsstationen](#servers-and-computers).
    - Fahren Sie fort, und [aktualisieren Sie Active Directory (AD) mit Benutzern](#bkmk_hydrate).

1. Eine [[!INCLUDE [Product short](includes/product-short.md)]-Instanz,](install-step1.md) die [mit AD verbunden](install-step2.md) ist.
1. Sie müssen die neueste Version des [!INCLUDE [Product short](includes/product-short.md)]-Sensors auf den Domänencontroller Ihres Labs [herunterladen](install-step3.md) und [installieren](install-step4.md).
1. Vertrautheit mit [Arbeitsstationen mit privilegiertem Zugriff](/windows-server/identity/securing-privileged-access/privileged-access-workstations) und [SAMR-Richtlinie](/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).

## <a name="recommendations"></a>Empfehlungen

Sie sollten die Setupanweisungen für die Testumgebung genau einhalten. Je genauer Ihr Lab dem vorgeschlagenen Labsetup entspricht, desto einfacher können Sie die [!INCLUDE [Product short](includes/product-short.md)]-Testverfahren befolgen. Nachdem das Lab eingerichtet ist, können Sie Aktionen mit den vorgeschlagenen Tools zur Erforschung von Hackerangriffen ausführen und die [!INCLUDE [Product short](includes/product-short.md)]-Erkennungen dieser Aktionen überprüfen.

Ihr abgeschlossenes Testumgebungssetup sollte dem folgenden Diagramm so ähnlich wie möglich sein:

![Setup des [!INCLUDE [Product short](includes/product-short.md)]-Testlabs](media/playbook-setup-lab.png)

### <a name="servers-and-computers"></a>Server und Computer

Diese Tabelle enthält ausführliche Informationen zu den Computern und den erforderlichen Konfigurationen. IP-Adressen werden nur zu Referenzzwecken bereitgestellt, damit Sie Sachverhalte leicht nachvollziehen können.

In den Beispielen dieses Tutorials lautet der Gesamtstruktur-NetBIOS-Name **CONTOSO.AZURE**.

| FQDN | OS | IP | Zweck |
|------|-------|---------|--------------|
| ContosoDC.contoso.azure | Windows Server 2012 R2 | 10.0.24.4 | Domänencontroller mit lokal installiertem [!INCLUDE [Product short](includes/product-short.md)]-Sensor |
| VictimPC.contoso.azure | Windows 10 | 10.0.24.5 |PC des Opfers |
| AdminPC.contoso.azure | Windows 10  | 10.0.24.6 | PC des Domänenadministrators (auch als „Sichere Administratorarbeitsstation“ oder „Privilegierte Administratorarbeitsstation“ bezeichnet) |

### <a name="active-directory-users-and-groups"></a>Active Directory-Benutzer und -Gruppen

In dieser Testumgebung gibt es drei Hauptbenutzer und ein Dienstkonto. Das Dienstkonto ist für [!INCLUDE [Product short](includes/product-short.md)] bestimmt und wird sowohl zur LDAP-Synchronisierung als auch für SAMR verwendet.

Es gibt eine Sicherheitsgruppe namens „Helpdesk“, der Ron HelpDesk angehört. Diese SG simuliert den Helpdesk. Dieser SG ist ein Gruppenrichtlinienobjekt zugeordnet, das unseren Helpdesk-Mitgliedern lokale Administratorrechte auf den entsprechenden Computern gewährt. Dieses Setup wird verwendet, um ein realistisches Verwaltungsmodell in einer Produktionsumgebung zu simulieren.

| Vollständig | Vollständiger Name | SAMAccount | Zweck |
|--|--|--|
| Jeff Leatherman | JeffL | Bald Opfer eines unglaublich effektiven Phishingangriffs |
| Ron HelpDesk | RonHD | Ron ist der Ansprechpartner im IT-Team von Contoso. RonHD ist Mitglied der Sicherheitsgruppe „Helpdesk“. |
| Samira Abbasi | SamiraA | Bei Contoso ist diese Benutzerin unsere Domänenadministratorin. |
| [!INCLUDE [Product short](includes/product-short.md)] Dienst | AATPService | Dienstkonto von [!INCLUDE [Product short](includes/product-short.md)] | account |

## <a name="product-short-base-lab-environment"></a>Grundlegendes Testlab von [!INCLUDE [Product short](includes/product-short.md)]

Um das Basislab zu konfigurieren, fügen wir Active Directory Benutzer und Gruppen hinzu und bearbeiten eine SAM-Richtlinie sowie eine vertrauliche Gruppe in [!INCLUDE [Product short](includes/product-short.md)].

### <a name="hydrate-active-directory-users-on-contosodc"></a><a name="bkmk_hydrate"></a> Aktualisieren von Active Directory-Benutzern auf ContosoDC

Um die Testumgebung zu vereinfachen, haben wir den Vorgang so automatisiert, dass fiktive Benutzer und Gruppen in Active Directory erstellt werden. Dieses Skript wird als Voraussetzung für dieses Tutorial ausgeführt. Sie können das Skript verwenden oder ändern, um die Active Directory-Umgebung ihrer Testumgebung zu aktualisieren. Wenn Sie kein Skript verwenden möchten, können Sie dies manuell tun.

Führen Sie als Domänenadministrator auf ContosoDC Folgendes aus, um unsere Active Directory-Benutzer zu aktualisieren:

```powerShell
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

# Take note of the "AATPService" user below which will be our service account for [!INCLUDE [Product short](includes/product-short.md)].
# Create new AD user [!INCLUDE [Product short](includes/product-short.md)] Service

New-ADUser -Name AatpService -DisplayName "Azure ATP/ATA Service" -PasswordNeverExpires $true -AccountPassword $AATPService -Enabled $true
```

### <a name="configure-sam-r-capabilities-from-contosodc"></a>Konfigurieren von SAM-R-Funktionen von ContosoDC

Damit der [!INCLUDE [Product short](includes/product-short.md)]-Dienst ordnungsgemäß die SAM-R-Enumeration ausführen und Lateral Movement-Pfade erstellen kann, müssen Sie die SAM-Richtlinie bearbeiten.

1. Sie finden Ihre SAM-Richtlinie unter: **Richtlinien \> Windows-Einstellungen \> Sicherheitseinstellungen \> Lokale Richtlinien \> Sicherheitsoptionen \> „Netzwerkzugriff: Clients einschränken, die Remoteaufrufe an SAM ausführen dürfen“** .

    ![Ändern Sie die Gruppenrichtlinie, um [!INCLUDE [Product short](includes/product-short.md)] die Verwendung der Funktionen für den Lateral Movement-Pfad zu gestatten.](media/playbook-labsetup-localgrouppolicies3.png)

1. Fügen Sie das [!INCLUDE [Product short](includes/product-short.md)]-Dienstkonto (AATPService) der Liste zulässiger Konten hinzu, die diese Aktion auf Ihren modernen Windows-Systemen ausführen können.

    ![Hinzufügen des Diensts](media/samr-add-service.png)

### <a name="add-sensitive-group-to-product-short"></a>Hinzufügen von vertraulichen Gruppen zu [!INCLUDE [Product short](includes/product-short.md)]

Wenn Sie die Sicherheitsgruppe „Helpdesk“ als **vertrauliche Gruppe** hinzufügen, können Sie das [!INCLUDE [Product short](includes/product-short.md)]-Feature für Lateral Movement-Diagramme verwenden. Das Markieren hoch sensibler Benutzer und Gruppen, die nicht unbedingt Domänenadministratoren sind, jedoch über Berechtigungen für zahlreiche Ressourcen verfügen, ist eine bewährte Methode.

1. Wählen Sie im [!INCLUDE [Product short](includes/product-short.md)]-Portal **Konfiguration** aus.

1. Klicken Sie unter **Erkennung** auf **Entitätstag**.

    ![[!INCLUDE [Product short](includes/product-short.md)]-Entitätstags](media/entity-tags.png)
1. Geben Sie im Abschnitt **Sensibel** den Namen „Helpdesk“ für **Sensible Gruppen** ein, und klicken Sie anschließend auf das Zeichen **+** , um diese hinzuzufügen.
    ![Markieren von „Helpdesk“ als vertrauliche [!INCLUDE [Product short](includes/product-short.md)]-Gruppe, um Lateral Movement-Diagramme und Berichte für diese berechtigte Gruppe zu aktivieren](media/playbook-labsetup-helpdesksensitivegroup.png)
1. Klicken Sie auf **Speichern**.

### <a name="product-short-lab-base-setup-checklist"></a>Checkliste zur grundlegenden Einrichtung des [!INCLUDE [Product short](includes/product-short.md)]-Labs

An diesem Punkt sollten Sie über ein grundlegendes [!INCLUDE [Product short](includes/product-short.md)]-Lab verfügen. [!INCLUDE [Product short](includes/product-short.md)] sollte zur Verwendung bereit und die Benutzer sollten bereitgestellt sein. Überprüfen Sie die Checkliste, um sicherzustellen, dass die Basistestumgebung vollständig ist.

| Schritt  | Schritt | Aktion | Status |
|--|--|--|
| 1 | [!INCLUDE [Product short](includes/product-short.md)]-Sensor auf ContosoDC installiert (erforderlicher Schritt) | - [ ] |
| 2 | Benutzer und Gruppen in Active Directory erstellt | - [ ] |
| 3 | [!INCLUDE [Product short](includes/product-short.md)]-Dienstkontoberechtigungen für SAMR ordnungsgemäß konfiguriert | - [ ] |
| 4 | Sicherheitsgruppe „Helpdesk“ als **vertrauliche Gruppe** in [!INCLUDE [Product short](includes/product-short.md)] hinzugefügt | - [ ] |](includes/product-other.md)]| - [ ] |

## <a name="set-up-the-lab-workstations"></a>Einrichten der Testumgebungs-Arbeitsstationen

Nachdem Sie sich vergewissert haben, dass Ihr grundlegendes [!INCLUDE [Product short](includes/product-short.md)]-Lab eingerichtet ist, können Sie zur Vorbereitung auf die nächsten drei Tutorials in dieser Reihe mit der Konfiguration der Arbeitsstation beginnen. Wir aktivieren unseren VictimPC und AdminPC, um diese Testumgebung zu aktivieren.

### <a name="victimpc-local-policies"></a>Lokale VictimPC-Richtlinien

Der nächste Schritt für Ihre Testumgebung ist das Vervollständigen der Einrichtung der lokalen Richtlinie. Für **VictimPC** sind sowohl JeffL als auch die Helpdesk-Sicherheitsgruppe Mitglied der lokalen Gruppe „Administrators“. Wie bei vielen Organisationen ist JeffL ein Administrator auf seinem eigenen Gerät, **VictimPC**.

Richten Sie als lokaler Administrator Richtlinien durch Ausführen des automatischen PowerShell-Skripts ein:

```powerShell
# Add JeffL to local Administrators group on VictimPC
Add-LocalGroupMember -Group "Administrators" -Member "Contoso\JeffL"
# Add Helpdesk to local Administrators group on VictimPC
Add-LocalGroupMember -Group "Administrators" -Member "Contoso\Helpdesk"
```

Überprüfen Sie die Gruppe „Administrators“ auf **VictimPC** , sodass Sie sicher sind, dass sie mindestens „Helpdesk“ und JeffL als Mitglieder hat:

![„Helpdesk“ und JeffL sollten in der lokalen Administratorengruppe für VictimPC sein.](media/playbook-labsetup-localgrouppolicies2.png)

### <a name="simulate-helpdesk-support-on-victimpc"></a><a name="helpdesk-simulation"></a> Simulieren von Helpdesksupport auf VictimPC

Um ein funktionierendes und verwaltetes Netzwerk zu simulieren, erstellen Sie auf **VictimPC** eine geplante Aufgabe zur Ausführung des Prozesses „cmd.exe“ als **RonHD**.

1. Öffnen Sie auf VictimPC ein **PowerShell-Konsolenfenster mit erhöhten Rechten** , und führen Sie den folgenden Befehl aus:

    ```powerShell
    $action = New-ScheduledTaskAction -Execute 'cmd.exe'
    $trigger = New-ScheduledTaskTrigger -AtLogOn
    $runAs = 'Contoso\RonHD'
    $ronHHDPass = 'FightingTiger$'
    Register-ScheduledTask -TaskName "RonHD Cmd.exe - AATP SA Playbook" -Trigger $trigger -User $runAs -Password $ronHHDPass -Action $action
    ```

1. Melden Sie sich beim Computer als **JeffL** an. Der Prozess „cmd.exe“ wird im Kontext von RonHD nach der Anmeldung gestartet und simuliert die Verwaltung des Computers durch Helpdesk.

### <a name="turn-off-antivirus-on-victimpc"></a>Deaktivieren von Virenschutzprogrammen auf VictimPC

Deaktivieren Sie für Testzwecke alle Virenschutzprogramme in der Testumgebung. So ist sichergestellt, dass wir uns während dieser Übungen auf [!INCLUDE [Product short](includes/product-short.md)] konzentrieren können und uns nicht mit Techniken zur Virenabwehr beschäftigen müssen.

Einige der Tools im nächsten Abschnitt können Sie erst herunterladen, wenn Sie Virenschutzprogramme deaktivieren. Außerdem müssen Sie die Tools nach dem Deaktivieren von Virenschutzprogrammen erneut herunterladen, wenn Virenschutzprogramme aktiviert sind, nachdem die Angriffstools bereitgestellt wurden.

### <a name="stage-common-hacker-tools"></a>Bereitstellen allgemeiner Hackertools

> [!WARNING]
> Die folgenden Tools sind nur für Forschungszwecke vorgesehen. Microsoft ist **nicht** Besitzer dieser Tools und kann für deren Verhalten nicht garantieren. Diese Tools sollten **nur** in einer Testumgebung ausgeführt werden.

Zur Ausführung der Playbooks zu [!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnungen sind die folgenden Tools erforderlich.

| Tool | URL |
|----|-----|
| Mimikatz | [GitHub – Mimikatz](https://github.com/gentilkiwi/mimikatz) |
| PowerSploit | [GitHub – PowerSploit](https://github.com/PowerShellMafia/PowerSploit) |
| PsExec | [Microsoft Docs](/sysinternals/downloads/psexec) |
| NetSess | [JoeWare-Tools](https://www.joeware.net/freetools) |

Wir danken den Autoren dieser Forschungstools, dass sie der Community ermöglichen, Cyberrisiken und deren Auswirkungen besser zu verstehen.

### <a name="adminpc-local-policies"></a>Lokale Richtlinien für AdminPC

Für **AdminPC** muss **Helpdesk** der lokalen Gruppe „Administrators“ hinzugefügt werden. Entfernen Sie dann „Domänenadministratoren“ aus der lokalen Gruppe „Administrators“. Dieser Schritt stellt sicher, dass Samira, eine Domänenadministratorin, kein Administrator von AdminPC ist. Dies ist eine bewährte Methode für sichere Anmeldeinformationen. Führen Sie diesen Schritt manuell aus, oder verwenden Sie das bereitgestellte PowerShell-Skript.

1. Fügen Sie **Helpdesk** zu **AdminPC** hinzu, und *entfernen* Sie „Domänenadministratoren“ durch Ausführen des folgenden PowerShell-Skripts aus der lokalen Administratorgruppe:

    ```powerShell
    # Add Helpdesk to local Administrators group
    Add-LocalGroupMember -Group "Administrators" -Member "Contoso\Helpdesk"
    # Remove Domain Admins from local Administrators group
    Remove-LocalGroupMember -Group "Administrators" -Member "Domain Admins"
    ```

1. Nach der Ausführung des Skripts befindet sich **Helpdesk** in der lokalen Liste **Administratoren** > **Mitglieder** von **AdminPC**.
![„Helpdesk“ in der lokalen Administratorengruppe für AdminPC](media/playbook-labsetup-localgrouppolicies1.png)

### <a name="simulate-domain-activities-from-adminpc"></a>Simulieren von Domänenaktivitäten von AdminPC

Simulierte Domänenaktivitäten sind von SamiraA erforderlich. Dieser Schritt kann manuell ausgeführt werden, oder verwenden Sie das bereitgestellte PowerShell-Skript. Das PowerShell-Skript greift alle 5 Minuten auf den Domänencontroller zu, und so wird Netzwerkaktivität als Samira simuliert.

Führen Sie als **SamiraA** das folgende Skript in einer PowerShell-Eingabeaufforderung in AdminPC aus:

```powerShell
while ($true)
{
    Invoke-Expression "dir \\ContosoDC\c$"
    Start-Sleep -Seconds 300
}
```

### <a name="workstation-setup-checklist"></a>Checkliste für das Arbeitsstationssetup

Überprüfen Sie die Checkliste, um sicherzustellen, dass das Arbeitsstationssetup vollständig ist.

| Schritt | Reagieren| Schritt | Aktion | Status |
|--|--|--|
| 1 | Fügen Sie JeffL und Helpdesk als lokale Administratoren auf VictimPC hinzu. | - [ ] |
| 2 | Erstellen Sie geplante Aufgaben, die als RonHD auf VictimPC ausgeführt werden. | - [ ] |
| 3 | Deaktivieren Sie Virenschutzprogramme auf VictimPC. | - [ ] |
| 4 | Stellen Sie Hackertools auf VictimPC bereit. | - [ ] |
| 5 | Hinzufügen von „Helpdesk“ zur lokalen Gruppe „Administrators“ von AdminPC und Entfernen von Domänenadministratoren daraus | - [ ] |
| 6 | Führen Sie das PowerShell-Skript als Samira aus, um Domänenaktivitäten zu simulieren. | - [ ] |Ausführen des PowerShell-Skripts als Samira zum Simulieren von Domänenaktivitäten | - [ ] |

## <a name="mission-accomplished"></a>Mission erfüllt!

Ihr [!INCLUDE [Product short](includes/product-short.md)]-Lab ist jetzt einsatzbereit. Bei der Auswahl der in dieser Einrichtung verwendeten Methoden wurde berücksichtigt, dass Ressourcen (von *etwas* oder *jemandem* ) verwaltet werden müssen, und die Verwaltung lokale Administratorrechte erfordert. Es gibt andere Möglichkeiten, einen Verwaltungsworkflow in der Testumgebung zu simulieren:

- Protokollieren des ein- und ausgehenden Datenverkehrs von VictimPC mit dem Konto von RonHD
- Hinzufügen einer anderen Version einer geplanten Aufgabe
- Eine RDP-Sitzung
- Ausführen von „runas“ in der Befehlszeile

Wählen Sie für optimale Ergebnisse eine Simulationsmethode, die Sie in Ihrer Testumgebung durchgängig automatisieren können.

## <a name="next-steps"></a>Nächste Schritte

Testen Sie Ihre [!INCLUDE [Product short](includes/product-short.md)]-Labumgebung mithilfe der [!INCLUDE [Product short](includes/product-short.md)]-Playbooks zu Sicherheitswarnungen für die einzelnen Phasen der „Kill Chain“ für Cyberangriffe. Beginnen Sie mit der Reconnaissancephase.

> [!div class="nextstepaction"]
> [Playbook zur [!INCLUDE [Product short](includes/product-short.md)]-Reconnaissance](playbook-reconnaissance.md)

## <a name="join-the-community"></a>Beitritt zur Community

Haben Sie weitere Fragen, oder möchten Sie mit anderen über [!INCLUDE [Product short](includes/product-short.md)] und damit verbundene Sicherheitsaspekte diskutieren? Treten Sie noch heute der [[!INCLUDE [Product short](includes/product-short.md)]Community](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) bei.
