---
title: Untersuchen von Angriffen mit Lateral Movement-Pfaden mit ATA | Microsoft Dokumentation
description: Dieser Artikel beschreibt, wie Angriffe mit Lateral Movement-Pfaden mit Azure Advanced Threat Analytics (ATA) erkannt werden können.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 710f01bd-c878-4406-a7b2-ce13f98736ea
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: dc03cfe1719541dac0f8509c0f8f22987ecb96bb
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/22/2018
---
*Gilt für: Advanced Threat Analytics Version 1.9*

# <a name="investigating-lateral-movement-paths-with-ata"></a>Untersuchen von Lateral Movement-Pfaden mit ATA

Selbst wenn Sie sich sehr darum bemühen, Ihre sensiblen Benutzer zu schützen, Ihre Administratoren über komplexe Kennwörter verfügen, die regelmäßig geändert werden, deren Computer festgeschrieben sind, und ihre Daten sicher gespeichert sind, können Angreifer immer noch Lateral Movement-Pfade nutzen, um auf sensible Konten zuzugreifen. Bei Angriffen über Lateral Movement-Pfade nutzen Angreifer Instanzen aus, wenn sich sensible Benutzer auf einem Computer anmelden, auf dem ein nicht sensibler Benutzer über lokale Berechtigungen verfügt. Dann können sich Angreifer lateral bewegen, auf den weniger sensiblen Benutzer zugreifen und sich auf dem Computer bewegen, um die Anmeldeinformationen des sensiblen Benutzers abzugreifen. 

## <a name="what-is-a-lateral-movement-path"></a>Was ist ein Lateral Movement-Pfad?

Lateral Movement bedeutet, dass ein Angreifer proaktiv nicht-sensible Konten benutzt, um Zugriff auf sensible Konten zu erhalten. Die Angreifer können alle Methoden verwenden, die im [Handbuch zu verdächtigen Aktivitäten](suspicious-activity-guide.md) beschrieben werden, um das erste nicht sensible Kennwort zu erhalten. Dann werden Tools wie Bloodhound verwendet, um herauszufinden, wer die Administratoren in Ihrem Netzwerk sind, und auf welche Computer sie zugegriffen haben. Sie können dann auf die Daten auf Ihren Domänencontrollern zugreifen, um herauszufinden, wer über welche Konten bzw. über Zugriff auf Ressourcen und Dateien verfügt, um dann die Anmeldeinformationen von anderen (teilweise sensiblen) Benutzern zu stehlen, die auf den Computern gespeichert sind, auf die sie bereits Zugriff hatten. Infolgedessen bewegen sie sich lateral durch weitere Benutzer und Ressourcen, bis sie Administratorrechte auf Ihr Netzwerk erhalten. 

Mit ATA können Sie Lateral Movement-Angriffe in Ihrem Netzwerk verhindern.

## <a name="discovery-your-at-risk-sensitive-accounts"></a>Ermittlung Ihrer gefährdeten sensiblen Konten

Folgen Sie diesen Schritten, um zu ermitteln, welche sensiblen Konten in Ihrem Netzwerk aufgrund einer Verbindung mit nicht sensiblen Konten oder Ressourcen anfällig sind. Um Ihr Netzwerk vor Lateral Movement-Angriffen zu schützen, arbeitet ATA rückwärts und gibt Ihnen eine Übersicht, die von Ihren privilegierten Konten ausgeht und Ihnen anzeigt, welche Benutzer und Geräte sich auf den lateralen Pfaden dieser Benutzer und deren Anmeldeinformationen befinden.

1. Klicken Sie im Menü der ATA-Konsole auf das Symbol „Berichte“ ![Symbol „Berichte“](./media/ata-report-icon.png).

2. Wenn keine Lateral Movement-Pfade gefunden wurden, ist der Bericht unter **Lateral Movement-Pfade zu sensiblen Konten** abgeblendet. Wenn Lateral Movement-Pfade mit relevanten Daten gefunden wurden, wird aus den Daten des Berichts automatisch das frühste Datum ausgewählt. 

 ![Berichte](./media/reports.png)

3. Klicken Sie auf **Herunterladen**.

