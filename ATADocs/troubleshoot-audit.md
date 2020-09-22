---
title: Arbeiten mit ATA-Überwachungsprotokollen
description: In diesem Artikel wird beschrieben, wie Sie mit ATA-Überwachungsprotokollen im Windows-Ereignisprotokoll arbeiten können.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1d186a96-ef70-4787-aa64-c03d1db94ce0
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 14f818e8149e239f8c7b88487b4fb388ad557458
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2020
ms.locfileid: "90910814"
---
# <a name="working-with-ata-audit-logs"></a>Arbeiten mit ATA-Überwachungsprotokollen


[!INCLUDE [Banner for top of topics](includes/banner.md)]

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Die ATA-Überwachungsprotokolle befinden Sich im Windows-Ereignisprotokoll unter **Anwendungen und Dienste** und dann unter **Microsoft-ATA** sowohl in ATA Center als auch auf ATA-Gateway-Computern.

Das Überwachungsprotokoll von ATA Center enthält:
- Informationen zu verdächtigen Aktivitäten
- Integritäts Warnungen (Seite Integrität)
- Logins in der ATA-Konsole
- alle Konfigurationsänderungen*

Das Überwachungsprotokoll vom ATA-Gateway enthält:
- Konfigurationsänderungen des Gateways* 

(Alle Konfigurationsänderungen des ATA-Gateways werden im ATA Center konfiguriert, werden aber trotzdem noch auf dem Gatewaycomputer selbst überwacht.)

*Das Überwachungsprotokoll zu Konfigurationsänderungen enthält sowohl die vorherige als auch die neue Konfiguration.


## <a name="see-also"></a>Weitere Informationen
- [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
