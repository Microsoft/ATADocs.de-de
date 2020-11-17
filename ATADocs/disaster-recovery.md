---
title: Notfall Wiederherstellung für Advanced Threat Analytics
description: Beschreibt, wie Sie die ATA-Funktionalität nach einem Notfall schnell wiederherstellen können
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 05/02/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 7620e171-76d5-4e3f-8b03-871678217a3a
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 578e8ecdd598b404c570d41e71d487cf798cb602
ms.sourcegitcommit: e844155ea57f73dfe2b47f4c5c1c7f5292ccbf1e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2020
ms.locfileid: "94690787"
---
# <a name="ata-disaster-recovery"></a>ATA-Notfallwiederherstellung

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Dieser Artikel beschreibt, wie Sie ATA Center und Ihre ATA-Funktionalität schnell wiederherstellen können, wenn die ATA Center-Funktionalität verloren gegangen ist, die ATA-Gateways jedoch noch funktionieren. 

>[!NOTE]
> Der beschriebene Prozess stellt keine zuvor erkannten verdächtigen Aktivitäten wieder her, sorgt jedoch dafür, dass ATA Center wieder voll funktionstüchtig ist. Darüber hinaus wird der erforderliche Lernzeitraum für einige Verhaltenserkennungen neu gestartet, jedoch sind die meisten Erkennungen, die ATA nach der Wiederherstellung von ATA Center zurückgibt, betriebsbereit. 

## <a name="back-up-your-ata-center-configuration"></a>Sichern Ihrer ATA Center-Konfiguration

1. Die ATA Center-Konfiguration wird alle 4 Stunden in einer Datei gesichert. Suchen Sie die neueste Sicherungskopie der ATA Center-Konfiguration, und speichern Sie sie auf einem separaten Computer. Eine ausführliche Erläuterung zum Auffinden dieser Dateien finden Sie unter [Exportieren und Importieren der ATA-Konfiguration](ata-configuration-file.md). 
1. Exportieren Sie das Zertifikats für ATA Center.
    1. Navigieren Sie im Zertifikat-Manager zu **Zertifikate (lokaler Computer)**  ->  **persönliche**  -> **Zertifikate**, und wählen Sie **ATA Center** aus.
    2. Klicken Sie mit der rechten Maustaste auf **ATA Center**, wählen Sie **Alle Tasks** und dann **Exportieren** aus. 
     ![Zertifikat für ATA Center](media/ata-center-cert.png)
    3. Befolgen Sie die Anweisungen zum Exportieren des Zertifikats, und stellen Sie sicher, dass Sie auch den privaten Schlüssel exportieren.
    4. Sichern Sie die exportierte Zertifikatsdatei auf einem separaten Computer.

   > [!NOTE] 
   > Wenn der private Schlüssel nicht exportiert werden konnte, müssen Sie ein neues Zertifikat erstellen, es auf ATA bereitstellen, wie in [Ändern des Zertifikats für ATA Center](modifying-ata-center-configuration.md) beschrieben, und es dann exportieren. 

## <a name="recover-your-ata-center"></a>Wiederherstellen von ATA Center

1. Erstellen Sie einen neuen Windows Server-Computer mit der gleichen IP-Adresse und dem gleichen Computernamen wie beim vorherigen ATA Center-Computer.
1. Importieren Sie das zuvor gesicherte Zertifikat auf dem neuen Server.
1. Befolgen Sie die Anweisungen unter [Deploy the ATA Center (Bereitstellen von ATA Center)](install-ata-step1.md) auf dem neu erstellten Windows Server-Computer. Die ATA-Gateways müssen nicht noch einmal bereitgestellt werden. Erhalten Sie eine Aufforderung zur Angabe eines Zertifikats, dann stellen Sie das Zertifikat bereit, das Sie bei der Sicherung der ATA Center-Konfiguration exportiert haben. 
![Wiederherstellung von ATA Center](media/disaster-recovery-deploymentss.png)
1. Beenden Sie den ATA Center-Dienst.
1. Importieren Sie die gesicherte ATA Center-Konfiguration:
    1. Entfernen Sie das Systemprofildokument von ATA Center aus MongoDB: 
        1. Gehen Sie unter **C:\Programme\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**. 
        2. Ausführen von `mongo.exe ATA` 
        3. Führen Sie zum Entfernen des Standardsystemprofils diesen Befehl aus: `db.SystemProfile.remove({})`
        4. Verlassen Sie die Mongo-Shell, und kehren Sie zur Eingabeaufforderung zurück, indem Sie `exit` eingeben.
    2. Führen Sie den folgenden Befehl `mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert` mithilfe der Sicherungsdatei aus Schritt 1 aus.</br>
    Eine ausführliche Erläuterung zum Auffinden und Importieren von Sicherungsdateien finden Sie unter [Exportieren und Importieren der ATA-Konfiguration](ata-configuration-file.md). 
    3. Starten Sie den ATA Center-Dienst.
    4. Öffnen Sie die ATA-Konsole. Sie sollten alle ATA-Gateways auf der Registerkarte „Konfiguration/Gateways“ verknüpft sehen.
    5. Definieren Sie einen [**Verzeichnisdienstebenutzer**](install-ata-step2.md), und wählen Sie eine [**Domänencontrollersynchronisierung**](install-ata-step5.md) aus. 






## <a name="see-also"></a>Weitere Informationen
- [ATA-Voraussetzungen](ata-prerequisites.md)
- [ATA-Kapazitätsplanung](ata-capacity-planning.md)
- [Konfigurieren der Ereignissammlung](install-ata-step6.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-collection.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
