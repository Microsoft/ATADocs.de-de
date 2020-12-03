---
title: Festlegen von Microsoft Defender for Identity-Benachrichtigungen
description: Beschreibt, wie Microsoft Defender for Identity-Sicherheitswarnungen festgelegt werden, damit Sie bei verdächtigen Aktivitäten benachrichtigt werden.
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: 49d78935b9246797b1d83f24a06a7ffe16f57699
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/03/2020
ms.locfileid: "96544469"
---
# <a name="set-product-long-notifications"></a>Festlegen von [!INCLUDE [Product long](includes/product-long.md)]-Benachrichtigungen

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
