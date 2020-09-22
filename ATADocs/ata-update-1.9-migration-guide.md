---
title: Migrations Handbuch zu Advanced Threat Analytics Update to 1,9
description: Methoden zum Aktualisieren von ATA auf Version 1.9
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/25/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 2946310a-8e4e-48fc-9450-fc9647efeb22
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 2277e8eb6cbfb9c61dd0e814d6f2170599ff9c86
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2020
ms.locfileid: "90911815"
---
# <a name="updating-ata-to-version-19"></a>Aktualisieren von ATA auf Version 1.9

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

> [!NOTE] 
> Wenn ATA nicht in Ihrer Umgebung installiert ist, laden Sie die vollständige ATA-Version (enthält Version 1.9) herunter, und führen Sie die unter [Installieren von ATA](install-ata-step1.md) beschriebene Standardinstallation aus.

Wenn Sie bereits über ATA Version 1.8 verfügen, zeigt die vorliegende Anleitung die für die Aktualisierung der Bereitstellung erforderlichen Schritte auf.

> [!NOTE] 
>  Nur ATA 1.8 (Update 1.8.6645) und Version 1.8 Update 1 (1.8.6765) können auf ATA Version 1.9 aktualisiert werden. Alle früheren Versionen von ATA können nicht direkt auf ATA 1.9 aktualisiert werden.

So aktualisieren Sie auf ATA 1.9:

1.  [Laden Sie die Updateversion von ATA 1.9 aus dem Download Center](https://www.microsoft.com/download/details.aspx?id=56725) oder die vollständige Version aus dem [Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics) herunter.<br>
In der Migrationsversion kann die Datei nur für die Aktualisierung von ATA 1.8 verwendet werden. In der Version aus dem Evaluationszentrum wird die gleiche Installationsdatei („Microsoft ATA Center Setup.exe“) für die Installation einer neuen Bereitstellung von ATA und zum Aktualisieren von vorhandener Bereitstellungen verwendet.

1. Aktualisieren von ATA Center

1. Aktualisieren der ATA-Gateways

    > [!IMPORTANT]
    > Aktualisieren Sie alle ATA-Gateways, damit ATA ordnungsgemäß funktioniert.

### <a name="step-1-update-the-ata-center"></a>Schritt 1: Aktualisieren von ATA Center

1. Sichern Sie die Datenbank (optional):

   - Falls ATA Center als virtueller Computer ausgeführt wird und Sie einen Prüfpunkt erstellen möchten, fahren Sie den virtuellen Computer zunächst herunter.

   - Wenn das ATA-Center auf einem physischen Server läuft, finden Sie unter [Notfallwiederherstellung](disaster-recovery.md) weitere Informationen zum Sichern der Datenbank.

1. Führen Sie die Installationsdatei **Microsoft ATA Center Setup.exe** aus, und befolgen Sie die Anweisungen auf dem Bildschirm, um das Update zu installieren.

   - Wählen Sie auf der Seite **Willkommen** Ihre Sprache aus, und klicken Sie auf **Weiter**.

   - Wenn Sie die automatischen Updates in Version 1.8 nicht aktiviert haben, werden Sie aufgefordert, für ATA die Verwendung von Microsoft Update für ATA einzurichten, um auf dem neuesten Stand zu bleiben.  Wählen Sie auf der Seite Microsoft Update die Option **Microsoft Update beim Suchen nach Updates verwenden (empfohlen) aus**.
     ![ATA-Aktualisierung](media/ata_ms_update.png)
     
     Dadurch werden die Windows-Einstellungen angepasst und Updates für ATA aktiviert. 
    
   - Über die Anzeige **Partielle Datenmigration** erfahren Sie, dass zuvor erfasster Datenverkehr, Ereignisse, Entitäten und Ermittlungen von verknüpften Daten gelöscht wurden. Alle Erkennungen funktionieren sofort, mit Ausnahme von ungewöhnlichem Verhalten, ungewöhnlichen Änderungen von Gruppen, Reconnaissance mithilfe von Verzeichnisdiensten (SAM-R) und Erkennungen von Herunterstufungen der Verschlüsselung. Bei diesen Ausnahmen dauert es erfahrungsgemäß bis zu drei Wochen, um ein vollständiges Profil zu erstellen. 
     
     ![Partielle ATA-Migration](media/partial-migration.png)

   - Klicken Sie auf **Aktualisieren**. Nachdem Sie auf „Aktualisieren“ geklickt haben, ist ATA bis zum Abschluss der Aktualisierung offline.

1. Nachdem das Update von ATA Center erfolgreich abgeschlossen wurde, klicken Sie auf **Starten**, um das Fenster **Updates** in der ATA-Konsole für die ATA-Gateways zu öffnen.

    ![Update success screen](media/migration-center-success.png)

1. Wenn Sie das automatische Update für Ihre ATA-Gateways schon im Fenster **Updates** festgelegt haben, wird zu diesem Zeitpunkt ein Update durchgeführt. Klicken Sie andernfalls neben jedem ATA-Gateway auf **Aktualisieren**.
  
    ![Abbildung „Gateways aktualisieren“](media/migration-update-gw.png)

  
> [!IMPORTANT] 
> Aktualisieren Sie alle ATA-Gateways, damit ATA ordnungsgemäß funktioniert.
 
> [!NOTE] 
> Wechseln Sie zum Installieren neuer ATA-Gateways zum Bildschirm **Gateways** , klicken Sie auf **gatewaysetup herunterladen** , um das ATA 1,9-gatewayinstallationspaket zu erhalten, und befolgen Sie die Anweisungen für die neue Gatewayinstallation [gemäß der Beschreibung Installieren Sie das ATA-Gateway](install-ata-step4.md).


## <a name="see-also"></a>Weitere Informationen

- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
