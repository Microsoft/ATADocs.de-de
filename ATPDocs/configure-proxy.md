---
title: Konfigurieren Ihres Proxys oder Ihrer Firewall zum Aktivieren der Microsoft Defender for Identity-Kommunikation mit dem Sensor
description: Hier wird beschrieben, wie Sie Ihren Proxy oder Ihre Firewall so einrichten, dass die Kommunikation zwischen dem Microsoft Defender for Identity-Clouddienst und Microsoft Defender for Identity-Sensoren möglich ist.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6b2b620895d0a59886a140ff340b6772744c6bac
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2020
ms.locfileid: "94848651"
---
# <a name="configure-endpoint-proxy-and-internet-connectivity-settings-for-your-product-long-sensor"></a>Konfigurieren der Einstellungen für Endpunktproxy und Internetkonnektivität für Ihren [!INCLUDE [Product long](includes/product-long.md)]-Sensor

Jeder [!INCLUDE [Product long](includes/product-long.md)]-Sensor erfordert Internetkonnektivität mit dem [!INCLUDE [Product short](includes/product-short.md)]-Clouddienst, damit er erfolgreich betrieben werden und Sensordaten melden kann. In einigen Organisationen sind die Domänencontroller nicht direkt mit dem Internet verbunden, sondern über eine Webproxyverbindung.

Es wird empfohlen, den Proxyserver mithilfe der Befehlszeile zu konfigurieren. Dadurch wird sichergestellt, dass nur die [!INCLUDE [Product short](includes/product-short.md)]-Sensordienste über den Proxy kommunizieren.

## <a name="configure-proxy-server-using-the-command-line"></a>Konfigurieren des Proxyservers über die Befehlszeile

Sie können den Proxyserver während der Sensorinstallation mithilfe der folgenden Befehlszeilenoptionen konfigurieren.

### <a name="syntax"></a>Syntax

"Azure ATP sensor Setup.exe" [/quiet] [/Help] [ProxyUrl="http://proxy.internal.com"] [ProxyUserName="domain\proxyuser"] [ProxyUserPassword="ProxyPassword"]

### <a name="switch-descriptions"></a>Beschreibungen der Befehlszeilenoptionen

> [!div class="mx-tableFixed"]
>
> |Name|Syntax|Erforderlich für die unbeaufsichtigte Installation?|Beschreibung|
> |-------------|----------|---------|---------|
> |ProxyUrl|ProxyUrl="http\://proxy.contoso.com:8080"|Nein|Gibt die ProxyUrl und die Portnummer für den [!INCLUDE [Product short](includes/product-short.md)]-Sensor an.|
> |ProxyUserName|ProxyUserName="Contoso\ProxyUser"|Nein|Wenn Ihr Proxydienst eine Authentifizierung erfordert, geben Sie einen Benutzernamen im Format „DOMÄNE\Benutzer“ an.|
> |ProxyUserPassword|ProxyUserPassword="P@ssw0rd"|Nein|Gibt das Kennwort für den Proxybenutzernamen an. *Anmeldeinformationen werden verschlüsselt und vom [!INCLUDE [Product short](includes/product-short.md)]-Sensor lokal gespeichert.|

## <a name="alternative-methods-to-configure-your-proxy-server"></a>Alternative Methoden zum Konfigurieren des Proxyservers

Sie können eine der folgenden alternativen Methoden verwenden, um den Proxyserver zu konfigurieren. Beim Konfigurieren der Proxyeinstellungen mithilfe dieser Methoden leiten andere Dienste, die im Kontext als lokales System oder lokaler Dienst ausgeführt werden, den Datenverkehr auch über den Proxy weiter.

