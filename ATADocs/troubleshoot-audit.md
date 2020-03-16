---
title: Arbeiten mit ATA-Überwachungsprotokollen
description: In diesem Artikel wird beschrieben, wie Sie mit ATA-Überwachungsprotokollen im Windows-Ereignisprotokoll arbeiten können.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: rkarlin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1d186a96-ef70-4787-aa64-c03d1db94ce0
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1cec90e620591cd51f572e87f4d5e0296ee16d69
ms.sourcegitcommit: 11fff9d4ebf1c50b04f7789a22c80cdbc3e4416a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2020
ms.locfileid: "79414113"
---
# <a name="working-with-ata-audit-logs"></a>Arbeiten mit ATA-Überwachungsprotokollen


*Gilt für: Advanced Threat Analytics Version 1.9*

Die ATA-Überwachungsprotokolle befinden Sich im Windows-Ereignisprotokoll unter **Anwendungen und Dienste** und dann unter **Microsoft-ATA** sowohl in ATA Center als auch auf ATA-Gateway-Computern.

Das Überwachungsprotokoll von ATA Center enthält:
-   Informationen zu verdächtigen Aktivitäten
-   Überwachungswarnungen (Integritätsseite)
-   Logins in der ATA-Konsole
-   alle Konfigurationsänderungen*

Das Überwachungsprotokoll vom ATA-Gateway enthält:
-   Konfigurationsänderungen des Gateways* 

(Alle Konfigurationsänderungen des ATA-Gateways werden im ATA Center konfiguriert, werden aber trotzdem noch auf dem Gatewaycomputer selbst überwacht.)

*Das Überwachungsprotokoll zu Konfigurationsänderungen enthält sowohl die vorherige als auch die neue Konfiguration.


## <a name="see-also"></a>Weitere Informationen:
- [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
