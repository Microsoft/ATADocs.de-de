---
title: Installieren von ATA | Microsoft ATA
description: Im letzten Schritt beim Installieren von ATA konfigurieren Sie die Subnetze mit kurzer Leasedauer und den Honeytoken-Benutzer.
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/28/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: e3b690767e5c6f5561a97a73eccfbf50ddb04148
ms.openlocfilehash: 57fe1272e95f69ef9d614505bbef0bb6c1d8ccb6


---

*Gilt für: Advanced Threat Analytics Version 1.7*



# Installieren von ATA – Schritt 6

>[!div class="step-by-step"]
[« Schritt 5](install-ata-step5.md)

## Schritt 6: Konfigurieren von IP-Adressausschlüssen und Honeytoken-Benutzern
ATA ermöglicht den Ausschluss von bestimmten IP-Adressen und IP-Subnetzen von zwei Typen von Erkennungen: **DNS-Reconnaissance** und **Pass-the-Ticket**. 

Angenommen, ein **DNS-Reconnaissance-Ausschluss** könnte eine Sicherheitsprüfung sein, die DNS als Überprüfungsmechanismus verwendet. Der Ausschluss hilft ATA, Überprüfungen dieser Art zu ignorieren. Ein Beispiel für einen *Pass-the-Ticket*-Ausschluss ist ein NAT-Gerät.    

ATA ermöglicht auch die Konfiguration eines Honeytoken-Benutzers, der als ein Trap für böswillige Teilnehmer verwendet wird – jede Authentifizierung die Ihrem (normalerweise ruhenden) Konto zugeordnet ist, löst eine Warnung aus.

Führen Sie folgende Schritte durch, um dies zu konfigurieren:

1.  Klicken Sie in der ATA-Konsole auf das Symbol „Einstellungen“, und wählen Sie **Konfiguration** aus.

    ![ATA-Konfigurationseinstellungen](media/ATA-config-icon.JPG)

2.  Geben Sie unter **Ausnahmen für die Erkennung** Folgendes für die *DNS-Reconnaissance*- oder die *Pass-the-Ticket*-IP-Adressen an. Verwenden Sie das CIDR-Format, z.B. `192.168.1.0/24`, und klicken Sie auf das *Pluszeichen*.

    ![Änderungen speichern](media/ATA-exclusions.png)

3.  Geben Sie unter **Einstellungen für die Erkennung** die Honeytoken-Konto-SIDs ein, und klicken Sie auf das Pluszeichen. Beispiel: `S-1-5-21-72081277-1610778489-2625714895-10511`.

    ![ATA-Konfigurationseinstellungen](media/ATA-honeytoken.png)

    > [!NOTE]
    > Die SID für einen Benutzer finden Sie, indem Sie in der ATA-Konsole nach dem Benutzer suchen und dann auf die Registerkarte **Kontoinformationen** klicken. 

4.  Klicken Sie auf **Speichern**.


Damit haben Sie Microsoft Advanced Threat Analytics erfolgreich bereitgestellt.

Sie können nun die Angriffszeitleiste auf erkannte verdächtige Aktivitäten prüfen sowie nach Benutzern oder Computern suchen und deren Profile anzeigen.

ATA startet sofort die automatische Überprüfung auf verdächtige Aktivitäten. Einige Aktivitäten, beispielsweise bestimmtes verdächtiges Verhalten, ist erst wieder verfügbar, nachdem ATA Verhaltensprofile erstellen konnte (nach mindestens drei Wochen).


>[!div class="step-by-step"]
[« Schritt 5](install-ata-step5.md)


## Weitere Informationen

- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Voraussetzungen für ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)




<!--HONumber=Aug16_HO5-->


