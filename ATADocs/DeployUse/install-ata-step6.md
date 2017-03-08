---
title: "Installieren von Advanced Threat Analytics – Schritt 6 | Microsoft-Dokumentation"
description: Im letzten Schritt der Installation von ATA konfigurieren Sie den Honeytoken-Benutzer.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 70b8c4886f1c7459412eafc0646abfe1cc5d37d3
ms.sourcegitcommit: 49e892a82275efa5146998764e850959f20d3216
translationtype: HT
---
*Gilt für: Advanced Threat Analytics Version 1.7*



# <a name="install-ata---step-6"></a>Installieren von ATA – Schritt 6

>[!div class="step-by-step"]
[« Schritt 5](install-ata-step5.md)

## <a name="step-6-configure--ip-address-exclusions-and-honeytoken-user"></a>Schritt 6: Konfigurieren von IP-Adressausschlüssen und Honeytoken-Benutzern
ATA ermöglicht den Ausschluss bestimmter IP-Adressen von zwei Arten der Erkennung: **DNS-Reconnaissance** und **Pass-the-Ticket**. 

Angenommen, ein **DNS-Reconnaissance-Ausschluss** könnte eine Sicherheitsprüfung sein, die DNS als Überprüfungsmechanismus verwendet. Der Ausschluss hilft ATA, Überprüfungen dieser Art zu ignorieren. Ein Beispiel für einen *Pass-the-Ticket*-Ausschluss ist ein NAT-Gerät.    

ATA ermöglicht auch die Konfiguration eines Honeytoken-Benutzers, der als ein Trap für böswillige Teilnehmer verwendet wird – jede Authentifizierung die Ihrem (normalerweise ruhenden) Konto zugeordnet ist, löst eine Warnung aus.

Führen Sie folgende Schritte durch, um dies zu konfigurieren:

1.  Klicken Sie in der ATA-Konsole auf das Symbol „Einstellungen“, und wählen Sie **Konfiguration** aus.

    ![ATA-Konfigurationseinstellungen](media/ATA-config-icon.JPG)

2.  Geben Sie unter **Ausnahmen für die Erkennung** die IP-Adresse für *DNS-Reconnaissance* oder *Pass-the-Ticket* ein, und klicken Sie auf das *Pluszeichen*.

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


## <a name="see-also"></a>Siehe auch

- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Voraussetzungen für ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)

