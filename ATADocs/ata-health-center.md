---
title: "Überwachen von Systemintegrität und Ereignissen von Advanced Threat Analytics| Microsoft-Dokumentation"
description: "Mit ATA Health Center lässt sich die Integrität des ATA-Diensts überprüfen, und es werden Warnungen über mögliche Probleme sowie Systemereignisse in der Ereignisanzeige angezeigt."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 08/28/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: d6c783b2-46c5-4211-b21a-d6b17f08d03d
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: cdd046eeaca1d8aeb7ea3afa001b34b82cb468b0
ms.sourcegitcommit: 46dd0e695f16a0dd23bbfa140eba15ea6a34d7af
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2017
---
*Gilt für: Advanced Threat Analytics Version 1.8*


# <a name="working-with-ata-system-health-and-events"></a>Arbeiten mit der Systemintegrität und Ereignissen von ATA

## <a name="ata-health-center"></a>ATA Health Center
Mit ATA Health Center lässt sich die Leistung des ATA-Diensts überprüfen, und es werden Warnungen über Probleme angezeigt.

## <a name="working-with-the-ata-health-center"></a>Arbeiten mit dem ATA Health Center
Das ATA Health Center zeigt Probleme durch einen roten Punkt über dem Health Center-Symbol auf der Menüleiste an.

![Roter Punkt auf der Symbolleiste für das ATA-Integritätscenter](media/ATA-Health-Center-Alert-red-dot.png)

### <a name="managing-ata-health"></a>Verwalten der ATA-Integrität
Um den Gesamtzustand des Systems zu überprüfen, klicken Sie auf der Menüleiste auf das Health Center-Symbol. ![ATA Health Center-Symbol](media/ATA-red-dot.png)

-   Sie können alle offenen Warnungen auf **Schließen**, **Unterdrücken** oder **Löschen** festlegen, indem Sie auf die drei Punkte in der Ecke einer Warnung klicken und die gewünschte Option auswählen.

-   **Öffnen**: In dieser Liste werden alle neuen verdächtigen Aktivitäten angezeigt.

-   **Auflösen**: Wird verwendet, um verdächtige Aktivitäten nachzuverfolgen, die Sie identifiziert, untersucht und behoben oder entschärft haben.

    > [!NOTE]
    > ATA kann geschlossene Aktivitäten wieder öffnen, wenn sie innerhalb eines kurzen Zeitraums erneut erkannt werden.

-   **Unterdrücken**: Das Unterdrücken einer Aktivität bedeutet, dass Sie sie gerade ignorieren möchten und nur wieder gewarnt werden möchten, wenn es eine neue Instanz gibt. Das bedeutet, dass wenn es eine ähnliche Warnung gibt, ATA diese nicht mehr öffnen würde. Wen die Warnung jedoch für 7 Tage lang angehalten ist und anschließend wieder angezeigt wird, werden Sie erneut gewarnt.

- **Verwerfen**: Wenn Sie eine Warnung verwerfen, wird Sie aus dem System aus der Datenbank gelöscht, und Sie können sie NICHT mehr wiederherstellen. Nachdem Sie auf „Verwerfen“ geklickt haben, können Sie alle verdächtigen Aktivitäten für den gleichen Typ löschen.



![Abbildung eines ATA Health Center-Problems](media/ATA-Health-Issue.JPG)






## <a name="see-also"></a>Siehe auch

- [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
