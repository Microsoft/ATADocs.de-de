---
title: "Arbeiten mit verdächtigen Aktivitäten in Advanced Threat Analytics | Microsoft-Dokumentation"
description: "Beschreibt, wie Sie von ATA identifizierte verdächtige Aktivitäten überprüfen."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 08/28/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 44d7c899-816c-4f7f-91d3-84a09d291a24
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 62ce117423a189a1c2ce00b862f323db6ed328cb
ms.sourcegitcommit: 46dd0e695f16a0dd23bbfa140eba15ea6a34d7af
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2017
---
*Gilt für: Advanced Threat Analytics Version 1.8*



# <a name="working-with-suspicious-activities"></a>Arbeiten mit verdächtigen Aktivitäten
In diesem Thema werden die Grundlagen des Arbeitens mit Advanced Threat Analytics erläutert.

## <a name="review-suspicious-activities-on-the-attack-time-line"></a>Überprüfen verdächtiger Aktivitäten auf der Angriffszeitachse
Nachdem Sie sich bei der ATA-Konsole angemeldet haben, gelangen Sie automatisch zur **Zeitachse mit den offenen verdächtigen Aktivitäten**. Die verdächtigen Aktivitäten werden in chronologischer Reihenfolge aufgeführt, wobei sich die neuesten verdächtigen Aktivitäten oben auf der Zeitachse befinden.
Zu jeder verdächtigen Aktivität stehen folgende Informationen zur Verfügung:

-   Die beteiligten Entitäten, einschließlich Benutzer, Computer, Server, Domänencontroller und Ressourcen

-   Uhrzeiten und Zeitrahmen der verdächtigen Aktivitäten

-   Schweregrad der verdächtigen Aktivitäten: „Hoch“, „Mittel“ oder „Niedrig“

-   Staus: „Offen“, „Aufgelöst“ oder „Unterdrückt“.

-   Möglichkeit für Folgendes:

    -   Teilen der verdächtigen Aktivität mit anderen Personen in Ihrer Organisation per E-Mail.

    -   Exportieren der verdächtigen Aktivität nach Excel.

    -   Hinzufügen einer Notiz zu der verdächtigen Aktivität.

    -   Bereitstellen von Eingaben zur verdächtigen Aktivität.

-   Empfehlungen zur Reaktion auf die verdächtige Aktivität

> [!NOTE]
> -   Wenn Sie mit der Maus auf einen Benutzer oder Computer zeigen, wird ein Miniprofil der Entität angezeigt. Dieses enthält zusätzliche Informationen zur Entität und die Anzahl von verdächtigen Aktivitäten, mit denen die Entität verknüpft ist.
> -   Wenn Sie auf eine Entität klicken, gelangen Sie zum Entitätsprofil des Benutzers oder Computers.

![Abbildung der Zeitachse für verdächtige Aktivitäten von ATA](media/ATA-Suspicious-Activity-Timeline.JPG)

## <a name="filter-suspicious-activities-list"></a>Filtern der Liste der verdächtigen Aktivitäten
So filtern Sie die Liste der verdächtigen Aktivitäten

1.  Wählen Sie auf der linken Seite des Bildschirms im Bereich **Filtern nach** eine der folgenden Optionen aus: **Alle**, **Offen**, **Geschlossen** oder **Unterdrückt**.

2.  Um die Liste weiter zu filtern, wählen Sie **Hoch**, **Mittel** oder **Niedrig** aus.

**Schweregrad von verdächtigen Aktivitäten**

-   **Niedrig**

    Weist auf verdächtige Aktivitäten hin, die zu Angriffen durch böswillige Benutzer oder Software führen können, um Zugriff auf Organisationsdaten zu erlangen.

-   **Mittel**

    Weist auf verdächtige Aktivitäten hin, die für bestimmte Identitäten das Risiko schwerwiegenderer Angriffe erhöhen und zu Identitätsdiebstahl oder Berechtigungsausweitung führen können.

-   **Hoch**

    Weist auf verdächtige Aktivitäten hin, die zu Identitätsdiebstahl, Berechtigungsausweitung oder anderen Angriffen mit schwerwiegenden Auswirkungen führen können.




## <a name="remediating-suspicious-activities"></a>Beheben verdächtiger Aktivitäten
Sie können den Status einer verdächtigen Aktivität ändern, indem Sie auf den aktuellen Status der verdächtigen Aktivität klicken und eine der folgenden Optionen auswählen: **Offen**, **Unterdrückt**, **Aufgelöst** oder **Verworfen**.
Klicken Sie dafür auf die drei Punkte in der oberen rechten Ecke einer besonders verdächtigen Aktivität, um die Liste der verfügbaren Aktionen anzuzeigen.

![ATA-Aktionen für verdächtige Aktivitäten](./media/sa-actions.png)

**Status von verdächtigen Aktivitäten**

-   **Öffnen**: In dieser Liste werden alle neuen verdächtigen Aktivitäten angezeigt.

-   **Auflösen**: Wird verwendet, um verdächtige Aktivitäten nachzuverfolgen, die Sie identifiziert, untersucht und behoben oder entschärft haben.

    > [!NOTE]
    > ATA kann geschlossene Aktivitäten wieder öffnen, wenn sie innerhalb eines kurzen Zeitraums erneut erkannt werden.

-   **Unterdrücken**: Das Unterdrücken einer Aktivität bedeutet, dass Sie sie gerade ignorieren möchten und nur wieder gewarnt werden möchten, wenn es eine neue Instanz gibt. Das bedeutet, dass wenn es eine ähnliche Warnung gibt, ATA diese nicht mehr öffnen würde. Wen die Warnung jedoch für 7 Tage lang angehalten ist und anschließend wieder angezeigt wird, werden Sie erneut gewarnt.

- **Verwerfen**: Wenn Sie eine Warnung verwerfen, wird Sie aus dem System aus der Datenbank gelöscht, und Sie können sie NICHT mehr wiederherstellen. Nachdem Sie auf „Verwerfen“ geklickt haben, können Sie alle verdächtigen Aktivitäten für den gleichen Typ löschen.

- **Ausschließen**: Die Möglichkeit, eine Entität davor zu bewahren, mehr bestimmte Warnungstypen auszugeben. Sie können z.B. ATA darauf festlegen, eine bestimmte Entität (Benutzer oder Computer) auszuschließen, sodass diese keine Warnung für einen bestimmten Typ einer verdächtigen Aktivität ausgibt, wie etwa ein bestimmter Administrator, der remoten Code oder eine Sicherheitsüberprüfung ausführt, die DNS-Reconnaissance durchführt. Zusätzlich zur Möglichkeit, Ausnahmen direkt zur verdächtigen Aktivität hinzuzufügen, da sie in der Zeitleiste erkannt wurde, können Sie auch auf die Seite „Konfiguration“ zu **Ausnahmen** wechseln. Für jede verdächtige Aktivität können Sie so manuell ausgeschlossene Entitäten oder Subnetze hinzufügen oder entfernen (z.B. für Pass-the-Ticket). 
> [!NOTE]
> Die Seiten für die Konfiguration können nur von ATA-Administratoren bearbeitet werden.


## <a name="related-videos"></a>Verwandte Videos
- [Joining the security community](https://channel9.msdn.com/Shows/Microsoft-Security/Join-the-Security-Community) (Der Sicherheitscommunity beitreten)


## <a name="see-also"></a>Siehe auch
- [Verdächtige ATA-Aktivitäten – Playbook](http://aka.ms/ataplaybook)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Ändern der ATA-Konfiguration](modifying-ata-center-configuration.md)
