---
title: Unbeaufsichtigte Installation von Advanced Threat Analytics | Microsoft-Dokumentation
description: Hier wird die unbeaufsichtigte Installation von ATA beschrieben.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 08/29/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: c38db312ea877b63580d745153aa58ea34a160a6
ms.sourcegitcommit: 9ce330726e5de8c05eae6a20d3e6c1d8bef3cd0e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/29/2017
---
*Gilt für: Advanced Threat Analytics Version 1.8*


# <a name="ata-silent-installation"></a>Unbeaufsichtigte ATA-Installation
Dieser Artikel enthält Anweisungen zur unbeaufsichtigten Installation von ATA.

## <a name="prerequisites"></a>Voraussetzungen

ATA Version 1.8 erfordert die Installation von Microsoft .NET Framework 4.6.1. 

Beim Installieren oder Aktualisieren von ATA, wird .Net Framework 4.6.1 automatisch als Teil der Bereitstellung von Microsoft ATA installiert.

> [!Note] 
> Die Installation von .Net Framework 4.6.1 macht möglicherweise einen Neustart des Servers erforderlich. Wenn Sie beim das ATA-Gateway auf Domänencontrollern installieren, sollten Sie ein Wartungsfenster für diese Domänencontroller planen.
Wenn Sie die Methode zur unbeaufsichtigten Installation von ATA verwenden, ist das Installationsprogramm so konfiguriert, dass der Server am Ende der Installation automatisch neu gestartet wird (falls erforderlich). Aufgrund eines Windows Installer-Fehlers, kann das „/norestart“-Flag nicht verlässlich verwendet werden, um sicherzustellen, dass der Server keinen Neustart ausführt. Führen Sie also nur eine unbeaufsichtigte Installation während der Anzeige eines Wartungsfensters aus.

Zum Verfolgen des Fortschritts der Bereitstellung überwachen Sie die Protokolle des ATA-Installationsprogramms unter **%AppData%\Local\Temp**.


## <a name="install-the-ata-center"></a>Installieren von ATA Center

Verwenden Sie zum Installieren von ATA Center den folgenden Befehl:

**Syntax**:

    "Microsoft ATA Center Setup.exe" [/quiet] [/Help] [--LicenseAccepted] [NetFrameworkCommandLineArguments="/q"] [InstallationPath="<InstallPath>"] [DatabaseDataPath= "<DBPath>"] [CenterIpAddress=<CenterIPAddress>] [CenterPort=<CenterPort>] [CenterCertificateThumbprint="<CertThumbprint>"] 
    [ConsoleIpAddress=<ConsoleIPAddress>] [ConsoleCertificateThumbprint="<CertThumbprint >"]
    
**Installationsoptionen**:

> [!div class="mx-tableFixed"]
|Name|Syntax|Erforderlich für die unbeaufsichtigte Installation?|Beschreibung|
|-------------|----------|---------|---------|
|Quiet|/quiet|Ja|Führt das Installationsprogramm ohne Benutzeroberfläche und Eingabeaufforderungen aus.|
|Hilfe|/help|Nein|Stellt Hilfe und eine Kurzübersicht bereit. Zeigt die korrekte Verwendung des Installationsbefehl einschließlich einer Liste aller Optionen und Verhaltensweisen an.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Ja|Legt die Parameter für die Installation von .Net Framework fest. Muss festgelegt werden, um die unbeaufsichtigte Installation von .Net Framework zu erzwingen.|
|LicenseAccepted|--LicenseAccepted|Ja|Gibt an, dass die Lizenz gelesen und genehmigt wurde. Muss für die unbeaufsichtigte Installation festgelegt werden.|

**Installationsparameter**:

