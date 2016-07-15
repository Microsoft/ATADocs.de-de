---
title: Verwalten von Telemetrieeinstellungen | Microsoft Advanced Threat Analytics
description: "Beschreibt die von ATA gesammelten Daten und enthält eine schrittweise Anleitung zum Deaktivieren der Datensammlung."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: c6b3196f6093b909e8d97f9a9ac230e35807eb72


---

# Verwalten von Telemetrieeinstellungen
Advanced Threat Analytics (ATA) sammelt anonymisierte Telemetriedaten über ATA und überträgt die Daten über eine HTTPS-Verbindung an Microsoft-Server.  Diese Daten werden von Microsoft zur Verbesserung von zukünftigen ATA-Versionen verwendet.

## Gesammelte Daten
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

### Datensammlung deaktivieren
Führen Sie die folgenden Schritte aus, um das Sammeln und Senden von Telemetriedaten an Microsoft zu beenden:

1.  Melden Sie sich bei der ATA-Konsole an, klicken Sie auf der Symbolleiste auf die drei Punkte, und wählen Sie **Info** aus.

2.  Deaktivieren Sie das Kontrollkästchen für **Senden Sie uns Nutzungsinformationen, um uns bei der Verbesserung der Benutzerfreundlichkeit zu unterstützen**.

## Weitere Informationen
- [Neuerungen in Version 1.6](/advanced-threat-analytics/understand-explore/whats-new-version-1.6)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jun16_HO4-->


