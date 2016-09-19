---
title: Migrationshandbuch zum Update auf ATA 1.7 | Microsoft ATA
description: Prozeduren zum Aktualisieren von ATA auf Version 1.7
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: fb65eb41-b215-4530-93a2-0b8991f4e980
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: e3b690767e5c6f5561a97a73eccfbf50ddb04148
ms.openlocfilehash: 5c20c41c3fe587f18087d64f4f84c1df65072fde


---

# Migrationshandbuch zur Aktualisierung auf ATA 1.7
Das Update auf ATA 1.7 bietet Verbesserungen in folgenden Bereichen:

-   Neue Erkennungen

-   Verbesserungen an vorhandenen Erkennungen
  

## Aktualisieren von ATA auf Version 1.7
> [!NOTE] 
> Wenn ATA in Ihrer Umgebung nicht installiert ist, laden Sie die vollständige ATA-Version (enthält Version 1.7) herunter, und befolgen Sie die unter [Installieren von ATA](/advanced-threat-analytics/deploy-use/install-ata) beschriebene Standardinstallation.

Wenn ATA Version 1.6 bereits bereitgestellt wurde, zeigt die vorliegende Anleitung die für die Aktualisierung der Bereitstellung erforderlichen Schritte.

> [!NOTE] 
> ATA 1.7 kann nicht direkt auf ATA 1.4 oder 1.5 installiert werden. Sie müssen zuerst ATA 1.6 installieren. 

So aktualisieren Sie auf ATA, Version 1.7:

1.  [Herunterladen von Update 1.7](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics)<br>
In dieser Version wird die gleiche Installationsdatei („Microsoft ATA Center Setup.exe“) für die Installation einer neuen Bereitstellung von ATA und zum Aktualisieren von vorhandener Bereitstellungen verwendet.

2.  Aktualisieren von ATA Center

4.  Aktualisieren der ATA-Gateways

    > [!IMPORTANT]
    > Aktualisieren Sie alle ATA-Gateways, damit ATA ordnungsgemäß funktioniert.

### Schritt 1: Aktualisieren von ATA Center

1.  Sichern Sie die Datenbank (optional):

    -   Falls das ATA Center als virtueller Computer ausgeführt wird und Sie einen Prüfpunkt erstellen möchten, fahren Sie den virtuellen Computer zunächst herunter.

    -   Wenn ATA Center auf einem physischen Server ausgeführt wird, befolgen Sie die empfohlene Vorgehensweise zum [Sichern der MongoDB](https://docs.mongodb.org/manual/core/backups/).

2.  Führen Sie die Installationsdatei **Microsoft ATA Center Setup.exe** aus, und befolgen Sie die Anweisungen auf dem Bildschirm, um das Update zu installieren.

    -  Wählen Sie auf der Seite **Willkommen** Ihre Sprache aus, und klicken Sie auf **Weiter**.

    -  Wenn Sie die automatischen Updates in Version 1.6 nicht aktiviert haben, werden Sie aufgefordert, ATA für die Verwendung von Microsoft Update für ATA festzulegen, um auf dem neuesten Stand zu bleiben.  Wählen Sie auf der Microsoft Update-Seite **Microsoft Update für die Suche nach Updates verwenden (empfohlen)** aus.
    ![Abbildung zum Aktualisieren von ATA](media/ata_ms_update.png) Damit ändern Sie die Windows-Einstellungen so, dass Updates für andere Microsoft-Produkte (einschließlich ATA) möglich sind, wie hier zu sehen. 
     ![Abbildung von Windows AutoUpdate](media/ata_installupdatesautomatically.png)

    -  Wählen Sie im Bildschirm **Datenmigration** aus, ob Sie alle Daten oder nur einen Teil davon migrieren möchten. Wenn Sie nur einen Teil der Daten migrieren, werden Ihr zuvor erfasster Netzwerkdatenverkehr und die Verhaltensprofile nicht migriert. Das bedeutet, dass es drei Wochen dauert, bis die Erkennung für ungewöhnliches Verhalten ein vollständiges Profil besitzt, um die Erkennung anormaler Aktivität zu aktivieren. Während dieser drei Wochen arbeiten alle anderen ATA-Erkennungen ordnungsgemäß. Für die Installation der **teilweise** Migration der Daten wird deutlich weniger Zeit benötigt. Wenn Sie die Option **vollständige** Datenmigration auswählen, nimmt der Abschluss der Installation möglicherweise sehr viel Zeit in Anspruch. Die auf dem Bildschirm **Datenmigration** aufgeführten Werte für die geschätzte Dauer und den benötigte Speicherplatz hängen von der Menge des zuvor erfassten Netzwerkdatenverkehr ab, den Sie in früheren Versionen von ATA gespeichert haben. Bevor Sie **Teilweise** oder **Vollständig** auswählen, überprüfen Sie diese Anforderungen.  
    
    ![ATA-Datenmigration](media/migration data migration.png)

    -  Klicken Sie auf **Aktualisieren**. Nachdem Sie auf „Aktualisieren“ geklickt haben, ist ATA bis zum Abschluss der Aktualisierung offline.

4.  Nachdem das Update von ATA Center erfolgreich abgeschlossen wurde, klicken Sie auf **Starten**, um das Fenster **Updates** in der ATA-Konsole für die ATA-Gateways zu öffnen.
    ![Update success screen](media/migration center success.png)

5.  Wenn Sie das automatische Update für Ihre ATA-Gateways schon im Fenster **Updates** festgelegt haben, werden Sie zu diesem Zeitpunkt ein Update durchführen. Falls dies nicht der Fall sein sollte, klicken Sie auf **Aktualisieren** neben jedem ATA-Gateway.
  ![Abbildung „Gateways aktualisieren“](media/migration update gw.png)

  
> [!IMPORTANT] 
> Aktualisieren Sie alle ATA-Gateways, damit ATA ordnungsgemäß funktioniert.
> Der konfigurierte Syslog-Überwachungsport wird für alle Gateways auf 514 geändert.
 
    > [!NOTE] 
    > To install new ATA Gateways, go the **Gateways** screen and click **Download Gateway Setup** to get the ATA 1.7 installation package and follow the instructions for new Gateway installation as described in [Step 4. Install the ATA Gateway](/advanced-threat-analytics/deploy-use/install-ata-step4) .



## Weitere Informationen

- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Aug16_HO5-->


