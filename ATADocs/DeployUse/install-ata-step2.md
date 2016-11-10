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
ms.sourcegitcommit: f334f9c8440e4bb0202579de220f6530d0aabad8
ms.openlocfilehash: 3f78d0dd6b1e3f419c7e72e0449f77e7d2b3167d


---

*Gilt für: Advanced Threat Analytics Version 1.7*



# <a name="install-ata-step-2"></a>Installieren von ATA – Schritt 2

>[!div class="step-by-step"]
[« Schritt 1](install-ata-step1.md)
[Schritt 3 »](install-ata-step3.md)

## <a name="step-2-provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>Schritt 2. Geben Sie einen Benutzernamen und ein Kennwort an, um eine Verbindung mit Ihrer Active Directory-Gesamtstruktur herzustellen

Beim ersten Öffnen der ATA-Konsole wird der folgende Bildschirm angezeigt:

![ATA welcome stage 1](media/ATA_1.7-welcome-provide-username.png)

1.  Geben Sie die folgenden Informationen ein, und klicken Sie anschließend auf **Speichern**.

    |Feld|Kommentare|
    |---------|------------|
    |**Benutzername** (erforderlich)|Geben Sie den schreibgeschützten Benutzernamen ein, z.B. **ATAuser**.|
    |**Kennwort** (erforderlich)|Geben Sie das Kennwort für den schreibgeschützten Benutzer ein, z. B. **Pencil1**.|
    |**Domäne** (erforderlich)|Geben Sie die Domäne für den schreibgeschützten Benutzer ein, z. B. **contoso.com**. **Hinweis:** Es ist wichtig, dass Sie den vollqualifizierten Domänennamen (FQDN) der Domäne eingeben, in der sich das Benutzerkonto befindet. Wenn sich das Konto des Benutzers beispielsweise in der Domäne „corp.contoso.com“ befindet, müssen Sie `corp.contoso.com` und nicht „contoso.com“ eingeben.|

2. Optional können Sie auf **Testverbindung** klicken, um die Konnektivität zur Domäne zu testen und um zu prüfen, ob der Zugriff mit den bereitgestellten Anmeldeinformationen erfolgreich ist. Dies ist nur möglich, wenn das ATA-Center mit der Domäne verbunden ist.   

    Nachdem Ihre Eingaben gespeichert wurden, ändert sich die Willkommensnachricht in der Konsole folgendermaßen: ![ATA welcome stage 1 finished](media/ATA_1.7-welcome-provide-username-finished.png)

3. Klicken Sie in der Konsole auf **Download Gateway setup and install the first Gateway** (Herunterladen des Gateway-Setups und Installieren des ersten Gateways) um den Vorgang fortzusetzen.


>[!div class="step-by-step"]
[« Schritt 1](install-ata-step1.md)
[Schritt 3 »](install-ata-step3.md)


## <a name="see-also"></a>Siehe auch

- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Voraussetzungen für ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=Oct16_HO5-->