- [Konfigurieren des Proxyservers mithilfe von WinINet](#configure-proxy-server-using-wininet)
- [Konfigurieren des Proxyservers mithilfe der Registrierung](#configure-proxy-server-using-the-registry)

### <a name="configure-proxy-server-using-wininet"></a>Konfigurieren des Proxyservers mithilfe von WinINet

Sie können den Proxyserver über die WinINet-Proxykonfiguration konfigurieren, damit der [!INCLUDE [Product short](includes/product-short.md)]-Sensor Diagnosedaten melden und mit dem [!INCLUDE [Product short](includes/product-short.md)]-Clouddienst kommunizieren kann, wenn ein Computer keine Verbindung mit dem Internet herstellen darf. Wenn Sie WinHTTP für die Proxykonfiguration verwenden, müssen Sie dennoch WinINet-Browserproxyeinstellungen für die Kommunikation zwischen dem Sensor und dem [!INCLUDE [Product short](includes/product-short.md)]-Clouddienst konfigurieren.

Beachten Sie bei der Proxykonfiguration, dass der eingebettete [!INCLUDE [Product short](includes/product-short.md)]-Sensordienst im Systemkontext mit dem **LocalService**-Konto wird. Der [!INCLUDE [Product short](includes/product-short.md)]-Sensorupdatedienst wird im Systemkontext mit dem **LocalSystem**-Konto ausgeführt.

> [!NOTE]
> Wenn Sie in Ihrer Netzwerktopologie einen transparenten Proxy oder WPAD verwenden, müssen Sie WinINet nicht für den Proxy konfigurieren.

### <a name="configure-proxy-server-using-the-registry"></a>Konfigurieren des Proxyservers mithilfe der Registrierung

Sie können den Proxyserver auch manuell über einen registrierungsbasierten statischen Proxy konfigurieren, damit der [!INCLUDE [Product short](includes/product-short.md)]-Sensor Diagnosedaten melden und mit dem [!INCLUDE [Product short](includes/product-short.md)]-Clouddienst kommunizieren kann, wenn ein Computer keine Verbindung mit dem Internet herstellen darf.

> [!NOTE]
> Die Änderungen an der Registrierung sollten nur auf „LocalService“ und „LocalSystem“ angewendet werden.

Der statische Proxy kann über die Registrierung konfiguriert werden. Sie müssen die Proxykonfiguration, die Sie im Benutzerkontext verwenden, in „LocalSystem“ und „LocalService“ kopieren. So kopieren Sie Ihre Benutzerkontext-Proxyeinstellungen

1. Stellen Sie sicher, dass Sie diese Registrierungsschlüssel sichern, bevor Sie sie bearbeiten.

1. Suchen Sie in der Registrierung den Wert `DefaultConnectionSettings` als REG_BINARY unter dem Registrierungsschlüssel `HKCU\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings`, und kopieren Sie ihn.

1. Wenn „LocalSystem“ nicht über die richtigen Proxyeinstellungen verfügt (weil sie nicht konfiguriert sind oder sich von „Current_User“ unterscheiden), kopieren Sie die Proxyeinstellung von „Current_User“ in „LocalSystem“. Unter dem Registrierungsschlüssel `HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings`.

1. Fügen Sie den Wert `DefaultConnectionSettings` von „Current_User“ als REG_BINARY ein.

1. Wenn „LocalService“ nicht über die richtigen Proxyeinstellungen verfügt, kopieren Sie die Proxyeinstellung von „Current_User“ in „LocalService“. Unter dem Registrierungsschlüssel `HKU\S-1-5-19\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings`.

1. Fügen Sie den Wert `DefaultConnectionSettings` von „Current_User“ als REG_BINARY ein.

> [!NOTE]
> Dies wirkt sich auf alle Anwendungen aus, einschließlich der Windows-Dienste, die WinINET mit „LocalService“- und „LocalSystem“-Kontext verwenden.

<a name="enable-access-to-azure-atp-service-urls-in-the-proxy-server"></a>

## <a name="enable-access-to-product-short-service-urls-in-the-proxy-server"></a>Aktivieren des Zugriffs auf [!INCLUDE [Product short](includes/product-short.md)]-Dienst-URLs im Proxyserver

Um Zugriff auf [!INCLUDE [Product short](includes/product-short.md)] zu ermöglichen, wird empfohlen, Datenverkehr zu den folgenden URLs zuzulassen. Die URLs werden automatisch der richtigen Dienstidentifizierung für Ihre [!INCLUDE [Product short](includes/product-short.md)]-Instanz zugeordnet.

- `<your-instance-name>.atp.azure.com`: für Konsolenkonnektivität. Beispiel: `contoso-corp.atp.azure.com`

- `<your-instance-name>sensorapi.atp.azure.com`: für die Sensorkonnektivität. Beispiel: `contoso-corpsensorapi.atp.azure.com`

Sie können auch die IP-Adressbereiche im Azure-Diensttag (**AzureAdvancedThreatProtection**) verwenden, um den Zugriff auf [!INCLUDE [Product short](includes/product-short.md)] zu ermöglichen. Weitere Informationen zu Diensttags finden Sie unter [Diensttags des virtuellen Netzwerks](/azure/virtual-network/service-tags-overview) oder in der Datei [Herunterladen der Diensttags](https://www.microsoft.com/download/details.aspx?id=56519).

Wenn Sie den Zugriff noch besser steuern möchten, lassen Sie Datenverkehr für die relevanten Endpunkte aus der folgenden Tabelle zu:

|Dienstidentifizierung|*.atp.azure.com-DNS-Eintrag|
|----|----|
|USA |`triprd1wcusw2sensorapi.atp.azure.com`<br>`triprd1wcuswb3sensorapi.atp.azure.com`<br>`triprd1wcuse3sensorapi.atp.azure.com`|
|US GCC High|`https://triff1wcva2sensorapi.atp.azure.us`|
|Europa|`triprd1wceun2sensorapi.atp.azure.com`<br>`triprd1wceuw3sensorapi.atp.azure.com`|
|Asia|`triprd1wcasse2sensorapi.atp.azure.com`|
|Vereinigtes Königreich|`triprd1wcuks2sensorapi.atp.azure.com`|

> [!NOTE]
>
> - Um ein Maximum an Sicherheit und Datenschutz zu gewährleisten, verwendet [!INCLUDE [Product short](includes/product-short.md)] eine zertifikatbasierte gegenseitige Authentifizierung zwischen jedem [!INCLUDE [Product short](includes/product-short.md)]-Sensor und dem [!INCLUDE [Product short](includes/product-short.md)]-Cloud-Back-End. Wenn in Ihrer Umgebung eine SSL-Überprüfung verwendet wird, stellen Sie sicher, dass diese Überprüfung für die gegenseitige Authentifizierung konfiguriert ist, sodass der Authentifizierungsprozess nicht beeinträchtigt wird.
> - Die IP-Adressen des [!INCLUDE [Product short](includes/product-short.md)]-Diensts können sich zuweilen ändern. Wenn Sie IP-Adressen manuell konfigurieren oder Ihr Proxy automatisch DNS-Namen in ihre IP-Adresse auflöst und so verwendet, sollten Sie in regelmäßigen Abständen überprüfen, ob die konfigurierten IP-Adressen weiterhin auf dem neuesten Stand sind.

## <a name="see-also"></a>Weitere Informationen

- [Configure event forwarding (Konfigurieren der Ereignisweiterleitung)](configure-event-forwarding.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
