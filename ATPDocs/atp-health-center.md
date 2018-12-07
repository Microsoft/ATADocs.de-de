---
title: Überwachen von Systemintegrität und Ereignissen von Azure Advanced Threat Protection| Microsoft-Dokumentation
description: Im Integritätscenter für den Azure ATP-Arbeitsbereich können Sie überprüfen, wie der Azure ATP-Dienst funktioniert, und es werden Warnungen über mögliche Probleme sowie Systemereignisse in der Ereignisanzeige angezeigt.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 11/28/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 1b7e72c3-a538-443f-981c-398ffafa5ab8
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 100964d904c7cda48e75cb5401fbba8a3ec0718e
ms.sourcegitcommit: f4f2a1b2c674c4dba7a46ece0624f5ea10c4865e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/02/2018
ms.locfileid: "52744658"
---
*Gilt für: Azure Advanced Threat Protection*


# <a name="working-with-azure-atp-workspace-health-and-events"></a>Arbeiten mit der Integrität und den Ereignissen des Azure ATP-Arbeitsbereichs

## <a name="azure-atp-workspace-health-center"></a>Integritätscenter für den Azure ATP-Arbeitsbereich 

Im Integritätscenter für den Azure ATP-Arbeitsbereich erhalten Sie Informationen zur Leistung des Arbeitsbereichs und möglichen Problemen.

## <a name="working-with-the-azure-atp-workspace-health-center"></a>Arbeiten mit dem Integritätscenter des Azure ATP-Arbeitsbereichs

Das Integritätscenter für den Azure ATP-Arbeitsbereich zeigt Probleme durch einen roten Punkt über dem Symbol für das Integritätscenter auf der Menüleiste an.

![Symbolleiste mit rotem Punkt im Integritätscenter für den Azure ATP-Arbeitsbereich](media/atp-health-bar.png)

### <a name="managing-azure-atp-workspace-health"></a>Verwalten der Integrität des Azure ATP-Arbeitsbereichs
Um den Gesamtzustand des Arbeitsbereichs zu überprüfen, klicken Sie auf der Menüleiste auf das Symbol für das Integritätscenter. ![Symbol für das Integritätscenter für den Azure ATP-Arbeitsbereich](media/atp-red-dot.png)

-   Sie können alle offenen Probleme auf **Schließen** oder **Unterdrücken** festlegen, indem Sie auf die drei Punkte in der Ecke einer Warnung klicken und die gewünschte Option anklicken.

-   **Öffnen**: In dieser Liste werden alle neuen verdächtigen Aktivitäten angezeigt.

-   **Auflösen**: Wird verwendet, um verdächtige Aktivitäten nachzuverfolgen, die Sie identifiziert, untersucht oder entschärft haben.

    > [!NOTE]
    > Azure ATP kann geschlossene Aktivitäten wieder öffnen, wenn diese innerhalb eines kurzen Zeitraums erneut erkannt werden.
    
-   **Unterdrücken**: Das Unterdrücken einer Aktivität bedeutet, dass Sie sie gerade ignorieren möchten und nur wieder gewarnt werden möchten, wenn es eine neue Instanz gibt. Wenn eine ähnliche Warnung ausgelöst wird, wird diese von Azure ATP nicht erneut geöffnet. Wenn die Warnung jedoch für sieben Tage angehalten wurde und anschließend erneut auftritt, werden Sie erneut gewarnt.

-   **Erneut öffnen**: Eine geschlossener oder unterdrückter Alarm kann erneut geöffnet werden, sodass es auf der Zeitachse als **Offen** angezeigt wird.

-   **Löschen:** Sie können Sicherheitswarnungen auch über die Zeitachse für verdächtige Aktivitäten löschen. Wenn Sie allerdings eine Warnung löschen, wird diese vollständig aus der Instanz gelöscht, und Sie können diese nicht wiederherstellen. Nachdem Sie auf „Verwerfen“ geklickt haben, können Sie alle Sicherheitswarnungen für den gleichen Typ löschen.



![Abbildung eines Problems im Azure ATP-Integritätscenter](media/atp-health-issue.png)






## <a name="see-also"></a>Weitere Informationen

- [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
