---
title: Arbeiten mit Entitätenprofilen in der Advanced Threat Analytics-Konsole | Microsoft-Dokumentation
description: Informationen zum Untersuchen von Entitäten über die Anzeige „Benutzerprofile“ in der ATA-Konsole
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: barbkess
ms.date: 3/25/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 581a3257-32dc-453f-b84e-b9f99186f5d3
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 014bf17948c1a0fe342cf01d98932d876df914e8
ms.sourcegitcommit: 62b631f64a639f5df04bf805755f26c69b40e8e4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/29/2019
ms.locfileid: "58638914"
---
# <a name="investigating-entity-profiles"></a>Untersuchen von Entitätsprofilen


*Gilt für: Advanced Threat Analytics Version 1.9*

Über das Entitätsprofil erhalten Sie Zugriff auf ein Dashboard, das für eine detaillierte Untersuchung von Benutzern, Computern, Geräten und Ressourcen, auf die sie zugreifen können, sowie auf deren Verlauf, ausgerichtet ist. Die Profilseite nutzt den neuen logischen Aktivitätenübersetzer von ATA, der eine Gruppe von Aktivitäten (für bis zu eine Minute zusammengefasst) überprüfen und diese in genau eine logische Aktivität gruppieren kann, um die tatsächlichen Aktivitäten der Benutzer zu verdeutlichen.

Wenn Sie auf die Profilseite einer Entität zugreifen möchten, klicken Sie auf der Zeitachse der verdächtigen Aktivität auf den Namen der Entität, z.B. den Benutzernamen.

Im Menü im linken Bereich erhalten Sie Informationen zu Active Directory, die zu der Entität verfügbar sind: E-Mail-Adresse, Domäne, Datum der ersten Aktivität. Wenn die Entität sensibel ist, wird angegeben, warum dies der Fall ist. Es wird z.B. angezeigt, ob der Benutzer oder das Mitglied einer sensiblen Gruppe als sensibel markiert ist.
Wenn es sich um einen sensiblen Benutzer handelt, wird das entsprechende Symbol unterhalb des Benutzernamens angezeigt.

## <a name="view-entity-activities"></a>Anzeigen von Entitätsaktivitäten

Wenn Sie alle vom Benutzer ausgeführten Aktivitäten oder die Aktivitäten sehen möchten, die auf einer Entität durchgeführt werden, klicken Sie auf die Registerkarte **Aktivitäten**. 

 ![Aktivitäten des Benutzerprofils](media/user-profile-activities.png)

Standardmäßig wird im Hauptbereich des Entitätenprofils eine Zeitachse der Aktivitäten der Entität angezeigt (Verlauf von bis zu sechs Monaten). Über diese Zeitachse können Sie Detailinformationen zu den Entitäten anzeigen, auf die der Benutzer zugreift, bzw. können Sie die Benutzer abrufen, die auf die Entität zugegriffen haben.

Im oberen Bereich können Sie Kacheln für die Zusammenfassung anzeigen, in denen eine schnelle Übersicht aller wissenswerten Informationen zu Ihrer Entität angezeigt werden. Die Kacheln ändern sich anhand des Entitätstyps. Für Benutzer wird Folgendes angezeigt:
- Die Anzahl der offenen verdächtigen Aktivitäten für den Benutzer
- Die Anzahl der Computer, auf denen der Benutzer angemeldet ist
- Die Anzahl der Ressourcen, auf die der Benutzer zugegriffen hat
- Die Standorten, von denen sich der Benutzer im VPN-Netzwerk angemeldet hat

  ![Entitätsmenü](media/entity-menu.png)

Für Computer wird Folgendes angezeigt:
- Die Anzahl der offenen verdächtigen Aktivitäten für den Computer
- Die Anzahl der auf dem Computer angemeldeten Benutzer
- Die Anzahl der Ressourcen, auf die von diesem Computer aus zugegriffen wurde
- Die Anzahl der Standorte, von denen über den Computer auf das VPN-Netzwerk zugegriffen wurde
- Eine Liste der vom Computer verwendeten IP-Adressen

  ![Computer mit Entitätsmenü](media/entity-computer.png)

Wenn Sie die Schaltfläche **Filter by** (Filtern nach) oberhalb der Aktivitätszeitachse verwenden, können Sie die Aktivitäten nach Aktivitätstyp filtern. Außerdem können Sie auch einen bestimmten (störenden) Aktivitätstyp herausfiltern. Dies erweist sich für die Untersuchung als sehr nützlich, wenn Sie die Grundlagen der Funktionsweise einer Entität im Netzwerk nachvollziehen möchten. Sie können auch ein bestimmtes Datum auswählen und die Aktivitäten als „Nach Excel gefiltert“ exportieren. In der exportierten Datei ist dann eine Seite mit Änderungen der Verzeichnisdienste (Dinge, die sich in Active Directory für das Konto geändert haben) und eine separate Seite mit den Aktivitäten enthalten. 

## <a name="view-directory-data"></a>Anzeigen der Verzeichnisdaten

In der Registerkarte **Verzeichnisdaten** erhalten Sie statische Informationen, die über Active Directory verfügbar sind, einschließlich Sicherheitsflags für die Benutzerzugriffssteuerung. Außerdem zeigt ATA Gruppenmitgliedschaften für den Benutzer an, damit Sie überprüfen können, ob der Benutzer über eine direkte oder eine rekursive Mitgliedschaft verfügt. Für Gruppen führt ATA die jeweiligen Mitglieder auf.

 ![Verzeichnisdaten des Benutzerprofils](media/user-profile-dir-data.png)

Im Abschnitt **Benutzerzugriffssteuerung** werden die Sicherheitseinstellungen für ATA aufgelistet, die Sie überprüfen sollten. Sie können wichtige Flags zum Benutzer abrufen, die z.B. festlegen, ob der Benutzer die EINGABETASTE drücken kann, um das Kennwort zu umgehen, oder ob der Benutzer über ein Kennwort verfügt, das nicht abläuft. 

## <a name="view-lateral-movement-paths"></a>Anzeigen von Lateral Movement-Pfaden

Wenn Sie auf die Registerkarte **Lateral Movements-Pfade** klicken, wird Ihnen eine vollständige, dynamische und klickbare Imagemap angezeigt, in der die Lateral Movement-Pfade, die im Zusammenhang mit diesem Benutzer stehen, visuell dargestellt werden, die verwendet werden können, um in Ihr Netzwerk einzudringen.

Die Map enthält eine Liste, die Auskunft darüber gibt, wie viele Hops zwischen Computern oder Benutzern notwendig wären, damit ein Angreifer ein sensibles Konto gefährden kann. Wenn der Benutzer selbst über ein sensibles Konto verfügt, können Sie zudem sehen, wie viele Ressourcen und Konten direkt mit dem Konto verbunden sind. Weitere Informationen erhalten Sie unter [Lateral Movement-Pfade](use-case-lateral-movement-path.md). 

 ![Lateral Movement-Pfade zum Benutzerprofil](media/user-profile-lateral-movement-paths.png)


## <a name="see-also"></a>Weitere Informationen
[Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
