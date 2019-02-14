---
title: Untersuchen von Angriffen mit Lateral Movement-Pfaden mit ATA | Microsoft Dokumentation
description: Dieser Artikel beschreibt, wie Angriffe mit Lateral Movement-Pfaden mit Azure Advanced Threat Analytics (ATA) erkannt werden können.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: barbkess
ms.date: 6/14/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 710f01bd-c878-4406-a7b2-ce13f98736ea
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: ec01c5b4a5a824df6959461271b763e7fe3d7cd7
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2019
ms.locfileid: "56076792"
---
# <a name="investigating-lateral-movement-paths-with-ata"></a>Untersuchen von Lateral Movement-Pfaden mit ATA


*Gilt für: Advanced Threat Analytics Version 1.9*

Selbst wenn Sie sich sehr darum bemühen, Ihre sensiblen Benutzer zu schützen, Ihre Administratoren über komplexe Kennwörter verfügen, die regelmäßig geändert werden, deren Computer festgeschrieben sind, und ihre Daten sicher gespeichert sind, können Angreifer immer noch Lateral Movement-Pfade nutzen, um auf sensible Konten zuzugreifen. Bei Angriffen über Lateral Movement-Pfade nutzen Angreifer Instanzen aus, wenn sich sensible Benutzer auf einem Computer anmelden, auf dem ein nicht sensibler Benutzer über lokale Berechtigungen verfügt. Dann können sich Angreifer lateral bewegen, auf den weniger sensiblen Benutzer zugreifen und sich auf dem Computer bewegen, um die Anmeldeinformationen des sensiblen Benutzers abzugreifen. 

## <a name="what-is-a-lateral-movement-path"></a>Was ist ein Lateral Movement-Pfad?

Lateral Movement bedeutet, dass ein Angreifer nicht sensible Konten benutzt, um Zugriff auf sensible Konten zu erhalten. Dies kann mithilfe der im [Leitfaden zu verdächtigen Aktivitäten](suspicious-activity-guide.md) beschriebenen Methoden erfolgen. Der Angreifer kann die Daten auf Ihren Domänencontrollern nutzen, um zu erfahren, wer die Administratoren in Ihrem Netzwerk sind und auf welche Computer zugegriffen werden kann. 

Mit ATA können Sie Lateral Movement-Angriffe in Ihrem Netzwerk verhindern.

## <a name="discovery-your-at-risk-sensitive-accounts"></a>Ermittlung Ihrer gefährdeten sensiblen Konten

Befolgen Sie diese Schritte, um zu ermitteln, welche sensiblen Konten in Ihrem Netzwerk aufgrund einer Verbindung mit nicht sensiblen Konten oder Ressourcen innerhalb eines bestimmten Zeitraums anfällig sind. 

1. Klicken Sie im Menü der ATA-Konsole auf das Symbol „Berichte“ ![Symbol „Berichte“](./media/ata-report-icon.png).

2. Wenn keine Lateral Movement-Pfade gefunden wurden, ist der Bericht unter **Lateral Movement-Pfade zu sensiblen Konten** abgeblendet. Wenn Lateral Movement-Pfade mit relevanten Daten gefunden wurden, wird aus den Daten des Berichts automatisch das frühste Datum ausgewählt. 

   ![-Berichte](./media/reports.png)

3. Klicken Sie auf **Herunterladen**.

4. Die erstellte Excel-Datei gibt Ihnen Informationen über gefährdete sensible Konten. Die Registerkarte **Zusammenfassung** liefert Graphen mit Informationen über die Anzahl sensibler Konten und Computer, sowie Durchschnittswerte für gefährdete Ressourcen. Die Registerkarte **Details** enthält eine Liste von sensiblen Konten, um die Sie sich kümmern sollten. Beachten Sie, dass die Pfade in der Vergangenheit verfügbar waren. Es kann also durchaus sein, dass sie heute nicht mehr verfügbar sind.


## <a name="investigate"></a>Untersuchen

Da Sie nun wissen, welche sensiblen Konten gefährdet sind, können Sie sich eingehend mit ATA beschäftigen und mehr darüber erfahren, wie man präventive Maßnahmen ergreift.