> [!div class="mx-tableFixed"]
|Name|Syntax|Erforderlich für die unbeaufsichtigte Installation?|Beschreibung|
|-------------|----------|---------|---------|
|InstallationPath|InstallationPath=„<InstallPath>"|Nein|Legt den Pfad für die Installation der ATA-Binärdateien fest. Standardpfad: „C:\Programme\Microsoft Advanced Threat Analytics\Center“.|
|DatabaseDataPath|DatabaseDataPath= „<DBPath>"|Nein|Legt den Pfad für den Datenordner der ATA-Datenbank fest. Standardpfad: „C:\Programme\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data“.|
|CenterIpAddress|CenterIpAddress=<CenterIPAddress>|Ja|Legt die IP-Adresse des ATA Center-Diensts fest.|
|CenterPort|CenterPort=<CenterPort>|Ja|Legt den Netzwerkport des ATA Center-Diensts fest.|
|CenterCertificateThumbprint|CenterCertificateThumbprint=„<CertThumbprint>"|Nein|Legt den Zertifikatsfingerabdruck für den ATA Center-Dienst fest. Dieses Zertifikat schützt die Kommunikation zwischen ATA Center und dem ATA-Gateway. Wird diese Option nicht festgelegt, wird bei der Installation ein selbstsigniertes Zertifikat generiert.|
|ConsoleIpAddress|ConsoleIpAddress=<ConsoleIPAddress>|Ja|Legt die IP-Adresse der ATA-Konsole fest.|
|ConsoleCertificateThumbprint|ConsoleCertificateThumbprint=„<CertThumbprint >“|Nein|Gibt den Zertifikatsfingerabdruck für die ATA-Konsole an. Dieses Zertifikat wird zum Überprüfen der Identität der Website der ATA-Konsole verwendet. Wird diese Option nicht festgelegt, wird bei der Installation ein selbstsigniertes Zertifikat generiert.|

**Beispiele**: So installieren Sie ATA Center mit Standardinstallationspfaden und einer einzigen IP-Adresse:

    "Microsoft ATA Center Setup.exe" /quiet --LicenseAccepted NetFrameworkCommandLineArguments="/q" CenterIpAddress=192.168.0.10
    CenterPort=444 ConsoleIpAddress=192.168.0.10

So installieren Sie ATA Center mit Standardinstallationspfaden, zwei IP-Adressen und benutzerdefinierten Zertifikatfingerabdrücken:

    "Microsoft ATA Center Setup.exe" /quiet --LicenseAccepted NetFrameworkCommandLineArguments ="/q" CenterIpAddress=192.168.0.10 CenterPort=443 CenterCertificateThumbprint= ‎"1E2079739F624148ABDF502BF9C799FCB8C7212F"
    ConsoleIpAddress=192.168.0.11  ConsoleCertificateThumbprint="G9530253C976BFA9342FD1A716C0EC94207BFD5A"

## <a name="update-the-ata-center"></a>Aktualisieren von ATA Center

Verwenden Sie zum Aktualisieren von ATA Center den folgenden Befehl:

**Syntax**:

    "Microsoft ATA Center Setup.exe" [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]


**Installationsoptionen**:

> [!div class="mx-tableFixed"]
|Name|Syntax|Erforderlich für die unbeaufsichtigte Installation?|Beschreibung|
|-------------|----------|---------|---------|
|Quiet|/quiet|Ja|Führt das Installationsprogramm ohne Benutzeroberfläche und Eingabeaufforderungen aus.|
|Hilfe|/help|Nein|Stellt Hilfe und eine Kurzübersicht bereit. Zeigt die korrekte Verwendung des Installationsbefehl einschließlich einer Liste aller Optionen und Verhaltensweisen an.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Ja|Legt die Parameter für die Installation von .Net Framework fest. Muss festgelegt werden, um die unbeaufsichtigte Installation von .Net Framework zu erzwingen.|


Beim Aktualisieren von ATA erkennt das Installationsprogramm automatisch, dass ATA bereits auf dem Server installiert ist, und es ist keine Option für die Updateinstallation erforderlich.

