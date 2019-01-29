---
title: Behandlung von bekannten Problemen bei Azure ATP | Microsoft-Dokumentation
description: Beschreibt, wie Sie häufige Fehler in Azure ATP beheben können.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 23386e36-2756-4291-923f-fa8607b5518a
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6592d381f8a7e6d3f661a67a101ed5d1191a2b66
ms.sourcegitcommit: a0ebb0b6f140d4abf091ebd9d756b975b3d96b9d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/23/2019
ms.locfileid: "54458500"
---
# <a name="troubleshooting-azure-atp-known-issues"></a>Behandlung von bekannten Problemen bei Azure ATP 


## <a name="deployment-log-location"></a>Speicherort des Bereitstellungsprotokolls
 
Die Azure ATP-Bereitstellungsprotokolle befinden sich im temporären Verzeichnis des Benutzers, der das Produkt installiert hat. Beim Standardinstallationsspeicherort lautet der Pfad: C:\Benutzer\Administrator\AppData\Local\Temp (oder ein Verzeichnis über „%temp%“). Weitere Informationen finden Sie unter [Problembehandlung für den Azure Advanced Threat Protection-Sensor (ATP) mithilfe der ATP-Protokolle](troubleshooting-atp-using-logs.md).

## <a name="proxy-authentication-problem-presents-as-a-licensing-error"></a>Proxyauthentifizierungsproblem wird als Lizenzierungsfehler dargestellt

Während der Sensorinstallation erhalten Sie die folgende Fehlermeldung:  **Der Sensor konnte aufgrund von Lizenzierungsproblemen nicht registriert werden**.

Bereitstellungsprotokolleinträge: [1C 60: 1AA8] [2018-03-24T23:59:13] i000: 2018-03-25 02:59:13.1237 Info  InteractiveDeploymentManager ValidateCreateSensorAsync returned [\[]validateCreateSensorResult=LicenseInvalid[\]] [1C60:1AA8][2018-03-24T23:59:56]i000: 2018-03-25 02:59:56.4856 Info  InteractiveDeploymentManager ValidateCreateSensorAsync returned [\[]validateCreateSensorResult=LicenseInvalid[\]] [1C60:1AA8][2018-03-25T00:27:56]i000: 2018-03-25 03:27:56.7399 Debug SensorBootstrapperApplication Engine.Quit [\[]deploymentResultStatus=1602 isRestartRequired=False[\]] [1C60:15B8][2018-03-25T00:27:56]i500: Wird heruntergefahren, Exitcode: 0x642


**Ursache**:

In einigen Fällen, bei Kommunikation über einen Proxy, könnte dieser während der Authentifizierung dem Azure ATP-Sensor mit Fehler 401 oder 403 anstelle des Fehlers 407 antworten. Der Azure ATP-Sensor interpretiert Fehler 401 oder 403 als Lizenzierungsproblem und nicht als Proxyauthentifizierungsproblem. 

**Lösung:**

Stellen Sie sicher, dass der Sensor über den konfigurierten Proxy ohne Authentifizierung zu „*. atp.azure.com“ navigieren kann. Weitere Informationen finden Sie unter [Konfigurieren von Endpunktproxy- und Internetkonnektivitätseinstellungen für Ihren Azure ATP-Sensor](configure-proxy.md).




## Problem mit NIC-Teamvorgängen beim Azure ATP-Sensor <a name="nic-teaming"></a>

Wenn Sie versuchen, den ATP-Sensor auf einem Computer zu installieren, der mit einem NIC-Teaming-Adapter konfiguriert ist, wird ein Installationsfehler gemeldet. Wenn Sie den ATP-Sensor auf einem Computer installieren möchten, der mit NIC-Teamvorgang konfiguriert ist, gehen Sie wie folgt vor:

Wenn Sie den Sensor noch nicht installiert haben:

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

Mithilfe von Azure Advanced Threat Protection können Sie Azure ATP in Windows Defender ATP integrieren. Weitere Informationen finden Sie unter [Integrieren von Azure ATP in Windows Defender ATP](integrate-wd-atp.md). 

## <a name="vmware-virtual-machine-sensor-issue"></a>Problem mit dem Sensor des virtuellen VMware-Computers

Wenn Sie einen Azure-ATP-Sensor auf virtuellen VMware-Computern verwenden, erhalten Sie möglicherweise die Überwachungswarnung **Ein Teil des Netzwerkdatenverkehrs wird nicht analysiert**. Dies tritt aufgrund von Konfigurationskonflikten in VMware auf.

So beheben Sie das Problem

Legen Sie die folgenden Einstellungen in der NIC-Konfiguration des virtuellen Computers auf **0** (null) oder **Deaktiviert** fest: TsoEnable, LargeSendOffload, TSO Offload, Giant TSO Offload.
> [!NOTE]
> Für Azure ATP-Sensoren müssen Sie in der NIC-Konfiguration nur **IPv4 TSO Offload** deaktivieren.

 ![VMware-Sensorproblem](./media/vm-sensor-issue.png)

## <a name="see-also"></a>Weitere Informationen
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Azure ATP capacity planning (Azure ATP-Kapazitätsplanung)](atp-capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-forwarding.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)