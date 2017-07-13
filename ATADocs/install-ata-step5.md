---
title: "Installieren von Advanced Threat Analytics – Schritt 5 | Microsoft-Dokumentation"
description: "Im fünften Schritt beim Installieren von ATA konfigurieren Sie die Einstellungen für das ATA-Gateway."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 06/12/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 2a5b6652-2aef-464c-ac17-c7e5f12f920f
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 6952a239eb5f11cdfefc9ce201f9a765e61de8e8
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/30/2017
---
*Gilt für: Advanced Threat Analytics Version 1.8*



# Installieren von ATA – Schritt 5
<a id="install-ata---step-5" class="xliff"></a>

>[!div class="step-by-step"]
[« Schritt 4](install-ata-step4.md)
[Schritt 6 »](install-ata-step6.md)


## Schritt 5: Konfigurieren der Einstellungen des ATA-Gateways
<a id="step-5-configure-the-ata-gateway-settings" class="xliff"></a>
Führen Sie nach der Installation des ATA-Gateways die folgenden Schritte aus, um die Einstellungen für das ATA-Gateway zu konfigurieren.

1.  Gehen Sie in der ATA-Konsole zu **Konfiguration**, und wählen Sie unter **System** **Gateways** aus.
   
     ![Abbildung – Konfigurieren der Gatewayeinstellungen](media/ata-gw-config-1.png)


2.  Klicken Sie auf das Gateway, das Sie konfigurieren möchten, und geben Sie die folgenden Informationen ein:

    ![Abbildung – Konfigurieren der Gatewayeinstellungen](media/ATA-Gateways-config-2.png)

  - **Beschreibung:**: Geben Sie eine Beschreibung für das ATA-Gateway ein (optional).
  - **Domänencontroller mit Portspiegelung (FQDN)** (benötigt für das ATA-Gateway; kann nicht für das ATA-Lightweight-Gateway geändert werden): Geben Sie den vollqualifizierten Domänennamen (FQDN) Ihres Domänencontrollers ein, und klicken Sie auf das Pluszeichen, um ihn der Liste hinzuzufügen. z. B. **dc01.contoso.com**.

      Die folgenden Informationen gelten für die Server, die Sie in der Liste **Domänencontroller** eingeben.
      - Alle Domänencontroller, deren Datenverkehr vom ATA-Gateway mittels Portspiegelung überwacht wird, müssen in der Liste **Domänencontroller** aufgeführt sein. Wenn ein Domänencontroller nicht in der Liste **Domänencontroller** aufgeführt ist, werden verdächtige Aktivitäten möglicherweise nicht wie erwartet erkannt.
      - Mindestens ein Domänencontroller in der Liste sollte ein globaler Katalog sein. Dadurch kann ATA Computer- und Benutzerobjekte in anderen Domänen in der Gesamtstruktur auflösen.

  - **Netzwerkadapter für Erfassung** (erforderlich):
  - Wählen Sie für ein ATA-Gateway auf einem dedizierten Server die Netzwerkadapter aus, als Zielspiegelport konfiguriert sind. Diese empfangen den Datenverkehr des gespiegelten Domänencontrollers.
  - Für ein ATA-Lightweight-Gateway sollten dies alle Netzwerkadapter sein, die für die Kommunikation mit anderen Computern in Ihrer Organisation verwendet werden.


  - **Kandidat für die Domänensynchronisierung**: Alle ATA-Gateways, die als Kandidat für die Domänensynchronisierung festgelegt sind, können die Synchronisierung zwischen ATA und Ihrer Active Directory-Domäne übernehmen. Je nach Größe der Domäne ist die erste Synchronisierung ressourcenintensiv und kann einige Zeit dauern. Standardmäßig sind nur ATA-Gateways Kandidaten als Kandidaten für die Domänensynchronisierung festgelegt.
   Es empfiehlt sich, alle ATA-Gateways auf Remotestandorten als Kandidaten für die Domänensynchronisierung zu deaktivieren.
   Wenn Ihr Domänencontroller schreibgeschützt ist, verwenden Sie ihn nicht als Kandidat für die Domänensynchronisierung. Weitere Informationen finden Sie unter [ATA-Architektur](ata-architecture.md#ata-lightweight-gateway-features).

  > [!NOTE] 
  > Es dauert einige Minuten, bis der ATA-Gatewaydienst das erste Mal nach der Installation gestartet wird, da der Cache der Parser zur Netzwerkerfassung erstellt wird.
  > Die Konfigurationsänderungen werden bei der nächsten geplanten Synchronisierung zwischen dem ATA-Gateway und ATA Center auf den ATA-Gateway angewendet.

3. Optional können Sie den [Syslog-Listener und die Windows-Ereignisweiterleitungssammlung](configure-event-collection.md) festlegen. 
4. Aktivieren Sie **ATA-Gateway automatisch aktualisieren**, damit das ATA-Gateway bei künftigen Versionen während des Updates von ATA Center automatisch aktualisiert wird.

5. Klicken Sie auf **Speichern**.


## Überprüfen von Installationen
<a id="validate-installations" class="xliff"></a>
Gehen Sie wie folgt vor, um zu überprüfen, ob das ATA-Gateway erfolgreich bereitgestellt wurde:

1.  Überprüfen Sie, ob der Dienst **Microsoft Advanced Threat Analytics-Gateway** ausgeführt wird. Es kann einige Minuten dauern, bis der Dienst nach dem Speichern der ATA-Gatewayeinstellungen gestartet wird.

2.  Wenn der Dienst nicht gestartet wird, überprüfen Sie die Datei „Microsoft.Tri.Gateway-Errors.log“ im Standardordner „%programfiles%\Microsoft Advanced Threat Analytics\Gateway\Logs“. Hilfe finden Sie in der [ATA-Problembehandlung](troubleshooting-ata-known-errors.md).

3.  Wenn es sich um die Installation des ersten ATA-Gateways handelt, melden Sie sich nach einigen Minuten in der ATA-Konsole an, und öffnen Sie den Benachrichtigungsbereich, indem Sie von der rechten Seite des Bildschirms wischen. Daraufhin sollte eine Liste der **kürzlich gelernten Entitäten** auf der Benachrichtigungsleiste rechts in der Konsole angezeigt werden.

4.  Klicken Sie auf dem Desktop auf die Verknüpfung **Microsoft Advanced Threat Analytics**, um eine Verbindung mit der ATA-Konsole herzustellen. Melden Sie sich mit den gleichen Benutzeranmeldeinformationen an, die Sie auch zum Installieren von ATA Center verwendet haben.
5.  Suchen Sie in der Konsole auf der Suchleiste nach einem bestimmten Objekt, z. B. einem Benutzer oder einer Gruppe in Ihrer Domäne.
6.  Öffnen Sie den Systemmonitor. Klicken Sie in der Struktur „Leistung“ auf **Systemmonitor** und dann auf das Plussymbol, um **einen Leistungsindikator hinzuzufügen**. Erweitern Sie **Microsoft ATA Gateway**, scrollen Sie nach unten zu **Network Listener PEF Captured Messages/Sec**, und fügen Sie diesen Leistungsindikator hinzu. Vergewissern Sie sich dann, ob im Diagramm Aktivitäten angezeigt werden.

    ![Abbildung – Hinzufügen von Leistungsindikatoren](media/ATA-performance-monitoring-add-counters.png)


>[!div class="step-by-step"]
[« Schritt 4](install-ata-step4.md)
[Schritt 6 »](install-ata-step6.md)

## Weitere Informationen
<a id="see-also" class="xliff"></a>

- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Voraussetzungen für ATA](ata-prerequisites.md)

