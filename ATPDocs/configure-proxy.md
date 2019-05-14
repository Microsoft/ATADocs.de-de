---
title: Konfigurieren Ihres Proxy oder der Firewall zum Aktivieren der Azure ATP-Kommunikation mit dem Sensor | Microsoft-Dokumentation
description: Beschreibt, wie Sie Ihre Firewall oder den Proxyserver so einrichten, um die Kommunikation zwischen dem Azure ATP-Clouddienst und den Azure ATP-Sensoren zuzulassen.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 9c173d28-a944-491a-92c1-9690eb06b151
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7598c10724295312b19a2ccb0fbdd57328edd9a4
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2019
ms.locfileid: "65196743"
---
# <a name="configure-endpoint-proxy-and-internet-connectivity-settings-for-your-azure-atp-sensor"></a>Konfigurieren von Endpunktproxy- und Internetkonnektivitätseinstellungen für Ihren Azure ATP-Sensor

Jeder Azure Advanced Threat Protection-Sensor (ATP) erfordert Internetkonnektivität mit dem Azure ATP-Clouddienst, damit er erfolgreich verwendet werden kann. In einigen Organisationen sind die Domänencontroller nicht direkt mit dem Internet verbunden, sondern über eine Webproxyverbindung. Für jeden Azure ATP-Sensor ist es erforderlich, dass Sie die Microsoft WinINET-Proxykonfiguration (Windows-Internet) verwenden, um Sensordaten zu melden und mit Azure ATP zu kommunizieren. Wenn Sie WinHTTP für die Proxykonfiguration verwenden, müssen Sie dennoch WinINET-Browserproxyeinstellungen für die Kommunikation zwischen dem Sensor und dem Azure ATP-Clouddienst konfigurieren.


Wenn Sie den Proxy konfigurieren, müssen Sie wissen, dass der eingebettete Azure ATP-Sensordienst im Systemkontext mit dem Konto **LocalService** ausgeführt wird, und der Azure ATP-Sensorupdatedienst wird im Systemkontext mit dem Konto **LocalSystem** ausgeführt. 

> [!NOTE]
> Wenn Sie in Ihrer Netzwerktopologie einen transparenten Proxy oder WPAD verwenden, müssen Sie WinINET nicht für den Proxy konfigurieren.

## <a name="configure-the-proxy"></a>Konfigurieren des Proxys 

Konfigurieren Sie den Proxyserver manuell mithilfe eines registrierungsbasierten statischen Proxys, damit der Azure ATP-Sensor Diagnosedaten melden und mit dem Azure ATP-Clouddienst kommunizieren kann, wenn ein Computer keine Verbindung mit dem Internet herstellen darf.

> [!NOTE]
> Die Änderungen an der Registrierung sollten nur auf „LocalService“ und „LocalSystem“ angewendet werden.

Der statische Proxy kann über die Registrierung konfiguriert werden. Sie müssen die Proxykonfiguration, die Sie im Benutzerkontext verwenden, in „LocalSystem“ und „LocalService“ kopieren. So kopieren Sie Ihre Benutzerkontext-Proxyeinstellungen

1.   Stellen Sie sicher, dass Sie diese Registrierungsschlüssel sichern, bevor Sie sie bearbeiten.

2. Suchen Sie in der Registrierung den Wert `DefaultConnectionSettings` als REG_BINARY unter dem Registrierungsschlüssel `HKCU\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings`, und kopieren Sie ihn.
 
2.  Wenn „LocalSystem“ nicht über die richtigen Proxyeinstellungen verfügt (weil sie nicht konfiguriert sind oder sich von „Current_User“ unterscheiden), kopieren Sie die Proxyeinstellung von „Current_User“ in „LocalSystem“. Unter dem Registrierungsschlüssel `HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings`.

3.  Fügen Sie den Wert `DefaultConnectionSettings` von „Current_User“ als REG_BINARY ein.

4.  Wenn „LocalService“ nicht über die richtigen Proxyeinstellungen verfügt, kopieren Sie die Proxyeinstellung von „Current_User“ in „LocalService“. Unter dem Registrierungsschlüssel `HKU\S-1-5-19\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings`.

5.  Fügen Sie den Wert `DefaultConnectionSettings` von „Current_User“ als REG_BINARY ein.

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
> Wenn Sie eine SSL-Überprüfung des Azure ATP-Netzwerkdatenverkehrs durchführen (zwischen dem Sensor und dem Azure ATP-Dienst), muss die SSL-Überprüfung die gegenseitige Überprüfung unterstützen.


## <a name="see-also"></a>Weitere Informationen
- [Configure event forwarding (Konfigurieren der Ereignisweiterleitung)](configure-event-forwarding.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
