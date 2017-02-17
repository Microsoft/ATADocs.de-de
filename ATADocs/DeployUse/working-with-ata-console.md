---
title: Verstehen der Advanced Threat Analytics-Konsole | Microsoft-Dokumentation
description: Beschreibt die Anmeldung bei der ATA-Konsole sowie die Komponenten der Konsole.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 1/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1bf264d9-9697-44b5-9533-e1c498da4f07
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b28cb3a0da844b7c460c03726222bc775a9e47da
ms.openlocfilehash: cb712537b42c4e86ed24607e70c614e8d37025c0


---

*Gilt für: Advanced Threat Analytics Version 1.7*



# <a name="working-with-the-ata-console"></a>Arbeiten mit der ATA-Konsole

Verwenden Sie die ATA-Konsole, um die von ATA erkannten verdächtigen Aktivitäten zu überwachen und darauf zu reagieren.

## <a name="enabling-access-to-the-ata-console"></a>Aktivieren des Zugriffs auf die ATA-Konsole
Sie müssen sich mit einem Benutzer anmelden, dem die richtige ATA-Rolle für den Zugriff auf die ATA-Konsole zugewiesen wurde, damit die Anmeldung auf der Konsole erfolgreich verläuft. Weitere Informationen zur rollenbasierten Zugriffssteuerung (role-based access control; RBAC) in ATA finden Sie unter [Working with ATA role groups](ata-role-groups.md) (Arbeiten mit ATA-Rollengruppen).

## <a name="logging-into-the-ata-console"></a>Anmelden bei der ATA-Konsole

1. Klicken Sie auf dem Desktop des ATA Center-Servers auf das Symbol für die **Microsoft ATA-Konsole**, oder öffnen Sie einen Browser, und navigieren Sie zur ATA-Konsole.

    ![Symbol für den ATA-Server](media/ata-server-icon.png)

>[!NOTE]
> Sie können auch entweder in ATA Center oder auf dem ATA-Gateway einen Browser öffnen und zu der IP-Adresse navigieren, die Sie während der ATA Center-Installation für die ATA-Konsole konfiguriert haben.    

2.  Geben Sie Ihren Benutzernamen und Ihr Kennwort ein, und klicken Sie auf **Anmelden**.

![Abbildung des ATA-Anmeldebildschirms](media/ATA-log-in-screen.png)


## <a name="the-ata-console"></a>Die ATA-Konsole

Die ATA-Konsole stellt Ihnen einen schnellen Überblick über alle verdächtigen Aktivitäten in zeitlicher Reihenfolge zur Verfügung. Sie ermöglicht es Ihnen, sich die Details einer Aktivität anzusehen und Aktionen entsprechend der jeweiligen Aktivität auszuführen. Die Konsole zeigt außerdem Warnungen und Benachrichtigungen an, um Probleme mit dem ATA-Netzwerk oder neue Aktivitäten hervorzuheben, die als verdächtig eingestuft werden.

Dies sind die wichtigsten Elemente der ATA-Konsole.


### <a name="attack-time-line"></a>Angriffszeitachse

Dies ist die Standardzielseite, auf die Sie gelangen, wenn Sie sich bei der ATA-Konsole anmelden. Standardmäßig werden alle offenen verdächtigen Aktivitäten auf der Angriffszeitachse angezeigt. Sie können die Angriffszeitachse filtern, um alle verdächtigen Aktivitäten bzw. offene, verworfene oder aufgelöste verdächtige Aktivitäten anzuzeigen. Außerdem wird der Schweregrad angezeigt, der den einzelnen Aktivitäten zugewiesen wurde.

![Abbildung der Angriffszeitachse in ATA](media/attack-timeline-1.7.png)

Weitere Informationen finden Sie unter [Arbeiten mit verdächtigen Aktivitäten](/advanced-threat-analytics/deploy-use/working-with-suspicious-activities).

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

Warnungen des Integritätscenters können verworfen oder aufgelöst werden, und sie sind in Abhängigkeit von ihrem Schweregrad als „Hoch“, „Mittel“ oder „Niedrig“ kategorisiert. Wenn Sie eine Warnung auflösen, die vom ATA-Dienst als noch aktiv erkannt wird, wird sie automatisch in die Liste der offenen Warnungen verschoben. Wenn das System erkennt, dass für eine Warnung keine Ursache mehr vorliegt (die Situation wurde behoben), wird sie automatisch in die Liste der aufgelösten Warnungen verschoben.

### <a name="user-and-computer-profiles"></a>Benutzer- und Computerprofil

ATA erstellt ein Profil für jeden Benutzer und Computer im Netzwerk. Im Benutzerprofil zeigt ATA allgemeine Informationen an, z. B. die Gruppenmitgliedschaft, kürzliche Anmeldungen und Ressourcen, auf die kürzlich zugegriffen wurde.

![Benutzerprofil](media/user-profile.png)

Im Computerprofil zeigt ATA allgemeine Informationen an, z. B. kürzliche Anmeldungen und Ressourcen, auf die kürzlich zugegriffen wurde.

![Computerprofil](media/computer-profile.png)

ATA stellt auf folgenden Seiten zusätzliche Informationen zu Entitäten (Computer, Geräte, Benutzer) bereit: „Zusammenfassung“, „Aktivitäten“ und „Verdächtige Aktivitäten“.

Ein Profil, das ATA nicht vollständig auflösen konnte, wird durch das Symbol eines halb gefüllten Kreises gekennzeichnet.


![Abbildung eines nicht aufgelösten Profils in ATA](media/ATA-Unresolved-Profile.jpg)

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



<!--HONumber=Feb17_HO1-->