**Beispiele**: So führen Sie ein unbeaufsichtigtes Update von ATA Center aus. Das ATA Center-Update kann in großen Umgebungen etwas Zeit in Anspruch nehmen. Überwachen Sie die ATA-Protokolle, um den Fortschritt des Updates zu verfolgen.

        "Microsoft ATA Center Setup.exe" /quiet NetFrameworkCommandLineArguments="/q"

## <a name="uninstall-the-ata-center-silently"></a>Unbeaufsichtigte Deinstallation von ATA Center

Verwenden Sie den folgenden Befehl, um eine unbeaufsichtigte Deinstallation von ATA Center auszuführen: **Syntax**:

    Microsoft ATA Center Setup.exe [/quiet] [/Uninstall] [/Help]
     [--DeleteExistingDatabaseData]

**Installationsoptionen**:

> [!div class="mx-tableFixed"]
|Name|Syntax|Erforderlich für die unbeaufsichtigte Deinstallation?|Beschreibung|
|-------------|----------|---------|---------|
|Quiet|/quiet|Ja|Führt das Deinstallationsprogramm ohne Benutzeroberfläche und Eingabeaufforderungen aus.|
|Deinstallieren|/uninstall|Ja|Führt die unbeaufsichtigte Deinstallation von ATA Center vom Server aus.|
|Hilfe|/help|Nein|Stellt Hilfe und eine Kurzübersicht bereit. Zeigt die korrekte Verwendung des Installationsbefehl einschließlich einer Liste aller Optionen und Verhaltensweisen an.|

**Installationsparameter**:

> [!div class="mx-tableFixed"]
|Name|Syntax|Erforderlich für die unbeaufsichtigte Deinstallation?|Beschreibung|
|-------------|----------|---------|---------|
|DeleteExistingDatabaseData|DeleteExistingDatabaseData|Nein|Löscht alle Dateien in der vorhandenen Datenbank.|

**Beispiele**: So führen Sie eine unbeaufsichtigte Deinstallation von ATA Center vom Server aus und entfernen alle vorhandenen Datenbankdaten:


    "Microsoft ATA Center Setup.exe" /quiet /uninstall --DeleteExistingDatabaseData

## <a name="ata-gateway-silent-installation"></a>Unbeaufsichtigte Installation des ATA-Gateways

> [!NOTE]
> Bei der unbeaufsichtigten Bereitstellung des ATA-Lightweight-Gateways über System Center Configuration Manager oder ein anderes System für die Softwarebereitstellung empfiehlt es sich, zwei Bereitstellungspakete zu erstellen:</br>– Net Framework 4.6.1 einschließlich Neustart des Domänencontrollers</br>– ATA Gateway </br>Machen Sie das ATA-Gateway-Paket abhängig von der .Net Framework-Paketbereitstellung. </br>Rufen Sie das [.Net Framework 4.6.1-Paket für die Offlinebereitstellung](https://www.microsoft.com/download/details.aspx?id=49982) ab. 


Verwenden Sie den folgenden Befehl für eine unbeaufsichtigte Installation des ATA-Gateways:

**Syntax**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/Help] [NetFrameworkCommandLineArguments ="/q"] 
    [ConsoleAccountName="<AccountName>"] 
    [ConsoleAccountPassword="<AccountPassword>"]

> [!NOTE]
> Wenn Sie auf einem mit einer Domäne verbundenen Computer arbeiten und sich mit Ihrem ATA-Administratorbenutzernamen und dem dazugehörigen Kennwort angemeldet haben, ist die Eingabe Ihrer Anmeldeinformationen hier nicht notwendig.


**Installationsoptionen**:

> [!div class="mx-tableFixed"]
|Name|Syntax|Erforderlich für die unbeaufsichtigte Installation?|Beschreibung|
|-------------|----------|---------|---------|
|Quiet|/quiet|Ja|Führt das Installationsprogramm ohne Benutzeroberfläche und Eingabeaufforderungen aus.|
|Hilfe|/help|Nein|Stellt Hilfe und eine Kurzübersicht bereit. Zeigt die korrekte Verwendung des Installationsbefehl einschließlich einer Liste aller Optionen und Verhaltensweisen an.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Ja|Legt die Parameter für die Installation von .Net Framework fest. Muss festgelegt werden, um die unbeaufsichtigte Installation von .Net Framework zu erzwingen.|

