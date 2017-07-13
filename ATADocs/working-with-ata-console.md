---
title: Verstehen der Advanced Threat Analytics-Konsole | Microsoft-Dokumentation
description: Beschreibt die Anmeldung bei der ATA-Konsole sowie die Komponenten der Konsole.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/2/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1bf264d9-9697-44b5-9533-e1c498da4f07
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 3d687087dd9e1ae7f7642f9fdd7d89420f3bec27
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
*Gilt für: Advanced Threat Analytics Version 1.8*



# Arbeiten mit der ATA-Konsole
<a id="working-with-the-ata-console" class="xliff"></a>

Verwenden Sie die ATA-Konsole, um die von ATA erkannten verdächtigen Aktivitäten zu überwachen und darauf zu reagieren.

Das Eingeben der ?-Taste stellt die Tastenkombinationen für den Zugriff auf das ATA-Portal bereit. 

## Aktivieren des Zugriffs auf die ATA-Konsole
<a id="enabling-access-to-the-ata-console" class="xliff"></a>
Sie müssen sich mit einem Benutzer anmelden, dem die richtige ATA-Rolle für den Zugriff auf die ATA-Konsole zugewiesen wurde, damit die Anmeldung auf der Konsole erfolgreich verläuft. Weitere Informationen zur rollenbasierten Zugriffssteuerung (role-based access control; RBAC) in ATA finden Sie unter [Working with ATA role groups](ata-role-groups.md) (Arbeiten mit ATA-Rollengruppen).

## Anmelden bei der ATA-Konsole
<a id="logging-into-the-ata-console" class="xliff"></a>

1. Klicken Sie auf dem Desktop des ATA Center-Servers auf das Symbol für die **Microsoft ATA-Konsole**, oder öffnen Sie einen Browser, und navigieren Sie zur ATA-Konsole.

    ![Symbol für den ATA-Server](media/ata-server-icon.png)

>[!NOTE]
> Sie können auch entweder in ATA Center oder auf dem ATA-Gateway einen Browser öffnen und zu der IP-Adresse navigieren, die Sie während der ATA Center-Installation für die ATA-Konsole konfiguriert haben.    

2.  Wenn der Computer, auf dem ATA Center installiert ist, und der Computer, von dem aus Sie versuchen, auf die ATA-Konsole zuzugreifen, beide zu einer Domäne gehören, unterstützt ATA das einmalige Anmelden, das in der Windows-Authentifizierung integriert ist. Sollten sie sich bereits an Ihrem Computer angemeldet haben, verwendet ATA dieses Token, um sich bei der ATA-Konsole anzumelden. Sie können sich auch mit einer Smartcard anmelden. Ihre Berechtigungen in ATA entsprechen dann Ihrer [Administratorrolle](ata-role-groups.md).

> [!NOTE]
> Stellen Sie sicher, dass Sie sich an dem Computer anmelden, von dem aus Sie auf die ATA-Konsole zugreifen möchten. Verwenden Sie hierzu Ihren ATA-Administratorbenutzernamen und das dazugehörige Kennwort. Alternativ können Sie Ihren Browser als ein anderer Benutzer ausführen oder sich von Windows abmelden und danach mit Ihrem ATA-Administratorbenutzerkonto anmelden. Um die ATA-Konsole aufzufordern, nach Anmeldeinformationen zu fragen, greifen Sie mithilfe einer IP-Adresse auf die Konsole zu, und Sie werden aufgefordert, Anmeldeinformationen einzugeben.

Stellen Sie bei der Anmeldung mit SSO sicher, dass der Standort der ATA-Konsole als lokale Intranetsite in Ihrem Browser definiert ist, und dass Sie auf diese mit einem Kurznamen oder einem Localhost zugreifen.

