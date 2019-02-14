---
title: Installieren von Advanced Threat Analytics – Schritt 2 | Microsoft-Dokumentation
description: Im zweiten Schritt beim Installieren von ATA konfigurieren Sie die Domänenverbindungseinstellungen auf dem ATA Center-Server.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 12/30/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: ebe3878ff8334367fad5260bc4bbd1cbd6b4613e
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2019
ms.locfileid: "56076197"
---
# <a name="install-ata---step-2"></a>Installieren von ATA – Schritt 2

*Gilt für: Advanced Threat Analytics Version 1.9*

> [!div class="step-by-step"]
> [« Schritt 1](install-ata-step1.md)
> [Schritt 3 »](install-ata-step3.md)

## <a name="step-2-provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>Schritt 2. Geben Sie einen Benutzernamen und ein Kennwort an, um eine Verbindung mit Ihrer Active Directory-Gesamtstruktur herzustellen

Beim ersten Öffnen der ATA-Konsole wird der folgende Bildschirm angezeigt:

![ATA welcome stage 1](media/ATA_1.7-welcome-provide-username.png)

1.  Geben Sie die folgenden Informationen ein, und klicken Sie anschließend auf **Speichern**.

    |Feld|Kommentare|
    |---------|------------|
    |**Benutzername** (erforderlich)|Geben Sie den schreibgeschützten Benutzernamen ein, z. B. **ATAuser**. **Hinweis:** Verwenden Sie **nicht** das UPN-Format für Ihren Benutzernamen.|
    |**Kennwort** (erforderlich)|Geben Sie das Kennwort für den schreibgeschützten Benutzer ein. Beispiel: **Pencil1**.|
    |**Domäne** (erforderlich)|Geben Sie die Domäne für den schreibgeschützten Benutzer ein, z. B. **contoso.com**. **Hinweis:** Es ist wichtig, dass Sie den vollqualifizierten Domänennamen (FQDN) der Domäne eingeben, in der sich das Benutzerkonto befindet. Wenn sich das Konto des Benutzers beispielsweise in der Domäne „corp.contoso.com“ befindet, müssen Sie `corp.contoso.com` und nicht „contoso.com“ eingeben.|

2. Sie können auf **Testverbindung** klicken, um die Konnektivität zur Domäne zu testen und um zu prüfen, ob der Zugriff mit den bereitgestellten Anmeldeinformationen erfolgreich ist. Dies ist möglich, wenn ATA Center mit der Domäne verbunden ist.    

    Nachdem Ihre Eingaben gespeichert wurden, ändert sich die Willkommensnachricht in der Konsole folgendermaßen: ![ATA welcome stage 1 finished](media/ATA_1.7-welcome-provide-username-finished.png)

3. Klicken Sie in der Konsole auf **Download Gateway setup and install the first Gateway** (Herunterladen des Gateway-Setups und Installieren des ersten Gateways) um den Vorgang fortzusetzen.


> [!div class="step-by-step"]
> [« Schritt 1](install-ata-step1.md)
> [Schritt 3 »](install-ata-step3.md)


## <a name="see-also"></a>Weitere Informationen
## <a name="related-videos"></a>Verwandte Videos
- [Übersicht über die ATA-Bereitstellung](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Auswählen des richtigen ATA-Gatewaytyps](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Weitere Informationen
- [Handbuch für die ATA POC-Bereitstellung](http://aka.ms/atapoc)
- [Tool zur Bemessung von ATA-Gateways](http://aka.ms/atasizingtool)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Voraussetzungen für ATA](ata-prerequisites.md)
