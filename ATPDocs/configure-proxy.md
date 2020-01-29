---
title: Konfigurieren Ihres Proxy oder der Firewall zum Aktivieren der Azure ATP-Kommunikation mit dem Sensor | Microsoft-Dokumentation
description: Beschreibt, wie Sie Ihre Firewall oder den Proxyserver so einrichten, um die Kommunikation zwischen dem Azure ATP-Clouddienst und den Azure ATP-Sensoren zuzulassen.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 09/23/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 9c173d28-a944-491a-92c1-9690eb06b151
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 88d6c9fddc0a9e8db8d63a64618b7ab9c14a092f
ms.sourcegitcommit: 1a0cc214568bf12041d11e037dfe56a8d9e707c2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/23/2020
ms.locfileid: "76706221"
---
# <a name="configure-endpoint-proxy-and-internet-connectivity-settings-for-your-azure-atp-sensor"></a>Konfigurieren von Endpunktproxy- und Internetkonnektivitätseinstellungen für Ihren Azure ATP-Sensor

Jeder Azure Advanced Threat Protection-Sensor (ATP) erfordert Internetkonnektivität mit dem Azure ATP-Clouddienst, damit er erfolgreich verwendet werden kann. In einigen Organisationen sind die Domänencontroller nicht direkt mit dem Internet verbunden, sondern über eine Webproxyverbindung. Für jeden Azure ATP-Sensor ist es erforderlich, dass Sie die Microsoft WinINET-Proxykonfiguration (Windows-Internet) verwenden, um Sensordaten zu melden und mit Azure ATP zu kommunizieren. Wenn Sie WinHTTP für die Proxykonfiguration verwenden, müssen Sie dennoch WinINET-Browserproxyeinstellungen für die Kommunikation zwischen dem Sensor und dem Azure ATP-Clouddienst konfigurieren.

Beachten Sie bei der Proxykonfiguration, dass der eingebettete Azure ATP-Sensordienst mit dem Konto **LocalService** und der Azure ATP-Sensorupdatedienst mit dem Konto **LocalSystem** im Systemkontext ausgeführt wird.

> [!NOTE]
> Wenn Sie in Ihrer Netzwerktopologie einen transparenten Proxy oder WPAD verwenden, müssen Sie WinINET nicht für den Proxy konfigurieren.

## <a name="configure-the-proxy"></a>Konfigurieren des Proxys

Sie können Ihre Proxyeinstellungen während der Sensorinstallation konfigurieren, indem Sie die unter [Proxy-Authentifizierung](https://docs.microsoft.com/azure-advanced-threat-protection/atp-silent-installation#proxy-authentication) definierten Parameter verwenden.

### <a name="proxy-authentication"></a>Proxy-Authentifizierung

Verwenden Sie die folgenden Befehle, um die Proxyauthentifizierung abzuschließen:

**Syntax**:

> [!div class="mx-tableFixed"]
>
> |Name|Syntax|Erforderlich für die unbeaufsichtigte Installation?|Beschreibung|
> |-------------|----------|---------|---------|
> |ProxyUrl|ProxyUrl="https\://proxy.contoso.com:8080"|Nein|Gibt die ProxyUrl und die Portnummer für den Azure ATP Sensor an.|
> |ProxyUserName|ProxyUserName="Contoso\ProxyUser"|Nein|Wenn Ihr Proxydienst eine Authentifizierung erfordert, geben Sie einen Benutzernamen im Format „DOMÄNE\Benutzer“ an.|
> |ProxyUserPassword|ProxyUserPassword="P@ssw0rd"|Nein|Gibt das Kennwort für den Proxybenutzernamen an. *Anmeldeinformationen werden verschlüsselt und lokal vom Azure ATP-Sensor gespeichert.|

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

Lassen Sie Datenverkehr für folgende URLs zu, um den Zugriff auf Azure ATP zu ermöglichen:

- \<Name_der_Instanz>.atp.azure.com: für die Konsolenkonnektivität. Beispielsweise „Contoso-corp.atp.azure.com“

- \<Name_der_Instanz>.sensorapi.atp.azure.com: für die Sensorkonnektivität. Beispielsweise „contoso-corpsensorapi.atp.azure.com“

Die vorherigen URLs werden automatisch der richtigen Dienstidentifizierung für Ihre Azure ATP-Instanz zugeordnet. Wenn Sie den Zugriff noch besser steuern möchten, lassen Sie Datenverkehr für die relevanten Endpunkte aus der folgenden Tabelle zu:

|Dienstidentifizierung|*.atp.azure.com-DNS-Eintrag|
|----|----|
|USA |triprd1wcusw1sensorapi.atp.azure.com<br>triprd1wcuswb1sensorapi.atp.azure.com<br>triprd1wcuse1sensorapi.atp.azure.com|
|Europa|triprd1wceun1sensorapi.atp.azure.com<br>triprd1wceuw1sensorapi.atp.azure.com|
|Asien|triprd1wcasse1sensorapi.atp.azure.com|

> [!NOTE]
>
> - Um ein Maximum an Sicherheit und Datenschutz zu gewährleisten, verwendet Azure ATP eine zertifikatbasierte gegenseitige Authentifizierung zwischen jedem Azure ATP-Sensor und dem Azure ATP-Cloud-Back-End. Wenn in Ihrer Umgebung eine SSL-Überprüfung verwendet wird, stellen Sie sicher, dass diese Überprüfung für die gegenseitige Authentifizierung konfiguriert ist, sodass der Authentifizierungsprozess nicht beeinträchtigt wird.
> - Sie können auch das Azure-Diensttag (**AzureAdvancedThreatProtection**) verwenden, um den Zugriff auf Azure ATP zu ermöglichen. Weitere Informationen zu Diensttags finden Sie unter [Diensttags des virtuellen Netzwerks](https://docs.microsoft.com/azure/virtual-network/service-tags-overview) oder in der Datei [Herunterladen der Diensttags](https://www.microsoft.com/download/details.aspx?id=56519).

## <a name="see-also"></a>Weitere Informationen

- [Configure event forwarding (Konfigurieren der Ereignisweiterleitung)](configure-event-forwarding.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