> [!NOTE]
> Zusätzlich zum Protokollieren jeder verdächtigen Aktivität und Integritätswarnung wird jede Konfigurationsänderung, die Sie in der ATA-Konsole vornehmen, im Windows-Ereignisprotokoll auf dem ATA Center-Computer unter **Applications and services log** (Protokoll für Anwendungen und Dienste) und dann unter **Microsoft ATA** überprüft. Es wird ebenso jede Anmeldung bei der ATA-Konsole überprüft.<br></br>  Eine Konfiguration, die das ATA-Gateway betrifft, wird auch im Windows-Ereignisprotokoll des ATA-Gateway-Computers protokolliert. 



## Die ATA-Konsole
<a id="the-ata-console" class="xliff"></a>

Die ATA-Konsole stellt Ihnen einen schnellen Überblick über alle verdächtigen Aktivitäten in zeitlicher Reihenfolge zur Verfügung. Sie ermöglicht es Ihnen, sich die Details einer Aktivität anzusehen und Aktionen entsprechend der jeweiligen Aktivität auszuführen. Die Konsole zeigt außerdem Warnungen und Benachrichtigungen an, um Probleme mit dem ATA-Netzwerk oder neue Aktivitäten hervorzuheben, die als verdächtig eingestuft werden.

Dies sind die wichtigsten Elemente der ATA-Konsole.


### Angriffszeitachse
<a id="attack-time-line" class="xliff"></a>

Dies ist die Standardzielseite, auf die Sie gelangen, wenn Sie sich bei der ATA-Konsole anmelden. Standardmäßig werden alle offenen verdächtigen Aktivitäten auf der Angriffszeitachse angezeigt. Sie können die Angriffszeitachse filtern, um alle verdächtigen Aktivitäten bzw. offene, verworfene oder aufgelöste verdächtige Aktivitäten anzuzeigen. Außerdem wird der Schweregrad angezeigt, der den einzelnen Aktivitäten zugewiesen wurde.

![Abbildung der Angriffszeitachse in ATA](media/ATA-Suspicious-Activity-Timeline.jpg)

Weitere Informationen finden Sie unter [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md).

### Benachrichtigungsleiste
<a id="notification-bar" class="xliff"></a>

Wenn eine neue verdächtige Aktivität erkannt wurde, wird auf der rechten Seite automatisch die Benachrichtigungsleiste geöffnet. Wenn seit Ihrer letzten Anmeldung neue verdächtige Aktivitäten erkannt wurden, wird die Benachrichtigungsleiste geöffnet, nachdem Sie sich erfolgreich angemeldet haben. Sie können jederzeit auf den Pfeil auf der rechten Seite klicken, um auf die Benachrichtigungsleiste zuzugreifen.

![Abbildung der ATA-Benachrichtigungsleiste](media/notification-bar-1.7.png)

### Filterbereich
<a id="filtering-panel" class="xliff"></a>

Sie können basierend auf Status und Schweregrad filtern, welche verdächtigen Aktivitäten auf der Angriffszeitachse oder auf der Registerkarte für verdächtige Aktivitäten des Entitätsprofils angezeigt werden.

### Suchleiste
<a id="search-bar" class="xliff"></a>

Im obersten Menü finden Sie eine Suchleiste. Sie können nach einem bestimmten Benutzer, einem Computer oder Gruppen in ATA suchen. Beginnen Sie als Versuch einfach mit der Eingabe.

![Abbildung der Suche in der ATA-Konsole](media/ATA-console-search.png)

### Integritätscenter
<a id="health-center" class="xliff"></a>

Das Integritätscenter warnt Sie, wenn in Ihrer ATA-Bereitstellung etwas nicht ordnungsgemäß funktioniert.

![Abbildung des ATA-Integritätscenters](media/ATA-Health-Issue.jpg)

Jedes Mal, wenn auf Ihrem System ein Problem auftritt, z. B. ein Verbindungsfehler oder ein getrenntes ATA-Gateway, können Sie dies am Symbol für das Integritätscenter erkennen, auf dem ein roter Punkt angezeigt wird. ![Abbildung des roten Punkts auf dem Symbol für das ATA-Integritätscenter](media/ATA-Health-Center-Alert-red-dot.png)

