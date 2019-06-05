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
ms.sourcegitcommit: 37b572e0e9e4bb874c7965f66de0ee8b6fbe5416
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/04/2019
ms.locfileid: "66500637"
---
# <a name="investigate-lateral-movement-paths-with-ata"></a>Untersuchen von lateral Movement-Pfaden mit ATA


*Gilt für: Advanced Threat Analytics Version 1.9*

Selbst wenn Sie sich sehr darum bemühen, Ihre sensiblen Benutzer zu schützen, Ihre Administratoren über komplexe Kennwörter verfügen, die regelmäßig geändert werden, deren Computer festgeschrieben sind, und ihre Daten sicher gespeichert sind, können Angreifer immer noch Lateral Movement-Pfade nutzen, um auf sensible Konten zuzugreifen. Lateral-Movement-Angriffen nutzt der Angreifer Instanzen wenn sensible Benutzer auf einem Computer anmelden, in dem ein nicht sensibler Benutzer lokale Rechte verfügt. Dann können sich Angreifer lateral bewegen, auf den weniger sensiblen Benutzer zugreifen und sich auf dem Computer bewegen, um die Anmeldeinformationen des sensiblen Benutzers abzugreifen. 

## <a name="what-is-a-lateral-movement-path"></a>Was ist ein Lateral Movement-Pfad?

Lateral Movement bedeutet, dass ein Angreifer nicht sensible Konten benutzt, um Zugriff auf sensible Konten zu erhalten. Dies kann mithilfe der im [Handbuch zu verdächtigen Aktivitäten](suspicious-activity-guide.md) beschriebenen Methoden erfolgen. Angreifer verwenden lateral Movement-Angriffe, die Administratoren in Ihrem Netzwerk zu identifizieren, und erfahren, welche Computer, die sie zugreifen können. Mit diesen Informationen und weitere wechselt kann der Angreifer die Daten auf Ihren Domänencontrollern nutzen. 

Mit ATA können Sie Lateral Movement-Angriffe in Ihrem Netzwerk verhindern.

## <a name="discovery-your-at-risk-sensitive-accounts"></a>Ermittlung Ihrer gefährdeten sensiblen Konten

Gehen Sie folgendermaßen vor, um zu ermitteln, welche sensiblen Konten in Ihrem Netzwerk aufgrund einer Verbindung nicht sensiblen Konten oder Ressourcen, die innerhalb eines bestimmten Zeitraums, anfällig sind: 

1. Klicken Sie im Menü der ATA-Konsole auf das Symbol „Berichte“ ![Symbol „Berichte“](./media/ata-report-icon.png).

2. Wenn keine Lateral Movement-Pfade gefunden wurden, ist der Bericht unter **Lateral Movement-Pfade zu sensiblen Konten** abgeblendet. Wenn Lateral Movement-Pfade mit relevanten Daten gefunden wurden, wird aus den Daten des Berichts automatisch das frühste Datum ausgewählt. 

   ![Berichte](./media/reports.png)

3. Klicken Sie auf **herunterladen**.

4. Die Excel-Datei, die erstellt wird enthält Details zu Ihrem sensiblen Konten gefährdet. Die Registerkarte **Zusammenfassung** liefert Graphen mit Informationen über die Anzahl sensibler Konten und Computer, sowie Durchschnittswerte für gefährdete Ressourcen. Die Registerkarte **Details** enthält eine Liste von sensiblen Konten, um die Sie sich kümmern sollten. Beachten Sie, dass die Pfade in der Vergangenheit verfügbar waren. Es kann also durchaus sein, dass sie heute nicht mehr verfügbar sind.


## <a name="investigate"></a>Untersuchen

Da Sie nun wissen, welche sensiblen Konten gefährdet sind, können Sie sich eingehend mit ATA beschäftigen und mehr darüber erfahren, wie man präventive Maßnahmen ergreift.

