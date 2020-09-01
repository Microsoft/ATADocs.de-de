---
title: Behandlung von bekannten Problemen bei Azure ATP
description: Beschreibt, wie Sie häufige Fehler in Azure ATP beheben können.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 04/28/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 23386e36-2756-4291-923f-fa8607b5518a
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4de688b3ea1c80f8ed0e517baf9da3b469a8d82a
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88956719"
---
# <a name="troubleshooting-azure-atp-known-issues"></a>Behandlung von bekannten Problemen bei Azure ATP

## <a name="sensor-failure-communication-error"></a>Kommunikationsfehler durch Sensorfehler

Sie erhalten folgenden Sensorfehler:

System.Net.Http.HttpRequestException: Fehler beim Senden der Anforderung. ---> System.Net.WebException: Es konnte keine Verbindung mit dem Remoteserver hergestellt werden ---> System.Net.Sockets.SocketException: Fehler beim Herstellen der Verbindung, weil die Gegenstelle nach einer bestimmten Zeitspanne nicht ordnungsgemäß reagiert hat, oder die hergestellte Verbindung konnte nicht aufrechterhalten werden, weil der verbundene Host nicht reagiert hat...

**Lösung:**

Stellen Sie sicher, dass die Kommunikation für Localhost an TCP-Port 444 nicht blockiert ist. Weitere Informationen zu den Voraussetzungen für Azure ATP finden Sie unter [Ports](atp-prerequisites.md#ports).

## <a name="deployment-log-location"></a>Speicherort des Bereitstellungsprotokolls

Die Azure ATP-Bereitstellungsprotokolle befinden sich im temporären Verzeichnis des Benutzers, der das Produkt installiert hat. Beim Standardinstallationsspeicherort lautet der Pfad: C:\Benutzer\Administrator\AppData\Local\Temp (oder ein Verzeichnis über „%temp%“). Weitere Informationen finden Sie unter [Problembehandlung für den Azure Advanced Threat Protection-Sensor (ATP) mithilfe der ATP-Protokolle](troubleshooting-atp-using-logs.md).

## <a name="proxy-authentication-problem-presents-as-a-licensing-error"></a>Proxyauthentifizierungsproblem wird als Lizenzierungsfehler dargestellt

Während der Sensorinstallation erhalten Sie die folgende Fehlermeldung:  **Der Sensor konnte aufgrund von Lizenzierungsproblemen nicht registriert werden**.

**Einträge im Bereitstellungsprotokoll:**

[1C60:1AA8][2018-03-24T23:59:13]i000: 2018-03-25 02:59:13.1237 Info  InteractiveDeploymentManager ValidateCreateSensorAsync returned [validateCreateSensorResult=LicenseInvalid]] [1C60:1AA8][2018-03-24T23:59:56]i000: 2018-03-25 02:59:56.4856 Info  InteractiveDeploymentManager ValidateCreateSensorAsync returned [validateCreateSensorResult=LicenseInvalid]] [1C60:1AA8][2018-03-25T00:27:56]i000: 2018-03-25 03:27:56.7399 Debug SensorBootstrapperApplication Engine.Quit [deploymentResultStatus=1602 isRestartRequired=False]] [1C60:15B8][2018-03-25T00:27:56]i500: Wird heruntergefahren, Exitcode: 0x642

**Ursache**:

In einigen Fällen, bei Kommunikation über einen Proxy, könnte dieser während der Authentifizierung dem Azure ATP-Sensor mit Fehler 401 oder 403 anstelle des Fehlers 407 antworten. Der Azure ATP-Sensor interpretiert Fehler 401 oder 403 als Lizenzierungsproblem und nicht als Proxyauthentifizierungsproblem.

**Lösung:**

Stellen Sie sicher, dass der Sensor über den konfigurierten Proxy ohne Authentifizierung zu „*. atp.azure.com“ navigieren kann. Weitere Informationen finden Sie unter [Konfigurieren von Endpunktproxy- und Internetkonnektivitätseinstellungen für Ihren Azure ATP-Sensor](configure-proxy.md).

## <a name="proxy-authentication-problem-presents-as-a-connection-error"></a>Darstellung des Proxyauthentifizierungsproblems als Verbindungsfehler

Während der Sensorinstallation erhalten Sie die folgende Fehlermeldung: **The sensor failed to connect to service.** (Fehler beim Herstellen einer Verbindung vom Sensor zum Dienst.)

**Ursache:**

Das Problem kann durch einen transparenten Proxykonfigurationsfehler auf Server Core verursacht werden, wenn beispielsweise das von Azure ATP benötigte Stammzertifikat nicht aktuell oder nicht vorhanden ist.

**Lösung:**

