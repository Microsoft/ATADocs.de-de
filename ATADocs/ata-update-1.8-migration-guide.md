---
title: Migrationshandbuch zur Aktualisierung auf Advanced Threat Analytics 1.8 | Microsoft-Dokumentation
description: Prozeduren zum Aktualisieren von ATA auf Version 1.8
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/5/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e5a9718c-b22e-41f7-a614-f00fc4997682
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1042f464f424d2805542a8145d2e09d592fe8a51
ms.sourcegitcommit: 53b56220fa761671442da273364bdb3d21269c9e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/05/2017
---
# Aktualisieren von ATA auf Version 1.8
<a id="updating-ata-to-version-18" class="xliff"></a>

> [!NOTE] 
> Wenn ATA in Ihrer Umgebung nicht installiert ist, laden Sie die vollständige ATA-Version (enthält Version 1.8) herunter, und befolgen Sie die unter [Installieren von ATA](install-ata-step1.md) beschriebene Standardinstallation.

Wenn ATA Version 1.7 bereits bereitgestellt wurde, zeigt die vorliegende Anleitung die für die Aktualisierung der Bereitstellung erforderlichen Schritte.

> [!NOTE] 
>  Nur ATA Version 1.7 Update 1 und 1.7 Update 2 können auf ATA Version 1.8 aktualisiert werden. Alle früheren Versionen von ATA können nicht direkt auf ATA Version 1.8 aktualisiert werden.

So aktualisieren Sie auf ATA Version 1.8:

1.  [Laden Sie die Updateversion von ATA 1.8 aus dem Download Center herunter](https://www.microsoft.com/download/details.aspx?id=55536) oder die vollständige Version aus dem [Eval Center](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics).<br>
In der Migrationsversion kann die Datei nur für die Aktualisierung von ATA 1.7 verwendet werden. In der Version aus dem Evaluationszentrum wird die gleiche Installationsdatei („Microsoft ATA Center Setup.exe“) für die Installation einer neuen Bereitstellung von ATA und zum Aktualisieren von vorhandener Bereitstellungen verwendet.

2.  Aktualisieren von ATA Center

4.  Aktualisieren der ATA-Gateways

    > [!IMPORTANT]
    > Aktualisieren Sie alle ATA-Gateways, damit ATA ordnungsgemäß funktioniert.

### Schritt 1: Aktualisieren von ATA Center
<a id="step-1-update-the-ata-center" class="xliff"></a>

1.  Sichern Sie die Datenbank (optional):

    -   Falls das ATA Center als virtueller Computer ausgeführt wird und Sie einen Prüfpunkt erstellen möchten, fahren Sie den virtuellen Computer zunächst herunter.

    -   Wenn das ATA-Center auf einem physischen Server läuft, finden Sie unter [Notfallwiederherstellung](disaster-recovery.md) weitere Informationen zum Sichern der Datenbank.

2.  Führen Sie die Installationsdatei **Microsoft ATA Center Setup.exe** aus, und befolgen Sie die Anweisungen auf dem Bildschirm, um das Update zu installieren.

    -  Wählen Sie auf der Seite **Willkommen** Ihre Sprache aus, und klicken Sie auf **Weiter**.

    -  Wenn Sie die automatischen Updates in Version 1.7 nicht aktiviert haben, werden Sie aufgefordert, ATA für die Verwendung von Microsoft Update für ATA festzulegen, um auf dem neuesten Stand zu bleiben.  Wählen Sie auf der Microsoft Update-Seite **Microsoft Update für die Suche nach Updates verwenden (empfohlen)** aus.
    ![ATA-Aktualisierung](media/ata_ms_update.png)
     
     Damit ändern Sie die Windows-Einstellungen so, dass Updates für andere Microsoft-Produkte (einschließlich ATA) möglich sind, wie hier zu sehen. 
    ![Automatisches Windows-Update](media/ata_installupdatesautomatically.png)

    -  Wählen Sie im Bildschirm **Datenmigration** aus, ob Sie alle Daten oder nur einen Teil davon migrieren möchten. Wenn Sie nur Teildaten migrieren möchten, funktionieren alle Erkennungen sofort, mit Ausnahme der Erkennung von ungewöhnlichem Verhalten, da es drei Wochen dauert, bis ein vollständige Profil erstellt wurde.  
    
    Für die Installation der **teilweisen** Migration der Daten wird deutlich weniger Zeit benötigt. Wenn Sie die Option **vollständige** Datenmigration auswählen, nimmt der Abschluss der Installation möglicherweise sehr viel Zeit in Anspruch. Achten Sie darauf, sich die geschätzte Dauer und den erforderlichen Speicherplatz anzuschauen. Diese sind beide auf der Seite **Datenmigration** aufgelistet. Diese Zahlen sind abhängig von der von Ihnen in vorherigen ATA-Versionen gespeicherten Menge an erfasstem Datenverkehr. Auf der Seite unten können Sie sich z.B. eine Datenmigration aus einer großen Datenbank ansehen:
         
    ![ATA-Datenmigration](media/migration-data-migration.png)

    -  Klicken Sie auf **Aktualisieren**. Nachdem Sie auf „Aktualisieren“ geklickt haben, ist ATA bis zum Abschluss der Aktualisierung offline.

4.  Nachdem das Update von ATA Center erfolgreich abgeschlossen wurde, klicken Sie auf **Starten**, um das Fenster **Updates** in der ATA-Konsole für die ATA-Gateways zu öffnen.

    ![Update success screen](media/migration-center-success.png)

5.  Wenn Sie das automatische Update für Ihre ATA-Gateways schon im Fenster **Updates** festgelegt haben, werden Sie zu diesem Zeitpunkt ein Update durchführen. Falls dies nicht der Fall sein sollte, klicken Sie auf **Aktualisieren** neben jedem ATA-Gateway.
  
![Abbildung „Gateways aktualisieren“](media/migration-update-gw.png)

  
> [!IMPORTANT] 
> Aktualisieren Sie alle ATA-Gateways, damit ATA ordnungsgemäß funktioniert.
 
> [!NOTE] 
> Wechseln Sie zum Installieren neuer ATA-Gateways zum Bildschirm **Gateways**, klicken Sie auf **Gatewaysetup herunterladen**, um das ATA 1.8-Gateway-Installationspaket zu erhalten, und folgen Sie den Anweisungen zum Installieren eines neuen Gateways in [Schritt 4. Installieren des ATA-Gateways](install-ata-step4.md).


## Weitere Informationen
<a id="see-also" class="xliff"></a>

- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
