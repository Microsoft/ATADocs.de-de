---
title: Einrichten von Azure Advanced Threat Protection-Benachrichtigungen
description: Beschreibt, wie Azure ATP-Sicherheitswarnungen festgelegt werden, damit Sie bei verdächtigen Aktivitäten benachrichtigt werden.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 09/29/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 4308f03e-b2a7-4e38-a750-540ff94faa81
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b60044cbc2ccf05ff1802ecce6e3e11d42543f97
ms.sourcegitcommit: dd8435ba20f76a6fc4590980c040c6fc7ec6c62b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/29/2020
ms.locfileid: "91451738"
---
# <a name="set-azure-atp-notifications"></a>Festlegen von Azure ATP-Benachrichtigungen

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Azure ATP kann Sie darüber benachrichtigen, wenn eine verdächtige Aktivität oder eine Integritätswarnung ermittelt wird, und gibt eine Sicherheitswarnung oder Integritätswarnung per E-Mail aus.

Legen Sie folgende Parameter fest, damit Benachrichtigungen an eine bestimmte E-Mail-Adresse gesendet werden:

1. Klicken Sie im Azure ATP-Portal in der Symbolleiste erst auf die Einstellungsoption und dann auf **Konfiguration**.

    ![Symbol der Azure ATP-Konfigurationseinstellungen](media/atp-config-menu.png)

1. Klicken Sie auf **Benachrichtigungen**.
1. Fügen Sie unter **E-Mail-Benachrichtigungen** die E-Mail-Adressen für die Benachrichtigungen hinzu, die Sie empfangen möchten: entweder für neue Warnungen (verdächtige Aktivitäten) oder neue Integritätsprobleme.

    > [!NOTE]
    >
    > - E-Mails werden nur für Benachrichtigungen mit definierten E-Mail-Adressen gesendet.
    > - E-Mail-Benachrichtigungen über verdächtige Aktivitäten werden nur beim Erstellen der verdächtigen Aktivität gesendet.

1. Klicken Sie auf **Speichern**.

    ![Azure ATP-Benachrichtigungen](media/atp-notifications.png)

## <a name="see-also"></a>Weitere Informationen

- [Konfigurieren der Ereignissammlung](configure-event-collection.md)

- [Set Syslog settings (Einrichten der Syslog-Einstellungen)](setting-syslog.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
