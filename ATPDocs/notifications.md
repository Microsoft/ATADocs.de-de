---
title: Festlegen von Microsoft Defender for Identity-Benachrichtigungen
description: Beschreibt, wie Microsoft Defender for Identity-Sicherheitswarnungen festgelegt werden, damit Sie bei verdächtigen Aktivitäten benachrichtigt werden.
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: ad02fab44b76fc9d30af59a331ec5243796224d5
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533646"
---
# <a name="set-microsoft-defender-for-identity-notifications"></a>Festlegen von Microsoft Defender for Identity-Benachrichtigungen

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