Warnungen des Integritätscenters können verworfen oder aufgelöst werden, und sie sind in Abhängigkeit von ihrem Schweregrad als „Hoch“, „Mittel“ oder „Niedrig“ kategorisiert. Wenn Sie eine Warnung auflösen, die vom ATA-Dienst als noch aktiv erkannt wird, wird sie automatisch in die Liste der offenen Warnungen verschoben. Wenn das System erkennt, dass für eine Warnung keine Ursache mehr vorliegt (die Situation wurde behoben), wird sie automatisch in die Liste der aufgelösten Warnungen verschoben.

### Benutzer- und Computerprofil
<a id="user-and-computer-profiles" class="xliff"></a>

ATA erstellt ein Profil für jeden Benutzer und Computer im Netzwerk. Im Benutzerprofil zeigt ATA allgemeine Informationen an, z. B. die Gruppenmitgliedschaft, kürzliche Anmeldungen und Ressourcen, auf die kürzlich zugegriffen wurde. Es wird auch eine Liste der Orte bereitgestellt, wo der Benutzer über VPN eine Verbindung hergestellt hat. Eine Liste der Gruppenmitgliedschaften, die ATA als sensibel einstuft, finden Sie unten.

![Benutzerprofil](media/user-profile.png)

Im Computerprofil zeigt ATA allgemeine Informationen an, z.B. kürzliche Anmeldungen und Ressourcen, auf die kürzlich zugegriffen wurde.

![Computerprofil](media/computer-profile.png)

ATA stellt auf folgenden Seiten zusätzliche Informationen zu Entitäten (Computer, Geräte, Benutzer) bereit: „Zusammenfassung“, „Aktivitäten“ und „Verdächtige Aktivitäten“.

Ein Profil, das ATA nicht vollständig auflösen konnte, wird durch das Symbol eines halb gefüllten Kreises gekennzeichnet.


![Abbildung eines nicht aufgelösten Profils in ATA](media/ATA-Unresolved-Profile.jpg)

### Sensible Gruppen
<a id="sensitive-groups" class="xliff"></a>

Die folgende Liste von Gruppen werden von ATA als **sensibel** eingestuft. Das sind Gruppen, die als Besitzer administrativer Privilegien gekennzeichnet werden und die Warnungen ausgeben, die mit sensiblen Konten übereinstimmen:

- Domänencontroller der Organisation ohne Schreibzugriff 
- Domänen-Admins 
- Domänencontroller 
- Schema-Admins
- Organisations-Admins 
- Gruppenrichtlinienersteller-Besitzer 
- Schreibgeschützter Domänencontroller 
- Administratoren  
- Hauptbenutzer  
- Konten-Operatoren  
- Server-Operatoren   
- Druck-Operatoren
- Sicherungsoperatoren
- Replikatoren 
- Remotedesktopbenutzer 
- Netzwerkkonfigurations-Operatoren 
- Eingehende Gesamtstruktur-Vertrauensstellung 
- DNS-Administratoren 


### Miniprofil
<a id="mini-profile" class="xliff"></a>

An jeder Stelle in der Konsole, an der eine einzelne Entität angezeigt wird, z. B. ein Benutzer oder ein Computer, wird automatisch ein Miniprofil geöffnet, wenn Sie mit der Maus auf die Entität zeigen. Das Miniprofil enthält die folgenden Informationen (sofern verfügbar):

![Abbildung des ATA-Miniprofils](media/ATA-mini-profile.jpg)

-   Name

-   Bild

-   E-Mail

-   Telefon

-   Anzahl der verdächtigen Aktivitäten nach Schweregrad



## Weitere Informationen
<a id="see-also" class="xliff"></a>
[Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
