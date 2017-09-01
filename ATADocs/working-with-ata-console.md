---
title: Verstehen der Advanced Threat Analytics-Konsole | Microsoft-Dokumentation
description: Beschreibt die Anmeldung bei der ATA-Konsole sowie die Komponenten der Konsole.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 8/28/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1bf264d9-9697-44b5-9533-e1c498da4f07
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 793273aeea3c78b54d4dc189acaff9bdf8ae58f9
ms.sourcegitcommit: 46dd0e695f16a0dd23bbfa140eba15ea6a34d7af
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2017
---
*Gilt für: Advanced Threat Analytics Version 1.8*



# <a name="working-with-the-ata-console"></a>Arbeiten mit der ATA-Konsole

Verwenden Sie die ATA-Konsole, um die von ATA erkannten verdächtigen Aktivitäten zu überwachen und darauf zu reagieren.

Das Eingeben der ?-Taste stellt die Tastenkombinationen für den Zugriff auf das ATA-Portal bereit. 

## <a name="enabling-access-to-the-ata-console"></a>Aktivieren des Zugriffs auf die ATA-Konsole
Sie müssen sich mit einem Benutzer anmelden, dem die richtige ATA-Rolle für den Zugriff auf die ATA-Konsole zugewiesen wurde, damit die Anmeldung auf der Konsole erfolgreich verläuft. Weitere Informationen zur rollenbasierten Zugriffssteuerung (role-based access control; RBAC) in ATA finden Sie unter [Working with ATA role groups](ata-role-groups.md) (Arbeiten mit ATA-Rollengruppen).

## <a name="logging-into-the-ata-console"></a>Anmelden bei der ATA-Konsole

>[!NOTE]
 > Ab ATA 1.8 erfolgt die Anmeldung in der ATA-Konsole über das einmalige Anmelden.

1. Klicken Sie auf dem Desktop des ATA Center-Servers auf das Symbol für die **Microsoft ATA-Konsole**, oder öffnen Sie einen Browser, und navigieren Sie zur ATA-Konsole.

    ![Symbol für den ATA-Server](media/ata-server-icon.png)

 >[!NOTE]
 > Sie können auch entweder in ATA Center oder auf dem ATA-Gateway einen Browser öffnen und zu der IP-Adresse navigieren, die Sie während der ATA Center-Installation für die ATA-Konsole konfiguriert haben.    

2.  Wenn der Computer, auf dem ATA Center installiert ist, und der Computer, von dem aus Sie versuchen, auf die ATA-Konsole zuzugreifen, beide zu einer Domäne gehören, unterstützt ATA das einmalige Anmelden, das in der Windows-Authentifizierung integriert ist. Sollten sie sich bereits an Ihrem Computer angemeldet haben, verwendet ATA dieses Token, um sich bei der ATA-Konsole anzumelden. Sie können sich auch mit einer Smartcard anmelden. Ihre Berechtigungen in ATA entsprechen dann Ihrer [Administratorrolle](ata-role-groups.md).

 > [!NOTE]
 > Stellen Sie sicher, dass Sie sich an dem Computer anmelden, von dem aus Sie auf die ATA-Konsole zugreifen möchten. Verwenden Sie hierzu Ihren ATA-Administratorbenutzernamen und das dazugehörige Kennwort. Alternativ können Sie Ihren Browser als ein anderer Benutzer ausführen oder sich von Windows abmelden und danach mit Ihrem ATA-Administratorbenutzerkonto anmelden. Um die ATA-Konsole aufzufordern, nach Anmeldeinformationen zu fragen, greifen Sie mithilfe einer IP-Adresse auf die Konsole zu, und Sie werden aufgefordert, Anmeldeinformationen einzugeben.

3. Stellen Sie bei der Anmeldung mit SSO sicher, dass der Standort der ATA-Konsole als lokale Intranetsite in Ihrem Browser definiert ist, und dass Sie auf diese mit einem Kurznamen oder einem Localhost zugreifen.

> [!NOTE]
> Zusätzlich zum Protokollieren jeder verdächtigen Aktivität und Integritätswarnung wird jede Konfigurationsänderung, die Sie in der ATA-Konsole vornehmen, im Windows-Ereignisprotokoll auf dem ATA Center-Computer unter **Applications and services log** (Protokoll für Anwendungen und Dienste) und dann unter **Microsoft ATA** überprüft. Es wird ebenso jede Anmeldung bei der ATA-Konsole überprüft.<br></br>  Eine Konfiguration, die das ATA-Gateway betrifft, wird auch im Windows-Ereignisprotokoll des ATA-Gateway-Computers protokolliert. 



## <a name="the-ata-console"></a>Die ATA-Konsole

Die ATA-Konsole stellt Ihnen einen schnellen Überblick über alle verdächtigen Aktivitäten in zeitlicher Reihenfolge zur Verfügung. Sie ermöglicht es Ihnen, sich die Details einer Aktivität anzusehen und Aktionen entsprechend der jeweiligen Aktivität auszuführen. Die Konsole zeigt außerdem Warnungen und Benachrichtigungen an, um Probleme mit dem ATA-Netzwerk oder neue Aktivitäten hervorzuheben, die als verdächtig eingestuft werden.