3. Die erstellte Excel-Datei gibt Ihnen Informationen über gefährdete sensible Konten. Die Registerkarte **Zusammenfassung** liefert Graphen mit Informationen über die Anzahl sensibler Konten und Computer, sowie Durchschnittswerte für gefährdete Ressourcen. Die Registerkarte **Details** enthält eine Liste von sensiblen Konten, um die Sie sich kümmern sollten.


## <a name="investigate"></a>Untersuchen

Da Sie nun wissen, welche sensiblen Konten gefährdet sind, können Sie sich eingehend mit ATA beschäftigen und mehr darüber erfahren, wie man präventive Maßnahmen ergreift.

1. Suchen Sie in der ATA-Konsole nach dem Benutzer (z.B. Samira Abbasi), dessen Konto unter **Lateral Movement-Pfade zu sensiblen Konten** als anfällig aufgelistet wird. Sie können auch nach dem Lateral Movement-Badge suchen, das dem Entitätsprofil hinzugefügt wird, wenn sich die Entität im ![Symbol „Lateral“](./media/lateral-movement-icon.png) oder im ![Pfadsymbol](./media/paths-icon.png) eines Lateral Movement-Pfads befindet.

2. Klicken Sie auf der sich öffnenden Benutzerprofilseite auf die Registerkarte **Lateral Movement-Pfade**.

3. Das angezeigte Diagramm stellt Ihnen eine Übersicht der möglichen Pfade zu Ihrem sensiblen Benutzer bereit. Der Graph zeigt die Verbindungen der letzten zwei Tage an und ist somit aktuell.

4. Überprüfen Sie den Graphen, um weitere Informationen über die Offenlegung der Anmeldeinformationen Ihres sensiblen Benutzers zu erhalten. Beispielsweise können Sie in der Übersicht von Samira Abbasi über den abgeblendeten Pfeil **Angemeldet als** anzeigen lassen, wo sich Samira mit ihren privilegierten Anmeldeinformationen angemeldet hat. In diesem Fall wurden Samiras sensible Anmeldeinformationen auf dem Computer „REDMOND-WA-DEV“ gespeichert. Überprüfen Sie anschließend, welche anderen Benutzer sich an welchen Computern angemeldet haben und die größte Offenlegung von Daten und das höchste Sicherheitsrisiko darstellten. Über den schwarzen Pfeil **Administrator auf** können Sie sich anzeigen lassen, wer Administratorrechte für die Ressource hat. In diesem Beispiel hat jeder in der Gruppe „Contoso All“ Zugriff auf die Benutzeranmeldeinformationen dieser Ressource.  

 ![Lateral Movement-Pfade zum Benutzerprofil](media/user-profile-lateral-movement-paths.png)


## <a name="preventative-best-practices"></a>Empfohlene präventive Methoden

- Sie können Lateral Movement-Angriffe am besten verhindern, indem Sie sicherstellen, dass sensible Benutzer ihre Administratoranmeldeinformationen nur dann verwenden, wenn sie sich an festgeschriebenen Computern anmelden, auf denen kein nicht sensibler Benutzer über Administratorrechte verfügt. Stellen Sie in dem Beispiel sicher, dass sich die Benutzerin Samira mit einem Benutzernamen oder Kennwort anmeldet, die von ihren Administratoranmeldeinformationen abweicht, wenn sie auf REDMOND-WA-DEV zugreifen muss. Stattdessen können Sie auch die Gruppe „Contoso All“ aus der Gruppe der lokalen Administratoren unter REDMOND-WA-DEV entfernen.

- Außerdem wird empfohlen, sicherzustellen, dass niemand über unnötige lokale administrative Berechtigungen verfügt. Im Beispiel sollten Sie überprüfen, ob jeder in der Gruppe „Contoso All“ wirklich Administratorrechte für „REDMOND-WA-DEV“ benötigt.

- Es ist immer von Vorteil, wenn Personen nur Zugriff auf notwendige Ressourcen haben. Wie Sie im Beispiel sehen können, erweitert Oscar Posada Samiras Offenlegung von Daten signifikant. Ist es erforderlich, Mitglied in der Gruppe „Contoso All“ zu sein? Könnten Sie Untergruppen erstellen, um die Offenlegung von Daten zu minimieren?


## <a name="see-also"></a>Weitere Informationen
- [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
