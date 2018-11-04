---
title: Azure Advanced Threat Protection | Filtern und Durchsuchen von überwachten Aktivitäten | Microsoft-Dokumentation
description: Dieser Artikel bietet einen Überblick über die Vorgehensweise zum Filtern und Durchsuchen von überwachten Aktivitäten mit Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/28/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: a546703b-d5a9-404d-9e87-125523bb8421
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: fb3839d5348f11b13176375be84ecd46d44fa365
ms.sourcegitcommit: 3ab48f180aa0276f4e19cf7cd567581c7b4324cc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/28/2018
ms.locfileid: "50202474"
---
*Gilt für: Azure Advanced Threat Protection*


# <a name="azure-atp-monitored-activities-search-and-filter"></a>Durchsuchen und Filtern von überwachten Azure ATP-Aktivitäten 

Die von Azure ATP in Ihrem Netzwerk erkannten Aktivitäten können während Ihrer Recherche und Untersuchung in Sicherheitswarnungen für einfaches Drilldown und Organisation durchsucht und gefiltert werden.  

Wählen Sie auf der Azure ATP-Zeitachse eine beliebige Entität in Ihrem Netzwerk (DC, Computer oder Benutzer) als Filterzugriffspunkt aus. Wählen Sie als Nächstes aus, ob Sie nach dem Typ **Sicherheitswarnung**, **Aktivität** oder einer beliebigen Kombination filtern möchten. Sobald der Filter angewendet wurde, wird die Bedrohungszeitachse der Entität mit den gefilterten Informationen aktualisiert. Ihre gefilterten Warnungen und Aktivitäten können auch heruntergeladen werden, um Ihre Untersuchung oder Nachverfolgung in anderen Tools fortzusetzen. 

![Filtern von Warnungen und Aktivitäten](./media/activities-filter.png)

So filtern Sie Warnungen und Aktivitäten:
 1. Wählen Sie die zu untersuchende Entität in der Azure ATP-Zeitachse aus. 
 2. Klicken Sie auf **Filtern nach**, und wählen Sie die Warnungen und/oder Aktivitäten aus, die gefiltert werden sollen. 
 3. Klicken Sie auf **Übernehmen**. Die Entitätszeitachse wird entsprechend den ausgewählten Filtern aktualisiert. 
 4. Um die gefilterten Aktivitäten herunterzuladen, klicken Sie auf **Downloadaktivitäten**, und wählen Sie den Datumsbereich für Ihren heruntergeladenen Bericht aus. 
 5. Wenn Sie die Entitätszeitachse zurücksetzen möchten, um alle Warnungen und Aktivitäten anzuzeigen, klicken Sie auf **Zurücksetzen**, oder schließen Sie den Filter. 


## <a name="see-also"></a>Weitere Informationen
- [Untersuchen von Entitäten](investigate-entity.md)
- [Überwachen von Warnungen](monitoring-alerts.md)
- [Arbeiten mit Sicherheitswarnungen](working-with-suspicious-activities.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)