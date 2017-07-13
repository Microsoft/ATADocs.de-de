---
title: "Installieren von Advanced Threat Analytics – Schritt 1 | Microsoft-Dokumentation"
description: "Im ersten Schritt beim Installieren von ATA wird ATA Center auf den ausgewählten Server heruntergeladen und dort installiert."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/12/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 97fa1522ca43cf92416ac845b8886f2905e9981b
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
*Gilt für: Advanced Threat Analytics Version 1.8*


# Installieren von ATA – Schritt 1
<a id="install-ata---step-1" class="xliff"></a>

>[!div class="step-by-step"]
[Schritt 2 »](install-ata-step2.md)

Diese Installationsschritte stellen Anweisungen zur Durchführung einer Neuinstallation von ATA 1.8 bereit. Informationen zum Aktualisieren einer vorhandenen früheren ATA-Bereitstellungsversion finden Sie im [ATA-Migrationshandbuch für Version 1.8](ata-update-1.8-migration-guide.md).

> [!IMPORTANT] 
> Wenn Sie Windows 2012 R2 verwenden, installieren Sie vor ATA das Update KB2934520 auf dem ATA Center-Server und den ATA-Gatewayservern, da andernfalls bei der ATA-Installation dieses Update installiert wird und inmitten der ATA-Installation ein Neustart erforderlich ist.

## Schritt 1: Herunterladen und Installieren von ATA Center
<a id="step-1-download-and-install-the-ata-center" class="xliff"></a>
Nachdem Sie überprüft haben, ob der Server die Anforderungen erfüllt, können Sie mit der Installation von ATA Center fortfahren.
    
> [!NOTE]
>Wenn Sie eine Lizenz für Enterprise Mobility + Security (EMS) direkt über das Office 365-Portal oder über das Cloud Solution Partner-Lizenzmodell (CSP) erworben haben, und Sie keinen Zugriff auf ATA über das Microsoft Volume Licensing Center (VLSC) verfügen, kontaktieren Sie den Microsoft-Kundendienst, um den Prozess zum Aktivieren von Advanced Threat Analytics (ATA) abzurufen.

Führen Sie die folgenden Schritte auf dem ATA Center-Server aus.

