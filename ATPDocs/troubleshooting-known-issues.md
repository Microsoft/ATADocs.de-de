---
title: Problembehandlung bei Microsoft Defender für bekannte Probleme
description: Hier wird beschrieben, wie Sie Probleme in Microsoft Defender für die Identität beheben.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 09/07/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: e37e413a355db72e04e1b6f72a71c570148c9f04
ms.sourcegitcommit: 4563d22ad0fc63022a57c5d2d4fbc425e900bf84
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/23/2020
ms.locfileid: "96028698"
---
# <a name="troubleshooting-product-long-known-issues"></a>Problembehandlung bei [!INCLUDE [Product long](includes/product-long.md)] bekannten Problemen

## <a name="sensor-failure-communication-error"></a>Kommunikationsfehler durch Sensorfehler

Sie erhalten folgenden Sensorfehler:

System.Net.Http.HttpRequestException: Fehler beim Senden der Anforderung. ---> System.Net.WebException: Es konnte keine Verbindung mit dem Remoteserver hergestellt werden ---> System.Net.Sockets.SocketException: Fehler beim Herstellen der Verbindung, weil die Gegenstelle nach einer bestimmten Zeitspanne nicht ordnungsgemäß reagiert hat, oder die hergestellte Verbindung konnte nicht aufrechterhalten werden, weil der verbundene Host nicht reagiert hat...

**Lösung:**

Stellen Sie sicher, dass die Kommunikation für Localhost an TCP-Port 444 nicht blockiert ist. Weitere Informationen zu den [!INCLUDE [Product long](includes/product-long.md)] Voraussetzungen finden Sie unter [Ports](prerequisites.md#ports).

## <a name="deployment-log-location"></a>Speicherort des Bereitstellungsprotokolls

Die [!INCLUDE [Product short](includes/product-short.md)] Bereitstellungs Protokolle befinden sich im temporären Verzeichnis des Benutzers, der das Produkt installiert hat. Beim Standardinstallationsspeicherort lautet der Pfad: C:\Benutzer\Administrator\AppData\Local\Temp (oder ein Verzeichnis über „%temp%“). Weitere Informationen finden Sie unter [Problembehandlung [!INCLUDE [Product short](includes/product-short.md)] mithilfe von Protokollen](troubleshooting-using-logs.md) .

## <a name="proxy-authentication-problem-presents-as-a-licensing-error"></a>Proxyauthentifizierungsproblem wird als Lizenzierungsfehler dargestellt

Während der Sensorinstallation erhalten Sie die folgende Fehlermeldung:  **Der Sensor konnte aufgrund von Lizenzierungsproblemen nicht registriert werden**.

**Einträge im Bereitstellungsprotokoll:**

[1C60:1AA8][2018-03-24T23:59:13]i000: 2018-03-25 02:59:13.1237 Info  InteractiveDeploymentManager ValidateCreateSensorAsync returned [validateCreateSensorResult=LicenseInvalid]] [1C60:1AA8][2018-03-24T23:59:56]i000: 2018-03-25 02:59:56.4856 Info  InteractiveDeploymentManager ValidateCreateSensorAsync returned [validateCreateSensorResult=LicenseInvalid]] [1C60:1AA8][2018-03-25T00:27:56]i000: 2018-03-25 03:27:56.7399 Debug SensorBootstrapperApplication Engine.Quit [deploymentResultStatus=1602 isRestartRequired=False]] [1C60:15B8][2018-03-25T00:27:56]i500: Wird heruntergefahren, Exitcode: 0x642

**Ursache**:

In einigen Fällen kann bei der Kommunikation über einen Proxy während der Authentifizierung auf den [!INCLUDE [Product short](includes/product-short.md)] Sensor mit dem Fehler 401 oder 403 anstelle des Fehlers 407 geantwortet werden. Der [!INCLUDE [Product short](includes/product-short.md)] Sensor interpretiert den Fehler 401 oder 403 als Lizenzierungs Problem und nicht als Proxy Authentifizierungs Problem.

**Lösung:**

Stellen Sie sicher, dass der Sensor über den konfigurierten Proxy ohne Authentifizierung zu „*. atp.azure.com“ navigieren kann. Weitere Informationen finden Sie unter [Konfigurieren von Endpunktproxy- und Internetkonnektivitätseinstellungen für Ihren Azure ATP-Sensor](configure-proxy.md).