Dies sind die wichtigsten Elemente der ATA-Konsole.


### <a name="attack-time-line"></a>Angriffszeitachse

Dies ist die Standardzielseite, auf die Sie gelangen, wenn Sie sich bei der ATA-Konsole anmelden. Standardmäßig werden alle offenen verdächtigen Aktivitäten auf der Angriffszeitachse angezeigt. Sie können die Angriffszeitachse filtern, um alle bzw. offene, verworfene oder unterdrückte verdächtige Aktivitäten anzuzeigen. Außerdem wird der Schweregrad angezeigt, der den einzelnen Aktivitäten zugewiesen wurde.

![Abbildung der Angriffszeitachse in ATA](media/ATA-Suspicious-Activity-Timeline.jpg)

Weitere Informationen finden Sie unter [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md).

### <a name="notification-bar"></a>Benachrichtigungsleiste

Wenn eine neue verdächtige Aktivität erkannt wurde, wird auf der rechten Seite automatisch die Benachrichtigungsleiste geöffnet. Wenn seit Ihrer letzten Anmeldung neue verdächtige Aktivitäten erkannt wurden, wird die Benachrichtigungsleiste geöffnet, nachdem Sie sich erfolgreich angemeldet haben. Sie können jederzeit auf den Pfeil auf der rechten Seite klicken, um auf die Benachrichtigungsleiste zuzugreifen.

![Abbildung der ATA-Benachrichtigungsleiste](media/notification-bar-1.7.png)

### <a name="filtering-panel"></a>Filterbereich

Sie können basierend auf Status und Schweregrad filtern, welche verdächtigen Aktivitäten auf der Angriffszeitachse oder auf der Registerkarte für verdächtige Aktivitäten des Entitätsprofils angezeigt werden.

### <a name="search-bar"></a>Suchleiste

Im obersten Menü finden Sie eine Suchleiste. Sie können nach einem bestimmten Benutzer, einem Computer oder Gruppen in ATA suchen. Beginnen Sie als Versuch einfach mit der Eingabe.

![Abbildung der Suche in der ATA-Konsole](media/ATA-console-search.png)

### <a name="health-center"></a>Integritätscenter

Das Integritätscenter warnt Sie, wenn in Ihrer ATA-Bereitstellung etwas nicht ordnungsgemäß funktioniert.

![Abbildung des ATA-Integritätscenters](media/ATA-Health-Issue.jpg)

Jedes Mal, wenn auf Ihrem System ein Problem auftritt, z. B. ein Verbindungsfehler oder ein getrenntes ATA-Gateway, können Sie dies am Symbol für das Integritätscenter erkennen, auf dem ein roter Punkt angezeigt wird. ![Abbildung des roten Punkts auf dem Symbol für das ATA-Integritätscenter](media/ATA-Health-Center-Alert-red-dot.png)

### <a name="user-and-computer-profiles"></a>Benutzer- und Computerprofil

ATA erstellt ein Profil für jeden Benutzer und Computer im Netzwerk. Im Benutzerprofil zeigt ATA allgemeine Informationen an, z. B. die Gruppenmitgliedschaft, kürzliche Anmeldungen und Ressourcen, auf die kürzlich zugegriffen wurde. Es wird auch eine Liste der Orte bereitgestellt, wo der Benutzer über VPN eine Verbindung hergestellt hat. Eine Liste der Gruppenmitgliedschaften, die ATA als sensibel einstuft, finden Sie unten.

![Benutzerprofil](media/user-profile.png)

Im Computerprofil zeigt ATA allgemeine Informationen an, z.B. kürzliche Anmeldungen und Ressourcen, auf die kürzlich zugegriffen wurde.

![Computerprofil](media/computer-profile.png)

ATA stellt auf folgenden Seiten zusätzliche Informationen zu Entitäten (Computer, Geräte, Benutzer) bereit: „Zusammenfassung“, „Aktivitäten“ und „Verdächtige Aktivitäten“.

Ein Profil, das ATA nicht vollständig auflösen konnte, wird durch das Symbol eines halb gefüllten Kreises gekennzeichnet.


![Abbildung eines nicht aufgelösten Profils in ATA](media/ATA-Unresolved-Profile.jpg)

### <a name="sensitive-groups"></a>Sensible Gruppen

Die folgende Liste von Gruppen werden von ATA als **sensibel** eingestuft. Jede Entität, die Mitglied dieser Gruppen ist, wird als sensibel angesehen:

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


### <a name="mini-profile"></a>Miniprofil

An jeder Stelle in der Konsole, an der eine einzelne Entität angezeigt wird, z. B. ein Benutzer oder ein Computer, wird automatisch ein Miniprofil geöffnet, wenn Sie mit der Maus auf die Entität zeigen. Das Miniprofil enthält die folgenden Informationen (sofern verfügbar):

![Abbildung des ATA-Miniprofils](media/ATA-mini-profile.jpg)

-   Name

-   Bild

-   E-Mail

-   Telefon

-   Anzahl der verdächtigen Aktivitäten nach Schweregrad



## <a name="see-also"></a>Weitere Informationen
[Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
