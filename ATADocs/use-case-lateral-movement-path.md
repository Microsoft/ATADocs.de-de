---
title: Untersuchen von Angriffen mit lateral Movement-Pfaden mit ATA | Microsoft-Dokumentation
description: Dieser Artikel beschreibt, wie Angriffe mit Lateral Movement-Pfaden mit Azure Advanced Threat Analytics (ATA) erkannt werden können.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 06/14/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 710f01bd-c878-4406-a7b2-ce13f98736ea
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 2f020838d182b99b1f5f42455330b2b0ce5aa88f
ms.sourcegitcommit: 6dd002b5a34f230aaada55a6f6178c2f9e1584d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2019
ms.locfileid: "66500637"
---
# <a name="investigate-lateral-movement-paths-with-ata"></a>Untersuchen von Lateral Movement-Pfaden mit ATA


*Gilt für: Advanced Threat Analytics Version 1.9*

Selbst wenn Sie sich sehr darum bemühen, Ihre sensiblen Benutzer zu schützen, Ihre Administratoren über komplexe Kennwörter verfügen, die regelmäßig geändert werden, deren Computer festgeschrieben sind, und ihre Daten sicher gespeichert sind, können Angreifer immer noch Lateral Movement-Pfade nutzen, um auf sensible Konten zuzugreifen. Bei lateral Movement-Angriffen nutzt der Angreifer Instanzen, wenn vertrauliche Benutzer sich bei einem Computer anmelden, auf dem ein nicht sensibler Benutzer über lokale Rechte verfügt. Dann können sich Angreifer lateral bewegen, auf den weniger sensiblen Benutzer zugreifen und sich auf dem Computer bewegen, um die Anmeldeinformationen des sensiblen Benutzers abzugreifen. 

## <a name="what-is-a-lateral-movement-path"></a>Was ist ein Lateral Movement-Pfad?

Lateral Movement bedeutet, dass ein Angreifer nicht sensible Konten benutzt, um Zugriff auf sensible Konten zu erhalten. Dies kann mithilfe der im [Handbuch zu verdächtigen Aktivitäten](suspicious-activity-guide.md) beschriebenen Methoden erfolgen. Angreifer verwenden lateral Movement, um die Administratoren in Ihrem Netzwerk zu identifizieren und zu erfahren, auf welche Computer Sie zugreifen können. Mit diesen Informationen und weiteren Verschiebungen kann der Angreifer die Daten auf Ihren Domänen Controllern nutzen. 

Mit ATA können Sie Lateral Movement-Angriffe in Ihrem Netzwerk verhindern.

## <a name="discovery-your-at-risk-sensitive-accounts"></a>Ermittlung Ihrer gefährdeten sensiblen Konten

Führen Sie die folgenden Schritte aus, um zu ermitteln, welche sensiblen Konten in Ihrem Netzwerk aufgrund der Verbindung mit nicht sensiblen Konten oder Ressourcen in einem bestimmten Zeitraum anfällig sind: 

1. Klicken Sie im Menü der ATA-Konsole auf das Symbol „Berichte“ ![Symbol „Berichte“](./media/ata-report-icon.png).

2. Wenn keine lateral Movement-Pfade gefunden werden, ist der Bericht unter **lateral Movement-Pfade zu sensiblen Konten**ausgegraut. Wenn lateral Movement-Pfade vorhanden sind, wählen die Datumsangaben des Berichts automatisch das erste Datum aus, wenn relevante Daten vorhanden sind. 

   ![Berichte](./media/reports.png)

3. Klicken Sie auf **Herunterladen**.

4. Die Excel-Datei, die erstellt wird, enthält Details zu den gefährdeten sensiblen Konten. Die Registerkarte **Zusammenfassung** liefert Graphen mit Informationen über die Anzahl sensibler Konten und Computer, sowie Durchschnittswerte für gefährdete Ressourcen. Die Registerkarte **Details** enthält eine Liste von sensiblen Konten, um die Sie sich kümmern sollten. Beachten Sie, dass die Pfade in der Vergangenheit verfügbar waren. Es kann also durchaus sein, dass sie heute nicht mehr verfügbar sind.


## <a name="investigate"></a>Untersuchen

