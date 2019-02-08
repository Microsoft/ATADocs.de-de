---
title: Automatisches Installieren von Azure Advanced Threat Protection | Microsoft-Dokumentation
description: Hier wird die automatische Installation von Azure ATP beschrieben.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 12/05/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 24eca4c6-c949-42ea-97b9-41ef0fb611f1
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 1710b5f2f96814f2dbe3229473b06c8a963fd380
ms.sourcegitcommit: cc5017770583042ef8bf90c9c0ece020a0166b91
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/31/2019
ms.locfileid: "55480980"
---
# <a name="azure-atp-switches-and-silent-installation"></a>Azure ATP-Switches und automatische Installation
Dieser Artikel enthält Anleitungen und Informationen zu Azure ATP-Switches und der automatischen Installation.

## <a name="prerequisites"></a>Voraussetzungen

Azure ATP erfordert die Installation von Microsoft .NET Framework 4.7. 

Beim Installieren von Azure ATP wird .NET Framework 4.7 automatisch als Teil der Bereitstellung von Azure ATP installiert.

> [!IMPORTANT] 
> Stellen Sie sicher, dass Sie die neueste Version von .NET Framework installiert haben. Wenn Sie eine frühere Version von .NET installiert haben, bleibt die automatische Azure ATP-Installation in einer Schleife hängen und schlägt fehl. 

> [!NOTE] 
> Die Installation von .Net Framework 4.7 macht möglicherweise einen Neustart des Servers erforderlich. Wenn Sie den Azure ATP-Sensor auf Domänencontrollern installieren, sollten Sie die Planung eines Wartungsfensters für diese Domänencontroller in Betracht ziehen.
Wenn Sie die automatische Installation von Azure ATP verwenden, ist das Installationsprogramm so konfiguriert, dass der Server am Ende der Installation automatisch neu gestartet wird (falls erforderlich). Stellen Sie sicher, dass Sie die automatische Installation nur während eines Wartungsfensters ausführen. Aufgrund eines Windows Installer-Fehlers kann mit dem *norestart*-Flag nicht mehr verlässlich sichergestellt werden, dass der Server keinen Neustart ausführt.

Zur Nachverfolgung des Bereitstellungsfortschritts überwachen Sie die Protokolle des Azure ATP-Installationsprogramms unter **%AppData%\Local\Temp**.


## <a name="azure-atp-sensor-silent-installation"></a>Automatische Installation des Azure ATP-Sensors

