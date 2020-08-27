---
title: Überwachen der System Integrität und Ereignisse von Advanced Threat Analytics
description: Mit ATA Health Center lässt sich die Integrität des ATA-Diensts überprüfen, und es werden Warnungen über mögliche Probleme sowie Systemereignisse in der Ereignisanzeige angezeigt.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: d6c783b2-46c5-4211-b21a-d6b17f08d03d
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 4479de3764f9cceffe9a3ed401aa20332a985498
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88954220"
---
# <a name="working-with-ata-system-health-and-events"></a>Arbeiten mit der Systemintegrität und Ereignissen von ATA

*Gilt für: Advanced Threat Analytics Version 1.9*

## <a name="ata-health-center"></a>ATA Health Center

Mit ATA Health Center lässt sich die Leistung des ATA-Diensts überprüfen, und es werden Warnungen über Probleme angezeigt.

## <a name="working-with-the-ata-health-center"></a>Arbeiten mit dem ATA Health Center
Das ATA Health Center zeigt Probleme durch einen roten Punkt über dem Health Center-Symbol auf der Menüleiste an.

![Roter Punkt auf der Symbolleiste für das ATA-Integritätscenter](media/ATA-Health-Center-Alert-red-dot.png)

### <a name="managing-ata-health"></a>Verwalten der ATA-Integrität
Um den Gesamtzustand des Systems zu überprüfen, klicken Sie auf der Menüleiste auf das Health Center-Symbol. ![ATA Health Center-Symbol](media/ATA-red-dot.png)

- Sie können alle offenen Warnungen auf **Schließen**, **Unterdrücken** oder **Löschen** festlegen, indem Sie auf die drei Punkte in der Ecke einer Warnung klicken und die gewünschte Option auswählen.

-   **Öffnen**: In dieser Liste werden alle neuen verdächtigen Aktivitäten angezeigt.

-   **Auflösen**: Wird verwendet, um verdächtige Aktivitäten nachzuverfolgen, die Sie identifiziert, untersucht oder entschärft haben.

    > [!NOTE]
    > ATA kann geschlossene Aktivitäten wieder öffnen, wenn sie innerhalb eines kurzen Zeitraums erneut erkannt werden.

-   **Unterdrücken**: Das Unterdrücken einer Aktivität bedeutet, dass Sie sie gerade ignorieren möchten und nur wieder gewarnt werden möchten, wenn es eine neue Instanz gibt. Wenn es eine ähnliche Warnung gibt, wird diese von ATA nicht mehr geöffnet. Wenn die Warnung jedoch für sieben Tage angehalten wurde und anschließend erneut auftritt, werden Sie erneut gewarnt.

- **Verwerfen**: Wenn Sie eine Warnung verwerfen, wird sie aus dem System und aus der Datenbank gelöscht und kann von Ihnen NICHT mehr wiederhergestellt werden. Nachdem Sie auf „Verwerfen“ geklickt haben, können Sie alle verdächtigen Aktivitäten für den gleichen Typ löschen.



![Abbildung eines ATA Health Center-Problems](media/ATA-Health-Issue.JPG)






## <a name="see-also"></a>Weitere Informationen

- [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
