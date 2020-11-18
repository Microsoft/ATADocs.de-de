---
title: Überwachen von Microsoft Defender auf Integrität und Ereignisse des Identitäts Systems
description: Verwenden Sie das Integritäts Center, um zu überprüfen, wie der Microsoft Defender für Identity-Dienst funktioniert, und dass Sie über mögliche Probleme informiert werden und Systemereignisse in der Ereignisanzeige anzeigen können.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 5bf828278e0223aaaf52b41932b2612c7225dd7f
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2020
ms.locfileid: "94847937"
---
# <a name="work-with-product-long-health-and-events"></a>Arbeiten mit Integrität [!INCLUDE [Product long](includes/product-long.md)] und Ereignissen

## <a name="product-long-health-center"></a>[!INCLUDE [Product long](includes/product-long.md)] Integritäts Center

Das Integritäts [!INCLUDE [Product long](includes/product-long.md)] Center informiert Sie über die [!INCLUDE [Product short](includes/product-short.md)] Leistung Ihrer Instanz und benachrichtigt Sie, wenn Probleme auftreten.

## <a name="working-with-the-product-short-health-center"></a>Arbeiten mit dem Integritäts [!INCLUDE [Product short](includes/product-short.md)] Center

Das Integritäts [!INCLUDE [Product short](includes/product-short.md)] Center informiert Sie darüber, dass ein Problem vorliegt, indem eine Warnung (ein roter Punkt) über dem Integritäts Center-Symbol in der Navigationsleiste ausgelöst wird.

![[! INCLUDE [Product Short] (includes/Product-Short. MD)] Integritäts Center-rote Punkt-Symbolleiste](media/health-bar.png)

### <a name="managing-product-short-health"></a>Verwalten [!INCLUDE [Product short](includes/product-short.md)] der Integrität

Wählen Sie zum Überprüfen der Gesamt Integrität Ihrer [!INCLUDE [Product short](includes/product-short.md)] Instanz die Option **Health** ![ [! INCLUDE [Product Short] (includes/Produkt-Short. MD)] Integritäts Center Symbol](media/red-dot.png)

- Sie können alle offenen Probleme auf **Schließen** oder **Unterdrücken** festlegen, indem Sie auf die drei Punkte in der Ecke einer Warnung klicken und die gewünschte Option anklicken.

- **Öffnen**: In dieser Liste werden alle neuen verdächtigen Aktivitäten angezeigt.

- **Auflösen**: Wird verwendet, um verdächtige Aktivitäten nachzuverfolgen, die Sie identifiziert, untersucht oder entschärft haben.

    > [!NOTE]
    > [!INCLUDE [Product short](includes/product-short.md)] kann eine geschlossene Aktivität erneut öffnen, wenn die gleiche Aktivität innerhalb eines kurzen Zeitraums wiedererkannt wird.

- **Unterdrücken**: Das Unterdrücken einer Aktivität bedeutet, dass Sie sie gerade ignorieren möchten und nur wieder gewarnt werden möchten, wenn es eine neue Instanz gibt. Wenn eine ähnliche Warnung vorliegt, wird [!INCLUDE [Product short](includes/product-short.md)] Sie nicht erneut geöffnet. Wenn die Warnung jedoch für sieben Tage angehalten wurde und anschließend erneut auftritt, werden Sie erneut gewarnt.

- **Erneut öffnen**: Eine geschlossener oder unterdrückter Alarm kann erneut geöffnet werden, sodass es auf der Zeitachse als **Offen** angezeigt wird.

- **Löschen:** Sie können Sicherheitswarnungen auch über die Zeitachse für verdächtige Aktivitäten löschen. Wenn Sie allerdings eine Warnung löschen, wird diese vollständig aus der Instanz gelöscht, und Sie können diese nicht wiederherstellen. Nachdem Sie auf „Verwerfen“ geklickt haben, können Sie alle Sicherheitswarnungen für den gleichen Typ löschen.

![[! INCLUDE [Product Short] (includes/Produkt-Short. MD)] Integritäts Center-Probleme Bild](media/health-issue.png)

## <a name="see-also"></a>Weitere Informationen

- [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
