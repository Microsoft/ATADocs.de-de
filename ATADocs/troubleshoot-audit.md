---
title: Arbeiten mit ATA-Überwachungsprotokollen | Microsoft-Dokumentation
description: In diesem Artikel wird beschrieben, wie Sie mit ATA-Überwachungsprotokollen im Windows-Ereignisprotokoll arbeiten können.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: barbkess
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 1d186a96-ef70-4787-aa64-c03d1db94ce0
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 020ae7a28e2120c51c873b5e67adb14436c56ad1
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2019
ms.locfileid: "56076477"
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


## <a name="see-also"></a>Weitere Informationen
- [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
