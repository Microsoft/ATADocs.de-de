---
title: Überwachen von Microsoft Defender auf Integrität und Ereignisse des Identitäts Systems
description: Verwenden Sie das Integritäts Center, um zu überprüfen, wie der Microsoft Defender für Identity-Dienst funktioniert, und dass Sie über mögliche Probleme informiert werden und Systemereignisse in der Ereignisanzeige anzeigen können.
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: ac03020c559a860fded89a496bc927da06fce3d9
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/16/2021
ms.locfileid: "100534292"
---
# <a name="work-with-microsoft-defender-for-identity-health-and-events"></a>Arbeiten Sie mit Microsoft Defender für Identitäts Integrität und-Ereignisse

## <a name="microsoft-defender-for-identity-health-center"></a>Microsoft Defender für Identity Health Center

Das Integritäts [!INCLUDE [Product long](includes/product-long.md)] Center informiert Sie über die [!INCLUDE [Product short](includes/product-short.md)] Leistung Ihrer Instanz und benachrichtigt Sie, wenn Probleme auftreten.

## <a name="working-with-the-defender-for-identity-health-center"></a>Arbeiten mit Defender für Identity Health Center

Das Integritäts [!INCLUDE [Product short](includes/product-short.md)] Center informiert Sie darüber, dass ein Problem vorliegt, indem eine Warnung (ein roter Punkt) über dem Integritäts Center-Symbol in der Navigationsleiste ausgelöst wird.

![[! INCLUDE [Product Short] (includes/Product-Short. MD)] Integritäts Center-rote Punkt-Symbolleiste](media/health-bar.png)

### <a name="managing-defender-for-identity-health"></a>Verwalten von Defender für Identity Health

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
