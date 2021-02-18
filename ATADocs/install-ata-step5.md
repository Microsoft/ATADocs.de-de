---
title: 'Installieren von Advanced Threat Analytics: Schritt 5'
description: Im fünften Schritt beim Installieren von ATA konfigurieren Sie die Einstellungen für das ATA-Gateway.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 2a5b6652-2aef-464c-ac17-c7e5f12f920f
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 6bcb99a86cfab977ec6a1ab590313a7878e9e4e2
ms.sourcegitcommit: 5bf0c6a204b71126306a0c64108eaf9cb7fc042f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/18/2021
ms.locfileid: "101097486"
---
# <a name="install-ata---step-5"></a>Installieren von ATA – Schritt 5

[!INCLUDE [Banner for top of topics](includes/banner.md)]

> [!div class="step-by-step"]
> [«Schritt 4](install-ata-step4.md) 
>  [Schritt 6»](install-ata-step6.md)

## <a name="step-5-configure-the-ata-gateway-settings"></a>Schritt 5. Konfigurieren der Einstellungen des ATA-Gateways

Führen Sie nach der Installation des ATA-Gateways die folgenden Schritte aus, um die Einstellungen für das ATA-Gateway zu konfigurieren.

1. Gehen Sie in der ATA-Konsole zu **Konfiguration**, und wählen Sie unter **System****Gateways** aus.

    ![Konfigurieren der Gatewayeinstellungen, Phase 1](media/ata-gw-config-1.png)

