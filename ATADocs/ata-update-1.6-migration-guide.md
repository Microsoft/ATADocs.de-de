---
title: Migrations Handbuch zu Advanced Threat Analytics Update to 1,6
description: Prozeduren zum Aktualisieren von ATA auf Version 1.6
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 01/23/2017
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 0756ef64-3aef-4a69-8981-24fa8f285c6a
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 3c94379e73959d5fe22842d5286ce75673684cbf
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2020
ms.locfileid: "90909393"
---
# <a name="ata-update-to-16-migration-guide"></a>Migrationshandbuch zur Aktualisierung auf ATA 1.6

[!INCLUDE [Rebranding notice](includes/rebranding.md)]
Das Update auf ATA 1.6 bietet Verbesserungen in folgenden Bereichen:

- Neue Erkennungen

- Verbesserungen an vorhandenen Erkennungen

- Das ATA-Lightweight-Gateway

- Automatische Aktualisierungen

- Verbesserte ATA Center-Leistung

- Niedrigere Speicheranforderungen

- Unterstützung für IBM QRadar

## <a name="updating-ata-to-version-16"></a>Aktualisieren von ATA auf Version 1.6
> [!NOTE] 
> Wenn ATA in Ihrer Umgebung nicht installiert ist, laden Sie die vollständige ATA-Version (einschließlich Version 1,6) herunter, und befolgen Sie die unter [Installieren von ATA](install-ata-step1.md)beschriebene Standardinstallation.

Wenn ATA Version 1.5 bereits bereitgestellt wird, zeigt die vorliegende Anleitung die für die Aktualisierung der Bereitstellung erforderlichen Schritte.

> [!NOTE] 
> ATA 1.6 kann nicht direkt auf ATA 1.4 installiert werden. Sie müssen zuerst ATA 1.5 installieren. Wenn Sie versehentlich versucht haben, ATA 1.6 zu installieren, ohne zuerst ATA 1.5 zu installieren, wird folgende Fehlermeldung angezeigt: **Auf Ihrem Computer ist bereits eine neuere Version installiert.** Sie müssen die Elemente von ATA 1.6, die trotz des Fehlers bei der Installation auf dem Computer verbleiben, deinstallieren, bevor Sie ATA 1.5 installieren.

So aktualisieren Sie auf ATA, Version 1.6:

