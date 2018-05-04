---
title: Behandlung von bekannten Problemen bei Azure ATP | Microsoft-Dokumentation
description: Beschreibt, wie Sie häufige Fehler in Azure ATP beheben können.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/10/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 23386e36-2756-4291-923f-fa8607b5518a
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2112e9fea1f316ff12d87b3a477b78bff4457a5f
ms.sourcegitcommit: e0209c6db649a1ced8303bb1692596b9a19db60d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
*Gilt für: Azure Advanced Threat Protection*


# <a name="troubleshooting-azure-atp-known-issues"></a>Behandlung von bekannten Problemen bei Azure ATP 


## <a name="deployment-log-location"></a>Speicherort des Bereitstellungsprotokolls
 
Die Azure ATP-Bereitstellungsprotokolle befinden sich im temporären Verzeichnis des Benutzers, der das Produkt installiert hat. Sie sind im Standardinstallationsverzeichnis unter „C:\Benutzer\Administrator\AppData\Local\Temp“ (oder in dem „%temp%“ übergeordneten Verzeichnis) zu finden.

## <a name="azure-atp-sensor-nic-teaming-issue"></a>Problem mit NIC-Teamvorgang beim Azure ATP-Sensor

Wenn Sie versuchen, den ATP-Sensor auf einem Computer zu installieren, der mit einem NIC-Teaming-Adapter konfiguriert ist, wird ein Installationsfehler gemeldet. Wenn Sie den ATP-Sensor auf einem Computer installieren möchten, der mit NIC-Teamvorgang konfiguriert ist, gehen Sie wie folgt vor:

Wenn den Sensor noch nicht installiert haben:

1.  Laden Sie Npcap von [https://nmap.org/npcap/](https://nmap.org/npcap/) herunter.
2.  Deinstallieren Sie WinPcap (falls installiert).
3.  Installieren Sie Npcap mit den folgenden Optionen: loopback_support=no & winpcap_mode=yes
4.  Installieren Sie das Sensorpaket.

Wenn der Sensor bereits installiert ist:

1.  Laden Sie Npcap von [https://nmap.org/npcap/](https://nmap.org/npcap/) herunter.
2.  Deinstallieren Sie den Sensor.
3.  Deinstallieren Sie WinPcap.
4.  Installieren Sie Npcap mit den folgenden Optionen: loopback_support=no & winpcap_mode=yes
5.  Installieren Sie das Sensorpaket erneut.

## <a name="windows-defender-atp-integration-issue"></a>Problem mit der Windows Defender-ATP-Integration

Mithilfe von Azure Advanced Threat Protection können Sie Azure ATP in Windows Defender ATP integrieren. Die Integration ist derzeit nur aktiviert, wenn Sie ein Windows Defender ATP-Kunde für die private Vorschau sind. 

## <a name="vmware-virtual-machine-sensor-issue"></a>Problem mit dem Sensor des virtuellen VMware-Computers

Wenn Sie einen Azure-ATP-Sensor auf virtuellen VMware-Computern verwenden, erhalten Sie möglicherweise die Überwachungswarnung **Ein Teil des Netzwerkdatenverkehrs wird nicht analysiert**. Dies tritt aufgrund von Konfigurationskonflikten in VMware auf.

So beheben Sie das Problem

Legen Sie die folgenden Einstellungen in der NIC-Konfiguration der VM auf **0 (null)** oder **Deaktiviert** fest: TsoEnable, LargeSendOffload, TSO Offload, Giant TSO Offload.
> [!NOTE]
> Für Azure ATP-Sensoren müssen Sie in der NIC-Konfiguration nur **IPv4 TSO Offload** deaktivieren.

 ![VMware-Sensorproblem](./media/vm-sensor-issue.png)

## <a name="see-also"></a>Weitere Informationen
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Azure ATP capacity planning (Azure ATP-Kapazitätsplanung)](atp-capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)