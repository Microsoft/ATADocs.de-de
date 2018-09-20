---
title: Verwalten von systemgenerierten Advanced Threat Analytics-Protokollen | Microsoft-Dokumentation
description: Beschreibt die von ATA gesammelten Daten und enthält eine schrittweise Anleitung zum Deaktivieren der Datensammlung.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/26/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 0db1054f47d462251577a4d5251c07e8cd6283e8
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133408"
---
*Gilt für: Advanced Threat Analytics Version 1.9*



# <a name="manage-system-generated-logs-note"></a>Verwalten von systemgenerierten Protokollen> [!NOTE]

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

Advanced Threat Analytics (ATA) sammelt anonymisierte systemgenerierte Protokolldaten über ATA und überträgt die Daten über eine HTTPS-Verbindung an die Microsoft-Server.  Diese Daten werden von Microsoft zur Verbesserung von zukünftigen ATA-Versionen verwendet.

## <a name="data-collected"></a>Gesammelte Daten
Die gesammelten anonymisierten Daten enthalten folgende Parameter:

-   Leistungsindikatoren von ATA Center und vom ATA-Gateway

-   Produkt-ID von lizenzierten Kopien von ATA

-   Bereitstellungsdatum von ATA Center

-   Anzahl der bereitgestellten ATA-Gateways

-   Die folgenden anonymisierten Active Directory-Informationen:

    -   Domänen-ID für die erste Domäne der in alphabetischer Reihenfolge aufgelisteten Domänennamen

    -   Anzahl der Domänencontroller

    -   Anzahl der Domänencontroller, die von ATA über Portspiegelung überwacht werden

    -   Anzahl der Standorte

    -   Anzahl der Computer

    -   Anzahl der Gruppen

    -   Anzahl der Benutzer

-   Verdächtige Aktivitäten – die folgenden anonymisierten Daten werden für jede verdächtige Aktivität erfasst:

    (Computernamen, Benutzernamen und IP-Adressen werden **nicht** erfasst.)

    -   Art der verdächtigen Aktivität

    -   ID der verdächtigen Aktivität

    -   Status

    -   Start- und Endzeitpunkt

    -   Vorliegende Eingabe

- Integritätsprobleme – Die folgenden anonymisierten Daten werden für jedes Integritätsproblem erfasst:

    (Computernamen, Benutzernamen und IP-Adressen werden nicht erfasst.)

    -   Integritätsproblemtyp

    -   Integritätsproblem-ID

    -   Status

    -   Start- und Endzeitpunkt

- URL-Adressen der ATA-Konsole – URL-Adressen bei Verwendung der ATA-Konsole, d.h. welche Seiten in der ATA-Konsole besucht werden.


### <a name="disable-data-collection"></a>Datensammlung deaktivieren
Führen Sie die folgenden Schritte aus, um das Sammeln und Senden von Telemetriedaten an Microsoft zu beenden:

1.  Melden Sie sich bei der ATA-Konsole an, klicken Sie auf der Symbolleiste auf die drei Punkte, und wählen Sie **Info** aus.

2.  Deaktivieren Sie das Kontrollkästchen für **Senden Sie uns Nutzungsinformationen, um uns bei der Verbesserung der Benutzerfreundlichkeit zu unterstützen**.

## <a name="see-also"></a>Weitere Informationen
- [Behandeln von Problemen mit ATA mithilfe des Ereignisprotokolls](troubleshooting-ata-using-logs.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