Da Sie nun wissen, welche sensiblen Konten gefährdet sind, können Sie sich eingehend mit ATA beschäftigen und mehr darüber erfahren, wie man präventive Maßnahmen ergreift.

1. Suchen Sie in der ATA-Konsole nach dem Lateral Movement-Badge, das dem Entitätsprofil hinzugefügt wird, wenn sich die Entität in einem Lateral Movement-Pfad befindet. ![Symbol „lateral“](./media/lateral-movement-icon.png) oder das ![Symbol „Pfad“](./media/paths-icon.png). Dieses Badge ist verfügbar, wenn innerhalb der letzten zwei Tage ein Lateral Movement-Pfad aufgetreten ist.

2. Klicken Sie auf der sich öffnenden Benutzerprofilseite auf die Registerkarte **Lateral Movement-Pfade**.

3. Das angezeigte Diagramm bietet eine Übersicht der möglichen Pfade zum sensiblen Benutzer. Der Graph zeigt die Verbindungen der letzten zwei Tage an.

4. Überprüfen Sie den Graphen, um weitere Informationen über die Offenlegung der Anmeldeinformationen Ihres sensiblen Benutzers zu erhalten. In dieser Übersicht können Sie z. b. die Pfeile " **protokolliert von** grau" befolgen, um zu sehen, wo sich Samira mit ihren privilegierten Anmelde Informationen angemeldet hat. In diesem Fall wurden Samiras sensible Anmeldeinformationen auf dem Computer „REDMOND-WA-DEV“ gespeichert. Sehen Sie sich dann an, welche anderen Benutzer sich bei welchen Computern angemeldet haben. Über den schwarzen Pfeil **Administrator auf** können Sie sich anzeigen lassen, wer Administratorrechte für die Ressource hat. In diesem Beispiel hat jeder in der Gruppe **Contoso All** Zugriff auf die Benutzeranmeldeinformationen dieser Ressource.  

   ![Lateral Movement-Pfade für Benutzerprofile](media/user-profile-lateral-movement-paths.png)


## <a name="preventative-best-practices"></a>Empfohlene präventive Methoden

- Die beste Möglichkeit, lateral Movement zu verhindern, besteht darin sicherzustellen, dass sensible Benutzer Ihre Administrator Anmelde Informationen nur dann verwenden, wenn Sie sich bei festgeschriebenen Computern anmelden, bei denen es keinen nicht sensiblen Benutzer gibt, der auf demselben Computer über Administratorrechte verfügt. Vergewissern Sie sich im Beispiel, dass Samira Zugriff auf Redmond-WA-dev benötigt, indem Sie sich mit einem Benutzernamen und einem Kennwort anmelden, die nicht Ihren Administrator Anmelde Informationen entsprechen, oder entfernen Sie die Gruppe "alle" in der Gruppe "lokale Administratoren" auf Redmond-WA-dev.

- Außerdem wird empfohlen, sicherzustellen, dass niemand über unnötige lokale administrative Berechtigungen verfügt. Überprüfen Sie in diesem Beispiel, ob alle Benutzer in "..." für "Redmond-WA-dev" wirklich Administratorrechte benötigen.

- Stellen Sie sicher, dass Personen nur Zugriff auf die Ressourcen haben, die sie benötigen. Im Beispiel erhöht Oscar Posada die Anfälligkeit von Samiras Konto signifikant. Ist es erforderlich, dass Sie in der Gruppe " **alle**" in der Gruppe "alle" enthalten sind? Könnten Sie Untergruppen erstellen, um die Offenlegung von Daten zu minimieren?

> [!TIP]
> Wenn die Aktivität während der letzten zwei Tage nicht erkannt wird, wird das Diagramm nicht angezeigt, aber der Bericht "Lateral Movement Path" ist weiterhin verfügbar, um Informationen über lateral Movement-Pfade in den letzten 60 Tagen bereitzustellen.

> [!TIP]
> Um zu erfahren, wie Sie Ihre Server so einrichten, dass ATA die SAM-r-Vorgänge durchführt, die für die Erkennung von Lateral Movement-Pfaden erforderlich sind, [Konfigurieren Sie Sam-r](install-ata-step9-samr.md).




## <a name="see-also"></a>Weitere Informationen:
- [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
