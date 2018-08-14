---
title: Automatisches Installieren von Azure Advanced Threat Protection | Microsoft-Dokumentation
description: Hier wird die automatische Installation von Azure ATP beschrieben.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/7/2017
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 24eca4c6-c949-42ea-97b9-41ef0fb611f1
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b318e4eefe05aee9ab99221d4ccd1e20764047a2
ms.sourcegitcommit: 1de2b047c0e9f92a106169f7634c480f694baf10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/13/2018
ms.locfileid: "39631632"
---
*Gilt für: Azure Advanced Threat Protection*


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
> Bei der automatischen Bereitstellung des Azure ATP-Sensors über System Center Configuration Manager oder ein anderes System zur Softwarebereitstellung empfiehlt es sich, zwei Bereitstellungspakete zu erstellen:</br>– Net Framework 4.7 einschließlich Neustart des Domänencontrollers</br>– Azure ATP-Sensor. </br>Erstellen Sie eine Abhängigkeit des Azure ATP-Sensorpakets von der .NET Framework-Paketbereitstellung. </br>Rufen Sie das [.NET Framework 4.7-Paket für die Offlinebereitstellung](https://www.microsoft.com/download/details.aspx?id=49982) ab. 


Verwenden Sie den folgenden Befehl, um eine vollständig automatische Installation des Azure ATP-Sensors auszuführen:


**Syntax**:

    Azure ATP sensor Setup.exe /AccessKey=<Access Key> /quiet NetFrameworkCommandLineArguments ="/q" 
   

> [!NOTE]
> Kopieren Sie den Zugriffsschlüssel aus dem Arbeitsbereichsportal unter **Konfiguration** > **Sensor**.


**Installationsoptionen**:

> [!div class="mx-tableFixed"]
|Name|Syntax|Erforderlich für die unbeaufsichtigte Installation?|Beschreibung|
|-------------|----------|---------|---------|
|Quiet|/quiet|Ja |Führt das Installationsprogramm ohne Benutzeroberfläche und Eingabeaufforderungen aus.|
|Hilfe|/help|Nein|Stellt Hilfe und eine Kurzübersicht bereit. Zeigt die korrekte Verwendung des Installationsbefehl einschließlich einer Liste aller Optionen und Verhaltensweisen an.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Ja |Legt die Parameter für die Installation von .Net Framework fest. Muss festgelegt werden, um die unbeaufsichtigte Installation von .Net Framework zu erzwingen.|

**Installationsparameter**:

> [!div class="mx-tableFixed"]
|Name|Syntax|Erforderlich für die unbeaufsichtigte Installation?|Beschreibung|
|-------------|----------|---------|---------|
|AccessKey|AccessKey="\*\*"|Ja |Legt den Zugriffsschlüssel fest, mit dem der Azure ATP-Sensor beim Azure ATP-Arbeitsbereich registriert wird.|

**Beispiele**: Melden Sie sich für eine automatische Installation des Azure ATP-Sensors mit Ihren Azure ATP-Administratoranmeldeinformationen bei dem in die Domäne eingebundenen Computer an, sodass Sie bei der Installation keine Anmeldeinformationen angeben müssen. Registrieren Sie ihn alternativ mit den angegebenen Anmeldeinformationen beim Azure ATP-Clouddienst:

    "Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" 
    AccessKey="3WlO0uKW7lY6Lk0+dfkfkJQ0qZV6aSq5WxLf71+fuBhggCl/BMs9JxfAwi7oy9vYGviazUS1EPpzte7z8s4grw==" 
    

## <a name="update-the-azure-atp-sensor"></a>Aktualisieren des Azure ATP-Sensors

Verwenden Sie den folgenden Befehl, um den Azure ATP-Sensor automatisch zu aktualisieren:

**Syntax**:

    Azure ATP sensor Setup.exe [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]


**Installationsoptionen**:

> [!div class="mx-tableFixed"]
|Name|Syntax|Erforderlich für die unbeaufsichtigte Installation?|Beschreibung|
|-------------|----------|---------|---------|
|Quiet|/quiet|Ja |Führt das Installationsprogramm ohne Benutzeroberfläche und Eingabeaufforderungen aus.|
|Hilfe|/help|Nein|Stellt Hilfe und eine Kurzübersicht bereit. Zeigt die korrekte Verwendung des Installationsbefehl einschließlich einer Liste aller Optionen und Verhaltensweisen an.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Ja |Legt die Parameter für die Installation von .Net Framework fest. Muss festgelegt werden, um die unbeaufsichtigte Installation von .Net Framework zu erzwingen.|


**Beispiele**: So aktualisieren Sie den Azure ATP-Sensor automatisch:

    Azure ATP sensor Setup.exe /quiet NetFrameworkCommandLineArguments="/q"

## <a name="uninstall-the-azure-atp-sensor-silently"></a>Automatisches Deinstallieren des Azure ATP-Sensors

Verwenden Sie den folgenden Befehl, um den Azure ATP-Sensor automatisch zu deinstallieren: **Syntax**:

    Azure ATP sensor Setup.exe [/quiet] [/Uninstall] [/Help]
    
**Installationsoptionen**:

> [!div class="mx-tableFixed"]
|Name|Syntax|Erforderlich für die unbeaufsichtigte Deinstallation?|Beschreibung|
|-------------|----------|---------|---------|
|Quiet|/quiet|Ja |Führt das Deinstallationsprogramm ohne Benutzeroberfläche und Eingabeaufforderungen aus.|
|Deinstallieren|/uninstall|Ja |Führt die automatische Deinstallation von Azure ATP-Sensor vom Server aus.|
|Hilfe|/help|Nein|Stellt Hilfe und eine Kurzübersicht bereit. Zeigt die korrekte Verwendung des Installationsbefehl einschließlich einer Liste aller Optionen und Verhaltensweisen an.|

**Beispiele**: So deinstallieren Sie den Azure ATP-Sensor automatisch vom Server aus:


    Azure ATP sensor Setup.exe /quiet /uninstall
    



## <a name="see-also"></a>Weitere Informationen

- [Configure event forwarding (Konfigurieren der Ereignisweiterleitung)](configure-event-forwarding.md)
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)
