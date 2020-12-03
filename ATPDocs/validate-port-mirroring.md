---
title: Überprüfen der Portspiegelung in Microsoft Defender for Identity
description: Hier wird beschrieben, wie die ordnungsgemäße Konfiguration der Portspiegelung in Microsoft Defender for Identity überprüft wird.
ms.date: 10/27/2020
ms.topic: how-to
ms.openlocfilehash: 80944d45e92533a37edcbb855f913ea605bdef1d
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/03/2020
ms.locfileid: "96544265"
---
# <a name="validate-port-mirroring"></a>Überprüfen der Portspiegelung

Dieser Artikel ist für Sie nur interessant, wenn Sie den eigenständigen [!INCLUDE [Product long](includes/product-long.md)]-Sensor anstelle des [!INCLUDE [Product short](includes/product-short.md)]-Sensors bereitstellen.

> [!NOTE]
> Eigenständige [!INCLUDE [Product short](includes/product-short.md)]-Server unterstützen nicht die Erstellung von Protokolleinträgen für Ereignisablaufverfolgung für Windows (Event Tracing for Windows, ETW), die Daten für mehrere Erkennungen bereitstellen. Zur vollständigen Abdeckung Ihrer Umgebung empfiehlt es sich, den [!INCLUDE [Product short](includes/product-short.md)]-Sensor bereitzustellen.

Die folgenden Schritte führen Sie durch das Verfahren, mit dem Sie die ordnungsgemäße Konfiguration der Portspiegelung überprüfen. Damit [!INCLUDE [Product short](includes/product-short.md)] ordnungsgemäß funktioniert, muss der eigenständige [!INCLUDE [Product short](includes/product-short.md)]-Sensor den Datenverkehr zum und vom Domänencontroller anzeigen können. Als primäre Datenquelle verwendet [!INCLUDE [Product short](includes/product-short.md)] eine ausführliche Paketüberprüfung (Deep Packet Inspection) des Netzwerkdatenverkehrs zu und von den Domänencontrollern. Damit [!INCLUDE [Product short](includes/product-short.md)] den Netzwerkdatenverkehr anzeigen kann, muss die Portspiegelung konfiguriert sein. Die Portspiegelung kopiert den Datenverkehr von einem Port (dem Quellport) zu einem anderen Port (dem Zielport).

## <a name="validate-port-mirroring-using-net-mon"></a>Überprüfen von Portspiegelung mit Netzwerkmonitor (Network Monitor)

1. Installieren Sie den [Microsoft-Netzwerkmonitor 3.4](https://www.microsoft.com/download/details.aspx?id=4865) auf dem eigenständigen [!INCLUDE [Product short](includes/product-short.md)]-Sensor, den Sie überprüfen möchten.

    > [!IMPORTANT]
    > Wenn Sie Wireshark installieren, um die Portspiegelung zu überprüfen, starten Sie den Dienst des eigenständigen [!INCLUDE [Product short](includes/product-short.md)]-Sensors nach der Überprüfung neu.

1. Öffnen Sie Netzwerkmonitor, und erstellen Sie eine neue Registerkarte für die Erfassung.

    1. Wählen Sie nur den Netzwerkadapter **Erfassung** oder den Netzwerkadapter aus, der mit dem als Ziel der Portspiegelung konfigurierten Switchport verbunden ist.

    1. Stellen Sie sicher, dass „P-Modus“ aktiviert ist.

    1. Klicken Sie auf **Neue Erfassung**.

        ![Abbildung des Erstellens einer neuen Registerkarte für die Erfassung](media/port-mirroring-capture.png)

1. Geben Sie im Fenster „Anzeigefilter“ den folgenden Filter ein: **KerberosV5 oder LDAP**. Klicken Sie dann auf **Übernehmen**.

    ![Abbildung des Filters „KerberosV5 oder LDAP“](media/port-mirroring-filter-settings.png)

1. Klicken Sie auf **Start**, um die Erfassungssitzung zu starten. Wenn der Datenverkehr zum und vom Domänencontroller nicht angezeigt wird, überprüfen Sie die Konfiguration der Portspiegelung.

    ![Abbildung Starten der Erfassungssitzung](media/port-mirroring-capture-traffic.png)

    > [!NOTE]
    > Es ist wichtig, dass Ihnen der Datenverkehr zu und von den Domänencontrollern angezeigt wird.

1. Wenn Ihnen nur Datenverkehr in eine Richtung angezeigt wird, führen Sie mit Unterstützung Ihres Netzwerk- oder Virtualisierungsteams eine Problembehandlung für die Konfiguration der Portspiegelung durch.

## <a name="see-also"></a>Weitere Informationen

- [Configure event forwarding (Konfigurieren der Ereignisweiterleitung)](configure-event-forwarding.md)
- [Konfigurieren der Portspiegelung](configure-port-mirroring.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
