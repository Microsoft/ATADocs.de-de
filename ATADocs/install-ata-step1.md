---
title: 'Installieren von Advanced Threat Analytics: Schritt 1'
description: Im ersten Schritt beim Installieren von ATA wird ATA Center auf den ausgewählten Server heruntergeladen und dort installiert.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/07/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 3e50a48c6ffb108bee7c5b760a0368b04e3f0c61
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2020
ms.locfileid: "90911522"
---
# <a name="install-ata---step-1"></a>Installieren von ATA – Schritt 1

[!INCLUDE [Banner for top of topics](includes/banner.md)]

[!INCLUDE [Rebranding notice](includes/rebranding.md)]
> [!div class="step-by-step"]
> [Schritt 2»](install-ata-step2.md)

Diese Installationsschritte stellen Anweisungen zur Durchführung einer Neuinstallation von ATA 1.9 bereit. Informationen zum Aktualisieren einer vorhandenen früheren ATA-Bereitstellungsversion finden Sie im [ATA-Migrationshandbuch für Version 1.9](ata-update-1.9-migration-guide.md).

> [!IMPORTANT]
> Wenn Sie Windows 2012 R2 verwenden, installieren Sie vor ATA das Update KB2934520 auf dem ATA Center-Server und den ATA-Gatewayservern, da andernfalls bei der ATA-Installation dieses Update installiert wird und inmitten der ATA-Installation ein Neustart erforderlich ist.

## <a name="step-1-download-and-install-the-ata-center"></a>Schritt 1: Herunterladen und Installieren von ATA Center

Nachdem Sie überprüft haben, ob der Server die Anforderungen erfüllt, können Sie mit der Installation von ATA Center fortfahren.

> [!NOTE]
> Wenn Sie eine Lizenz für Enterprise Mobility + Security (EMS) direkt über das Microsoft 365-Portal oder über das Cloud Solution Partner-Lizenzmodell (CSP) erworben haben und Sie über keinen Zugriff auf ATA über das Microsoft Volume Licensing Center (VLSC) verfügen, kontaktieren Sie den Microsoft-Kundendienst, um den Prozess zum Aktivieren von Advanced Threat Analytics (ATA) abzurufen.

Führen Sie die folgenden Schritte auf dem ATA Center-Server aus.

1. Laden Sie ATA aus dem [Microsoft Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/default.aspx) oder dem [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/) oder [MSDN](/powerapps/developer/common-data-service/org-service/subscribe-sdk-assembly-updates-using-nuget)herunter.

1. Melden Sie sich bei dem Computer, auf dem Sie ATA Center installieren, als ein Benutzer an, der Mitglied der lokalen Administratorgruppe ist.

1. Führen Sie **Microsoft ATA Center Setup.exe** aus, und befolgen Sie die Anweisungen des Setup-Assistenten.

    > [!NOTE]
    > Stellen Sie sicher, dass Sie die Installationsdatei von einem lokalen Laufwerk und nicht von einer bereitgestellten ISO-Datei ausführen, um Probleme bei einem im Rahmen der Installation ggf. erforderlichen Neustart zu vermeiden.

1. Wenn Microsoft .NET Framework nicht installiert ist, werden Sie aufgefordert, es zu installieren, wenn Sie die Installation starten. Möglicherweise werden Sie nach der Installation von .NET Framework zu einem Neustart aufgefordert.
1. Wählen Sie auf der Seite **Willkommen** die Sprache aus, die für die ATA-Installations Bildschirme verwendet werden soll, und klicken Sie auf **weiter**.

1. Lesen Sie die Microsoft-Software-Lizenzbedingungen, aktivieren Sie das entsprechende Kontrollkästchen, wenn Sie den Bedingungen zustimmen, und klicken Sie anschließend auf **Weiter**.

1. Es wird empfohlen, für ATA die automatische Aktualisierung festzulegen. Wenn auf Ihrem Computer für Windows nicht die automatische Aktualisierung festgelegt ist, wird der Bildschirm **Verwenden Sie Microsoft Update, damit Ihr Computer sicher und auf dem aktuellen Stand bleibt** angezeigt.
    ![ATA-Aktualisierung](media/ata_ms_update.png)

1. Wählen Sie **Microsoft Update für die Suche nach Updates verwenden (empfohlen)**. Damit ändern Sie die Windows-Einstellungen so, dass Updates für andere Microsoft-Produkte (einschließlich ATA) möglich sind.

    ![Abbildung von Windows AutoUpdate](media/ata_installupdatesautomatically.png)