> [!NOTE]
> Bei der automatischen Bereitstellung des Azure ATP-Sensors über System Center Configuration Manager oder ein anderes System zur Softwarebereitstellung empfiehlt es sich, zwei Bereitstellungspakete zu erstellen:</br>– .NET Framework 4.7 einschließlich möglichem Neustart des Domänencontrollers</br>– Azure ATP-Sensor. </br>Erstellen Sie eine Abhängigkeit des Azure ATP-Sensorpakets von der .NET Framework-Paketbereitstellung. </br>Rufen Sie das [.NET Framework 4.7-Paket für die Offlinebereitstellung](https://support.microsoft.com/help/3186497/the-net-framework-4-7-offline-installer-for-windows) ab. 


Verwenden Sie den folgenden Befehl, um eine vollständig automatische Installation des Azure ATP-Sensors auszuführen:


**Syntax**:

    "Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="<Access Key>"

> [!NOTE]
> Kopieren Sie den Zugriffsschlüssel, der im Azure ATP-Portal auf der Seite **Sensor** im Abschnitt **Konfiguration** angezeigt wird.


**Installationsoptionen**:

> [!div class="mx-tableFixed"]
> 
> |Name|Syntax|Erforderlich für die unbeaufsichtigte Installation?|Beschreibung|
> |-------------|----------|---------|---------|
> |Quiet|/quiet|Ja|Führt das Installationsprogramm ohne Benutzeroberfläche und Eingabeaufforderungen aus.|
> |Hilfe|/help|Nein|Stellt Hilfe und eine Kurzübersicht bereit. Zeigt die korrekte Verwendung des Installationsbefehl einschließlich einer Liste aller Optionen und Verhaltensweisen an.|
> |NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Ja|Legt die Parameter für die Installation von .Net Framework fest. Muss festgelegt werden, um die unbeaufsichtigte Installation von .Net Framework zu erzwingen.|

**Installationsparameter**:

> [!div class="mx-tableFixed"]
> 
> |Name|Syntax|Erforderlich für die unbeaufsichtigte Installation?|Beschreibung|
> |-------------|----------|---------|---------|
> |AccessKey|AccessKey="\*\*"|Ja|Legt den Zugriffsschlüssel fest, mit dem der Azure ATP-Sensor bei der Azure ATP-Instanz registriert wird.|

**Beispiele**: Verwenden Sie den folgenden Befehl für eine automatische Installation des Azure ATP-Sensors:

    "Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="mmAOkLYCzfH8L/zUIsH24BIJBevlAWu7wUcSfIkRJufpuEojaDHYdjrNs0P3zpD+/bObKfLS0puD7biT5KDf3g=="


## <a name="update-the-azure-atp-sensor"></a>Aktualisieren des Azure ATP-Sensors

Verwenden Sie den folgenden Befehl, um den Azure ATP-Sensor automatisch zu aktualisieren:

**Syntax**:

    Azure ATP sensor Setup.exe [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]


**Installationsoptionen**:

> [!div class="mx-tableFixed"]
> 
> |Name|Syntax|Erforderlich für die unbeaufsichtigte Installation?|Beschreibung|
> |-------------|----------|---------|---------|
> |Quiet|/quiet|Ja|Führt das Installationsprogramm ohne Benutzeroberfläche und Eingabeaufforderungen aus.|
> |Hilfe|/help|Nein|Stellt Hilfe und eine Kurzübersicht bereit. Zeigt die korrekte Verwendung des Installationsbefehl einschließlich einer Liste aller Optionen und Verhaltensweisen an.|
> |NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Ja|Legt die Parameter für die Installation von .Net Framework fest. Muss festgelegt werden, um die unbeaufsichtigte Installation von .Net Framework zu erzwingen.|


**Beispiele**: So aktualisieren Sie den Azure ATP-Sensor automatisch

    Azure ATP sensor Setup.exe /quiet NetFrameworkCommandLineArguments="/q"

## <a name="uninstall-the-azure-atp-sensor-silently"></a>Automatisches Deinstallieren des Azure ATP-Sensors

Verwenden Sie den folgenden Befehl, um den Azure ATP-Sensor automatisch zu deinstallieren: **Syntax**:

    Azure ATP sensor Setup.exe [/quiet] [/Uninstall] [/Help]

**Installationsoptionen**:

> [!div class="mx-tableFixed"]
> 
> |Name|Syntax|Erforderlich für die unbeaufsichtigte Deinstallation?|Beschreibung|
> |-------------|----------|---------|---------|
> |Quiet|/quiet|Ja|Führt das Deinstallationsprogramm ohne Benutzeroberfläche und Eingabeaufforderungen aus.|
> |Deinstallieren|/uninstall|Ja|Führt die automatische Deinstallation von Azure ATP-Sensor vom Server aus.|
> |Hilfe|/help|Nein|Stellt Hilfe und eine Kurzübersicht bereit. Zeigt die korrekte Verwendung des Installationsbefehl einschließlich einer Liste aller Optionen und Verhaltensweisen an.|

**Beispiele**: So deinstallieren Sie den Azure ATP-Sensor automatisch vom Server aus


    Azure ATP sensor Setup.exe /quiet /uninstall




## <a name="see-also"></a>Weitere Informationen

- [Voraussetzungen für Azure ATP](atp-prerequisites.md)
- [Installieren des Azure ATP-Sensors](install-atp-step4.md)
- [Konfigurieren des Azure ATP-Sensors](install-atp-step5.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
