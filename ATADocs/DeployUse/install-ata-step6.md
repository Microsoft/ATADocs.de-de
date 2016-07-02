---
title: Installieren von ATA | Microsoft Advanced Threat Analytics
description: Im letzten Schritt beim Installieren von ATA konfigurieren Sie die Subnetze mit kurzer Leasedauer und den Honeytoken-Benutzer.
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: 76305bc5f55e956c787fe3e8bd954a56f40fc56f


---

# Installieren von ATA – Schritt 6

>[!div class="step-by-step"]
[« Schritt 5](install-ata-step5.md)

## Schritt 6: Konfigurieren der Subnetze mit kurzer Leasedauer und des Honeytoken-Benutzers
Subnetze mit kurzer Leasedauer sind Subnetze, bei denen die IP-Adresszuweisung sehr rasch wechselt, d. h. innerhalb von Sekunden oder Minuten. Dabei handelt es sich beispielsweise um IP-Adressen für Ihre virtuellen privaten Netzwerke oder um WLAN-IP-Adressen. Führen Sie die folgenden Schritte aus, um die Liste der in Ihrer Organisation verwendeten Subnetze mit kurzer Leasedauer einzugeben:

1.  Klicken Sie in der ATA-Konsole auf dem ATA-Gatewaycomputer auf das Symbol „Einstellungen“, und wählen Sie **Konfiguration** aus.

    ![ATA-Konfigurationseinstellungen](media/ATA-config-icon.JPG)

2.  Geben Sie unter **Erkennung** Folgendes für die Subnetze mit kurzer Leasedauer ein. Geben Sie die Subnetze mit kurzer Leasedauer im Notationsformat mit Schrägstrich ein, z. B. `192.168.0.0/24`, und klicken Sie auf das Pluszeichen.

3.  Geben Sie für die Honeytoken-Konto-SIDs die SID für das Benutzerkonto ein, das keine Netzwerkaktivität aufweist, und klicken Sie dann auf das Pluszeichen. Beispiel: `S-1-5-21-72081277-1610778489-2625714895-10511`.

    > [!NOTE]
    > Die SID für einen Benutzer finden Sie, indem Sie in der ATA-Konsole nach dem Benutzer suchen und dann auf die Registerkarte **Kontoinformationen** klicken. 

4.  Konfigurieren von Ausschlüssen: Sie können in der Konfiguration festlegen, dass IP-Adressen von bestimmten verdächtigen Aktivitäten ausgeschlossen werden. Weitere Informationen finden Sie unter [Arbeiten mit ATA-Erkennungseinstellungen](working-with-detection-settings.md).

5.  Klicken Sie auf **Speichern**.

![Änderungen speichern](media/ATA-VPN-Subnets.JPG)

Damit haben Sie Microsoft Advanced Threat Analytics erfolgreich bereitgestellt.

Sie können nun die Angriffszeitleiste auf erkannte verdächtige Aktivitäten prüfen sowie nach Benutzern oder Computern suchen und deren Profile anzeigen.

ATA startet sofort die automatische Überprüfung auf verdächtige Aktivitäten. Einige Aktivitäten, beispielsweise bestimmtes verdächtiges Verhalten, ist erst wieder verfügbar, nachdem ATA Verhaltensprofile erstellen konnte (nach mindestens drei Wochen).


>[!div class="step-by-step"]
[« Schritt 5](install-ata-step5.md)


## Weitere Informationen

- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Voraussetzungen für ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)




<!--HONumber=Jun16_HO4-->


