---
title: Untersuchen von Lateral Movement-Pfaden mit Azure ATP | Microsoft-Dokumentation
description: Dieser Artikel beschreibt, wie potenzielle Angriffe mit Lateral Movement-Pfaden mit Azure Advanced Threat Protection (ATP) erkannt und untersucht werden können.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 11/25/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 9295dc09-ecdb-44c0-906b-cba4c5c8f17c
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: bb460b699e0052f917ffcd6899d5cc1baa71182f
ms.sourcegitcommit: eac0aa855270b550dfb4b8c61b9cf0953f1e5204
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/26/2018
ms.locfileid: "52298269"
---
*Gilt für: Azure Advanced Threat Protection*

# <a name="using-azure-atp-lateral-movement-paths-lmps"></a>Verwenden von Azure ATP Lateral Movement-Pfaden (LMPs)

Lateral Movement-Angriffe können auf unterschiedliche Weise durchgeführt werden. Einige der von Angreifern am häufigsten verwendeten Methoden sind der [Diebstahl von Anmeldeinformationen](suspicious-activity-guide.md#) und [Pass-the-Ticket](suspicious-activity-guide.md)-Angriffe. Bei beiden Methoden werden nicht sensible Konten von den Angreifern für Seitenangriffe genutzt, indem sie nicht sensible Computer ausnutzen, die Anmeldeinformationen gemeinsam mit Konten, Endpunktgruppen und Computern mit sensiblen Konten verwenden. 

Verwenden Sie Azure ATP-LMPs, um potenzielle Lateral Movement-Pfade zu [untersuchen](#investigate) und zusammen mit Azure ATP-Sicherheitswarnungen ein besseres Verständnis davon zu bekommen, welche Aktionen in Ihrem Netzwerk wie durchgeführt wurden. Verwenden Sie den [Bericht über einen LMP zu einem sensiblen Konto](#discover-your-at-risk-sensitive-accounts), um alle sensiblen Konten mit potenziellen Lateral Movement-Pfaden in Ihrem Netzwerk nach Zeiträumen zu ermitteln.  

## <a name="investigate"></a>Untersuchen
Es gibt mehrere Möglichkeiten, LMPs zu verwenden und zu untersuchen. Suchen Sie im Azure ATP-Portal nach einer Entität, und untersuchen Sie sie dann über den Pfad oder die Aktivität. 

1. Suchen Sie über das Portal nach einem Benutzer oder Computer. Achten Sie darauf, ob ein Lateral Movement-Badge zu einem Entitätsprofil hinzugefügt wurde. Badges werden nur angezeigt, wenn eine Entität innerhalb der letzten 48 Stunden in einem potenziellen LMP erkannt wurde.  

   ![Symbol „lateral“](./media/lateral-movement-icon.png) oder ![Symbol „Pfad“](./media/paths-icon.png). 

2. Klicken Sie auf der sich öffnenden Benutzerprofilseite auf die Registerkarte **Lateral Movement-Pfade**. 

   ![Registerkarte „Azure ATP Lateral Movement Path (LMP)“ (Azure ATP-Lateral Movement-Pfad (LMP))](./media/lateral-movement-path-tab.png)

3. Das angezeigte Diagramm bietet eine Übersicht der möglichen Pfade zum sensiblen Benutzer in einem Zeitraum von 48 Stunden. Wenn in den letzten zwei Tagen keine Aktivität erkannt wurde, wird das Diagramm nicht angezeigt. Verwenden Sie die Option **Ein anderes Datum anzeigen**, um das Diagramm für die vorherigen Erkennungen von Lateral Movement-Pfaden für die Entität anzuzeigen. 

   ![LMP, Ein anderes Datum anzeigen](./media/atp-view-different-date.png)

4. Überprüfen Sie den Graphen, um weitere Informationen über die Offenlegung der Anmeldeinformationen Ihres sensiblen Benutzers zu erhalten. Beispielsweise können Sie in diesem Pfad über die grauen Pfeile **Angemeldet durch** anzeigen lassen, wo sich Nick mit seinen privilegierten Anmeldeinformationen angemeldet hat. In diesem Fall wurden Nicks sensible Anmeldeinformationen auf dem Computer „SHAREPOINT-SRV“ gespeichert. Sehen Sie sich dann an, welche anderen Benutzer sich an welchen Computern angemeldet haben und die größte Anfälligkeit und das höchste Sicherheitsrisiko verursachten. Über den schwarzen Pfeil **Administrator auf** können Sie sich anzeigen lassen, wer Administratorrechte für die Ressource hat. In diesem Beispiel hat jeder in der Gruppe „HelpDesk“ Zugriff auf die Benutzeranmeldeinformationen dieser Ressource.  

   ![Azure ATP-Lateral Movement-Pfad (LMP)](./media/atp-lmp.png)

## <a name="discover-your-at-risk-sensitive-accounts"></a>Ermittlung Ihrer gefährdeten sensiblen Konten

Führen Sie die folgenden Schritte aus, um alle sensiblen Konten in Ihrem Netzwerk zu ermitteln, die aufgrund einer Verbindung mit nicht sensiblen Konten, Gruppen oder Computern in Lateral Movement-Pfaden anfällig sind. 

1. Klicken Sie im Menü des Azure ATP-Portals auf das Symbol „Berichte“. ![Symbol „Berichte“](./media/atp-report-icon.png).

2. Wenn keine potenziellen Lateral Movement-Pfade gefunden wurden, ist der Bericht unter **Lateral Movement-Pfade zu sensiblen Konten** abgeblendet. Wenn potenzielle Lateral Movement-Pfade mit relevanten Daten gefunden wurden, wird aus den Daten des Berichts automatisch das früheste Datum ausgewählt. Der Bericht über Lateral Movement-Pfade enthält Daten für bis zu 60 Tage.

   ![Berichte](./media/reports.png)

3. Klicken Sie auf **Herunterladen**.

4. Es wird eine Excel-Datei erstellt, die Details zu potenziellen Lateral Movement-Pfaden und der Anfälligkeit sensibler Konten für die ausgewählten Daten enthält. Die Registerkarte **Zusammenfassung** liefert Diagramme mit Informationen über die Anzahl sensibler Konten und Computer sowie Durchschnittswerte für gefährdeten Zugriff. Die Registerkarte **Details** enthält eine Liste der sensiblen Konten, die Sie genauer untersuchen sollten. 

Der Bericht über Lateral Movement zu einem sensiblen Konto kann auch über das Feature „Geplante Berichte festlegen“ geplant werden. 

Beachten Sie, dass die tatsächlichen Pfade in dem herunterladbaren Bericht möglicherweise nicht mehr verfügbar sind, da sie möglicherweise bereits ermittelt und geändert oder behoben wurden. 

Wählen Sie verschiedene verfügbare Datumsangaben in der Kalenderauswahl, um vergangene LMPs beim Erstellen eines Berichts zu überprüfen. 

## <a name="see-also"></a>Weitere Informationen

- [Grundlagen zu Azure ATP-Lateral Movement-Pfaden](use-case-lateral-movement-path.md)
- [Konfigurieren von Azure ATP für das Ausführen von Remoteaufrufen an SAM](install-atp-step8-samr.md)
- [Arbeiten mit Sicherheitswarnungen](working-with-suspicious-activities.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)