---
title: Migrationshandbuch zur Aktualisierung auf Advanced Threat Analytics 1.8 | Microsoft-Dokumentation
description: Prozeduren zum Aktualisieren von ATA auf Version 1.8
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: barbkess
ms.date: 07/20/2017
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: e5a9718c-b22e-41f7-a614-f00fc4997682
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 85ef846b2e6548d6a7dc34ebb8a8be9c678e5bfe
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2019
ms.locfileid: "56076945"
---
# <a name="updating-ata-to-version-18"></a>Aktualisieren von ATA auf Version 1.8

> [!NOTE] 
> Wenn ATA in Ihrer Umgebung nicht installiert ist, laden Sie die vollständige ATA-Version (enthält Version 1.8) herunter, und befolgen Sie die unter [Installieren von ATA](install-ata-step1.md) beschriebene Standardinstallation.

Wenn ATA Version 1.7 bereits bereitgestellt wird, zeigt die vorliegende Anleitung die für die Aktualisierung der Bereitstellung erforderlichen Schritte.

> [!NOTE] 
>  Nur ATA Version 1.7 Update 1 und 1.7 Update 2 können auf ATA Version 1.8 aktualisiert werden. Alle früheren Versionen von ATA können nicht direkt auf ATA Version 1.8 aktualisiert werden.

So aktualisieren Sie auf ATA Version 1.8:

1.  [Laden Sie die Updateversion von ATA 1.8 aus dem Download Center herunter](https://www.microsoft.com/download/details.aspx?id=55536) oder die vollständige Version aus dem [Eval Center](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics).<br>
In der Migrationsversion kann die Datei nur für die Aktualisierung von ATA 1.7 verwendet werden. In der Version aus dem Evaluationszentrum wird die gleiche Installationsdatei („Microsoft ATA Center Setup.exe“) für die Installation einer neuen Bereitstellung von ATA und zum Aktualisieren von vorhandener Bereitstellungen verwendet.

2.  Aktualisieren von ATA Center

4.  Aktualisieren der ATA-Gateways

    > [!IMPORTANT]
    > Aktualisieren Sie alle ATA-Gateways, damit ATA ordnungsgemäß funktioniert.

### <a name="step-1-update-the-ata-center"></a>Schritt 1: Aktualisieren von ATA Center

1. Sichern Sie die Datenbank (optional):

   -   Falls ATA Center als virtueller Computer ausgeführt wird und Sie einen Prüfpunkt erstellen möchten, fahren Sie den virtuellen Computer zunächst herunter.

   -   Wenn das ATA-Center auf einem physischen Server läuft, finden Sie unter [Notfallwiederherstellung](disaster-recovery.md) weitere Informationen zum Sichern der Datenbank.

2. Führen Sie die Installationsdatei **Microsoft ATA Center Setup.exe** aus, und befolgen Sie die Anweisungen auf dem Bildschirm, um das Update zu installieren.

   - Wählen Sie auf der Seite **Willkommen** Ihre Sprache aus, und klicken Sie auf **Weiter**.

   - Wenn Sie die automatischen Updates in Version 1.7 nicht aktiviert haben, werden Sie aufgefordert, ATA für die Verwendung von Microsoft Update für ATA festzulegen, um auf dem neuesten Stand zu bleiben.  Wählen Sie auf der Microsoft Update-Seite **Microsoft Update für die Suche nach Updates verwenden (empfohlen)** aus.
     ![ATA-Aktualisierung](media/ata_ms_update.png)
     
     Dadurch werden die Windows-Einstellungen angepasst und Updates für ATA aktiviert. 
    
   - Wählen Sie im Bildschirm **Datenmigration** aus, ob Sie alle Daten oder nur einen Teil davon migrieren möchten. Wenn Sie nur Teildaten migrieren möchten, funktionieren alle Erkennungen sofort, mit Ausnahme der Erkennung von ungewöhnlichem Verhalten, da es drei Wochen dauert, bis ein vollständiges Profil erstellt wurde.  
    
   Für die Installation der **teilweisen** Migration der Daten wird deutlich weniger Zeit benötigt. Wenn Sie die Option **vollständige** Datenmigration auswählen, nimmt der Abschluss der Installation möglicherweise sehr viel Zeit in Anspruch. Achten Sie darauf, sich die geschätzte Dauer und den erforderlichen Speicherplatz anzuschauen. Diese sind beide auf der Seite **Datenmigration** aufgelistet. Diese Zahlen sind abhängig von der von Ihnen in vorherigen ATA-Versionen gespeicherten Menge an erfasstem Datenverkehr. Auf der Seite unten können Sie sich z.B. eine Datenmigration aus einer großen Datenbank ansehen:
         
   ![ATA-Datenmigration](media/migration-data-migration.png)

   -  Klicken Sie auf **Aktualisieren**. Nachdem Sie auf „Aktualisieren“ geklickt haben, ist ATA bis zum Abschluss der Aktualisierung offline.

3. Nachdem das Update von ATA Center erfolgreich abgeschlossen wurde, klicken Sie auf **Starten**, um das Fenster **Updates** in der ATA-Konsole für die ATA-Gateways zu öffnen.

   ![Update success screen](media/migration-center-success.png)

4. Wenn Sie das automatische Update für Ihre ATA-Gateways schon im Fenster **Updates** festgelegt haben, wird zu diesem Zeitpunkt ein Update durchgeführt. Klicken Sie andernfalls neben jedem ATA-Gateway auf **Aktualisieren**.
  
![Abbildung „Gateways aktualisieren“](media/migration-update-gw.png)

  
> [!IMPORTANT] 
> Aktualisieren Sie alle ATA-Gateways, damit ATA ordnungsgemäß funktioniert.
 
> [!NOTE] 
> Wechseln Sie zum Installieren neuer ATA-Gateways zum Bildschirm **Gateways**, klicken Sie auf **Gatewaysetup herunterladen**, um das ATA 1.8-Gateway-Installationspaket zu erhalten, und folgen Sie den Anweisungen zum Installieren eines neuen Gateways in [Schritt 4. Installieren des ATA-Gateways](install-ata-step4.md).


## <a name="see-also"></a>Weitere Informationen

- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