1. Suchen Sie in der ATA-Konsole nach dem Lateral Movement-Badge, das dem Entitätsprofil hinzugefügt wird, wenn sich die Entität in einem Lateral Movement-Pfad befindet. ![Symbol „lateral“](./media/lateral-movement-icon.png) oder ![Symbol „Pfad“](./media/paths-icon.png). Dieses Badge ist verfügbar, wenn innerhalb der letzten zwei Tage ein Lateral Movement-Pfad aufgetreten ist.

2. Klicken Sie auf der sich öffnenden Benutzerprofilseite auf die Registerkarte **Lateral Movement-Pfade**.

3. Das angezeigte Diagramm bietet eine Übersicht der möglichen Pfade zum sensiblen Benutzer. Der Graph zeigt die Verbindungen der letzten zwei Tage an.

4. Überprüfen Sie den Graphen, um weitere Informationen über die Offenlegung der Anmeldeinformationen Ihres sensiblen Benutzers zu erhalten. Beispielsweise können Sie in dieser Zuordnung über die grauen Pfeile **Angemeldet durch** anzeigen lassen, wo sich Samira mit ihren privilegierten Anmeldeinformationen angemeldet hat. In diesem Fall wurden Samiras sensible Anmeldeinformationen auf dem Computer „REDMOND-WA-DEV“ gespeichert. Überprüfen Sie anschließend, welche anderen Benutzer sich an welchen Computern angemeldet haben und die größte Offenlegung von Daten und das höchste Sicherheitsrisiko darstellten. Über den schwarzen Pfeil **Administrator auf** können Sie sich anzeigen lassen, wer Administratorrechte für die Ressource hat. In diesem Beispiel hat jeder in der Gruppe **Contoso All** Zugriff auf die Benutzeranmeldeinformationen dieser Ressource.  

   ![Lateral Movement-Pfade zum Benutzerprofil](media/user-profile-lateral-movement-paths.png)


## <a name="preventative-best-practices"></a>Empfohlene präventive Methoden

- Sie können Lateral Movement-Angriffe am besten verhindern, indem Sie sicherstellen, dass sensible Benutzer ihre Administratoranmeldeinformationen nur dann verwenden, wenn sie sich an festgeschriebenen Computern anmelden, auf denen kein nicht sensibler Benutzer über Administratorrechte verfügt. Stellen Sie in dem Beispiel sicher, dass sich die Benutzerin Samira mit einem Benutzernamen oder Kennwort anmeldet, die von ihren Administratoranmeldeinformationen abweicht, wenn sie auf REDMOND-WA-DEV zugreifen muss. Stattdessen können Sie auch die Gruppe „Contoso All“ aus der Gruppe der lokalen Administratoren unter REDMOND-WA-DEV entfernen.

- Außerdem wird empfohlen, sicherzustellen, dass niemand über unnötige lokale administrative Berechtigungen verfügt. Im Beispiel sollten Sie überprüfen, ob jeder in der Gruppe „Contoso All“ wirklich Administratorrechte für „REDMOND-WA-DEV“ benötigt.

- Stellen Sie sicher, dass Personen nur Zugriff auf die Ressourcen haben, die sie benötigen. Im Beispiel erhöht Oscar Posada die Anfälligkeit von Samiras Konto signifikant. Ist es erforderlich, dass er Mitglied in der Gruppe **Contoso All** ist? Könnten Sie Untergruppen erstellen, um die Offenlegung von Daten zu minimieren?

**Tipp:** Wenn während der vergangenen zwei Tage keine Aktivitäten ermittelt wurden, wird zwar der Graph nicht angezeigt, aber Sie können immer noch auf den Bericht zu den Lateral Movement-Pfaden zugreifen, der Informationen zu den Lateral Movement-Pfaden der vergangenen 60 Tage enthält.

**Tipp:** Unter [Konfigurieren von SAM-R](install-ata-step9-samr.md) finden Sie Informationen darüber, wie Sie auf Ihren Servern ATA das Ausführen des für die Lateral Movement-Pfaderkennung nötigen SAM-R-Vorgangs erlauben.




## <a name="see-also"></a>Weitere Informationen
- [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