**Installationsparameter**:

> [!div class="mx-tableFixed"]
|Name|Syntax|Erforderlich für die unbeaufsichtigte Installation?|Beschreibung|
|-------------|----------|---------|---------|
|ConsoleAccountName|ConsoleAccountName=„<AccountName>“|Ja|Legt den Namen des Benutzerkontos (user@domain.com) fest, mit dem das ATA-Gateway mit ATA Center registriert wird.|
|ConsoleAccountPassword|ConsoleAccountPassword=„<AccountPassword>"|Ja|Legt das Passwort für das Benutzerkonto (user@domain.com) fest, mit dem das ATA-Gateway mit ATA Center registriert wird.|

**Beispiele**: Für eine unbeaufsichtigte Installation des ATA-Gateway-Protokolls melden Sie sich auf dem mit einer Domäne verbundenen Computer mit Ihren ATA-Administratoranmeldeinformationen an, und Sie müssen keine Anmeldeinformationen angeben. Registrieren Sie es alternativ mit den angegebenen Anmeldeinformationen bei ATA Center:

    "Microsoft ATA Gateway Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" 
    ConsoleAccountName="user@contoso.com" ConsoleAccountPassword="userpwd"
    

## <a name="update-the-ata-gateway"></a>Aktualisieren des ATA-Gateways

Verwenden Sie den folgenden Befehl für ein unbeaufsichtigtes Update des ATA-Gateways:

**Syntax**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]


**Installationsoptionen**:

> [!div class="mx-tableFixed"]
|Name|Syntax|Erforderlich für die unbeaufsichtigte Installation?|Beschreibung|
|-------------|----------|---------|---------|
|Quiet|/quiet|Ja|Führt das Installationsprogramm ohne Benutzeroberfläche und Eingabeaufforderungen aus.|
|Hilfe|/help|Nein|Stellt Hilfe und eine Kurzübersicht bereit. Zeigt die korrekte Verwendung des Installationsbefehl einschließlich einer Liste aller Optionen und Verhaltensweisen an.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Ja|Legt die Parameter für die Installation von .Net Framework fest. Muss festgelegt werden, um die unbeaufsichtigte Installation von .Net Framework zu erzwingen.|


**Beispiele**: So führen Sie ein unbeaufsichtigtes Update des ATA-Gateways aus:

        Microsoft ATA Gateway Setup.exe /quiet NetFrameworkCommandLineArguments="/q"

## <a name="uninstall-the-ata-gateway-silently"></a>Unbeaufsichtigte Deinstallation des ATA-Gateways

Verwenden Sie den folgenden Befehl, um eine unbeaufsichtigte Deinstallation des ATA-Gateways auszuführen: **Syntax**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/Uninstall] [/Help]
    
**Installationsoptionen**:

> [!div class="mx-tableFixed"]
|Name|Syntax|Erforderlich für die unbeaufsichtigte Deinstallation?|Beschreibung|
|-------------|----------|---------|---------|
|Quiet|/quiet|Ja|Führt das Deinstallationsprogramm ohne Benutzeroberfläche und Eingabeaufforderungen aus.|
|Deinstallieren|/uninstall|Ja|Führt die unbeaufsichtigte Deinstallation des ATA-Gateways vom Server aus.|
|Hilfe|/help|Nein|Stellt Hilfe und eine Kurzübersicht bereit. Zeigt die korrekte Verwendung des Installationsbefehl einschließlich einer Liste aller Optionen und Verhaltensweisen an.|

**Beispiele**: So führen Sie eine unbeaufsichtigte Deinstallation des ATA-Gateways aus:


    Microsoft ATA Gateway Setup.exe /quiet /uninstall
    









## <a name="see-also"></a>Weitere Informationen

- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Voraussetzungen für ATA](ata-prerequisites.md)