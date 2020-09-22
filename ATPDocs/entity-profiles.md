---
title: Arbeiten mit Benutzerprofilen im Azure Advanced Threat Protection-Portal
description: Informationen zum Untersuchen von Benutzern über die Anzeige „Benutzerprofile“ im Azure ATP-Portal
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 09/15/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 17458706-79fb-4c23-aa42-66979164a45f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2a967a058d7bc16ee7fd78a278180a17e4b245ee
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2020
ms.locfileid: "90913131"
---
# <a name="understanding-entity-profiles"></a>Grundlegendes zu Entitätsprofilen

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

> [!NOTE]
> Die auf dieser Seite erläuterten Azure ATP-Features sind auch über das neue [Portal](https://portal.cloudappsecurity.com) zugänglich.

Über das Entitätsprofil erhalten Sie eine umfassende Entitätsseite, die für eine detaillierte Untersuchung von Benutzern, Computern, Geräten und Ressourcen, auf die sie zugreifen können, sowie auf deren Verlauf, ausgerichtet ist. Die Profilseite nutzt den neuen logischen Aktivitätenübersetzer von Azure ATP, der eine Gruppe von Aktivitäten (für bis zu eine Minute zusammengefasst) überprüfen und diese in genau eine logische Aktivität gruppieren kann, um die tatsächlichen Aktivitäten der Benutzer zu verdeutlichen.

Wenn Sie auf die Profilseite einer Entität zugreifen möchten, klicken Sie auf der Zeitachse der verdächtigen Aktivität auf den Namen der Entität, z.B. den Benutzernamen.

Im Menü im linken Bereich erhalten Sie Informationen zu Active Directory, die zu der Entität verfügbar sind: E-Mail-Adresse, Domäne, Datum der ersten Aktivität. Wenn die Entität sensibel ist, wird angegeben, warum dies der Fall ist. Es wird z.B. angezeigt, ob der Benutzer oder das Mitglied einer sensiblen Gruppe als sensibel markiert ist.
Wenn es sich um einen sensiblen Benutzer handelt, wird das Symbol unterhalb des Benutzernamens angezeigt.

## <a name="view-entity-activities"></a>Anzeigen von Entitätsaktivitäten

Wenn Sie alle vom Benutzer ausgeführten Aktivitäten oder die Aktivitäten sehen möchten, die auf einer Entität durchgeführt werden, klicken Sie auf die Registerkarte **Aktivitäten**. 

 ![Aktivitäten des Benutzerprofils](media/user-profile-activities.png)

Standardmäßig wird im Hauptbereich des Entitätsprofils eine Zeitachse der Aktivitäten der Entität angezeigt (Verlauf von bis zu sechs Monaten). Über diese Zeitachse können Sie Detailinformationen zu den Entitäten anzeigen, auf die der Benutzer zugreift, bzw. können Sie die Benutzer abrufen, die auf die Entität zugegriffen haben.

Im oberen Bereich können Sie die Kacheln „Zusammenfassung“ abrufen, über die Sie auf einem Blick eine schnelle Übersicht zu den wichtigsten Informationen zu Ihrer Entität erhalten. Sie sehen z.B., auf wie vielen Computern der Benutzer angemeldet ist, auf wie viele Ressourcen zugegriffen wurden und von welchen Standorten aus sich der Benutzer über VPN angemeldet hat (falls konfiguriert). 

Wenn Sie die Schaltfläche **Filter by** (Filtern nach) oberhalb der Aktivitätszeitachse verwenden, können Sie die Aktivitäten nach Aktivitätstyp filtern. Außerdem können Sie auch einen bestimmten (störenden) Aktivitätstyp herausfiltern. Dies erweist sich für die Untersuchung als nützlich, wenn Sie die Grundlagen der Funktionsweise einer Entität im Netzwerk nachvollziehen möchten. Sie können auch ein bestimmtes Datum auswählen und die Aktivitäten als „Nach Excel gefiltert“ exportieren. In der exportierten Datei ist dann eine Seite mit Änderungen der Verzeichnisdienste (Dinge, die sich in Active Directory für das Konto geändert haben) und eine separate Seite mit den Aktivitäten enthalten. 

## <a name="view-directory-data"></a>Anzeigen der Verzeichnisdaten

In der Registerkarte **Verzeichnisdaten** erhalten Sie statische Informationen, die über Active Directory verfügbar sind, einschließlich Sicherheitsflags für die Benutzerzugriffssteuerung. Außerdem zeigt Azure ATP Gruppenmitgliedschaften für den Benutzer an, damit Sie überprüfen können, ob der Benutzer über eine direkte oder eine rekursive Mitgliedschaft verfügt. Für Gruppen führt Azure ATP die jeweiligen Mitglieder auf.

 ![Verzeichnisdaten des Benutzerprofils](media/user-profile-dir-data.png)

Im Abschnitt **Benutzerzugriffssteuerung** werden die Sicherheitseinstellungen für Azure ATP aufgelistet, die für Sie von Belang sein könnten. Sie können wichtige Flags zum Benutzer abrufen, die z.B. festlegen, ob der Benutzer die EINGABETASTE drücken kann, um das Kennwort zu umgehen, oder ob der Benutzer über ein Kennwort verfügt, das nicht abläuft. 

## <a name="view-lateral-movement-paths"></a>Anzeigen von Lateral Movement-Pfaden

Wenn Sie auf die Registerkarte „Lateral Movements-Pfade“ klicken, wird Ihnen eine vollständige, dynamische und klickbare Imagemap angezeigt, in der die Lateral Movement-Pfade, die im Zusammenhang mit diesem Benutzer stehen visuell darzustellen, die verwendet werden können, um in Ihr Netzwerk einzudringen.

Die Map enthält eine Liste, die Auskunft darüber gibt, wie viele Hops zwischen Computern oder Benutzern notwendig wären, damit ein Angreifer ein sensibles Konto gefährden kann. Wenn der Benutzer über ein sensibles Konto verfügt, können Sie zudem sehen, wie viele Ressourcen und Konten mit dem Konto direkt verbunden sind.

Wenn in den letzten zwei Tagen für die Entität kein potenzieller Lateral Movement-Pfad festgestellt wurde, wird der Graph nicht angezeigt. Wählen Sie ein anderes Datum mit **Ansicht eines anderen Datums**, um frühere Graphs der Lateral Movement-Pfade anzuzeigen, die für diese Entität entdeckt wurden. Der [Lateral Movement-Pfad-Bericht](reports.md) ist immer verfügbar und enthält Informationen über die erkannten potenziellen Lateral Movement-Pfade und kann nach Zeit angepasst werden.  

Weitere Informationen erhalten Sie unter [Lateral Movement-Pfade](use-case-lateral-movement-path.md). 

 ![Lateral Movement-Pfade zum Benutzerprofil](media/user-profile-lateral-movement-paths.png)


## <a name="see-also"></a>Weitere Informationen:

- [Untersuchen von Pfaden mit seitlicher Verschiebung mit Azure ATP](use-case-lateral-movement-path.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
