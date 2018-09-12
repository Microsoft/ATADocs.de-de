---
title: Arbeiten mit verdächtigen Aktivitäten in Azure Advanced Threat Protection | Microsoft-Dokumentation
description: Beschreibt, wie Sie von Azure ATP identifizierte verdächtige Aktivitäten überprüfen.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/22/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: a06004bd-9f77-4e8e-a0e5-4727d6651a0f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4cf099faae920f23eeeaacdc8f10129005fdc896
ms.sourcegitcommit: 93a133430ac85d6db7afad5f6f2583b3a39c423a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/02/2018
ms.locfileid: "43469667"
---
*Gilt für: Azure Advanced Threat Protection*



# <a name="working-with-suspicious-activities"></a>Arbeiten mit verdächtigen Aktivitäten
In diesem Artikel werden die Grundlagen der Arbeit mit Azure Advanced Threat Protection erläutert.

## Überprüfen verdächtiger Aktivitäten auf der Angriffszeitachse <a name="review-suspicious-activities-on-the-attack-time-line"></a>
Nachdem Sie sich im Arbeitsbereichsportal für Azure ATP angemeldet haben, gelangen Sie automatisch zur **Zeitachse mit den offenen verdächtigen Aktivitäten**. Die verdächtigen Aktivitäten werden in chronologischer Reihenfolge aufgeführt, wobei sich die neuesten verdächtigen Aktivitäten oben auf der Zeitachse befinden.
Zu jeder verdächtigen Aktivität stehen folgende Informationen zur Verfügung:

-   Die beteiligten Entitäten, einschließlich Benutzer, Computer, Server, Domänencontroller und Ressourcen

-   Uhrzeiten und Zeitrahmen der verdächtigen Aktivitäten

-   Schweregrad der verdächtigen Aktivitäten: „Hoch“, „Mittel“ oder „Niedrig“

-   Staus: „Offen“, „Aufgelöst“ oder „Unterdrückt“.

-   Möglichkeit für Folgendes:

    -   Teilen der verdächtigen Aktivität mit anderen Personen in Ihrer Organisation per E-Mail.

    -   Exportieren der verdächtigen Aktivität nach Excel.

> [!NOTE]
> -   Wenn Sie mit der Maus auf einen Benutzer oder Computer zeigen, wird ein Miniprofil der Entität angezeigt. Dieses enthält zusätzliche Informationen zur Entität und die Anzahl von verdächtigen Aktivitäten, mit denen die Entität verknüpft ist.
> -   Wenn Sie auf eine Entität klicken, gelangen Sie zum Entitätsprofil des Benutzers oder Computers.

![Abbildung der Zeitachse für verdächtige Aktivitäten von Azure ATP](media/atp-sa-timeline.png)

## Erkennungen von Vorschauversionen<a name="preview-detections"></a>

Das Azure ATP-Forschungsteam arbeitet kontinuierlich daran, neue Erkennungen für neu entdeckte Angriffe zu implementieren. Da es sich bei Azure ATP um einen Clouddienst handelt, werden neue Erkennungen schnell veröffentlicht, damit Azure ATP-Kunden so schnell wie möglich von diesen profitieren können.

Diese Erkennungen werden als Vorschauversionen markiert, damit Sie die neuen Erkennungen schneller ermitteln können und wissen, dass sie neu für das Produkt sind. Wenn Sie die Erkennungen von Vorschauversionen deaktivieren, werden diese nicht mehr in der Azure ATP-Konsole (und auch nicht auf der Zeitachse oder in den Entitätsprofilen) angezeigt, und es werden keine Warnungen mehr geöffnet.

![Vorschauversion für VPN-Erkennungen](./media/preview-detection-vpn.png) 

Erkennungen von Vorschauversionen werden standardmäßig in Azure ATP aktiviert. 

Gehen Sie wie folgt vor, um die Erkennung von Vorschauversionen zu deaktivieren:

1. Klicken Sie in der Azure ATP-Konsole auf das Zahnradsymbol für Einstellungen.
2. Klicken Sie im Menü auf der linken Seite unter „Vorschauversion“ auf **Erkennungen**.
3. Verwenden Sie den Schieberegler, um die Erkennungen für Vorschauversionen zu (de)aktivieren.
 
![Erkennungen von Vorschauversionen](./media/preview-detections.png) 


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




## <a name="managing-suspicious-activities"></a>Verwalten verdächtiger Aktivitäten
Sie können den Status einer verdächtigen Aktivität ändern, indem Sie auf den aktuellen Status der verdächtigen Aktivität klicken und eine der folgenden Optionen auswählen: **Offen**, **Unterdrückt**, **Aufgelöst** oder **Verworfen**.
Klicken Sie dafür auf die drei Punkte in der oberen rechten Ecke einer besonders verdächtigen Aktivität, um die Liste der verfügbaren Aktionen anzuzeigen.

![Azure ATP-Aktionen für verdächtige Aktivitäten](./media/atp-sa-actions.png)

**Status von verdächtigen Aktivitäten**

-   **Öffnen**: In dieser Liste werden alle neuen verdächtigen Aktivitäten angezeigt.

-   **Auflösen**: Wird verwendet, um verdächtige Aktivitäten nachzuverfolgen, die Sie identifiziert, untersucht oder entschärft haben.

    > [!NOTE]
    > Azure ATP kann geschlossene Aktivitäten wieder öffnen, wenn diese innerhalb eines kurzen Zeitraums erneut erkannt werden.

-   **Unterdrücken**: Das Unterdrücken einer Aktivität bedeutet, dass Sie sie gerade ignorieren möchten und nur wieder gewarnt werden möchten, wenn es eine neue Instanz gibt. Wenn es also eine ähnliche Warnung gibt, wird diese von Azure ATP nicht erneut geöffnet. Wenn die Warnung jedoch für sieben Tage angehalten wurde und anschließend erneut auftritt, werden Sie erneut gewarnt.

- **Verwerfen**: Wenn Sie eine Warnung verwerfen, wird sie aus dem System und aus der Datenbank gelöscht und kann von Ihnen NICHT mehr wiederhergestellt werden. Nachdem Sie auf „Verwerfen“ geklickt haben, können Sie alle verdächtigen Aktivitäten für den gleichen Typ löschen.

- **Ausschließen**: Die Möglichkeit, eine Entität davor zu bewahren, mehr bestimmte Warnungstypen auszugeben. Sie können z.B. Azure ATP darauf festlegen, eine bestimmte Entität (Benutzer oder Computer) auszuschließen, sodass diese keine Warnung für einen bestimmten Typ einer verdächtigen Aktivität ausgibt, wie etwa ein bestimmter Administrator, der Remote-Code oder eine Sicherheitsüberprüfung ausführt, die DNS-Reconnaissance durchführt. Zusätzlich zur Möglichkeit, Ausnahmen direkt zur verdächtigen Aktivität hinzuzufügen, da sie in der Zeitleiste erkannt wurde, können Sie auch auf die Seite „Konfiguration“ zu **Ausnahmen** wechseln. Für jede verdächtige Aktivität können Sie so manuell ausgeschlossene Entitäten oder Subnetze hinzufügen oder entfernen (z.B. für Pass-the-Ticket). 

> [!NOTE]
> Die Seiten für die Konfiguration können nur von Azure ATP-Administratoren bearbeitet werden.


## <a name="see-also"></a>Weitere Informationen

- [Working with the Azure ATP workspace portal (Arbeiten mit dem Azure ATP-Arbeitsbereichsportal)](workspace-portal.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)