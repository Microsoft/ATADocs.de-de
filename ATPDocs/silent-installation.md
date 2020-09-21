---
title: Automatisches Installieren von Azure Advanced Threat Protection
description: Hier wird die automatische Installation von Azure ATP beschrieben.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 07/27/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 24eca4c6-c949-42ea-97b9-41ef0fb611f1
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 07eefcf95846384ad490fa815f2415b771b73955
ms.sourcegitcommit: 0c356b0860ae8663254e0cf6f04001bcc91ce207
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/21/2020
ms.locfileid: "90828388"
---
# <a name="azure-atp-switches-and-silent-installation"></a>Azure ATP-Switches und automatische Installation

Dieser Artikel enthält Anleitungen und Informationen zu Azure ATP-Switches und der automatischen Installation.

## <a name="prerequisites"></a>Voraussetzungen

Azure ATP setzt die Installation von Microsoft .NET Framework 4.7 oder höher voraus.

Beim Installieren von Azure ATP wird .NET Framework 4.7 automatisch als Teil der Bereitstellung von Azure ATP installiert, sofern .NET Framework 4.7 oder höher noch nicht installiert ist.

> [!NOTE]
> Die Installation von .Net Framework 4.7 macht möglicherweise einen Neustart des Servers erforderlich. Wenn Sie den Azure ATP-Sensor auf Domänencontrollern installieren, sollten Sie die Planung eines Wartungsfensters für diese Domänencontroller in Betracht ziehen.

Wenn Sie die automatische Installation von Azure ATP verwenden, ist das Installationsprogramm so konfiguriert, dass der Server am Ende der Installation automatisch neu gestartet wird (falls erforderlich). Stellen Sie sicher, dass Sie die automatische Installation nur während eines Wartungsfensters ausführen. Aufgrund eines Windows Installer-Fehlers kann mit dem *norestart*-Flag nicht mehr verlässlich sichergestellt werden, dass der Server keinen Neustart ausführt.

Zur Nachverfolgung des Bereitstellungsfortschritts überwachen Sie die Protokolle des Azure ATP-Installationsprogramms unter `%AppData%\Local\Temp`.

## <a name="azure-atp-sensor-silent-installation"></a>Automatische Installation des Azure ATP-Sensors