1. Suchen Sie in der ATA-Konsole nach dem Lateral Movement-Badge, das dem Entitätsprofil hinzugefügt wird, wenn sich die Entität in einem Lateral Movement-Pfad befindet. ![Symbol „lateral“](./media/lateral-movement-icon.png) oder ![Symbol „Pfad“](./media/paths-icon.png). Dieses Badge ist verfügbar, wenn innerhalb der letzten zwei Tage ein Lateral Movement-Pfad aufgetreten ist.

2. Klicken Sie auf der sich öffnenden Benutzerprofilseite auf die Registerkarte **Lateral Movement-Pfade**.

3. Das angezeigte Diagramm bietet eine Übersicht der möglichen Pfade zum sensiblen Benutzer. Der Graph zeigt die Verbindungen der letzten zwei Tage an.

4. Überprüfen Sie den Graphen, um weitere Informationen über die Offenlegung der Anmeldeinformationen Ihres sensiblen Benutzers zu erhalten. Z. B. in der Übersicht, Sie können folgen der **angemeldet als** abgeblendeten, wo sich Samira mit ihren privilegierten Anmeldeinformationen angemeldet. In diesem Fall wurden Samiras sensible Anmeldeinformationen auf dem Computer „REDMOND-WA-DEV“ gespeichert. Beobachten Sie dann die andere Benutzer angemeldet zu welchen Computern, die die meisten anzuzeigen und zu Sicherheitsrisiken erstellt. Über den schwarzen Pfeil **Administrator auf** können Sie sich anzeigen lassen, wer Administratorrechte für die Ressource hat. In diesem Beispiel hat jeder in der Gruppe **Contoso All** Zugriff auf die Benutzeranmeldeinformationen dieser Ressource.  

   ![Benutzer Profil lateral Movement-Pfade](media/user-profile-lateral-movement-paths.png)


## <a name="preventative-best-practices"></a>Empfohlene präventive Methoden

- Die beste Möglichkeit, lateral Movement-Angriffe zu verhindern, dass ist, um sicherzustellen, dass sensible Benutzer ihre Administratoranmeldeinformationen verwenden, nur wenn Anmeldung im Computer festgeschrieben, wenn kein nicht sensibler Benutzer mit Administratorrechten auf demselben Computer vorhanden ist. Stellen Sie in diesem Beispiel sicher, dass wenn Samira Zugriff auf REDMOND-WA-DEV, sie melden Sie sich mit Benutzername und Kennwort als ihren Administratoranmeldeinformationen benötigt, oder Entfernen der Gruppe "Contoso All" aus der lokalen Administratorengruppe auf REDMOND-WA-dev

- Außerdem wird empfohlen, sicherzustellen, dass niemand über unnötige lokale administrative Berechtigungen verfügt. Im Beispiel zu überprüfen, um festzustellen, ob alle Benutzer in Contoso alle wirklich Administratorrechte auf REDMOND-WA-dev benötigt.

- Stellen Sie sicher, dass Personen nur Zugriff auf die Ressourcen haben, die sie benötigen. Im Beispiel erhöht Oscar Posada die Anfälligkeit von Samiras Konto signifikant. Ist es erforderlich, dass sie in der Gruppe enthalten sein **Contoso alle**? Könnten Sie Untergruppen erstellen, um die Offenlegung von Daten zu minimieren?

> [!TIP]
> Wenn während der letzten zwei Tage keine Aktivitäten ermittelt wird, wird das Diagramm nicht angezeigt, aber der lateral Movement-Pfad-Bericht ist weiterhin verfügbar, um Informationen über lateral Movement-Pfaden der vergangenen 60 Tage bereitzustellen.

> [!TIP]
> Anweisungen dazu, wie auf Ihren Servern zum Zulassen von ATA zur Durchführung der SAM-R-Vorgänge für lateral Movement-Pfads, benötigt [Konfigurieren von SAM-R](install-ata-step9-samr.md).




## <a name="see-also"></a>Siehe auch
- [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
