---
title: Microsoft Defender für Identity Konfigurieren von Erkennungs Ausschlüsse und honeytoken-Konten
description: Konfigurieren des Ausschlusses von Erkennungen und von Honeytoken-Benutzern
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: e89beee20318fc5799e183af599bb10c91c0a35b
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/03/2020
ms.locfileid: "96543024"
---
# <a name="configure-detection-exclusions-and-honeytoken-accounts"></a>Konfigurieren von Ausschlüssen von Erkennungen und Honeytokenkonten

[!INCLUDE [Product long](includes/product-long.md)] ermöglicht den Ausschluss bestimmter IP-Adressen oder Benutzer aus einer Reihe von Erkennungen.

Angenommen, ein **DNS-Reconnaissance-Ausschluss** könnte eine Sicherheitsprüfung sein, die DNS als Überprüfungsmechanismus verwendet. Mit dem Ausschluss können [!INCLUDE [Product short](includes/product-short.md)] solche Scanner ignoriert werden.

[!INCLUDE [Product short](includes/product-short.md)] ermöglicht außerdem die Konfiguration von honeytoken-Konten, die als Traps für böswillige Actors verwendet werden. jede Authentifizierung, die mit diesen honeytoken-Konten verknüpft ist (normalerweise ruhende Weise), löst eine Warnung aus.

Dazu führen Sie folgende Schritte aus:

1. Klicken Sie im [!INCLUDE [Product short](includes/product-short.md)]-Portal auf das Symbol „Einstellungen“ und dann auf **Konfiguration**.

    ![[! Konfigurationseinstellungen für [Produkt Short] (includes/Product-Short. MD)] einschließen](media/config-menu.png)

1. Klicken Sie unter **Erkennung** auf **Entitätstag**.

1. Geben Sie unter **Honeytokenkonten** den Kontonamen des Honeytokens ein, und klicken Sie auf das **+** -Zeichen. Das Honeytoken-Kontenfeld kann gesucht werden und zeigt automatisch Entitäten in Ihrem Netzwerk an. Klicken Sie auf **Speichern**.

    ![Honeytoken](media/honeytoken-sensitive.png)

1. Klicken Sie auf **Ausschlüsse**. Geben Sie für jeden Bedrohungstyp ein Benutzerkonto oder eine IP-Adresse ein, das/die von der Erkennung ausgeschlossen werden soll.
1. Klicken Sie auf das *Plus*-Zeichen. Das Feld **Entität hinzufügen** (Benutzer oder Computer) kann durchsucht werden und wird automatisch mit Entitäten in Ihrem Netzwerk gefüllt. Weitere Informationen finden Sie unter [Ausschließen von Entitäten von Erkennungen](excluding-entities-from-detections.md) und im [Handbuch zu Sicherheitswarnungen](suspicious-activity-guide.md).

    ![Ausschließen von Entitäten von der Erkennung](media/exclusions.png)

1. Klicken Sie auf **Speichern**.

Herzlichen Glückwunsch, Sie haben die Bereitstellung erfolgreich abgeschlossen [!INCLUDE [Product long](includes/product-long.md)] !

Sie können nun die Angriffszeitleiste auf Sicherheitswarnungen prüfen, die aus erkannten Aktivitäten generiert wurden, sowie nach Benutzern oder Computern suchen und deren Profile anzeigen.

[!INCLUDE [Product short](includes/product-short.md)] die Überprüfung wird sofort gestartet. Einige Erkennungen, wie z. b. [verdächtige Ergänzungen von sensiblen Gruppen](domain-dominance-alerts.md#suspicious-additions-to-sensitive-groups-external-id-2024), erfordern einen Lernzeitraum und sind nicht sofort nach der [!INCLUDE [Product short](includes/product-short.md)] Bereitstellung verfügbar. Der Lernzeitraum für jede Warnung wird im ausführlichen Leitfaden zur [Sicherheitswarnung](suspicious-activity-guide.md)aufgeführt.

## <a name="see-also"></a>Weitere Informationen

- [[!INCLUDE [Product short](includes/product-short.md)]-Tool zur Größenanpassung](https://aka.ms/aatpsizingtool)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Voraussetzungen für [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
