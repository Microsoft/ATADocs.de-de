---
title: Automatisches Installieren von Microsoft Defender für Identity
description: Hier wird beschrieben, wie Microsoft Defender für die Identität im Hintergrund installiert wird.
ms.date: 01/11/2021
ms.topic: how-to
ms.openlocfilehash: 0c22f5bcbffd415a81b84c94570cfcd7387aab56
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/16/2021
ms.locfileid: "100534394"
---
# <a name="microsoft-defender-for-identity-switches-and-silent-installation"></a>Microsoft Defender für Identitätswechsel und unbeaufsichtigte Installation

Dieser Artikel enthält Anleitungen und Anweisungen für [!INCLUDE [Product long](includes/product-long.md)] Switches und eine unbeaufsichtigte Installation.

## <a name="prerequisites"></a>Voraussetzungen

[!INCLUDE [Product short](includes/product-short.md)] erfordert die Installation von Microsoft .NET Framework 4,7 oder höher.

Wenn Sie installieren [!INCLUDE [Product short](includes/product-short.md)] , wird .NET Framework 4,7 automatisch als Teil der Bereitstellung von installiert, [!INCLUDE [Product short](includes/product-short.md)] Wenn .NET Framework 4,7 oder höher nicht bereits installiert ist.

> [!NOTE]
> Die Installation von .Net Framework 4.7 macht möglicherweise einen Neustart des Servers erforderlich. Wenn Sie den [!INCLUDE [Product short](includes/product-short.md)] Sensor auf Domänen Controllern installieren, sollten Sie ein Wartungsfenster für die Domänen Controller planen.

Mithilfe [!INCLUDE [Product short](includes/product-short.md)] der automatischen Installation wird das Installationsprogramm so konfiguriert, dass der Server am Ende der Installation (falls erforderlich) automatisch neu gestartet wird. Stellen Sie sicher, dass Sie die automatische Installation nur während eines Wartungsfensters ausführen. Aufgrund eines Windows Installer-Fehlers kann mit dem *norestart*-Flag nicht mehr verlässlich sichergestellt werden, dass der Server keinen Neustart ausführt.

Um den Bereitstellungs Fortschritt zu verfolgen, überwachen Sie die [!INCLUDE [Product short](includes/product-short.md)] Installations Protokolle in `%AppData%\Local\Temp` .

## <a name="defender-for-identity-sensor-silent-installation"></a>Defender für die automatische Installation des Identitäts Sensors

> [!NOTE]
> Bei der automatischen bereit [!INCLUDE [Product short](includes/product-short.md)] Stellung des Sensors über System Center Configuration Manager oder ein anderes Software Bereitstellungs System wird empfohlen, zwei Bereitstellungs Pakete zu erstellen:</br>– Net Framework 4.7 oder höher, einschließlich möglichem Neustart des Domänencontrollers</br>- [!INCLUDE [Product short](includes/product-short.md)] k. </br>Machen Sie das [!INCLUDE [Product short](includes/product-short.md)] sensorpaket von der Bereitstellung der .NET Framework-Paket Bereitstellung abhängig. </br>Rufen Sie das [.NET Framework 4.7-Paket für die Offlinebereitstellung](https://support.microsoft.com/help/3186497/the-net-framework-4-7-offline-installer-for-windows) ab.

Verwenden Sie den folgenden Befehl, um eine vollständig automatische Installation des Sensors durchzuführen [!INCLUDE [Product short](includes/product-short.md)] :

**cmd.exe-Syntax**:

```dos
"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="<Access Key>"
```

**PowerShell-Syntax**:

```powershell
.\"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="<Access Key>"
```

> [!NOTE]
> Beim Verwenden der PowerShell-Syntax führt das Auslassen des Präfixes **./** zu einem Fehler, der eine automatische Installation verhindert.

> [!NOTE]
> Kopieren Sie den Zugriffsschlüssel aus dem [!INCLUDE [Product short](includes/product-short.md)] Portal **Konfigurations** Abschnitt der Seite " **Sensoren** ".

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
> |InstallationPath|InstallationPath=""|Nein|Legt den Pfad für die Installation von [!INCLUDE [Product short](includes/product-short.md)] Sensor Binärdateien fest. Standardpfad: %programfiles%\Azure Advanced Threat Protection sensor
> |AccessKey|AccessKey="\*\*"|Ja|Legt die Zugriffstaste fest, die zum Registrieren des [!INCLUDE [Product short](includes/product-short.md)] Sensors bei der-Instanz verwendet wird [!INCLUDE [Product short](includes/product-short.md)] .|

**Beispiele**:

Verwenden Sie den folgenden Befehl, um den Sensor automatisch zu installieren [!INCLUDE [Product short](includes/product-short.md)] :

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
> |ProxyUrl|ProxyUrl="http\://proxy.contoso.com:8080"|Nein|Gibt die ProxyUrl und die Portnummer für den [!INCLUDE [Product short](includes/product-short.md)]-Sensor an.|
> |ProxyUserName|ProxyUserName="Contoso\ProxyUser"|Nein|Wenn Ihr Proxydienst eine Authentifizierung erfordert, geben Sie einen Benutzernamen im Format „DOMÄNE\Benutzer“ an.|
> |ProxyUserPassword|ProxyUserPassword="P@ssw0rd"|Nein|Gibt das Kennwort für den Proxybenutzernamen an. *Anmeldeinformationen werden verschlüsselt und vom [!INCLUDE [Product short](includes/product-short.md)]-Sensor lokal gespeichert.|

Weitere Informationen zur Proxykonfiguration finden Sie unter [Konfigurieren von Endpunkt Proxy-und internetkonnektivitätseinstellungen für den [!INCLUDE [Product long](includes/product-long.md)] Sensor](configure-proxy.md).

## <a name="update-the-defender-for-identity-sensor"></a>Defender für Identitäts Sensor aktualisieren

Verwenden Sie den folgenden Befehl, um den Sensor automatisch zu aktualisieren [!INCLUDE [Product short](includes/product-short.md)] :

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

So aktualisieren Sie den Sensor im Hintergrund [!INCLUDE [Product short](includes/product-short.md)] :

```dos
"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q"
```

<a name="silently-uninstall-sensor"></a>

## <a name="uninstall-the-defender-for-identity-sensor-silently"></a>Deinstallieren Sie den Defender für den Identitäts Sensor im Hintergrund.

Verwenden Sie den folgenden Befehl, um eine unbeaufsichtigte Deinstallation des Sensors durchzuführen [!INCLUDE [Product short](includes/product-short.md)] :

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
> |Deinstallieren|/uninstall|Ja|Führt die unbeaufsichtigte Installation des [!INCLUDE [Product short](includes/product-short.md)] Sensors vom Server aus.|
> |Hilfe|/help|Nein|Stellt Hilfe und eine Kurzübersicht bereit. Zeigt die korrekte Verwendung des Installationsbefehl einschließlich einer Liste aller Optionen und Verhaltensweisen an.|

**Beispiele**:

So deinstallieren Sie den [!INCLUDE [Product short](includes/product-short.md)] Sensor automatisch vom Server:

```dos
"Azure ATP sensor Setup.exe" /quiet /uninstall
```

## <a name="see-also"></a>Weitere Informationen

- [Voraussetzungen für [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md)
- [Installieren des [!INCLUDE [Product short](includes/product-short.md)] Sensors](install-step4.md)
- [Konfigurieren des [!INCLUDE [Product short](includes/product-short.md)] Sensors](install-step5.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