1. Klicken Sie auf das Gateway, das Sie konfigurieren möchten, und geben Sie die folgenden Informationen ein:

    ![Konfigurieren der Gatewayeinstellungen, Phase 2](media/ATA-Gateways-config-2.png)

    - **Beschreibung:**: Geben Sie eine Beschreibung für das ATA-Gateway ein (optional).
    - **Domänencontroller mit Portspiegelung (FQDN)** (benötigt für das ATA-Gateway; kann nicht für das ATA-Lightweight-Gateway geändert werden): Geben Sie den vollqualifizierten Domänennamen (FQDN) Ihres Domänencontrollers ein, und klicken Sie auf das Pluszeichen, um ihn der Liste hinzuzufügen. z. B. **dc01.contoso.com**.

    Die folgenden Informationen gelten für die Server, die Sie in der Liste **Domänencontroller** eingeben.

    - Alle Domänencontroller, deren Datenverkehr vom ATA-Gateway mittels Portspiegelung überwacht wird, müssen in der Liste **Domänencontroller** aufgeführt sein. Wenn ein Domänencontroller nicht in der Liste **Domänencontroller** aufgeführt ist, werden verdächtige Aktivitäten möglicherweise nicht wie erwartet erkannt.
    - Mindestens ein Domänencontroller in der Liste sollte ein globaler Katalog sein. Dadurch kann ATA Computer- und Benutzerobjekte in anderen Domänen in der Gesamtstruktur auflösen.

    - **Netzwerkadapter für Erfassung** (erforderlich):
    - Wählen Sie für ein ATA-Gateway auf einem dedizierten Server die Netzwerkadapter aus, als Zielspiegelport konfiguriert sind. Diese empfangen den Datenverkehr des gespiegelten Domänencontrollers.
    - Für ein ATA-Lightweight-Gateway sollten dies alle Netzwerkadapter sein, die für die Kommunikation mit anderen Computern in Ihrer Organisation verwendet werden.

    - **Kandidat für die Domänensynchronisierung**: Alle ATA-Gateways, die als Kandidat für die Domänensynchronisierung festgelegt sind, können die Synchronisierung zwischen ATA und Ihrer Active Directory-Domäne übernehmen. Je nach Größe der Domäne ist die erste Synchronisierung ressourcenintensiv und kann einige Zeit dauern. Standardmäßig sind nur ATA-Gateways Kandidaten als Kandidaten für die Domänensynchronisierung festgelegt.
    Es empfiehlt sich, alle ATA-Gateways an Remotestandorten als Kandidaten für die Domänensynchronisierung zu deaktivieren.
    Wenn Ihr Domänencontroller schreibgeschützt ist, verwenden Sie ihn nicht als Kandidat für die Domänensynchronisierung. Weitere Informationen finden Sie unter [ATA-Architektur](ata-architecture.md#ata-lightweight-gateway-features).

    > [!NOTE]
    > Es dauert einige Minuten, bis der ATA-Gatewaydienst das erste Mal nach der Installation gestartet wird, da der Cache der Parser zur Netzwerkerfassung erstellt wird.
    > Die Konfigurationsänderungen werden bei der nächsten geplanten Synchronisierung zwischen dem ATA-Gateway und ATA Center auf das ATA-Gateway angewendet.

1. Optional können Sie den [Syslog-Listener und die Windows-Ereignisweiterleitungssammlung](configure-event-collection.md) festlegen.
1. Aktivieren Sie **ATA-Gateway automatisch aktualisieren**, damit das ATA-Gateway bei künftigen Versionen während des Updates von ATA Center automatisch aktualisiert wird.

1. Klicken Sie auf **Speichern**.

## <a name="validate-installations"></a>Überprüfen von Installationen

Gehen Sie wie folgt vor, um zu überprüfen, ob das ATA-Gateway erfolgreich bereitgestellt wurde:

1. Überprüfen Sie, ob der Dienst **Microsoft Advanced Threat Analytics-Gateway** ausgeführt wird. Es kann einige Minuten dauern, bis der Dienst nach dem Speichern der ATA-Gatewayeinstellungen gestartet wird.

1. Wenn der Dienst nicht gestartet wird, überprüfen Sie die Datei "Microsoft. Tri. Gateway-Errors. log" im folgenden Standardordner "%ProgramFiles%\Microsoft Advanced Threat analytics\gateway\logs", und überprüfen Sie die [ATA-Problem](troubleshooting-ata-known-errors.md) Behandlung auf Hilfe.

1. Wenn es sich um die Installation des ersten ATA-Gateways handelt, melden Sie sich nach einigen Minuten in der ATA-Konsole an, und öffnen Sie den Benachrichtigungsbereich, indem Sie von der rechten Seite des Bildschirms wischen. Daraufhin sollte eine Liste der **kürzlich gelernten Entitäten** auf der Benachrichtigungsleiste rechts in der Konsole angezeigt werden.

1. Klicken Sie auf dem Desktop auf die **Microsoft Advanced Threat Analytics** Verknüpfung, um eine Verbindung mit der ATA-Konsole herzustellen. Melden Sie sich mit den gleichen Benutzeranmeldeinformationen an, die Sie auch zum Installieren von ATA Center verwendet haben.
1. Suchen Sie in der Konsole auf der Suchleiste nach einem bestimmten Objekt, z. B. einem Benutzer oder einer Gruppe in Ihrer Domäne.
1. Öffnen Sie den Systemmonitor. Klicken Sie in der Struktur „Leistung“ auf **Systemmonitor** und dann auf das Plussymbol, um **einen Leistungsindikator hinzuzufügen**. Erweitern Sie **Microsoft ATA Gateway**, scrollen Sie nach unten zu **Network Listener PEF Captured Messages/Sec**, und fügen Sie diesen Leistungsindikator hinzu. Vergewissern Sie sich dann, ob im Diagramm Aktivitäten angezeigt werden.

    ![Abbildung – Hinzufügen von Leistungsindikatoren](media/ATA-performance-monitoring-add-counters.png)

### <a name="set-anti-virus-exclusions"></a>Festlegen von Ausnahmen für die Antivirensoftware

Schließen Sie nach der Installation des ATA-Gateways das ATA-Verzeichnis von ihrer Antivirenanwendung ab. Der Standard Speicherort in der Datenbank ist: **c:\Programme\Microsoft Advanced Threat Analytics \**.

Stellen Sie außerdem sicher, dass Sie auch die folgenden Prozesse vom AV-Scan ausschließen:

**Prozesse**  
Microsoft.Tri.Gateway.exe  
Microsoft.Tri.Gateway.Updater.exe

Wenn Sie ATA in einem anderen Verzeichnis installiert haben, stellen Sie sicher, dass Sie die Ordnerpfade entsprechend Ihrer Installation ändern.

> [!div class="step-by-step"]
> [«Schritt 4](install-ata-step4.md) 
>  [Schritt 6»](install-ata-step6.md)

## <a name="related-videos"></a>Verwandte Videos

- [Übersicht über die ATA-Bereitstellung](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Auswählen des richtigen ATA-Gatewaytyps](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)

## <a name="see-also"></a>Siehe auch

- [Handbuch für die ATA POC-Bereitstellung](/samples/browse/?redirectedfrom=TechNet-Gallery)
- [Tool zur Bemessung von ATA-Gateways](https://aka.ms/atasizingtool)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [ATA-Voraussetzungen](ata-prerequisites.md)