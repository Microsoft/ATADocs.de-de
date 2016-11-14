---
title: "Installieren von ATA – Schritt 1 | Microsoft ATA"
description: "Im ersten Schritt beim Installieren von ATA wird ATA Center auf den ausgewählten Server heruntergeladen und dort installiert."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 10/25/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: c71d5ed1c705de558f1144820703ffe84850679b
ms.openlocfilehash: cf7ae4eccdf70e4e8661ac55ec15fff00bc9c62e


---

*Gilt für: Advanced Threat Analytics Version 1.7*



# Installieren von ATA – Schritt 1

>[!div class="step-by-step"]
[Schritt 2 »](install-ata-step2.md)

Diese Installationsschritte stellen Anweisungen zur Durchführung einer Neuinstallation von ATA 1.7 bereit. Informationen zum Aktualisieren einer vorhandenen früheren ATA-Bereitstellungsversion finden Sie im [ATA-Migrationshandbuch für Version 1.7](/advanced-threat-analytics/understand-explore/ata-update-1.7-migration-guide).

> [!IMPORTANT] 
> Wenn Sie Windows 2012 R2 verwenden, installieren Sie vor ATA das Update KB2934520 auf dem ATA Center-Server und den ATA-Gatewayservern, da andernfalls bei der ATA-Installation dieses Update installiert wird und inmitten der ATA-Installation ein Neustart erforderlich ist.

## Schritt 1: Herunterladen und Installieren von ATA Center
Nachdem Sie überprüft haben, ob der Server die Anforderungen erfüllt, können Sie mit der Installation von ATA Center fortfahren.

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
    ![Abbildung – Aktualisieren von ATA](media/ata_ms_update.png)

8. Wählen Sie **Microsoft Update für die Suche nach Updates verwenden (empfohlen)**. Damit ändern Sie die Windows-Einstellungen so, dass Updates für andere Microsoft-Produkte (einschließlich ATA) möglich sind, wie hier zu sehen. 
    ![Abbildung von Windows AutoUpdate](media/ata_installupdatesautomatically.png)

8.  Geben Sie auf der Seite **ATA Center-Konfiguration** basierend auf Ihrer Umgebung die folgenden Informationen ein:

    |Feld|Beschreibung|Kommentare|
    |---------|---------------|------------|
    |Installationspfad|Dies ist der Speicherort, an dem ATA Center installiert wird. Standardmäßig ist dies „%programfiles%\Microsoft Advanced Threat Analytics\Center“.|Behalten Sie den Standardwert bei.|
    |Datenbankdatenpfad|Dies ist der Speicherort, an dem sich die MongoDB-Datenbankdateien befinden. Standardmäßig ist dies „%programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data“.|Ändern Sie den Speicherort, sodass ausreichend Speicherplatz für Ihre Größenanpassung verfügbar ist. **Hinweis:** <ul><li>In Produktionsumgebungen sollten Sie ein Laufwerk verwenden, das der Kapazitätsplanung entsprechend über ausreichend Speicherplatz verfügt.</li><li>Für umfangreiche Bereitstellungen sollte sich die Datenbank auf einem separaten physischen Datenträger befinden.</li></ul>Informationen zur Größenanpassung finden Sie unter [ATA-Kapazitätsplanung](/advanced-threat-analytics/plan-design/ata-capacity-planning).|
    |Center-Dienst – IP-Adresse: Port|Dies ist die IP-Adresse, auf die der ATA Center-Dienst in Bezug auf die Kommunikation von den ATA-Gateways lauscht.<br /><br />**Standardport:** 443|Klicken Sie auf den Pfeil nach unten, um die vom ATA Center-Dienst verwendete IP-Adresse auszuwählen.<br /><br />Die IP-Adresse und der Port des ATA Center-Diensts müssen sich von der IP-Adresse und dem Port der ATA-Konsole unterscheiden. Ändern Sie daher den Port der ATA-Konsole.|
    |SSL-Zertifikat für Center-Dienst|Dies ist das Zertifikat, das von der ATA-Konsole und vom ATA Center-Dienst verwendet wird.|Klicken Sie auf das Schlüsselsymbol, um ein installiertes Zertifikat auszuwählen oder bei der Bereitstellung in einer Testumgebung ein selbstsigniertes Zertifikat zu überprüfen.|
    |IP-Adresse für die Konsole|Dies ist die IP-Adresse, die für die ATA-Konsole verwendet wird.|Klicken Sie auf den Pfeil nach unten, um die von der ATA-Konsole verwendete IP-Adresse auszuwählen. **Hinweis:** Notieren Sie sich diese IP-Adresse für den Zugriff auf die ATA-Konsole über das ATA-Gateway.|
    
    ![Abbildung ATA Center-Konfiguration](media/ATA-Center-Configuration.png)

10.  Klicken Sie auf **Installieren**, um ATA Center und die zugehörigen Komponenten zu installieren.
    Bei der Installation von ATA Center werden die folgenden Komponenten installiert und konfiguriert:

    -   ATA Center-Dienst

    -   MongoDB

    -   Benutzerdefinierter Systemmonitor-Datensammlungssatz

    -   Selbstsignierte Zertifikate (sofern bei der Installation ausgewählt)

11.  Klicken Sie nach Abschluss der Installation auf **Starten**, um die Verbindung mit der ATA-Konsole herzustellen.
An dieser Stelle werden Sie automatisch zur Seite mit den **allgemeinen Einstellungen** weitergeleitet, auf der Sie die Konfiguration und Bereitstellung der ATA-Gateways fortsetzen können.
Da Sie sich mit einer IP-Adresse bei der Website anmelden, wird eine Warnung im Zusammenhang mit dem Zertifikat angezeigt. Das ist normal, und Sie sollten auf **Laden dieser Website fortsetzen** klicken.

### Überprüfen der Installation

1.  Überprüfen Sie, ob der Dienst **Microsoft Advanced Threat Analytics-Gateway** ausgeführt wird.
2.  Klicken Sie auf dem Desktop auf die Verknüpfung **Microsoft Advanced Threat Analytics**, um eine Verbindung mit der ATA-Konsole herzustellen. Melden Sie sich mit den gleichen Benutzeranmeldeinformationen an, die Sie auch zum Installieren von ATA Center verwendet haben.



>[!div class="step-by-step"]
[« Vor der Installation](preinstall-ata.md)
[Schritt 2 »](install-ata-step2.md)

## Weitere Informationen

- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Voraussetzungen für ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)




<!--HONumber=Oct16_HO4-->


