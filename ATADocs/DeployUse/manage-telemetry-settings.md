---
# required metadata

title: Verwalten von Telemetrieeinstellungen | Microsoft Advanced Threat Analytics
description: Beschreibt die von ATA gesammelten Daten und enthält eine schrittweise Anleitung zum Deaktivieren der Datensammlung.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Verwalten von Telemetrieeinstellungen
Advanced Threat Analytics (ATA) sammelt anonyme Telemetriedaten über ATA und überträgt die Daten über eine HTTPS-Verbindung an Microsoft-Server.  Diese Daten werden von Microsoft zur Verbesserung von zukünftigen ATA-Versionen verwendet.

## Gesammelte Daten
Die gesammelten Daten enthalten folgende Elemente:

-   Leistungsindikatoren aus ATA Center und dem ATA-Gateway

-   Produkt-ID nach Lizenzierung von ATA

-   Bereitstellungsdatum von ATA Center

-   Anzahl der bereitgestellten ATA-Gateways

-   Folgende Active Directory-Informationen:

    -   Domänen-ID für die erste Domäne der in alphabetischer Reihenfolge aufgelisteten Domänennamen

    -   Anzahl der Domänencontroller

    -   Anzahl der Domänencontroller, die von ATA über Portspiegelung überwacht werden

    -   Anzahl der Standorte

    -   Anzahl der Computer

    -   Anzahl der Gruppen

    -   Anzahl der Benutzer

-   Verdächtige Aktivitäten – die folgenden Daten werden für jede verdächtige Aktivität erfasst:

    (Computernamen, Benutzernamen und IP-Adressen werden **nicht** erfasst.)

    -   Art der verdächtigen Aktivität

    -   ID der verdächtigen Aktivität

    -   Status

    -   Start- und Endzeitpunkt

    -   Vorliegende Eingabe

### Datensammlung deaktivieren
Befolgen Sie zum Anhalten der Datensammlung und Senden von Telemetriedaten an Microsoft folgende Schritte:

1.  Melden Sie sich bei der ATA-Konsole an, klicken Sie auf der Symbolleiste auf die drei Punkte, und wählen Sie **Info** aus.

2.  Deaktivieren Sie das Kontrollkästchen für **Senden Sie uns Nutzungsinformationen, um uns bei der Verbesserung der Benutzerfreundlichkeit zu unterstützen**.

## Siehe auch
- [Neuerungen in Version 1.5](whats-new-version-1.5.md)
- [Neuerungen in Version 1.4](whats-new-version-1.4.md)
- [Unterstützung finden Sie in unserem Forum.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


