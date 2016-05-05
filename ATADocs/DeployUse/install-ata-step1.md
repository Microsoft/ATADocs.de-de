---
# required metadata

title: Installieren von ATA – Schritt 1 | Microsoft Advanced Threat Analytics
description: Im ersten Schritt beim Installieren von ATA wird ATA Center auf den ausgewählten Server heruntergeladen und dort installiert.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Installieren von ATA – Schritt 1

>[!div class="step-by-step"]
[« Vor der Installation](install-ata-preinstall.md)
[Schritt 2 »](install-ata-step2.md)

## Schritt 1: Herunterladen und Installieren von ATA Center
Nachdem Sie überprüft haben, ob der Server die Anforderungen erfüllt, können Sie mit der Installation von ATA Center fortfahren.

Führen Sie die folgenden Schritte auf dem ATA Center-Server aus.

1.  Laden Sie ATA vom [TechNet Evaluation Center](http://www.microsoft.com/en-us/evalcenter/) herunter.

2.  Melden Sie sich unter dem Namen eines Benutzers an, der Mitglied der lokalen Administratorengruppe ist.

3.  Führen Sie „Microsoft ATA Center Setup.exe“ an einer Eingabeaufforderung mit erhöhten Rechten aus, und befolgen Sie die Anweisungen des Setup-Assistenten.

4.  Wählen Sie auf der Seite **Willkommen** Ihre Sprache aus, und klicken Sie auf **Weiter**.

5.  Lesen Sie den Lizenzvertrag für Endbenutzer, und klicken Sie auf **Weiter**, sofern Sie die Lizenzbedingungen akzeptieren.

6.  Geben Sie auf der Seite **ATA Center-Konfiguration** basierend auf Ihrer Umgebung die folgenden Informationen ein:

    |Feld|Beschreibung|Kommentare|
    |---------|---------------|------------|
    |Installationspfad|Dies ist der Speicherort, an dem ATA Center installiert wird. Standardmäßig ist dies „%programfiles%\Microsoft Advanced Threat Analytics\Center“.|Behalten Sie den Standardwert bei.|
    |Datenbankdatenpfad|Dies ist der Speicherort, an dem sich die MongoDB-Datenbankdateien befinden. Standardmäßig ist dies „%programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data“.|Ändern Sie den Speicherort, sodass ausreichend Speicherplatz für Ihre Größenanpassung verfügbar ist. **Hinweis:** <ul><li>In Produktionsumgebungen sollten Sie ein Laufwerk verwenden, das der Kapazitätsplanung entsprechend über ausreichend Speicherplatz verfügt.</li><li>Für umfangreiche Bereitstellungen sollte sich die Datenbank auf einem separaten physischen Datenträger befinden.</li></ul>Informationen zur Größenanpassung finden Sie unter [ATA-Kapazitätsplanung](/advanced-threat-analytics/PlanDesign/ata-capacity-planning).|
    |Datenbankjournalpfad|Dies ist der Speicherort, an dem sich die Datenbankjournaldateien befinden. Standardmäßig ist dies „%programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data\journal“.|Für umfangreiche Bereitstellungen sollte sich das Datenbankjournal auf einem anderen physischen Datenträger als die Datenbank und das Systemlaufwerk befinden. Ändern Sie den Speicherort, sodass ausreichend Speicherplatz für das Datenbankjournal verfügbar ist.|
    |ATA Center-Dienst – IP-Adresse: Port|Dies ist die IP-Adresse, auf die der ATA Center-Dienst in Bezug auf die Kommunikation von den ATA-Gateways lauscht.<br /><br />**Standardport:** 443|Klicken Sie auf den Pfeil nach unten, um die vom ATA Center-Dienst verwendete IP-Adresse auszuwählen.<br /><br />Die IP-Adresse und der Port des ATA Center-Diensts müssen sich von der IP-Adresse und dem Port der ATA-Konsole unterscheiden. Ändern Sie daher den Port der ATA-Konsole.|
    |SSL-Zertifikat für ATA Center-Dienst|Dies ist das Zertifikat, das vom ATA Center-Dienst verwendet wird.|Klicken Sie auf das Schlüsselsymbol, um ein installiertes Zertifikat auszuwählen oder bei der Bereitstellung in einer Testumgebung ein selbstsigniertes Zertifikat zu überprüfen.|
    |IP-Adresse für ATA-Konsole|Dies ist die IP-Adresse, die von IIS für die ATA-Konsole verwendet wird.|Klicken Sie auf den Pfeil nach unten, um die von der ATA-Konsole verwendete IP-Adresse auszuwählen. **Hinweis:** Notieren Sie sich diese IP-Adresse für den Zugriff auf die ATA-Konsole über das ATA-Gateway.|
    |SSL-Zertifikat für ATA-Konsole|Dies ist das von IIS verwendete Zertifikat.|Klicken Sie auf das Schlüsselsymbol, um ein installiertes Zertifikat auszuwählen oder bei der Bereitstellung in einer Testumgebung ein selbstsigniertes Zertifikat zu überprüfen.|
    ![Abbildung ATA Center-Konfiguration](media/ATA-Center-Configuration.JPG)

7.  Klicken Sie auf **Installieren**, um ATA und die zugehörigen Komponenten zu installieren und die Verbindung zwischen ATA Center und der ATA-Konsole zu erstellen.

8.  Klicken Sie nach Abschluss der Installation auf **Starten**, um die Verbindung mit der ATA-Konsole herzustellen.

    Bei der Installation von ATA Center werden die folgenden Komponenten installiert und konfiguriert:

    -   Internetinformationsdienste (IIS)

    -   MongoDB

    -   ATA Center-Dienst und IIS-Site für die ATA-Konsole

    -   Benutzerdefinierter Systemmonitor-Datensammlungssatz

    -   Selbstsignierte Zertifikate (sofern bei der Installation ausgewählt)

> [!NOTE]
> Im Hinblick auf die Problembehandlung und Produkterweiterung wird empfohlen, dass Sie MongoVue und andere MongoDB-Add-Ins oder andere Drittanbietertools Ihrer Wahl installieren. Für MongoVue muss .NET Framework 3.5 installiert sein.

### Überprüfen der Installation

1.  Überprüfen Sie, ob der Microsoft Advanced Threat Analytics Center-Dienst ausgeführt wird.

2.  Klicken Sie auf dem Desktop auf die Verknüpfung „Microsoft Advanced Threat Analytics“, um eine Verbindung mit der ATA-Konsole herzustellen. Melden Sie sich mit den gleichen Benutzeranmeldeinformationen an, die Sie auch zum Installieren von ATA Center verwendet haben. Bei Ihrer ersten Anmeldung in der ATA-Konsole werden Sie automatisch zur Seite **Domänenverbindungseinstellungen** weitergeleitet, auf der Sie die Konfiguration und Bereitstellung der ATA-Gateways fortsetzen können.

3.  Überprüfen Sie die Fehlerdatei in der Datei **Microsoft.Tri.Center-Errors.log** im Standardspeicherort „%programfiles%\Microsoft Advanced Threat Analytics\Center\Logs“.

>[!div class="step-by-step"]
[« Vor der Installation](install-ata-preinstall.md)
[Schritt 2 »](install-ata-step2.md)

## Siehe auch

- [Unterstützung finden Sie in unserem Forum.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Konfigurieren der Ereignissammlung](/advanced-threat-analytics/plandesign/configure-event-collection)
- [Voraussetzungen für ATA](/advanced-threat-analytics/plandesign/ata-prerequisites)


<!--HONumber=Apr16_HO2-->


