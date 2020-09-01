---
title: Konfigurieren des Proxys oder der Firewall zum Aktivieren der Azure ATP-Kommunikation mit dem Sensor
description: Beschreibt, wie Sie Ihre Firewall oder den Proxyserver so einrichten, um die Kommunikation zwischen dem Azure ATP-Clouddienst und den Azure ATP-Sensoren zuzulassen.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 07/29/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 9c173d28-a944-491a-92c1-9690eb06b151
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 24fab947687183f40d5043678b24e12792d98233
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88956838"
---
# <a name="configure-endpoint-proxy-and-internet-connectivity-settings-for-your-azure-atp-sensor"></a>Konfigurieren von Endpunktproxy- und Internetkonnektivitätseinstellungen für Ihren Azure ATP-Sensor

Jeder Azure Advanced Threat Protection-Sensor (ATP) erfordert Internetkonnektivität mit dem Azure ATP-Clouddienst, damit er Sensordaten melden und erfolgreich verwendet werden kann. In einigen Organisationen sind die Domänencontroller nicht direkt mit dem Internet verbunden, sondern über eine Webproxyverbindung.

Es wird empfohlen, den Proxyserver mithilfe der Befehlszeile zu konfigurieren. Dadurch wird sichergestellt, dass nur die Azure ATP-Sensordienste über den Proxy kommunizieren.

## <a name="configure-proxy-server-using-the-command-line"></a>Konfigurieren des Proxyservers über die Befehlszeile

Sie können den Proxyserver während der Sensorinstallation mithilfe der folgenden Befehlszeilenoptionen konfigurieren.

### <a name="syntax"></a>Syntax

"Azure ATP sensor Setup.exe" [/quiet] [/Help] [ProxyUrl="https://proxy.internal.com"] [ProxyUserName="domain\proxyuser"] [ProxyUserPassword="ProxyPassword"]

### <a name="switch-descriptions"></a>Beschreibungen der Befehlszeilenoptionen

> [!div class="mx-tableFixed"]
>
> |Name|Syntax|Erforderlich für die unbeaufsichtigte Installation?|Beschreibung|
> |-------------|----------|---------|---------|
> |ProxyUrl|ProxyUrl="http\://proxy.contoso.com:8080"|Nein|Gibt die ProxyUrl und die Portnummer für den Azure ATP Sensor an.|
> |ProxyUserName|ProxyUserName="Contoso\ProxyUser"|Nein|Wenn Ihr Proxydienst eine Authentifizierung erfordert, geben Sie einen Benutzernamen im Format „DOMÄNE\Benutzer“ an.|
> |ProxyUserPassword|ProxyUserPassword="P@ssw0rd"|Nein|Gibt das Kennwort für den Proxybenutzernamen an. *Anmeldeinformationen werden verschlüsselt und lokal vom Azure ATP-Sensor gespeichert.|

## <a name="alternative-methods-to-configure-your-proxy-server"></a>Alternative Methoden zum Konfigurieren des Proxyservers

Sie können eine der folgenden alternativen Methoden verwenden, um den Proxyserver zu konfigurieren. Beim Konfigurieren der Proxyeinstellungen mithilfe dieser Methoden leiten andere Dienste, die im Kontext als lokales System oder lokaler Dienst ausgeführt werden, den Datenverkehr auch über den Proxy weiter.

- [Konfigurieren des Proxyservers mithilfe von WinINet](#configure-proxy-server-using-wininet)
- [Konfigurieren des Proxyservers mithilfe der Registrierung](#configure-proxy-server-using-the-registry)

### <a name="configure-proxy-server-using-wininet"></a>Konfigurieren des Proxyservers mithilfe von WinINet

Sie können den Proxyserver manuell mithilfe der Microsoft Windows Internet-Proxykonfiguration (WinINet) konfigurieren, damit der Azure ATP-Sensor Diagnosedaten melden und mit dem Azure ATP-Clouddienst kommunizieren kann, wenn ein Computer keine Verbindung mit dem Internet herstellen darf. Wenn Sie WinHTTP für die Proxykonfiguration verwenden, müssen Sie dennoch WinINET-Browserproxyeinstellungen für die Kommunikation zwischen dem Sensor und dem Azure ATP-Clouddienst konfigurieren.

Beachten Sie bei der Proxykonfiguration, dass der eingebettete Azure ATP-Sensordienst mit dem Konto **LocalService** und der Azure ATP-Sensorupdatedienst mit dem Konto **LocalSystem** im Systemkontext ausgeführt wird.

> [!NOTE]
> Wenn Sie in Ihrer Netzwerktopologie einen transparenten Proxy oder WPAD verwenden, müssen Sie WinINet nicht für den Proxy konfigurieren.

### <a name="configure-proxy-server-using-the-registry"></a>Konfigurieren des Proxyservers mithilfe der Registrierung

Sie können den Proxyserver auch manuell mithilfe eines registrierungsbasierten statischen Proxys konfigurieren, damit der Azure ATP-Sensor Diagnosedaten melden und mit dem Azure ATP-Clouddienst kommunizieren kann, wenn ein Computer keine Verbindung mit dem Internet herstellen darf.

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

## <a name="enable-access-to-azure-atp-service-urls-in-the-proxy-server"></a>Aktivieren des Zugriffs auf Azure ATP-Dienst-URLs im Proxyserver

Es wird empfohlen, Datenverkehr für folgende URLs zuzulassen, um den Zugriff auf Azure ATP zu ermöglichen: Die URLs werden automatisch der richtigen Dienstidentifizierung für Ihre Azure ATP-Instanz zugeordnet.

- `<your-instance-name>.atp.azure.com`: für Konsolenkonnektivität. Beispiel: `contoso-corp.atp.azure.com`

- `<your-instance-name>sensorapi.atp.azure.com`: für die Sensorkonnektivität. Beispiel: `contoso-corpsensorapi.atp.azure.com`

Sie können auch die IP-Adressbereiche im Azure-Diensttag (**AzureAdvancedThreatProtection**) verwenden, um den Zugriff auf Azure ATP zu ermöglichen. Weitere Informationen zu Diensttags finden Sie unter [Diensttags des virtuellen Netzwerks](/azure/virtual-network/service-tags-overview) oder in der Datei [Herunterladen der Diensttags](https://www.microsoft.com/download/details.aspx?id=56519).

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
> - Um ein Maximum an Sicherheit und Datenschutz zu gewährleisten, verwendet Azure ATP eine zertifikatbasierte gegenseitige Authentifizierung zwischen jedem Azure ATP-Sensor und dem Azure ATP-Cloud-Back-End. Wenn in Ihrer Umgebung eine SSL-Überprüfung verwendet wird, stellen Sie sicher, dass diese Überprüfung für die gegenseitige Authentifizierung konfiguriert ist, sodass der Authentifizierungsprozess nicht beeinträchtigt wird.
> - Gelegentlich können sich die IP-Adressen der Azure ATP-Dienstanbieter ändern. Wenn Sie IP-Adressen manuell konfigurieren oder Ihr Proxy automatisch DNS-Namen in ihre IP-Adresse auflöst und so verwendet, sollten Sie in regelmäßigen Abständen überprüfen, ob die konfigurierten IP-Adressen weiterhin auf dem neuesten Stand sind.

## <a name="see-also"></a>Weitere Informationen

- [Configure event forwarding (Konfigurieren der Ereignisweiterleitung)](configure-event-forwarding.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)