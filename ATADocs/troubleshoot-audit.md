---
title: "Arbeiten mit ATA-Überwachungsprotokollen | Microsoft-Dokumentation"
description: "In diesem Artikel wird beschrieben, wie Sie mit ATA-Überwachungsprotokollen im Windows-Ereignisprotokoll arbeiten können."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d186a96-ef70-4787-aa64-c03d1db94ce0
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 287bb370f216c2f921eb954dfd4a34ceb8f095c7
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/07/2017
---
*Gilt für: Advanced Threat Analytics Version 1.8*

# <a name="working-with-ata-audit-logs"></a>Arbeiten mit ATA-Überwachungsprotokollen

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


## <a name="see-also"></a>Siehe auch
- [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
