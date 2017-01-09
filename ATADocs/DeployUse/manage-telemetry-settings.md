---
title: Verwalten von Telemetrieeinstellungen | Microsoft Docs
description: "Beschreibt die von ATA gesammelten Daten und enthält eine schrittweise Anleitung zum Deaktivieren der Datensammlung."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 85e285c5d88e5916e0bf0eb7dd327cb4cb45b4cb
ms.openlocfilehash: c7366dcc2cbd7a9eba1503e5af3290ec4ac73c32


---

*Gilt für: Advanced Threat Analytics Version 1.7*



# <a name="manage-telemetry-settings"></a>Verwalten von Telemetrieeinstellungen
Advanced Threat Analytics (ATA) sammelt anonymisierte Telemetriedaten über ATA und überträgt die Daten über eine HTTPS-Verbindung an Microsoft-Server.  Diese Daten werden von Microsoft zur Verbesserung von zukünftigen ATA-Versionen verwendet.

## <a name="data-collected"></a>Gesammelte Daten
Die gesammelten anonymisierten Daten enthalten folgende Elemente:

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

- URL-Adressen der ATA-Konsole – URL-Adressen bei Verwendung der ATA-Konsole, d.h. welche Seite in der ATA-Konsole besucht werden.


### <a name="disable-data-collection"></a>Datensammlung deaktivieren
Führen Sie die folgenden Schritte aus, um das Sammeln und Senden von Telemetriedaten an Microsoft zu beenden:

1.  Melden Sie sich bei der ATA-Konsole an, klicken Sie auf der Symbolleiste auf die drei Punkte, und wählen Sie **Info** aus.

2.  Deaktivieren Sie das Kontrollkästchen für **Senden Sie uns Nutzungsinformationen, um uns bei der Verbesserung der Benutzerfreundlichkeit zu unterstützen**.

## <a name="see-also"></a>Siehe auch
- [Neuigkeiten in Version 1.6](/advanced-threat-analytics/understand-explore/whats-new-version-1.6)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jan17_HO1-->


