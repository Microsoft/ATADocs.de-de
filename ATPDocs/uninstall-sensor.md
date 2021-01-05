---
title: Deinstallieren von Microsoft Defender für Identity Sensor
description: In diesem Artikel wird beschrieben, wie Sie den Microsoft Defender für Identity-Sensor von Domänen Controllern deinstallieren.
ms.date: 12/22/2020
ms.topic: how-to
ms.openlocfilehash: f8a41923635509eaeb414d43e1bd19fe9cd3a813
ms.sourcegitcommit: 3a478353118670b8124bc62d33751d8ba6af109d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/23/2020
ms.locfileid: "97746907"
---
# <a name="uninstall-the-product-long-sensor"></a>Deinstallieren des [!INCLUDE [Product long](includes/product-long.md)] Sensors

In diesem Artikel wird beschrieben, wie Sie den [!INCLUDE [Product long](includes/product-long.md)] Sensor von Domänen Controllern für die folgenden Szenarien deinstallieren:

1. Deinstallieren eines Sensors von einem Domänen Controller
1. Entfernen eines verwaisten Sensors
1. Entfernen eines duplizierten Sensors

## <a name="uninstall-a-sensor-from-a-domain-controller"></a>Deinstallieren eines Sensors von einem Domänen Controller

In den folgenden Schritten wird beschrieben, wie Sie einen Sensor von einem Domänen Controller deinstallieren.

1. Melden Sie sich mit lokalen Administratorrechten beim Domänen Controller an.
1. Klicken Sie im Windows- **Startmenü** auf **Einstellungen**  >  **Systemsteuerung** Software  >  .
1. Wählen Sie die Sensorinstallation aus, klicken Sie auf **deinstallieren**, und befolgen Sie die Anweisungen zum Entfernen des Sensors.

## <a name="remove-an-orphaned-sensor"></a>Entfernen eines verwaisten Sensors

Dieses Szenario kann auftreten, wenn ein Domänen Controller gelöscht wurde, ohne zuvor den Sensor zu deinstallieren, und der Sensor im Portal angezeigt wird [!INCLUDE [Product short](includes/product-short.md)] .

1. Wechseln [!INCLUDE [Product short](includes/product-short.md)] Sie im Portal zu **Konfiguration** , und wählen Sie im Abschnitt **System** die Option **Sensoren** aus.
1. Suchen Sie nach dem verwaisten Sensor, und klicken Sie am Ende der Zeile auf **Löschen** (Papierkorb Symbol).

    ![Verwaiste löschen [! INCLUDE [Product Short] (includes/Product-Short. MD)] Sensor von der Seite "Sensoren"](media/delete-orphaned-sensor.png)

## <a name="remove-a-duplicate-sensor"></a>Entfernen eines duplizierten Sensors

Dieses Szenario kann nach einem direkten Sensor Upgrade auftreten, und der Sensor wird zweimal im [!INCLUDE [Product short](includes/product-short.md)] Portal angezeigt.

1. Wechseln [!INCLUDE [Product short](includes/product-short.md)] Sie im Portal zu **Konfiguration** , und wählen Sie im Abschnitt **System** die Option **Sensoren** aus.
1. Suchen Sie nach dem verwaisten Sensor, und klicken Sie am Ende der Zeile auf **Löschen** (Papierkorb Symbol).

## <a name="see-also"></a>Weitere Informationen

- [Automatischen Deinstallieren des [!INCLUDE [Product short](includes/product-short.md)] Sensors](silent-installation.md#silently-uninstall-sensor)
