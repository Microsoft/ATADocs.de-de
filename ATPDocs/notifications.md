---
title: Festlegen von Microsoft Defender for Identity-Benachrichtigungen
description: Beschreibt, wie Microsoft Defender for Identity-Sicherheitswarnungen festgelegt werden, damit Sie bei verdächtigen Aktivitäten benachrichtigt werden.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 1cb2ea1c5f853f6f3a56d4bcccd84b5958078329
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93275581"
---
# <a name="set-product-long-notifications"></a>Festlegen von [!INCLUDE [Product long](includes/product-long.md)]-Benachrichtigungen

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

[!INCLUDE [Product long](includes/product-long.md)] kann Sie darüber benachrichtigen, wenn eine verdächtige Aktivität oder eine Integritätswarnung ermittelt wird, und gibt eine Sicherheitswarnung oder Integritätswarnung per E-Mail aus.

Legen Sie folgende Parameter fest, damit Benachrichtigungen an eine bestimmte E-Mail-Adresse gesendet werden:

1. Klicken Sie im [!INCLUDE [Product short](includes/product-short.md)]-Portal in der Symbolleiste erst auf die Einstellungsoption und dann auf **Konfiguration**.

    ![Symbol für die [!INCLUDE [Product short](includes/product-short.md)]-Konfigurationseinstellungen](media/config-menu.png)

1. Klicken Sie auf **Benachrichtigungen**.
1. Fügen Sie unter **E-Mail-Benachrichtigungen** die E-Mail-Adressen für die Benachrichtigungen hinzu, die Sie empfangen möchten: entweder für neue Warnungen (verdächtige Aktivitäten) oder neue Integritätsprobleme.

    > [!NOTE]
    >
    > - E-Mails werden nur für Benachrichtigungen mit definierten E-Mail-Adressen gesendet.
    > - E-Mail-Benachrichtigungen über verdächtige Aktivitäten werden nur beim Erstellen der verdächtigen Aktivität gesendet.

1. Klicken Sie auf **Speichern**.

    ![[!INCLUDE [Product short](includes/product-short.md)]-Benachrichtigungen](media/notifications.png)

## <a name="see-also"></a>Weitere Informationen

- [Konfigurieren der Ereignissammlung](configure-event-collection.md)

- [Set Syslog settings (Einrichten der Syslog-Einstellungen)](setting-syslog.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