1. Um Problem beim Upgrade zu vermeiden, stellen Sie sicher, dass Sie die Schritte 8 bis 10 unter **Migrationsfehler, wenn auf ATA 1.6 aktualisiert wird** befolgen, wie in [Neuerungen in ATA 1.6](whats-new-version-1.6.md) beschrieben.
1. Stellen Sie sicher, dass genügend freier Speicherplatz für das Upgrade verfügbar ist. Sie können die Installation bis zur Bereitschaftsprüfung ausführen, um herauszufinden, wie viel Speicherplatz in etwa benötigt wird. Anschließend können Sie das Upgrade erneut starten, nachdem Sie die erforderliche Datenträgerkapazität zugewiesen haben.
1.  [Herunterladen von Update 1.6](https://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics)<br>
In dieser Version wird die gleiche Installationsdatei („Microsoft ATA Center Setup.exe“) für die Installation einer neuen Bereitstellung von ATA und zum Aktualisieren von vorhandener Bereitstellungen verwendet.

1. Aktualisieren von ATA Center

1. Downloaden des ATA-Gateway-Pakets

1. Aktualisieren der ATA-Gateways

    > [!IMPORTANT]
    > Aktualisieren Sie alle ATA-Gateways, damit ATA ordnungsgemäß funktioniert.

### <a name="step-1-update-the-ata-center"></a>Schritt 1: Aktualisieren von ATA Center

1. Sichern Sie die Datenbank (optional):

    - Falls ATA Center als virtueller Computer ausgeführt wird und Sie einen Prüfpunkt erstellen möchten, fahren Sie den virtuellen Computer zunächst herunter.

    - Wenn ATA Center auf einem physischen Server ausgeführt wird, befolgen Sie die empfohlene Vorgehensweise zum [Sichern von MongoDB](https://docs.mongodb.org/manual/core/backups/).

1. Führen Sie die Installationsdatei („Microsoft ATA Center Setup.exe“) aus, und befolgen Sie die Anweisungen auf dem Bildschirm, um das Update zu installieren.

    1.  Für ATA 1.6 muss .NET Framework 4.6.1 installiert sein. Wenn .NET Framework 4.6.1 noch nicht installiert ist, wird es als Teil der ATA-Installation installiert.
    
        > [!NOTE] 
        > Die Installation von .Net Framework 4.6.1 macht möglicherweise einen Neustart des Servers erforderlich. Die ATA-Installation wird erst nach dem Neustart des Servers fortgesetzt.
    
    2.  Wählen Sie auf der Seite **Willkommen** Ihre Sprache aus, und klicken Sie auf **Weiter**.

    3.  Lesen Sie den Lizenzvertrag für Endbenutzer, und klicken Sie auf **Weiter**, sofern Sie die Lizenzbedingungen akzeptieren.

    4.  Jetzt können Sie ATA mithilfe von Microsoft Update auf dem neuesten Stand halten.  Wählen Sie auf der Seite Microsoft Update die Option **Microsoft Update beim Suchen nach Updates verwenden (empfohlen) aus**.
    ![ATA-Aktualisierung](media/ata_ms_update.png) Damit ändern Sie die Windows-Einstellungen so, dass Updates für andere Microsoft-Produkte (einschließlich ATA) möglich sind, wie hier zu sehen. 
     ![Automatisches Windows-Update](media/ata_installupdatesautomatically.png)

    5.  Vor Beginn der Installation führt ATA eine Bereitschaftsprüfung aus. Schauen Sie sich die Ergebnisse der Überprüfung an, um sicherzustellen, dass die erforderlichen Komponenten erfolgreich konfiguriert sind und die Mindestmenge an Speicherplatz verfügbar ist. 
    ![ATA-Bereitschaftsprüfung](media/ata_install_readinesschecks.png)

    6.  Klicken Sie auf **Aktualisieren**. Nachdem Sie auf „Aktualisieren“ geklickt haben, ist ATA bis zum Abschluss der Aktualisierung offline.

1. Nach der Aktualisierung von ATA Center melden die ATA-Gateways, dass sie veraltet sind.

    ![Abbildung veralteter Gateways](media/ATA-center-outdated.png)

> [!IMPORTANT] 
> Aktualisieren Sie alle ATA-Gateways, damit ATA ordnungsgemäß funktioniert.

### <a name="step-2-download-the-ata-gateway-setup-package"></a>Schritt 2: Herunterladen des ATA-Gateway-Setuppakets
Nach dem Konfigurieren der Domänenverbindungseinstellungen können Sie das ATA-Gateway-Setuppaket herunterladen.

So laden Sie das ATA-Gateway-Paket herunter

1. Löschen Sie alle zuvor heruntergeladenen früheren Versionen des ATA-Gateway-Pakets.

1. Öffnen Sie auf dem ATA-Gatewaycomputer einen Browser, und geben Sie die IP-Adresse ein, die Sie in ATA Center für die ATA-Konsole konfiguriert haben. Wenn die ATA-Konsole geöffnet wird, klicken Sie auf das Symbol Einstellungen, und wählen Sie **Konfiguration**aus.

    ![Symbol für Konfigurationseinstellungen](media/ATA-config-icon.png)

1. Klicken Sie auf der Registerkarte **ATA-Gateways** auf ATA- **gatewaysetup herunterladen**.

1. Speichern Sie das Paket lokal.

Die ZIP-Datei enthält die folgenden Dateien:

- Installationsprogramm für ATA-Gateway

- Konfigurationseinstellungsdatei mit den erforderlichen Informationen für die Verbindung mit ATA Center

### <a name="step-3-update-the-ata-gateways"></a>Schritt 3: Aktualisieren der ATA-Gateways

1. Extrahieren Sie auf jedem ATA-Gateway die Dateien aus dem ATA-Gateway-Paket, und führen Sie die Datei **Microsoft ATA-Gateway-Setup.exe**aus.

    > [!NOTE] 
    > Sie können dieses ATA-Gateway-Paket auch verwenden, um neue ATA-Gateways zu installieren.

1. Die vorherigen Einstellungen werden beibehalten, es kann jedoch einige Minuten dauern, bis der Dienst neu gestartet wird.

1. Wiederholen Sie diesen Schritt für alle anderen bereitgestellten ATA-Gateways.

> [!NOTE] 
> Nach der erfolgreichen Aktualisierung eines ATA-Gateways wird die Benachrichtigung über die veraltete Version dieses Gateways ausgeblendet.

Alle ATA-Gateways wurden erfolgreich aktualisiert, wenn alle ATA-Gateways die erfolgreiche Synchronisierung melden und keine Meldungen über veraltete ATA-Gateways mehr angezeigt werden.

![Abbildung aktualisierter Gateways](media/ATA-gw-updated.png)


## <a name="see-also"></a>Weitere Informationen

- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
