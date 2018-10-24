---
title: Untersuchen von Lateral Movement-Angriffen mit Azure ATP | Microsoft-Dokumentation
description: Dieser Artikel beschreibt, wie Lateral Movement-Angriffe mit Azure Advanced Threat Protection (ATP) erkannt werden können.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: de15c920-8904-4124-8bdc-03abd9f667cf
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: e6a223405f4aa1e8daa1d393428db43c4e692daa
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/04/2018
ms.locfileid: "48783490"
---
*Gilt für: Azure Advanced Threat Protection*

# <a name="investigating-lateral-movement-paths-with-azure-atp"></a>Untersuchen von Angriffen mit Lateral Movement-Pfaden mit Azure ATP


Lateral Movement bedeutet, dass ein Angreifer nicht sensible Konten benutzt, um Zugriff auf sensible Konten zu erhalten. Dies kann mithilfe der im [Handbuch zu verdächtigen Aktivitäten](suspicious-activity-guide.md) beschriebenen Methoden erfolgen. Lateral Movement wird von Angreifern genutzt, um über nicht sensible Konten, die Anmeldeinformationen für Konten, Gruppen und Computer gemeinsam nutzen, Zugriff auf sensible Konten und Computer in Ihrem Netzwerk zu erhalten. Sobald ein Angreifer Zugriff erhalten hatte, kann er auch von den Daten auf Ihren Domänencontrollern profitieren.


## <a name="discover-your-at-risk-sensitive-accounts"></a>Ermittlung Ihrer gefährdeten sensiblen Konten

Führen Sie die folgenden Schritte aus, um zu ermitteln, welche sensiblen Konten in Ihrem Netzwerk aufgrund einer Verbindung mit nicht sensiblen Konten, Gruppen oder Computern anfällig sind. 

1. Klicken Sie im Menü des Azure ATP-Portals auf das Symbol „Berichte“. ![Symbol „Berichte“](./media/atp-report-icon.png).

2. Wenn keine potenziellen Lateral Movement-Pfade gefunden wurden, ist der Bericht unter **Lateral Movement-Pfade zu sensiblen Konten** abgeblendet. Wenn potenzielle Lateral Movement-Pfade mit relevanten Daten gefunden wurden, wird aus den Daten des Berichts automatisch das früheste Datum ausgewählt. Der Bericht über Lateral Movement-Pfade enthält Daten für bis zu 60 Tage.

 ![Berichte](./media/reports.png)

3. Klicken Sie auf **Herunterladen**.

4. Es wird eine Excel-Datei erstellt, die Details zu potenziellen Lateral Movement-Pfaden und der Anfälligkeit sensibler Konten für die ausgewählten Daten enthält. Die Registerkarte **Zusammenfassung** liefert Diagramme mit Informationen über die Anzahl sensibler Konten und Computer sowie Durchschnittswerte für gefährdeten Zugriff. Die Registerkarte **Details** enthält eine Liste der sensiblen Konten, die Sie genauer untersuchen sollten. Beachten Sie, dass die Pfade in dem herunterladbaren Bericht möglicherweise nicht mehr verfügbar sind, da sie im Verlauf der letzten 60 Tage ermittelt wurden und geändert worden sein können.


## <a name="investigate"></a>Untersuchen



1. Suchen Sie im Azure ATP-Portal nach dem Lateral Movement-Badge, das dem Entitätsprofil hinzugefügt wird, wenn sich die Entität in einem Lateral Movement-Pfad befindet. ![Symbol „lateral“](./media/lateral-movement-icon.png) oder ![Symbol „Pfad“](./media/paths-icon.png). Beachten Sie, dass Badges nur angezeigt werden, wenn in den letzten 48 Stunden ein Lateral Movement-Angriff stattgefunden hat. 

2. Klicken Sie auf der sich öffnenden Benutzerprofilseite auf die Registerkarte **Lateral Movement-Pfade**. 

3. Das angezeigte Diagramm bietet eine Übersicht der möglichen Pfade zum sensiblen Benutzer. Das Diagramm zeigt die möglichen Verbindungen, die in den letzten 48 Stunden beobachtet wurde. Wenn in den letzten zwei Tagen keine Aktivität erkannt wurde, wird das Diagramm nicht angezeigt. 

4. Überprüfen Sie den Graphen, um weitere Informationen über die Offenlegung der Anmeldeinformationen Ihres sensiblen Benutzers zu erhalten. Beispielsweise können Sie in dieser Zuordnung über den abgeblendeten Pfeil **Angemeldet durch** anzeigen lassen, wo sich Samira mit ihren privilegierten Anmeldeinformationen angemeldet hat. In diesem Fall wurden Samiras sensible Anmeldeinformationen auf dem Computer „REDMOND-WA-DEV“ gespeichert. Sehen Sie sich dann an, welche anderen Benutzer sich an welchen Computern angemeldet haben und die größte Anfälligkeit und das höchste Sicherheitsrisiko verursachten. Über den schwarzen Pfeil **Administrator auf** können Sie sich anzeigen lassen, wer Administratorrechte für die Ressource hat. In diesem Beispiel hat jeder in der Gruppe „Contoso All“ Zugriff auf die Benutzeranmeldeinformationen dieser Ressource.  

 ![Lateral Movement-Pfade zum Benutzerprofil](media/user-profile-lateral-movement-paths.png)


## <a name="preventative-best-practices"></a>Empfohlene präventive Methoden

- Sie können Lateral Movement-Angriffe am Besten verhindern, indem sie sicherstellen, dass sensible Benutzer ihre Administratoranmeldeinformationen nur dann verwenden, wenn sie sich an gehärteten Computern anmelden. Wenn die Administratorin Samira Zugriff auf „REDMOND-WA-DEV“ benötigt, sollten Sie im Beispiel sicherstellen, dass sie sich mit einem anderen Benutzernamen und Kennwort anmeldet als ihren Administratoranmeldeinformationen.

- Außerdem wird empfohlen, sicherzustellen, dass niemand unnötige administrative Berechtigungen hat. Im Beispiel sollten Sie überprüfen, ob jeder in der Gruppe „Contoso All“ wirklich Administratorrechte für „REDMOND-WA-DEV“ benötigt.

- Stellen Sie sicher, dass Personen nur Zugriff auf die Ressourcen haben, die sie benötigen. Im Beispiel erhöht Oscar Posada die Anfälligkeit von Samiras Konto signifikant. Ist es erforderlich, dass dieser Benutzer Mitglied in der Gruppe **Contoso All** ist? Können Untergruppen erstellt werden, mit denen sich die Anfälligkeit minimieren lässt?

**Tipp**: Auch wenn während der letzten 48 Stunden keine Aktivität erkannt wurde und das Diagramm nicht verfügbar ist, steht dennoch der Bericht zum Lateral Movement-Pfad zur Verfügung und stellt Ihnen Informationen zu potenziellen Lateral Movement-Pfaden bereit, die in den letzten 60 Tagen erkannt wurden. 

**Tipp**: Unter [Konfigurieren von SAM-R](install-atp-step8-samr.md) finden Sie Informationen darüber, wie Sie Ihre Clients und Server so einrichten, dass Azure ATP das Ausführen von den SAM-R-Vorgängen erlaubt wird, die für die Erkennung von Lateral Movement-Pfaden erforderlich sind.


## <a name="see-also"></a>Weitere Informationen

- [Konfigurieren von Azure ATP für das Ausführen von Remoteaufrufen an SAM](install-atp-step8-samr.md)
- [Arbeiten mit Sicherheitswarnungen](working-with-suspicious-activities.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)