1.  Laden Sie ATA aus dem [Microsoft Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/default.aspx), dem [TechNet-Evaluierungscenter](http://www.microsoft.com/evalcenter/) oder aus [MSDN](https://msdn.microsoft.com/subscriptions/downloads) herunter.

2.  Melden Sie sich bei dem Computer, auf dem Sie ATA Center installieren, als ein Benutzer an, der Mitglied der lokalen Administratorgruppe ist.

3.  Führen Sie **Microsoft ATA Center Setup.exe** aus, und befolgen Sie die Anweisungen des Setup-Assistenten.

> [!NOTE]   
> Stellen Sie sicher, dass Sie die Installationsdatei von einem lokalen Laufwerk und nicht von einer bereitgestellten ISO-Datei ausführen, um Probleme bei einem im Rahmen der Installation ggf. erforderlichen Neustart zu vermeiden.   

4.  Wenn Microsoft .Net Framework nicht installiert ist, werden Sie beim Starten der Installation aufgefordert, .Net Framework zu installieren. Möglicherweise werden Sie nach der Installation von .NET Framework zu einem Neustart aufgefordert.
5.  Wählen Sie auf der Seite **Willkommen** die Sprache für die ATA-Installationsbildschirme aus, und klicken Sie auf **Weiter**.

6.  Lesen Sie die Microsoft-Software-Lizenzbedingungen, aktivieren Sie das Kontrollkästchen, wenn Sie den Bedingungen zustimmen, und klicken Sie anschließend auf **Weiter**.

7.  Sie sollten festlegen, dass ATA automatisch aktualisiert wird. Wenn Windows nicht für dieses automatische Update auf dem Computer konfiguriert ist, wird der Bildschirm **Verwenden Sie Microsoft Update, damit Ihr Computer sicher und auf dem aktuellen Stand bleibt** angezeigt. 
    ![ATA-Aktualisierung](media/ata_ms_update.png)

8. Wählen Sie **Microsoft Update für die Suche nach Updates verwenden (empfohlen)**. Damit ändern Sie die Windows-Einstellungen so, dass Updates für andere Microsoft-Produkte (einschließlich ATA) möglich sind, wie hier zu sehen. 

    ![Abbildung von Windows AutoUpdate](media/ata_installupdatesautomatically.png)

8.  Geben Sie auf der Seite **Configure the Center (Konfigurieren von ATA Center)** basierend auf Ihrer Umgebung die folgenden Informationen ein:

    |Feld|Beschreibung|Kommentare|
    |---------|---------------|------------|
    |Installationspfad|Dies ist der Speicherort, an dem ATA Center installiert wird. Standardmäßig ist dies „%programfiles%\Microsoft Advanced Threat Analytics\Center“.|Behalten Sie den Standardwert bei.|
    |Datenbankdatenpfad|Dies ist der Speicherort, an dem sich die MongoDB-Datenbankdateien befinden. Standardmäßig ist dies „%programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data“.|Ändern Sie den Speicherort, sodass ausreichend Speicherplatz für Ihre Größenanpassung verfügbar ist. **Hinweis:** <ul><li>In Produktionsumgebungen sollten Sie ein Laufwerk verwenden, das der Kapazitätsplanung entsprechend über ausreichend Speicherplatz verfügt.</li><li>Für umfangreiche Bereitstellungen sollte sich die Datenbank auf einem separaten physischen Datenträger befinden.</li></ul>Informationen zur Größenanpassung finden Sie unter [ATA-Kapazitätsplanung](ata-capacity-planning.md).|
    |SSL-Zertifikat für Center-Dienst|Dies ist das Zertifikat, das von der ATA-Konsole und vom ATA Center-Dienst verwendet wird.|Klicken Sie auf das Schlüsselsymbol, um ein installiertes Zertifikat auszuwählen oder bei der Bereitstellung in einer Testumgebung ein selbstsigniertes Zertifikat zu überprüfen. Beachten Sie, dass Sie die Option zum Erstellen eines selbstsignierten Zertifikats in der Benutzeroberfläche des ACS-Filters haben.|
        
    ![Abbildung ATA Center-Konfiguration](media/ATA-Center-Configuration.png)

10.  Klicken Sie auf **Installieren**, um ATA Center und die zugehörigen Komponenten zu installieren.
    Bei der Installation von ATA Center werden die folgenden Komponenten installiert und konfiguriert:

    -   ATA Center-Dienst

    -   MongoDB

    -   Benutzerdefinierter Systemmonitor-Datensammlungssatz

    -   Selbstsignierte Zertifikate (sofern bei der Installation ausgewählt)

11.  Wenn die Installation abgeschlossen ist, klicken Sie auf **Start**, um die ATA-Konsole zu öffnen, und schließen Sie das Setup auf der Seite **Konfiguration**.
An dieser Stelle werden Sie automatisch zur Seite mit den **allgemeinen Einstellungen** weitergeleitet, auf der Sie die Konfiguration und Bereitstellung der ATA-Gateways fortsetzen können.
Da Sie sich mit einer IP-Adresse bei der Website anmelden, wird eine Warnung im Zusammenhang mit dem Zertifikat angezeigt. Das ist normal, und Sie sollten auf **Laden dieser Website fortsetzen** klicken.

### Überprüfen der Installation
<a id="validate-installation" class="xliff"></a>

1.  Überprüfen Sie, ob der Dienst **Microsoft Advanced Threat Analytics-Gateway** ausgeführt wird.
2.  Klicken Sie auf dem Desktop auf die Verknüpfung **Microsoft Advanced Threat Analytics**, um eine Verbindung mit der ATA-Konsole herzustellen. Melden Sie sich mit den gleichen Benutzeranmeldeinformationen an, die Sie auch zum Installieren von ATA Center verwendet haben.



>[!div class="step-by-step"]
[« Vor der Installation](configure-port-mirroring.md)
[Schritt 2 »](install-ata-step2.md)

## Siehe auch
<a id="see-also" class="xliff"></a>

- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Voraussetzungen für ATA](ata-prerequisites.md)

