---
title: Überwachen der System Integrität und Ereignisse von Azure Advanced Threat Protection
description: Überprüfen Sie mit dem Azure ATP-Integritätscenter, wie der Azure ATP-Dienst funktioniert, erhalten Sie Warnungen über mögliche Probleme, und zeigen Sie Systemereignisse in der Ereignisanzeige an.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 1/3/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 1b7e72c3-a538-443f-981c-398ffafa5ab8
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: fc192856a247ca4ee47e5e73ddc366bb7592a0c0
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2020
ms.locfileid: "90910395"
---
# <a name="work-with-azure-atp-health-and-events"></a>Arbeiten mit Azure ATP-Integrität und -Ereignissen

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

## <a name="azure-atp-health-center"></a>Azure ATP-Integritätscenter 

Im Azure ATP-Integritätscenter erhalten Sie Informationen zur Leistung Ihrer Azure ATP-Instanz und erhalten Warnungen, wenn Probleme vorliegen.

## <a name="working-with-the-azure-atp-health-center"></a>Arbeiten mit dem Azure ATP-Integritätscenter

Das Azure ATP-Integritätscenter zeigt Probleme durch einen roten Punkt über dem Symbol für das Integritätscenter auf der Menüleiste an.

![Symbolleiste mit rotem Punkt für das Azure ATP-Integritätscenter](media/atp-health-bar.png)

### <a name="managing-azure-atp-health"></a>Verwalten des Azure ATP-Integritätscenters
Um den Gesamtzustand Ihrer Azure ATP-Instanz zu überprüfen, klicken Sie in der Menüleiste auf das Symbol für das Integritätscenter: ![Symbol für das Azure ATP-Integritätscenter](media/atp-red-dot.png)

- Sie können alle offenen Probleme auf **Schließen** oder **Unterdrücken** festlegen, indem Sie auf die drei Punkte in der Ecke einer Warnung klicken und die gewünschte Option anklicken.

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