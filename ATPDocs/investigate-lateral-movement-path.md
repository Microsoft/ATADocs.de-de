---
title: Untersuchen von Lateral Movement-Pfaden mit Microsoft Defender for Identity
description: In diesem Artikel wird beschrieben, wie potenzielle Angriffe mit Lateral Movement-Pfaden mit Microsoft Defender for Identity erkannt und untersucht werden können.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: d489a02d600d82067f325d8b6f2c358f903f0908
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93276019"
---
# <a name="tutorial-use-lateral-movement-paths-lmps"></a>Tutorial: Verwendung von Lateral Movement-Pfaden (LMPs)

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

> [!NOTE]
> Die auf dieser Seite erläuterten [!INCLUDE [Product long](includes/product-long.md)]-Features sind auch über das neue [Portal](https://portal.cloudappsecurity.com) zugänglich.

Lateral Movement-Angriffe können auf unterschiedliche Weise durchgeführt werden. Einige der von Angreifern am häufigsten verwendeten Methoden sind der [Diebstahl von Anmeldeinformationen](suspicious-activity-guide.md#) und [Pass-the-Ticket](suspicious-activity-guide.md)-Angriffe. Bei beiden Methoden werden nicht sensible Konten von den Angreifern für Seitenangriffe genutzt, indem sie nicht sensible Computer ausnutzen, die Anmeldeinformationen gemeinsam mit Konten, Endpunktgruppen und Computern mit sensiblen Konten verwenden.

In diesem Tutorial erfahren Sie, wie [!INCLUDE [Product long](includes/product-long.md)]-LMPs verwendet werden können, um potenzielle Lateral Movement-Pfade zu [untersuchen](#investigate) und zusammen mit [!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnungen besser zu verstehen, welche Aktionen in Ihrem Netzwerk wie durchgeführt wurden. Zusätzlich verwenden Sie den [Bericht über LMPs zu einem sensiblen Konto](#discover-your-at-risk-sensitive-accounts), um alle sensiblen Konten mit potenziellen Lateral Movement-Pfaden in Ihrem Netzwerk nach Zeiträumen zu ermitteln.

> [!div class="checklist"]
>
> - Untersuchen von LMPs
> - Ermitteln Ihrer gefährdeten sensiblen Konten
> - Zugriff auf den **Bericht über Lateral Movement-Pfade zu sensiblen Konten**

## <a name="investigate"></a>Untersuchen

Es gibt mehrere Möglichkeiten, LMPs zu verwenden und zu untersuchen. Suchen Sie im [!INCLUDE [Product short](includes/product-short.md)]-Portal nach einer Entität, und untersuchen Sie diese dann über den Pfad oder die Aktivität.

1. Suchen Sie über das Portal nach einem Benutzer oder Computer. Achten Sie darauf, ob ein Lateral Movement-Badge zu einem Entitätsprofil hinzugefügt wurde. Badges werden nur angezeigt, wenn eine Entität innerhalb der letzten 48 Stunden in einem potenziellen LMP erkannt wurde.

    ![Symbol „lateral“](media/lateral-movement-icon.png) oder ![Symbol „Pfad“](media/paths-icon.png).

1. Klicken Sie auf der sich öffnenden Benutzerprofilseite auf die Registerkarte **Lateral Movement-Pfade**.

    ![Registerkarte für Lateral Movement-Pfade (LMPs) von [!INCLUDE [Product short](includes/product-short.md)]](media/lateral-movement-path-tab.png)

1. Das angezeigte Diagramm bietet eine Übersicht der möglichen Pfade zum sensiblen Benutzer in einem Zeitraum von 48 Stunden. Wenn in den letzten zwei Tagen keine Aktivität erkannt wurde, wird das Diagramm nicht angezeigt. Verwenden Sie die Option **Ein anderes Datum anzeigen** , um das Diagramm für die vorherigen Erkennungen von Lateral Movement-Pfaden für die Entität anzuzeigen.

    ![LMP, Ein anderes Datum anzeigen](media/view-different-date.png)

1. Überprüfen Sie den Graphen, um weitere Informationen über die Offenlegung der Anmeldeinformationen Ihres sensiblen Benutzers zu erhalten. Beispielsweise können Sie in diesem Pfad über die grauen Pfeile **Angemeldet durch** anzeigen lassen, wo sich Nick mit seinen privilegierten Anmeldeinformationen angemeldet hat. In diesem Fall wurden Nicks sensible Anmeldeinformationen auf dem Computer „SHAREPOINT-SRV“ gespeichert. Sehen Sie sich dann an, welche anderen Benutzer sich an welchen Computern angemeldet haben und die größte Anfälligkeit und das höchste Sicherheitsrisiko verursachten. Über den schwarzen Pfeil **Administrator auf** können Sie sich anzeigen lassen, wer Administratorrechte für die Ressource hat. In diesem Beispiel hat jeder in der Gruppe „HelpDesk“ Zugriff auf die Benutzeranmeldeinformationen dieser Ressource.

    ![Lateral Movement-Pfad (LMP) von [!INCLUDE [Product short](includes/product-short.md)]](media/lmp.png)

## <a name="discover-your-at-risk-sensitive-accounts"></a>Ermittlung Ihrer gefährdeten sensiblen Konten

Führen Sie die folgenden Schritte aus, um alle sensiblen Konten in Ihrem Netzwerk zu ermitteln, die aufgrund einer Verbindung mit nicht sensiblen Konten, Gruppen oder Computern in Lateral Movement-Pfaden anfällig sind.

1. Klicken Sie im Menü des [!INCLUDE [Product short](includes/product-short.md)]-Portals auf das Symbol „Berichte“ ![Symbol „Berichte“](media/report-icon.png).

1. Wenn keine potenziellen Lateral Movement-Pfade gefunden wurden, ist der Bericht unter **Lateral Movement-Pfade zu sensiblen Konten** abgeblendet. Wenn potenzielle Lateral Movement-Pfade mit relevanten Daten gefunden wurden, wird aus den Daten des Berichts automatisch das früheste Datum ausgewählt. Der Bericht über Lateral Movement-Pfade enthält Daten für bis zu 60 Tage.

    ![Screenshot: Auswahl des Berichtsdatums](media/reports.png)

1. Klicken Sie auf **Herunterladen**.

1. Es wird eine Excel-Datei erstellt, die Details zu potenziellen Lateral Movement-Pfaden und der Anfälligkeit sensibler Konten für die ausgewählten Daten enthält. Die Registerkarte **Zusammenfassung** liefert Diagramme mit Informationen über die Anzahl sensibler Konten und Computer sowie Durchschnittswerte für gefährdeten Zugriff. Die Registerkarte **Details** enthält eine Liste der sensiblen Konten, die Sie genauer untersuchen sollten.

## <a name="schedule-report"></a>Berichtszeitplan

Der Bericht über Lateral Movement zu einem sensiblen Konto kann auch über das Feature „Geplante Berichte festlegen“ geplant werden.

Beachten Sie, dass die tatsächlichen Pfade in dem herunterladbaren Bericht möglicherweise nicht mehr verfügbar sind, da sie möglicherweise bereits ermittelt und geändert oder behoben wurden.

Wählen Sie verschiedene verfügbare Datumsangaben in der Kalenderauswahl, um vergangene LMPs beim Erstellen eines Berichts zu überprüfen.

## <a name="next-steps"></a>Nächste Schritte

In diesem Tutorial haben Sie erfahren, wie LMPs zum Untersuchen von verdächtigen Aktivitäten eingesetzt werden. Um mehr über die an LMPs beteiligten Entitäten zu erfahren, fahren Sie mit dem Tutorial zur Untersuchung von Entitäten fort.

> [!div class="nextstepaction"]
> [Untersuchen von Entitäten](investigate-entity.md)

## <a name="see-also"></a>Weitere Informationen

- [Informationen zu Lateral Movement-Pfaden von [!INCLUDE [Product short](includes/product-short.md)]](use-case-lateral-movement-path.md)
- [Konfigurieren von [!INCLUDE [Product short](includes/product-short.md)] für das Ausführen von Remoteaufrufen an SAM](install-step8-samr.md)
- [Arbeiten mit Sicherheitswarnungen](working-with-suspicious-activities.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
