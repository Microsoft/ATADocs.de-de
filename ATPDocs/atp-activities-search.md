---
title: 'Azure Advanced Threat Protection: Filtern und Durchsuchen von überwachten Aktivitäten'
description: Dieser Artikel bietet einen Überblick über die Vorgehensweise zum Filtern und Durchsuchen von überwachten Aktivitäten mit Azure ATP.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 09/15/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: a546703b-d5a9-404d-9e87-125523bb8421
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f65643c9d1483df44d5cd43f8d849c8241a076ef
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88956940"
---
# <a name="azure-atp-monitored-activities-search-and-filter"></a>Durchsuchen und Filtern von überwachten Azure ATP-Aktivitäten 

> [!NOTE]
> Die auf dieser Seite erläuterten Azure ATP-Features sind auch über das neue [Portal](https://portal.cloudappsecurity.com) zugänglich.

Die von Azure ATP in Ihrem Netzwerk erkannten Aktivitäten können während Ihrer Recherche und Untersuchung in Sicherheitswarnungen für einfaches Drilldown und Organisation durchsucht und gefiltert werden.  

Wählen Sie auf der Azure ATP-Zeitachse eine beliebige Entität in Ihrem Netzwerk (DC, Computer oder Benutzer) als Filterzugriffspunkt aus. Wählen Sie als Nächstes aus, ob Sie nach dem Typ **Sicherheitswarnung**, **Aktivität** oder einer beliebigen Kombination filtern möchten. Sobald der Filter angewendet wurde, wird die Bedrohungszeitachse der Entität mit den gefilterten Informationen aktualisiert. Ihre gefilterten Warnungen und Aktivitäten können auch heruntergeladen werden, um Ihre Untersuchung oder Nachverfolgung in anderen Tools fortzusetzen. 

![Filtern von Warnungen und Aktivitäten](media/activities-filter.png)

So filtern Sie Warnungen und Aktivitäten:
 1. Wählen Sie die zu untersuchende Entität in der Azure ATP-Zeitachse aus. 
 2. Klicken Sie auf **Filtern nach**, und wählen Sie die Warnungen und/oder Aktivitäten aus, die gefiltert werden sollen. 
 3. Klicken Sie auf **Übernehmen**. Die Entitätszeitachse wird entsprechend den ausgewählten Filtern aktualisiert. 
 4. Um die gefilterten Aktivitäten herunterzuladen, klicken Sie auf **Downloadaktivitäten**, und wählen Sie den Datumsbereich für Ihren heruntergeladenen Bericht aus. 
 5. Wenn Sie die Entitätszeitachse zurücksetzen möchten, um alle Warnungen und Aktivitäten anzuzeigen, klicken Sie auf **Zurücksetzen**, oder schließen Sie den Filter. 


## <a name="see-also"></a>Weitere Informationen:
- [Untersuchen von Entitäten](investigate-entity.md)
- [Integritätswarnungen](health-alerts.md)
- [Arbeiten mit Sicherheitswarnungen](working-with-suspicious-activities.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)