1. Geben Sie auf der Seite **Configure the Center (Konfigurieren von ATA Center)** basierend auf Ihrer Umgebung die folgenden Informationen ein:

    |Feld|BESCHREIBUNG|Kommentare|
    |---------|---------------|------------|
    |Installationspfad|Dies ist der Speicherort, an dem ATA Center installiert wird. Standardmäßig ist dies „%programfiles%\Microsoft Advanced Threat Analytics\Center“.|Behalten Sie den Standardwert bei.|
    |Datenbankdatenpfad|Dies ist der Speicherort, an dem sich die MongoDB-Datenbankdateien befinden. Standardmäßig ist dies „%programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data“.|Ändern Sie den Speicherort, sodass ausreichend Speicherplatz für Ihre Größenanpassung verfügbar ist. **Hinweis:** <ul><li>In Produktionsumgebungen sollten Sie ein Laufwerk verwenden, das der Kapazitätsplanung entsprechend über ausreichend Speicherplatz verfügt.</li><li>Für umfangreiche Bereitstellungen sollte sich die Datenbank auf einem separaten physischen Datenträger befinden.</li></ul>Informationen zur Größenanpassung finden Sie unter [ATA-Kapazitätsplanung](ata-capacity-planning.md).|
    |SSL-Zertifikat für Center-Dienst|Dies ist das Zertifikat, das von der ATA-Konsole und vom ATA Center-Dienst verwendet wird.|Klicken Sie auf das Schlüsselsymbol, um ein installiertes Zertifikat auszuwählen, oder verwenden Sie das Kontrollkästchen, um ein selbstsigniertes Zertifikat zu erstellen.|

    ![Abbildung ATA Center-Konfiguration](media/ATA-Center-Configuration.png)

    > [!NOTE]
    > Achten Sie darauf, dass Sie sich auf Integritäts Warnungen bezüglich des SSL-Zertifikats Status und Ablauf Warnungen des Center-Dienstanbieter achten Wenn das Zertifikat abläuft, müssen Sie ATA vollständig neu bereitstellen.

1. Klicken Sie auf **Installieren**, um ATA Center und die zugehörigen Komponenten zu installieren.  
Bei der Installation von ATA Center werden die folgenden Komponenten installiert und konfiguriert:

    - ATA Center-Dienst

    - MongoDB

    - Benutzerdefinierter Systemmonitor-Datensammlungssatz

    - Selbstsignierte Zertifikate (sofern bei der Installation ausgewählt)

1. Wenn die Installation abgeschlossen ist, klicken Sie auf **Start**, um die ATA-Konsole zu öffnen und das Setup auf der Seite **Konfiguration** abzuschließen.
    Die Einstellungsseite **Allgemein** wird automatisch geöffnet, damit Sie die Konfiguration und Bereitstellung der ATA-Gateways fortsetzen können.
    Da Sie sich mit einer IP-Adresse bei der Website anmelden, wird eine Warnung im Zusammenhang mit dem Zertifikat angezeigt. Das ist normal, und Sie können auf **Laden dieser Website fortsetzen** klicken.

### <a name="validate-installation"></a>Überprüfen der Installation

1. Überprüfen Sie, ob der Dienst **Microsoft Advanced Threat Analytics Center** ausgeführt wird.
1. Klicken Sie auf dem Desktop auf die **Microsoft Advanced Threat Analytics** Verknüpfung, um eine Verbindung mit der ATA-Konsole herzustellen. Melden Sie sich mit den Benutzeranmeldeinformationen an, die Sie zum Installieren von ATA Center verwendet haben.

### <a name="set-anti-virus-exclusions"></a>Festlegen von Ausnahmen für die Antivirensoftware

Legen Sie nach der Installation von ATA Center das MongoDB-Datenbankverzeichnis als Ausnahme fest, damit dieses nicht fortlaufend von Ihrer Antivirenanwendung überprüft wird. Der Standardspeicherort in der Datenbank lautet **C:\Programme\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data**.

Stellen Sie sicher, dass Sie auch die folgenden Ordner und Prozesse von der Antivirusprüfung ausschließen:

**Ordner**  
C:\Programme\Microsoft Advanced Threat Analytics\Center\ParentKerberosAsBloomFilters  
C:\Programme\Microsoft Advanced Threat Analytics\Center\ParentKerberosTgsBloomFilters  
C:\Programme\Microsoft Advanced Threat Analytics\Center\Backup  
C:\Programme\Microsoft Advanced Threat Analytics\Center\Logs

**Prozesse**  
„mongod.exe“  
„Microsoft.Tri.Center.exe“

Wenn Sie ATA in einem anderen Verzeichnis installiert haben, stellen Sie sicher, dass Sie die Ordnerpfade entsprechend Ihrer Installation ändern.

> [!div class="step-by-step"]
> [«Vor der Installation](configure-port-mirroring.md) 
>  [Schritt 2»](install-ata-step2.md)

## <a name="related-videos"></a>Verwandte Videos

- [Auswählen des richtigen ATA-Gatewaytyps](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)
- [Übersicht über die ATA-Bereitstellung](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)

## <a name="see-also"></a>Weitere Informationen

- [Handbuch für die ATA POC-Bereitstellung](https://aka.ms/atapoc)
- [Tool zur Bemessung von ATA-Gateways](https://aka.ms/atasizingtool)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [ATA-Voraussetzungen](ata-prerequisites.md)