---
title: "Installieren von ATA – Schritt 2 | Microsoft ATA"
description: "Im zweiten Schritt beim Installieren von ATA konfigurieren Sie die Domänenverbindungseinstellungen auf dem ATA Center-Server."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 050f1ef0b39d69b64ede53243a7fa2d33d0e4813
ms.openlocfilehash: fc268bcb2e3d027b09fa3349427934f60783b971


---

*Gilt für: Advanced Threat Analytics Version 1.7*



# Installieren von ATA – Schritt 2

>[!div class="step-by-step"]
[« Schritt 1](install-ata-step1.md)
[Schritt 3 »](install-ata-step3.md)

## Schritt 2. Geben Sie einen Benutzernamen und ein Kennwort an, um eine Verbindung mit Ihrer Active Directory-Gesamtstruktur herzustellen

Beim ersten Öffnen der ATA-Konsole wird der folgende Bildschirm angezeigt:

![ATA welcome stage 1](media/ATA_1.7-welcome-provide-username.png)

1.  Geben Sie die folgenden Informationen ein, und klicken Sie anschließend auf **Speichern**.

    |Feld|Kommentare|
    |---------|------------|
    |**Benutzername** (erforderlich)|Geben Sie den schreibgeschützten Benutzernamen ein, z.B. **ATAuser**.|
    |**Kennwort** (erforderlich)|Geben Sie das Kennwort für den schreibgeschützten Benutzer ein, z. B. **Pencil1**.|
    |**Domäne** (erforderlich)|Geben Sie die Domäne für den schreibgeschützten Benutzer ein, z. B. **contoso.com**. **Hinweis:** Es ist wichtig, dass Sie den vollqualifizierten Domänennamen (FQDN) der Domäne eingeben, in der sich das Benutzerkonto befindet. Wenn sich das Konto des Benutzers beispielsweise in der Domäne „corp.contoso.com“ befindet, müssen Sie `corp.contoso.com` und nicht „contoso.com“ eingeben.|
    |Alle ATA-Gateways automatisch aktualisieren |Wenn Sie diese Einstellung aktivieren, werden bei künftigen Versionen während des Updates von ATA Center alle ATA-Gateways automatisch aktualisiert.|

    Nachdem Ihre Eingaben gespeichert wurden, ändert sich die Willkommensnachricht in der Konsole folgendermaßen: ![ATA welcome stage 1 finished](media/ATA_1.7-welcome-provide-username-finished.png)

2. Klicken Sie in der Konsole auf **Download Gateway setup and install the first Gateway** (Herunterladen des Gateway-Setups und Installieren des ersten Gateways) um den Vorgang fortzusetzen.


>[!div class="step-by-step"]
[« Schritt 1](install-ata-step1.md)
[Schritt 3 »](install-ata-step3.md)


## Siehe auch

- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Voraussetzungen für ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=Aug16_HO5-->


