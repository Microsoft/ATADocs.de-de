---
title: "Installieren von ATA – Schritt 5 | Microsoft ATA"
description: "Im fünften Schritt beim Installieren von ATA konfigurieren Sie die Einstellungen für das ATA-Gateway."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 2a5b6652-2aef-464c-ac17-c7e5f12f920f
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a5c7163bc7b1989672e587bfb4fa6a65cd4e3751
ms.openlocfilehash: 3e9f68e9868dc9aaf20fe9d1c4fe2b8bdd685291


---

# Installieren von ATA – Schritt 5

>[!div class="step-by-step"]
[« Schritt 4](install-ata-step4.md)
[Schritt 6 »](install-ata-step6.md)


## Schritt 5: Konfigurieren der Einstellungen des ATA-Gateways
Führen Sie nach der Installation des ATA-Gateways die folgenden Schritte aus, um die Einstellungen für das ATA-Gateway zu konfigurieren.

1.  Klicken Sie in der ATA-Konsole auf die Seite **Konfiguration**, und wählen Sie die Seite **ATA-Gateways** aus.

2.  Geben Sie die folgenden Informationen ein.

  - **Beschreibung**: <br>Geben Sie eine Beschreibung des ATA-Gateways ein (optional).
  - **Domänencontroller mit Portspiegelung (FQDN)** (erforderlich für das ATA-Gateway; kann für das ATA-Lightweight-Gateway nicht festgelegt werden): <br>Geben Sie den vollqualifizierten Domänennamen (FQDN) des Domänencontrollers ein, und klicken Sie auf das Pluszeichen, um ihn der Liste hinzuzufügen, z. B. **dc01.contoso.com**.<br /><br />![Abbildung eines Beispiel-FQDN](media/ATAGWDomainController.png)

Die folgenden Informationen gelten für die Server, die Sie in der Liste **Domänencontroller** eingeben: -   Alle Domänencontroller, deren Datenverkehr vom ATA-Gateway mittels Portspiegelung überwacht wird, müssen in der Liste **Domänencontroller** aufgeführt sein. Wenn ein Domänencontroller nicht in der Liste **Domänencontroller** aufgeführt ist, werden verdächtige Aktivitäten möglicherweise nicht wie erwartet erkannt.
-   Mindestens ein Domänencontroller in der Liste sollte ein globaler Katalogserver sein. Dadurch kann ATA Computer- und Benutzerobjekte in anderen Domänen in der Gesamtstruktur auflösen.

 - **Netzwerkadapter für Erfassung** (erforderlich):<br>
     - Wählen Sie für ein ATA-Gateway auf einem dedizierten Server die Netzwerkadapter aus, als Zielspiegelport konfiguriert sind. Diese empfangen den Datenverkehr des gespiegelten Domänencontrollers.
     - Für ein ATA-Lightweight-Gateway sollten dies alle Netzwerkadapter sein, die für die Kommunikation mit anderen Computern in Ihrer Organisation verwendet werden.

![Abbildung – Konfigurieren der Gatewayeinstellungen](media/ATA-Config-GW-Settings.jpg)

 - **Kandidat für die Domänensynchronisierung**<br>
Alle ATA-Gateways, die als Kandidat für die Domänensynchronisierung festgelegt sind, können die Synchronisierung zwischen ATA und Ihrer Active Directory-Domäne übernehmen. Je nach Größe der Domäne ist die erste Synchronisierung ressourcenintensiv und kann einige Zeit dauern. Standardmäßig werden nur ATA-Gateways als Kandidaten für die Domänensynchronisierung festgelegt. <br>Es empfiehlt sich, alle ATA-Gateways auf Remotestandorten als Kandidaten für die Domänensynchronisierung zu deaktivieren.<br>Wenn Ihr Domänencontroller schreibgeschützt ist, verwenden Sie ihn nicht als Kandidat für die Domänensynchronisierung. Weitere Informationen finden Sie unter [ATA-Architektur](/advanced-threat-analytics/plan-design/ata-architecture#ata-lightweight-gateway-features).

> [!NOTE] 
> Es dauert einige Minuten, bis der ATA-Gatewaydienst das erste Mal gestartet wird, da der Cache der Parser zur Netzwerkerfassung erstellt wird.<br>
> Die Konfigurationsänderungen werden bei der nächsten geplanten Synchronisierung zwischen dem ATA-Gateway und ATA Center auf den ATA-Gateway angewendet.



    

3. Optional können Sie den [Syslog-Listener und die Windows-Ereignisweiterleitungssammlung](configure-event-collection.md) festlegen. 
4. Aktivieren Sie **ATA-Gateway automatisch aktualisieren**, damit das ATA-Gateway bei künftigen Versionen während des Updates von ATA Center automatisch aktualisiert wird.
3.  Klicken Sie auf **Speichern**.


## Überprüfen von Installationen
Gehen Sie wie folgt vor, um zu überprüfen, ob das ATA-Gateway erfolgreich bereitgestellt wurde:

1.  Überprüfen Sie, ob der Dienst **Microsoft Advanced Threat Analytics-Gateway** ausgeführt wird. Es kann einige Minuten dauern, bis der Dienst nach dem Speichern der ATA-Gatewayeinstellungen gestartet wird.

2.  Wenn der Dienst nicht gestartet wird, überprüfen Sie die Datei „Microsoft.Tri.Gateway-Errors.log“ im Standardordner „%programfiles%\Microsoft Advanced Threat Analytics\Gateway\Logs“.

3.  Hilfe finden Sie in der [ATA-Problembehandlung](/advanced-threat-analytics/troubleshoot/troubleshooting-ata-known-errors).

4.  Wenn es sich um die Installation des ersten ATA-Gateways handelt, melden Sie sich nach einigen Minuten in der ATA-Konsole an, und öffnen Sie den Benachrichtigungsbereich, indem Sie von der rechten Seite des Bildschirms wischen. Daraufhin sollte eine Liste der **kürzlich gelernten Entitäten** auf der Benachrichtigungsleiste rechts in der Konsole angezeigt werden.

5.  Klicken Sie auf dem Desktop auf die Verknüpfung **Microsoft Advanced Threat Analytics**, um eine Verbindung mit der ATA-Konsole herzustellen. Melden Sie sich mit den gleichen Benutzeranmeldeinformationen an, die Sie auch zum Installieren von ATA Center verwendet haben.
6.  Suchen Sie in der Konsole auf der Suchleiste nach einem bestimmten Objekt, z. B. einem Benutzer oder einer Gruppe in Ihrer Domäne.
7.  Öffnen Sie den Systemmonitor. Klicken Sie in der Struktur „Leistung“ auf **Systemmonitor** und dann auf das Plussymbol, um **einen Leistungsindikator hinzuzufügen**. Erweitern Sie **Microsoft ATA Gateway**, scrollen Sie nach unten zu **Network Listener PEF Captured Messages/Sec**, und fügen Sie diesen Leistungsindikator hinzu. Vergewissern Sie sich dann, ob im Diagramm Aktivitäten angezeigt werden.

    ![Abbildung – Hinzufügen von Leistungsindikatoren](media/ATA-performance-monitoring-add-counters.png)


>[!div class="step-by-step"]
[« Schritt 4](install-ata-step4.md)
[Schritt 6 »](install-ata-step6.md)

## Siehe auch

- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Voraussetzungen für ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)




<!--HONumber=Jul16_HO3-->


