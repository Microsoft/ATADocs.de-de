---
title: Installieren von Advanced Threat Analytics (Schritt 2)
description: Im zweiten Schritt beim Installieren von ATA konfigurieren Sie die Domänenverbindungseinstellungen auf dem ATA Center-Server.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 12/30/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: e7f88831d10cfb1ba15d2fe650a056e7a3004d2f
ms.sourcegitcommit: 5bf0c6a204b71126306a0c64108eaf9cb7fc042f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/18/2021
ms.locfileid: "101097512"
---
# <a name="install-ata---step-2"></a>Installieren von ATA – Schritt 2

[!INCLUDE [Banner for top of topics](includes/banner.md)]

> [!div class="step-by-step"]
> [«Schritt 1](install-ata-step1.md) 
>  [Schritt 3»](install-ata-step3.md)

## <a name="step-2-provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>Schritt 2 Geben Sie einen Benutzernamen und ein Kennwort an, um eine Verbindung mit Ihrer Active Directory-Gesamtstruktur herzustellen

Beim ersten Öffnen der ATA-Konsole wird der folgende Bildschirm angezeigt:

![ATA welcome stage 1](media/ATA_1.7-welcome-provide-username.png)

1. Geben Sie die folgenden Informationen ein, und klicken Sie anschließend auf **Speichern**.

    |Feld|Kommentare|
    |---------|------------|
    |**Benutzername** (erforderlich)|Geben Sie den schreibgeschützten Benutzernamen ein, z.B. **ATAuser**. **Hinweis:** Verwenden Sie **nicht** das UPN-Format für Ihren Benutzernamen.|
    |**Kennwort** (erforderlich)|Geben Sie das Kennwort für den schreibgeschützten Benutzer ein, z. B. **Pencil1**.|
    |**Domäne** (erforderlich)|Geben Sie die Domäne für den schreibgeschützten Benutzer ein, z. B. **contoso.com**. **Hinweis:** Es ist wichtig, dass Sie den vollqualifizierten Domänennamen (FQDN) der Domäne eingeben, in der sich das Benutzerkonto befindet. Wenn sich das Konto des Benutzers beispielsweise in der Domäne „corp.contoso.com“ befindet, müssen Sie `corp.contoso.com` und nicht „contoso.com“ eingeben.|

1. Sie können auf **Testverbindung** klicken, um die Konnektivität zur Domäne zu testen und um zu prüfen, ob der Zugriff mit den bereitgestellten Anmeldeinformationen erfolgreich ist. Dies ist möglich, wenn ATA Center mit der Domäne verbunden ist.

    Nachdem Ihre Eingaben gespeichert wurden, ändert sich die Willkommensnachricht in der Konsole folgendermaßen: ![ATA welcome stage 1 finished](media/ATA_1.7-welcome-provide-username-finished.png)

1. Klicken Sie in der Konsole auf **Download Gateway setup and install the first Gateway** (Herunterladen des Gateway-Setups und Installieren des ersten Gateways) um den Vorgang fortzusetzen.

> [!div class="step-by-step"]
> [«Schritt 1](install-ata-step1.md) 
>  [Schritt 3»](install-ata-step3.md)

## <a name="related-videos"></a>Verwandte Videos

- [Übersicht über die ATA-Bereitstellung](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Auswählen des richtigen ATA-Gatewaytyps](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)

## <a name="see-also"></a>Siehe auch

- [Handbuch für die ATA POC-Bereitstellung](/samples/browse/?redirectedfrom=TechNet-Gallery)
- [Tool zur Bemessung von ATA-Gateways](https://aka.ms/atasizingtool)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [ATA-Voraussetzungen](ata-prerequisites.md)