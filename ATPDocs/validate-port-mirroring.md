---
title: "Überprüfen der Portspiegelung in Azure Advanced Threat Protection | Microsoft-Dokumentation"
description: "Beschreibt, wie die ordnungsgemäße Konfiguration der Portspiegelung in Azure ATP überprüft wird."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/3/2018
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 0a56cf27-9eaa-4ad0-ae6c-9d0484c69094
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 7628fa491ddbe477cab7eb414409028c0f94f44d
ms.sourcegitcommit: 84556e94a3efdf20ca1ebf89a481550d7f8f0f69
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
*Gilt für: Azure Advanced Threat Protection*



# <a name="validate-port-mirroring"></a>Überprüfen der Portspiegelung
> [!NOTE] 
> Dieser Artikel ist für Sie nur interessant, wenn Sie den eigenständigen Azure ATP-Sensor anstelle des Azure ATP-Sensors bereitstellen. Lesen Sie den Abschnitt [Choosing the right sensors for your deployment (Auswählen der richtigen Sensoren für die Bereitstellung)](atp-capacity-planning#choosing-the-right-sensor-type-for-your-deployment), um zu ermitteln, ob Sie den Azure ATP-Sensor verwenden müssen.
 
Die folgenden Schritte führen Sie durch das Verfahren, mit dem Sie die ordnungsgemäße Konfiguration der Portspiegelung überprüfen. Damit Azure ATP ordnungsgemäß funktioniert, muss der eigenständige Azure ATP-Sensor den Datenverkehr zum und vom Domänencontroller anzeigen können. Als primäre Datenquelle verwendet Azure ATP eine ausführliche Paketüberprüfung (Deep Packet Inspection) des Netzwerkdatenverkehrs zu und von den Domänencontrollern. Damit Azure ATP den Netzwerkdatenverkehr anzeigen kann, muss die Portspiegelung konfiguriert sein. Die Portspiegelung kopiert den Datenverkehr von einem Port (dem Quellport) zu einem anderen Port (dem Zielport).

## <a name="validate-port-mirroring-using-net-mon"></a>Überprüfen von Portspiegelung mit Netzwerkmonitor (Network Monitor)
1.  Installieren Sie den [Microsoft-Netzwerkmonitor 3.4](http://www.microsoft.com/download/details.aspx?id=4865) auf dem eigenständigen ATP-Sensor, den Sie überprüfen möchten.

    > [!IMPORTANT]
    > Wenn Sie Wireshark installieren, um die Portspiegelung zu überprüfen, starten Sie den Dienst des eigenständigen Azure ATP-Sensors nach der Überprüfung neu.

2.  Öffnen Sie Netzwerkmonitor, und erstellen Sie eine neue Registerkarte für die Erfassung.

    1.  Wählen Sie nur den Netzwerkadapter **Erfassung** oder den Netzwerkadapter aus, der mit dem als Ziel der Portspiegelung konfigurierten Switchport verbunden ist.

    2.  Stellen Sie sicher, dass „P-Modus“ aktiviert ist.

    3.  Klicken Sie auf **Neue Erfassung**.

        ![Abbildung des Erstellens einer neuen Registerkarte für die Erfassung](media/atp-port-mirroring-capture.png)

3.  Geben Sie im Fenster „Anzeigefilter“ den folgenden Filter ein: **KerberosV5 oder LDAP**. Klicken Sie dann auf **Übernehmen**.

    ![Abbildung des Filters „KerberosV5 oder LDAP“](media/atp-port-mirroring-filter-settings.png)

4.  Klicken Sie auf **Start**, um die Erfassungssitzung zu starten. Wenn der Datenverkehr zum und vom Domänencontroller nicht angezeigt wird, überprüfen Sie die Konfiguration der Portspiegelung.

    ![Abbildung Starten der Erfassungssitzung](media/atp-port-mirroring-capture-traffic.png)

    > [!NOTE]
    > Es ist wichtig, dass Ihnen der Datenverkehr zu und von den Domänencontrollern angezeigt wird.
    

5.  Wenn Ihnen nur Datenverkehr in eine Richtung angezeigt wird, führen Sie mit Unterstützung Ihres Netzwerk- oder Virtualisierungsteams eine Problembehandlung für die Konfiguration der Portspiegelung durch.

## <a name="see-also"></a>Weitere Informationen

- [Configure event forwarding (Konfigurieren der Ereignisweiterleitung)](configure-event-forwarding.md)
- [Konfigurieren der Portspiegelung](configure-port-mirroring.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)