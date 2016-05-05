---
# required metadata

title: Überprüfen der Portspiegelung | Microsoft Advanced Threat Analytics
description: Beschreibt, wie die ordnungsgemäße Konfiguration der Portspiegelung überprüft wird.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: ebd41719-c91a-4fdd-bcab-2affa2a2cace

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Überprüfen der Portspiegelung
Die folgenden Schritte führen Sie durch das Verfahren, mit dem Sie die ordnungsgemäße Konfiguration der Portspiegelung überprüfen. Damit ATA ordnungsgemäß funktioniert, muss das ATA-Gateway den Datenverkehr zum und vom Domänencontroller anzeigen können. Als primäre Datenquelle verwendet ATA eine ausführliche Paketüberprüfung (Deep Packet Inspection) des Netzwerkdatenverkehrs zu und von den Domänencontrollern. Damit ATA den Netzwerkdatenverkehr anzeigen kann, muss die Portspiegelung konfiguriert sein. Die Portspiegelung kopiert den Datenverkehr von einem Port (dem Quellport) zu einem anderen Port (dem Zielport).

1.  Installieren Sie [Microsoft Netzwerkmonitor 3.4](http://www.microsoft.com/download/details.aspx?id=4865) oder ein anderes Netzwerküberwachungstool.

    > [!IMPORTANT]
    > Installieren Sie auf dem ATA-Gateway nicht Microsoft Message Analyzer oder ein andere Software zur Erfassung des Datenverkehrs.

2.  Öffnen Sie Netzwerkmonitor, und erstellen Sie eine neue Registerkarte für die Erfassung.

    1.  Wählen Sie nur den Netzwerkadapter **Erfassung** oder den Netzwerkadapter aus, der mit dem als Ziel der Portspiegelung konfigurierten Switchport verbunden ist.

    2.  Stellen Sie sicher, dass „P-Modus“ aktiviert ist.

    3.  Klicken Sie auf **Neue Erfassung**.

        ![Abbildung des Erstellens einer neuen Registerkarte für die Erfassung](media/ATA-Port-Mirroring-Capture.jpg)

3.  Geben Sie im Fenster „Anzeigefilter“ den folgenden Filter ein: **KerberosV5 oder LDAP**. Klicken Sie dann auf **Übernehmen**.

    ![Abbildung des Filters „KerberosV5 oder LDAP“](media/ATA-Port-Mirroring-filter-settings.jpg)

4.  Klicken Sie auf **Start**, um die Erfassungssitzung zu starten. Wenn der Datenverkehr zum und vom Domänencontroller nicht angezeigt wird, überprüfen Sie die Konfiguration der Portspiegelung.

    > [!NOTE]
    > Es ist wichtig, dass Ihnen der Datenverkehr zu und von den Domänencontrollern angezeigt wird.
    >
    > ![Abbildung Starten der Erfassungssitzung](media/ATA-Port-Mirroring-Capture-traffic.jpg)

5.  Wenn Ihnen nur Datenverkehr in eine Richtung angezeigt wird, sollten Sie mit Unterstützung Ihres Netzwerk- oder Virtualisierungsteams eine Problembehandlung für die Konfiguration der Portspiegelung durchführen.

## Siehe auch

- [Konfigurieren der Portspiegelung](configure-port-mirroring.md)
- [Unterstützung finden Sie in unserem Forum.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