> [!NOTE]
> Bei der automatischen Bereitstellung des Azure ATP-Sensors über System Center Configuration Manager oder ein anderes System zur Softwarebereitstellung empfiehlt es sich, zwei Bereitstellungspakete zu erstellen:</br>– Net Framework 4.7 oder höher, einschließlich möglichem Neustart des Domänencontrollers</br>– Azure ATP-Sensor. </br>Erstellen Sie eine Abhängigkeit des Azure ATP-Sensorpakets von der .NET Framework-Paketbereitstellung. </br>Rufen Sie das [.NET Framework 4.7-Paket für die Offlinebereitstellung](https://support.microsoft.com/help/3186497/the-net-framework-4-7-offline-installer-for-windows) ab.

Verwenden Sie den folgenden Befehl, um eine vollständig automatische Installation des Azure ATP-Sensors auszuführen:

**cmd.exe-Syntax**:

```dos
"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="<Access Key>"
```

**PowerShell-Syntax**:

```powershell
./"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="<Access Key>"
```

> [!NOTE]
> Beim Verwenden der PowerShell-Syntax führt das Auslassen des Präfixes **./** zu einem Fehler, der eine automatische Installation verhindert.

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
> |InstallationPath|InstallationPath=""|Nein|Legt den Pfad für die Installation der Binärdateien des AATP-Sensors fest. Standardpfad: %programfiles%\Azure Advanced Threat Protection sensor
> |AccessKey|AccessKey="\*\*"|Ja|Legt den Zugriffsschlüssel fest, mit dem der Azure ATP-Sensor bei der Azure ATP-Instanz registriert wird.|

**Beispiele**:

Verwenden Sie den folgenden Befehl für eine automatische Installation des Azure ATP-Sensors:

```dos
"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="mmAOkLYCzfH8L/zUIsH24BIJBevlAWu7wUcSfIkRJufpuEojaDHYdjrNs0P3zpD+/bObKfLS0puD7biT5KDf3g=="
```

## <a name="proxy-authentication"></a>Proxy-Authentifizierung

Verwenden Sie die folgenden Befehle, um die Proxyauthentifizierung abzuschließen:

**Syntax**:

> [!div class="mx-tableFixed"]
>
> |Name|Syntax|Erforderlich für die unbeaufsichtigte Installation?|Beschreibung|
> |-------------|----------|---------|---------|
> |ProxyUrl|ProxyUrl="http\://proxy.contoso.com:8080"|Nein|Gibt die ProxyUrl und die Portnummer für den Azure ATP Sensor an.|
> |ProxyUserName|ProxyUserName="Contoso\ProxyUser"|Nein|Wenn Ihr Proxydienst eine Authentifizierung erfordert, geben Sie einen Benutzernamen im Format „DOMÄNE\Benutzer“ an.|
> |ProxyUserPassword|ProxyUserPassword="P@ssw0rd"|Nein|Gibt das Kennwort für den Proxybenutzernamen an. *Anmeldeinformationen werden verschlüsselt und lokal vom Azure ATP-Sensor gespeichert.|

## <a name="update-the-azure-atp-sensor"></a>Aktualisieren des Azure ATP-Sensors

Verwenden Sie den folgenden Befehl, um den Azure ATP-Sensor automatisch zu aktualisieren:

**Syntax**:

```dos
"Azure ATP sensor Setup.exe" [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]
```

**Installationsoptionen**:

> [!div class="mx-tableFixed"]
>
> |Name|Syntax|Erforderlich für die unbeaufsichtigte Installation?|Beschreibung|
> |-------------|----------|---------|---------|
> |Quiet|/quiet|Ja|Führt das Installationsprogramm ohne Benutzeroberfläche und Eingabeaufforderungen aus.|
> |Hilfe|/help|Nein|Stellt Hilfe und eine Kurzübersicht bereit. Zeigt die korrekte Verwendung des Installationsbefehl einschließlich einer Liste aller Optionen und Verhaltensweisen an.|
> |NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Ja|Legt die Parameter für die Installation von .Net Framework fest. Muss festgelegt werden, um die unbeaufsichtigte Installation von .Net Framework zu erzwingen.|

**Beispiele**:

So aktualisieren Sie den Azure ATP-Sensor automatisch

```dos
"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q"
```

## <a name="uninstall-the-azure-atp-sensor-silently"></a>Automatisches Deinstallieren des Azure ATP-Sensors

Verwenden Sie den folgenden Befehl, um den Azure ATP-Sensor automatisch zu deinstallieren:

**Syntax**:

```dos
"Azure ATP sensor Setup.exe" [/quiet] [/Uninstall] [/Help]
```

**Installationsoptionen**:

> [!div class="mx-tableFixed"]
>
> |Name|Syntax|Erforderlich für die unbeaufsichtigte Deinstallation?|Beschreibung|
> |-------------|----------|---------|---------|
> |Quiet|/quiet|Ja|Führt das Deinstallationsprogramm ohne Benutzeroberfläche und Eingabeaufforderungen aus.|
> |Deinstallieren|/uninstall|Ja|Führt die automatische Deinstallation von Azure ATP-Sensor vom Server aus.|
> |Hilfe|/help|Nein|Stellt Hilfe und eine Kurzübersicht bereit. Zeigt die korrekte Verwendung des Installationsbefehl einschließlich einer Liste aller Optionen und Verhaltensweisen an.|

**Beispiele**:

So deinstallieren Sie den Azure ATP-Sensor automatisch vom Server aus

```dos
"Azure ATP sensor Setup.exe" /quiet /uninstall
```

## <a name="see-also"></a>Weitere Informationen

- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](prerequisites.md)
- [Installieren des Azure ATP-Sensors](install-step4.md)
- [Konfigurieren des Azure ATP-Sensors](install-step5.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
