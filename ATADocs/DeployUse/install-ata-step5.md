---
# required metadata

title: Installieren von ATA – Schritt 5 | Microsoft Advanced Threat Analytics
description: Im fünften Schritt beim Installieren von ATA konfigurieren Sie die Einstellungen für das ATA-Gateway.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 2a5b6652-2aef-464c-ac17-c7e5f12f920f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Installieren von ATA – Schritt 5

>[!div class="step-by-step"]
[« Schritt 4](install-ata-step4.md)
[Schritt 6 »](install-ata-step6.md)


## Schritt 5: Konfigurieren der Einstellungen des ATA-Gateways
Führen Sie nach der Installation des ATA-Gateways die folgenden Schritte aus, um die Einstellungen für das ATA-Gateway zu konfigurieren.

1.  Klicken Sie auf dem ATA-Gatewaycomputer in der ATA-Konsole auf die Seite **Konfiguration**, und wählen Sie die Seite **ATA-Gateways** aus.

2.  Geben Sie die folgenden Informationen ein.



  - **Beschreibung**: <br>Geben Sie eine Beschreibung des ATA-Gateways ein (optional).
  - **Domänencontroller** (erforderlich): <br>Weitere Informationen zur Liste der Controller finden Sie weiter unten.<br>Geben Sie den vollqualifizierten Domänennamen (FQDN) des Domänencontrollers ein, und klicken Sie auf das Pluszeichen, um ihn der Liste hinzuzufügen, z. B. **dc01.contoso.com**.<br /><br />![Abbildung Beispiel-FQDN](media/ATAGWDomainController.png)<br>Die Objekte im ersten Domänencontroller in der Liste werden über LDAP-Abfragen synchronisiert. Je nach Größe der Domäne kann dies einige Zeit dauern.<br>
  **Hinweis:** <br>Stellen Sie sicher, dass der erste Domänencontroller **nicht** schreibgeschützt ist. Schreibgeschützte Domänencontroller sollten erst nach Abschluss der Erstsynchronisierung hinzugefügt werden.<br>


 - **Netzwerkadapter für Erfassung** (erforderlich):<br>Wählen Sie die Netzwerkadapter aus, die mit dem Switch verbunden und als Zielspiegelport zum Empfangen des Datenverkehrs vom Domänencontroller konfiguriert sind.|Wählen Sie den Netzwerkadapter für die Erfassung aus.
    ![Abbildung – Konfigurieren der Gatewayeinstellungen](media/ATA-Config-GW-Settings.jpg)

3.  Klicken Sie auf **Speichern**.

    > [!NOTE]
    > Es dauert einige Minuten, bis der ATA-Gatewaydienst das erste Mal gestartet wird, da der Cache der vom ATA-Gateway verwendeten Parser zur Netzwerkerfassung erstellt wird.

Die folgenden Informationen gelten für die Server, die Sie in der Liste **Domänencontroller** eingeben.

-   Der erste Domänencontroller in der Liste wird vom ATA-Gateway zum Synchronisieren der Objekte in der Domäne über LDAP-Abfragen verwendet. Je nach Größe der Domäne kann dies einige Zeit dauern.

-   Alle Domänencontroller, deren Datenverkehr vom ATA-Gateway mittels Portspiegelung überwacht wird, müssen in der Liste **Domänencontroller** aufgeführt sein. Wenn ein Domänencontroller nicht in der Liste **Domänencontroller** aufgeführt ist, werden verdächtige Aktivitäten möglicherweise nicht wie erwartet erkannt.

-   Stellen Sie sicher, dass der erste Domänencontroller **kein** schreibgeschützter Domänencontroller (RODC) ist.

    Schreibgeschützte Domänencontroller sollten erst nach Abschluss der Erstsynchronisierung hinzugefügt werden.

-   Mindestens ein Domänencontroller in der Liste sollte ein globaler Katalogserver sein. Dadurch kann ATA Computer- und Benutzerobjekte in anderen Domänen in der Gesamtstruktur auflösen.

Die Konfigurationsänderungen werden bei der nächsten geplanten Synchronisierung zwischen dem ATA-Gateway und ATA Center auf den ATA-Gateway angewendet.

### Überprüfen der Installation:
Gehen Sie wie folgt vor, um zu überprüfen, ob das ATA-Gateway erfolgreich bereitgestellt wurde:

1.  Überprüfen Sie, ob der Microsoft Advanced Threat Analytics-Gatewaydienst ausgeführt wird. Es kann einige Minuten dauern, bis der Dienst nach dem Speichern der ATA-Gatewayeinstellungen gestartet wird.

2.  Wenn der Dienst nicht gestartet wird, überprüfen Sie die Datei „Microsoft.Tri.Gateway-Errors.log“ im Standardordner „%programfiles%\Microsoft Advanced Threat Analytics\Gateway\Logs“, und suchen Sie nach Einträgen, die „transfer“ oder „service start“ enthalten.

3.  Überprüfen Sie die folgenden Leistungsindikatoren für das Microsoft ATA-Gateway:

    -   **NetworkListener Captured Messages/Sec:** Dieser Leistungsindikator gibt an, wie viele Nachrichten vom ATA-Gateway pro Sekunde erfasst werden. Der Wert sollte abhängig von der Anzahl der überwachten Domänencontroller und der Auslastung der einzelnen Domänencontroller im mittleren dreistelligen bis vierstelligen Bereich liegen. Ein- oder zweistellige Werte können auf ein Problem bei der Konfiguration der Portspiegelung hindeuten.

    -   **EntityTransfer Activity Transfers/Sec:** Dieser Wert sollte im Bereich einiger Hunderte alle paar Sekunden liegen.

4.  Wenn es sich um die Installation des ersten ATA-Gateways handelt, melden Sie sich nach einigen Minuten in der ATA-Konsole an, und öffnen Sie den Benachrichtigungsbereich, indem Sie von der rechten Seite des Bildschirms wischen. Daraufhin sollte eine Liste der **kürzlich gelernten Entitäten** auf der Benachrichtigungsleiste rechts in der Konsole angezeigt werden.

5.  So überprüfen Sie, ob die Installation erfolgreich durchgeführt wurde

    Suchen Sie in der Konsole auf der Suchleiste nach einem bestimmten Objekt, z. B. einem Benutzer oder einer Gruppe in Ihrer Domäne.

    Öffnen Sie den Systemmonitor. Klicken Sie in der Struktur „Leistung“ auf **Systemmonitor** und dann auf das Plussymbol, um **einen Leistungsindikator hinzuzufügen**. Erweitern Sie **Microsoft ATA Gateway**, scrollen Sie nach unten zu **NetworkListener Captured Messages/Sec**, und fügen Sie diesen Leistungsindikator hinzu. Vergewissern Sie sich dann, ob im Diagramm Aktivitäten angezeigt werden.

    ![Abbildung – Hinzufügen von Leistungsindikatoren](media/ATA-performance-monitoring-add-counters.png)


>[!div class="step-by-step"]
[« Schritt 4](install-ata-step4.md)
[Schritt 6 »](install-ata-step6.md)

## Siehe auch

- [Unterstützung finden Sie in unserem Forum.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Konfigurieren der Ereignissammlung](/advanced-threat-analytics/plandesign/configure-event-collection)
- [Voraussetzungen für ATA](/advanced-threat-analytics/plandesign/ata-prerequisites)


<!--HONumber=Apr16_HO2-->