## <a name="proxy-authentication-problem-presents-as-a-connection-error"></a>Darstellung des Proxyauthentifizierungsproblems als Verbindungsfehler

Während der Sensorinstallation erhalten Sie die folgende Fehlermeldung: **The sensor failed to connect to service.** (Fehler beim Herstellen einer Verbindung vom Sensor zum Dienst.)

**Ursache:**

Das Problem kann durch einen transparenten Proxy Konfigurationsfehler auf Server Core verursacht werden, z. b., wenn die Stamm Zertifikate, die für erforderlich [!INCLUDE [Product short](includes/product-short.md)] sind, nicht aktuell sind oder nicht vorhanden sind.

**Lösung:**

Führen Sie das folgende PowerShell-Cmdlet aus, um zu überprüfen, ob das [!INCLUDE [Product short](includes/product-short.md)] Vertrauenswürdige Stamm Zertifikat auf Server Core vorhanden ist. Im folgenden Beispiel werden die Stammzertifikate „DigiCert Baltimore Root“ und „DigiCert Global Root“ verwendet.

```powershell
Get-ChildItem -Path "Cert:\LocalMachine\Root" | where { $_.Thumbprint -eq "D4DE20D05E66FC53FE1A50882C78DB2852CAE474"} | fl
Get-ChildItem -Path "Cert:\LocalMachine\Root" | where { $_.Thumbprint -eq "df3c24f9bfd666761b268073fe06d1cc8d4f82a4"} | fl
```

```Output
Subject      : CN=Baltimore CyberTrust Root, OU=CyberTrust, O=Baltimore, C=IE
Issuer       : CN=Baltimore CyberTrust Root, OU=CyberTrust, O=Baltimore, C=IE
Thumbprint   : D4DE20D05E66FC53FE1A50882C78DB2852CAE474
FriendlyName : DigiCert Baltimore Root
NotBefore    : 5/12/2000 11:46:00 AM
NotAfter     : 5/12/2025 4:59:00 PM
Extensions   : {System.Security.Cryptography.Oid, System.Security.Cryptography.Oid, System.Security.Cryptography.Oid}

Subject      : CN=DigiCert Global Root G2, OU=www.digicert.com, O=DigiCert Inc, C=US
Issuer       : CN=DigiCert Global Root G2, OU=www.digicert.com, O=DigiCert Inc, C=US
Thumbprint   : DF3C24F9BFD666761B268073FE06D1CC8D4F82A4
FriendlyName : DigiCert Global Root G2
NotBefore    : 01/08/2013 15:00:00
NotAfter     : 15/01/2038 14:00:00
Extensions   : {System.Security.Cryptography.Oid, System.Security.Cryptography.Oid, System.Security.Cryptography.Oid}
```

Führen Sie die folgenden Schritte aus, wenn die Ausgabe nicht Ihren Erwartungen entspricht:

