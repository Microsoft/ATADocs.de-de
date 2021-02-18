---
title: Microsoft Defender für die Identitäts Erkennung Konfigurieren von Ausschlüssen
description: Konfiguration der Erkennungs Ausschlüsse.
ms.date: 02/17/2021
ms.topic: how-to
ms.openlocfilehash: 802b54f3185a50468fe4227d4099b9edbfc8f469
ms.sourcegitcommit: 5bf0c6a204b71126306a0c64108eaf9cb7fc042f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/18/2021
ms.locfileid: "101097367"
---
# <a name="configure-detection-exclusions"></a>Konfigurieren von Erkennungs Ausschlüssen

[!INCLUDE [Product long](includes/product-long.md)] ermöglicht den Ausschluss bestimmter IP-Adressen, Computer oder Benutzer aus einer Reihe von Erkennungen.

Angenommen, ein **DNS-Reconnaissance-Ausschluss** könnte eine Sicherheitsprüfung sein, die DNS als Überprüfungsmechanismus verwendet. Mit dem Ausschluss können [!INCLUDE [Product short](includes/product-short.md)] solche Scanner ignoriert werden.

## <a name="how-to-add-detection-exclusions"></a>Hinzufügen von Erkennungs Ausschlüsse

Es gibt zwei Möglichkeiten, Benutzer, Computer oder IP-Adressen für eine Erkennung manuell auszuschließen. Dies können Sie entweder auf der **Konfigurations** Seite unter **Ausschlüsse** oder direkt in der Sicherheitswarnung tun.

### <a name="from-the-configuration-page"></a>Auf der Seite "Konfiguration"

Gehen Sie folgendermaßen vor, um die Ausschlüsse auf der Seite Konfiguration zu konfigurieren:

1. Wählen Sie im [!INCLUDE [Product short](includes/product-short.md)]-Portal **Konfiguration** aus.

    ![[! Konfigurationseinstellungen für [Produkt Short] (includes/Product-Short. MD)] einschließen](media/config-menu.png)

1. Klicken Sie unter **Erkennung** auf **Ausschlüsse**.
1. Führen Sie für jede zu konfigurierende Erkennung die folgenden Schritte aus:
    1. Geben Sie eine IP-Adresse, einen Computer oder ein Benutzerkonto ein, die von der Erkennung ausgeschlossen werden sollen.
    1. Klicken Sie auf das Pluszeichen **(+)**.

    > [!TIP]
    > Das Feld Benutzer oder Computer ist durchsuchbar und wird automatisch mit Entitäten in Ihrem Netzwerk ausgefüllt. Weitere Informationen finden Sie im [Handbuch zur Sicherheitswarnung](suspicious-activity-guide.md).

    ![Ausschließen von Entitäten von der Erkennung](media/exclusions.png)

1. Klicken Sie auf **Speichern**.

### <a name="from-a-security-alert"></a>Aus einer Sicherheitswarnung

Gehen Sie folgendermaßen vor, um Ausschlüsse aus einer Sicherheitswarnung zu konfigurieren:

1. [!INCLUDE [Product short](includes/product-short.md)]Wählen Sie im Portal die Option **Zeitachse** aus.
1. Identifizieren Sie eine Warnung zu einer Aktivität für einen Benutzer, Computer oder eine IP-Adresse, die zum Ausführen der jeweiligen Aktivität berechtigt **ist** .

1. Klicken Sie rechts von der Warnung auf **mehr [...].**  >  **Schließen und ausschließen**. Die Aktion schließt die Warnung und ist nicht mehr in der Liste **geöffnete** Ereignisse in der Warnungs **Zeitachse** aufgeführt. Die Aktion fügt auch den Benutzer, Computer oder die IP-Adresse der Ausschlussliste für diese Warnung hinzu.

    ![Ausschließen einer Entität](media/exclude-in-sa.png)

[!INCLUDE [Product short](includes/product-short.md)] die Überprüfung wird sofort gestartet. Einige Erkennungen, wie z. b. [verdächtige Ergänzungen von sensiblen Gruppen](domain-dominance-alerts.md#suspicious-additions-to-sensitive-groups-external-id-2024), erfordern einen Lernzeitraum und sind nicht sofort nach der [!INCLUDE [Product short](includes/product-short.md)] Bereitstellung verfügbar. Der Lernzeitraum für jede Warnung wird im ausführlichen Leitfaden zur [Sicherheitswarnung](suspicious-activity-guide.md)aufgeführt.

## <a name="see-also"></a>Weitere Informationen

- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
