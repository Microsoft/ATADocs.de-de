---
title: "Notfallwiederherstellung für Advanced Threat Analytics | Microsoft-Dokumentation"
description: "Beschreibt, wie Sie die ATA-Funktionalität nach einem Notfall schnell wiederherstellen können"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 7620e171-76d5-4e3f-8b03-871678217a3a
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: ce06038a3c3f2e5a6f2a5d57ad814ab8393c0b0c
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/30/2017
---
*Gilt für: Advanced Threat Analytics Version 1.8*



# ATA-Notfallwiederherstellung
<a id="ata-disaster-recovery" class="xliff"></a>
Dieser Artikel beschreibt, wie Sie ATA Center und Ihre ATA-Funktionalität schnell wiederherstellen können, wenn die ATA Center-Funktionalität verloren gegangen ist, die ATA-Gateways jedoch noch funktionieren. 

>[!NOTE]
> Der beschriebene Prozess stellt keine zuvor erkannten verdächtigen Aktivitäten wieder her, sorgt jedoch dafür, dass ATA Center wieder voll funktionstüchtig ist. Darüber hinaus wird der erforderliche Lernzeitraum für einige Verhaltenserkennungen neu gestartet, jedoch sind die meisten Erkennungen, die ATA nach der Wiederherstellung von ATA Center zurückgibt, betriebsbereit. 

## Sichern Ihrer ATA Center-Konfiguration
<a id="back-up-your-ata-center-configuration" class="xliff"></a>

1. Die ATA Center-Konfiguration wird stündlich in einer Datei gesichert. Suchen Sie die neueste Sicherungskopie der ATA Center-Konfiguration, und speichern Sie sie auf einem separaten Computer. Eine ausführliche Erläuterung zum Auffinden dieser Dateien finden Sie unter [Exportieren und Importieren der ATA-Konfiguration](/advanced-threat-analytics/deploy-use/ata-configuration-file). 
2. Exportieren Sie das Zertifikats für ATA Center.
    1. Wechseln Sie im Zertifikat-Manager zu **Zertifikate (Lokaler Computer)** -> **Persönlich** ->**Zertifikate**, und wählen Sie **ATA Center** aus.
    2. Klicken Sie mit der rechten Maustaste auf **ATA Center**, wählen Sie **Alle Tasks** und dann **Exportieren** aus. 
     ![Zertifikat für ATA Center](media/ata-center-cert.png)
    3. Befolgen Sie die Anweisungen zum Exportieren des Zertifikats, und stellen Sie sicher, dass Sie auch den privaten Schlüssel exportieren.
    4. Sichern Sie die exportierte Zertifikatsdatei auf einem separaten Computer.

  > [!NOTE] 
  > Wenn der private Schlüssel nicht exportiert werden konnte, müssen Sie ein neues Zertifikat erstellen, es auf ATA bereitstellen, wie in [Ändern des Zertifikats für ATA Center](/advanced-threat-analytics/deploy-use/modifying-ata-config-centercert) beschrieben, und es dann exportieren. 

## Wiederherstellen von ATA Center
<a id="recover-your-ata-center" class="xliff"></a>

1. Erstellen Sie einen neuen Windows Server-Computer mit der gleichen IP-Adresse und dem gleichen Computernamen wie beim vorherigen ATA Center-Computer.
4. Importieren Sie das Zertifikat, das Sie in den oben genannten Vorgängen auf dem neuen Server gesichert haben.
5. Befolgen Sie die Anweisungen unter [Deploy the ATA Center (Bereitstellen von ATA Center)](/advanced-threat-analytics/deploy-use/install-ata-step1) auf dem neu erstellten Windows Server-Computer. Die ATA-Gateways müssen nicht noch einmal bereitgestellt werden. Erhalten Sie eine Aufforderung zur Angabe eines Zertifikats, dann stellen Sie das Zertifikat bereit, das Sie bei der Sicherung der ATA Center-Konfiguration exportiert haben. 
![Wiederherstellung von ATA Center](media/disaster-recovery-deploymentss.png)
6. Importieren Sie die gesicherte ATA Center-Konfiguration:
    1. Entfernen Sie das Systemprofildokument von ATA Center aus MongoDB: 
        1. Gehen Sie unter **C:\Programme\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**. 
        2. Ausführen von `mongo.exe` 
        3. Führen Sie zum Entfernen des Standardsystemprofils diesen Befehl aus: `db.SystemProfile.remove({})`
    2. Führen Sie den folgenden Befehl `mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert` mithilfe der Sicherungsdatei aus Schritt 1 aus.</br>
    Eine ausführliche Erläuterung zum Auffinden und Importieren von Sicherungsdateien finden Sie unter [Exportieren und Importieren der ATA-Konfiguration](/advanced-threat-analytics/deploy-use/ata-configuration-file). 
    3. Öffnen Sie die ATA-Konsole. Sie sollten alle ATA-Gateways auf der Registerkarte „Konfiguration/Gateways“ verknüpft sehen. 
    5. Definieren Sie einen [**Verzeichnisdienstebenutzer**](/advanced-threat-analytics/deploy-use/install-ata-step2), und wählen Sie eine [**Domänencontrollersynchronisierung**](/advanced-threat-analytics/deploy-use/install-ata-step5) aus. 






## Siehe auch
<a id="see-also" class="xliff"></a>
- [Voraussetzungen für ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA-Kapazitätsplanung](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Konfigurieren der Ereignissammlung](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Konfigurieren der Windows-Ereignisweiterleitung](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