Führen Sie das folgende PowerShell-Cmdlet aus, um zu überprüfen, ob das vertrauenswürdige Stammzertifikat für den Azure ATP-Dienst auf Server Core vorhanden ist. Im folgenden Beispiel wird das Stammzertifikat „DigiCert Baltimore Root“ verwendet.

```powershell
Get-ChildItem -Path "Cert:\LocalMachine\Root" | where { $_.Thumbprint -eq "D4DE20D05E66FC53FE1A50882C78DB2852CAE474"}
```

```Output
Subject      : CN=Baltimore CyberTrust Root, OU=CyberTrust, O=Baltimore, C=IE
Issuer       : CN=Baltimore CyberTrust Root, OU=CyberTrust, O=Baltimore, C=IE
Thumbprint   : D4DE20D05E66FC53FE1A50882C78DB2852CAE474
FriendlyName : DigiCert Baltimore Root
NotBefore    : 5/12/2000 11:46:00 AM
NotAfter     : 5/12/2025 4:59:00 PM
Extensions   : {System.Security.Cryptography.Oid, System.Security.Cryptography.Oid, System.Security.Cryptography.Oid}
```

Führen Sie die folgenden Schritte aus, wenn die Ausgabe nicht Ihren Erwartungen entspricht:

1. Laden Sie das [Baltimore CyberTrust-Stammzertifikat](https://cacert.omniroot.com/bc2025.crt) auf den Server Core-Computer herunter.
1. Führen Sie das folgende PowerShell-Cmdlet aus, um das Zertifikat zu installieren.

    ```powershell
    Import-Certificate -FilePath "<PATH_TO_CERTIFICATE_FILE>\bc2025.crt" -CertStoreLocation Cert:\LocalMachine\Root
    ```

## <a name="silent-installation-error-when-attempting-to-use-powershell"></a>Fehler bei der automatischen Installation beim Versuch, PowerShell zu verwenden

Sie versuchen, während der automatischen Sensorinstallation PowerShell zu verwenden, und erhalten folgenden Fehler:

```powershell
"Azure ATP sensor Setup.exe" "/quiet" NetFrameworkCommandLineArguments="/q" Acce ... Unexpected token '"/quiet"' in expression or statement."
```

**Ursache:**

Dieser Fehler wird dadurch verursacht, dass beim Verwenden von PowerShell das für die Installation erforderliche Präfix „./“ nicht einbezogen wurde.

**Lösung:**

Verwenden Sie den vollständigen Befehl für eine erfolgreiche Installation.

```powershell
./"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="<Access Key>"
```

## <a name="azure-atp-sensor-nic-teaming-issue"></a>Problem mit NIC-Teamvorgängen beim Azure ATP-Sensor <a name="nic-teaming"></a>

Wenn Sie versuchen, den ATP-Sensor auf einem Computer zu installieren, der mit einem NIC-Teaming-Adapter konfiguriert ist, wird ein Installationsfehler gemeldet. Wenn Sie den ATP-Sensor auf einem Computer installieren möchten, der mit NIC-Teamvorgang konfiguriert ist, gehen Sie wie folgt vor:

1. Laden Sie das Installationsprogramm für die Npcap-Version 0.9984 von [https://nmap.org/npcap/](https://nmap.org/npcap/dist/npcap-0.9984.exe) herunter.
    - Alternativ dazu können Sie die OEM-Version des Npcap-Treibers (der die automatische Installation unterstützt) vom Supportteam anfordern.
    - Kopien von Npcap werden nicht auf die Lizenzierungseinschränkung von fünf Kopien, fünf Computern oder fünf Benutzern angerechnet, wenn sie ausschließlich in Verbindung mit Azure ATP installiert und verwendet werden. Weitere Informationen finden Sie unter [NPCAP-Lizenzierung](https://github.com/nmap/npcap/blob/master/LICENSE).

Wenn Sie den Sensor noch nicht installiert haben:

1. Deinstallieren Sie WinPcap (falls installiert).
1. Installieren Sie Npcap mit den folgenden Optionen: loopback_support=no & winpcap_mode=yes.
    - Wenn Sie den GUI-Installer verwenden, deaktivieren Sie die **Loopbackunterstützung**, und aktivieren Sie den **WinPcap**-Modus.
1. Installieren Sie das Sensorpaket.

Wenn der Sensor bereits installiert ist:

1. Deinstallieren Sie den Sensor.
1. Deinstallieren Sie WinPcap.
1. Installieren Sie Npcap mit den folgenden Optionen: loopback_support=no & winpcap_mode=yes
    - Wenn Sie den GUI-Installer verwenden, deaktivieren Sie die **Loopbackunterstützung**, und aktivieren Sie den **WinPcap**-Modus.
1. Installieren Sie das Sensorpaket erneut.

## <a name="multi-processor-group-mode"></a>Modus „Mehrere Prozessorgruppen“

Unter den Windows-Betriebssystemen 2008 R2 und 2012 werden Azure ATP-Sensoren im Modus „Mehrere Prozessorgruppen“ nicht unterstützt.

Mögliche Problemumgehungen:

- Wenn Hyperthreading aktiviert ist, deaktivieren Sie es. Dadurch kann die Anzahl logischer Kerne möglicherweise weit genug reduziert werden, sodass eine Ausführung im Modus **Mehrere Prozessorgruppen** nicht notwendig ist.

- Wenn Ihr Computer weniger als 64 logische Kerne aufweist und auf einem HP-Host ausgeführt wird, können Sie möglicherweise die BIOS-Einstellung **NUMA Group Size Optimization** vom Standardwert **Clustered** in **Flat** ändern.

## <a name="microsoft-defender-atp-integration-issue"></a>Problem bei der Microsoft Defender ATP-Integration

Mithilfe von Azure Advanced Threat Protection können Sie Azure ATP in Microsoft Defender ATP integrieren. Weitere Informationen finden Sie unter [Integration von Azure ATP in Microsoft Defender ATP](integrate-wd-atp.md).

## <a name="vmware-virtual-machine-sensor-issue"></a>Problem mit dem Sensor des virtuellen VMware-Computers

Wenn Sie einen Azure-ATP-Sensor auf virtuellen VMware-Computern verwenden, erhalten Sie möglicherweise die Integritätswarnung **Ein Teil des Netzwerkdatenverkehrs wird nicht analysiert**. Als Ursache kommt ein Konfigurationskonflikt in VMware infrage.

So beheben Sie dieses Problem:

Legen Sie die folgenden Einstellungen in der NIC-Konfiguration des virtuellen Computers auf **Deaktiviert** fest: **IPv4-TSO-Offload**.

 ![VMware-Sensorproblem](media/vm-sensor-issue.png)

Verwenden Sie den folgenden Befehl, um zu überprüfen, ob die Abladung großer Sendungen (Large Send Offload, LSO) aktiviert oder deaktiviert ist:

`Get-NetAdapterAdvancedProperty | Where-Object DisplayName -Match "^Large*"`

![LSO-Status überprüfen](media/missing-network-traffic-health-alert.png)

Wenn LSO aktiviert ist, verwenden Sie den folgenden Befehl zur Deaktivierung:

`Disable-NetAdapterLso -Name {name of adapter}`

![LSO-Status deaktivieren](media/disable-lso-vmware.png)

## <a name="sensor-failed-to-retrieve-group-managed-service-account-gmsa-credentials"></a>Fehler beim Abrufen der Anmeldeinformationen für das gruppenverwaltete Dienstkonto durch den Sensor

Wenn Sie die folgende Integritätswarnung erhalten: **Anmeldeinformationen für Verzeichnisdienste nicht korrekt**

**Sensorprotokolleinträge:**

2020-02-17 14:01:36.5315 Info ImpersonationManager CreateImpersonatorAsync started [UserName=account_name Domain=domain1.test.local IsGroupManagedServiceAccount=True] 2020-02-17 14:01:36.5750 Info ImpersonationManager CreateImpersonatorAsync finished [UserName=account_name Domain=domain1.test.local IsSuccess=False]

**Sensor-Updater-Protokolleinträge:**

2020-02-17 14:02:19.6258 Warn GroupManagedServiceAccountImpersonationHelper GetGroupManagedServiceAccountAccessTokenAsync failed GMSA password could not be retrieved [errorCode=AccessDenied AccountName=account_name DomainDnsName=domain1.test.local]

**Ursache**:

Der Sensor konnte das angegebene gruppenverwaltete Dienstkonto nicht aus dem Azure ATP-Portal abrufen.

**Lösung:**

Stellen Sie sicher, dass die Anmeldeinformationen des gruppenverwalteten Dienstkontos korrekt sind und dem Sensor die erforderlichen Berechtigungen zum Abrufen der Anmeldeinformationen des Kontos erteilt wurden. In der angewandten Richtlinie sollten Sie das gMSA-Konto zu **Anmelden als Dienst** unter Zuweisungen von Benutzerrechten hinzufügen.

## <a name="report-downloads-cannot-contain-more-than-300000-entries"></a>Berichtsdownloads dürfen nicht mehr als 300.000 Einträge enthalten

Azure ATP unterstützt keine Berichtsdownloads mit mehr als 300.000 Einträgen pro Bericht. Die Berichte werden unvollständig gerendert, wenn mehr als 300.000 Einträge enthalten sind.

**Ursache**:

Dies ist eine technisch bedingte Begrenzung.

**Lösung:**

Keine bekannte Lösung.

## <a name="see-also"></a>Weitere Informationen

- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Azure ATP capacity planning (Azure ATP-Kapazitätsplanung)](atp-capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-forwarding.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