1. Laden Sie das [Baltimore CyberTrust-Stammzertifikat](https://cacert.omniroot.com/bc2025.crt) und [DigiCert Global Root G2](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt) auf den Server Core-Computer herunter.
1. Führen Sie das folgende PowerShell-Cmdlet aus, um das Zertifikat zu installieren.

    ```powershell
    Import-Certificate -FilePath "<PATH_TO_CERTIFICATE_FILE>\bc2025.crt" -CertStoreLocation Cert:\LocalMachine\Root
    Import-Certificate -FilePath "<PATH_TO_CERTIFICATE_FILE>\DigiCertGlobalRootG2.crt" -CertStoreLocation Cert:\LocalMachine\Root
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

## <a name="product-short-sensor-nic-teaming-issue"></a>[!INCLUDE [Product short](includes/product-short.md)] Problem mit dem Sensor NIC-Team Vorgang <a name="nic-teaming"></a>

Wenn Sie versuchen, den [!INCLUDE [Product short](includes/product-short.md)] Sensor auf einem Computer zu installieren, der mit einem NIC-Team Vorgangs Adapter konfiguriert ist, erhalten Sie einen Installationsfehler. Wenn Sie den [!INCLUDE [Product short](includes/product-short.md)] Sensor auf einem Computer installieren möchten, der mit NIC-Team Vorgang konfiguriert ist, befolgen Sie die folgenden Anweisungen:

1. Laden Sie das Installationsprogramm npcap Version 1,0 von herunter  [https://nmap.org/npcap/](https://nmap.org/npcap/dist/npcap-1.00.exe) .
    - Alternativ dazu können Sie die OEM-Version des Npcap-Treibers (der die automatische Installation unterstützt) vom Supportteam anfordern.
    - Kopien von npcap werden nicht in Bezug auf die fünf Kopier-, fünf Computer-oder Benutzer Lizenzierungs Einschränkungen gezählt, wenn Sie nur in Verbindung mit installiert und verwendet werden [!INCLUDE [Product short](includes/product-short.md)] . Weitere Informationen finden Sie unter [NPCAP-Lizenzierung](https://github.com/nmap/npcap/blob/master/LICENSE).

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

Unter den Windows-Betriebssystemen 2008 R2 und 2012 werden [!INCLUDE [Product short](includes/product-short.md)]-Sensoren im Modus Multi Processor Group (Mehrere Prozessorgruppen) nicht unterstützt.

Mögliche Problemumgehungen:

- Wenn Hyperthreading aktiviert ist, deaktivieren Sie es. Dadurch kann die Anzahl logischer Kerne möglicherweise weit genug reduziert werden, sodass eine Ausführung im Modus **Mehrere Prozessorgruppen** nicht notwendig ist.

- Wenn Ihr Computer weniger als 64 logische Kerne aufweist und auf einem HP-Host ausgeführt wird, können Sie möglicherweise die BIOS-Einstellung **NUMA Group Size Optimization** vom Standardwert **Clustered** in **Flat** ändern.

## <a name="microsoft-defender-for-endpoint-integration-issue"></a>Problem bei der Integration von Microsoft Defender for Endpoint

[!INCLUDE [Product short](includes/product-short.md)] ermöglicht die Integration in [!INCLUDE [Product short](includes/product-short.md)] Microsoft Defender for Endpoint. Weitere Informationen finden Sie [ [!INCLUDE [Product short](includes/product-short.md)] unter integrieren in Microsoft Defender for Endpoint](integrate-mde.md) .

## <a name="vmware-virtual-machine-sensor-issue"></a>Problem mit dem Sensor des virtuellen VMware-Computers

Wenn Sie über einen [!INCLUDE [Product short](includes/product-short.md)] Sensor auf virtuellen VMware-Computern verfügen, erhalten Sie möglicherweise die Integritäts Warnung, **dass der Netzwerk Datenverkehr nicht analysiert** wird. Als Ursache kommt ein Konfigurationskonflikt in VMware infrage.

So beheben Sie dieses Problem:

Legen Sie auf dem Gast Betriebssystem **in der** NIC-Konfiguration der virtuellen Maschine Folgendes fest: **IPv4 TSO Offload**.

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

Der Sensor konnte das angegebene GMSA-Konto nicht aus dem [!INCLUDE [Product short](includes/product-short.md)] Portal abrufen.

**Lösung:**

Stellen Sie sicher, dass die Anmeldeinformationen des gruppenverwalteten Dienstkontos korrekt sind und dem Sensor die erforderlichen Berechtigungen zum Abrufen der Anmeldeinformationen des Kontos erteilt wurden. In der angewandten Richtlinie sollten Sie das gMSA-Konto zu **Anmelden als Dienst** unter Zuweisungen von Benutzerrechten hinzufügen.

## <a name="report-downloads-cannot-contain-more-than-300000-entries"></a>Berichtsdownloads dürfen nicht mehr als 300.000 Einträge enthalten

[!INCLUDE [Product short](includes/product-short.md)] unterstützt keine Downloads von Berichten, die mehr als 300.000 Einträge pro Bericht enthalten. Die Berichte werden unvollständig gerendert, wenn mehr als 300.000 Einträge enthalten sind.

**Ursache**:

Dies ist eine technisch bedingte Begrenzung.

**Lösung:**

Keine bekannte Lösung.

## <a name="see-also"></a>Weitere Informationen

- [Voraussetzungen für [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md)
- [Kapazitätsplanung für [!INCLUDE [Product short](includes/product-short.md)]](capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-forwarding.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
