---
title: "Installieren von ATA – Schritt 2 | Microsoft ATA"
description: "Im zweiten Schritt beim Installieren von ATA konfigurieren Sie die Domänenverbindungseinstellungen auf dem ATA Center-Server."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a5c7163bc7b1989672e587bfb4fa6a65cd4e3751
ms.openlocfilehash: 54f5652e980dd8b62d5bbfb642e56eaac7d6e343


---

# Installieren von ATA – Schritt 2

>[!div class="step-by-step"]
[« Schritt 1](install-ata-step1.md)
[Schritt 3 »](install-ata-step3.md)

## Schritt 2. Konfigurieren der allgemeinen ATA-Gatewayeinstellungen
Die Einstellungen auf der Registerkarte **Allgemein** gelten für alle über ATA Center verwalteten ATA-Gateways.

Gehen Sie folgendermaßen vor, um die allgemeinen ATA-Gatewayeinstellungen zu konfigurieren:

1.  Öffnen Sie die ATA-Konsole, und melden Sie sich an. Entsprechende Anweisungen finden Sie unter [Arbeiten mit der ATA-Konsole](working-with-ata-console.md).

2.  Klicken Sie auf das Symbol „Einstellungen“, und wählen Sie **Konfiguration** aus.

    ![Einstellungen für ATA-Gateway-Konfiguration](media/ATA-config-icon.JPG)

3.  Geben Sie auf der Registerkarte **Allgemein** unter **ATA-Gateways** die folgenden Informationen ein, und klicken Sie auf **Speichern**.

    |Feld|Kommentare|
    |---------|------------|
    |**Benutzername** (erforderlich)|Geben Sie den schreibgeschützten Benutzernamen ein, z. B. **user1**.|
    |**Kennwort** (erforderlich)|Geben Sie das Kennwort für den schreibgeschützten Benutzer ein, z. B. **Pencil1**. **Hinweis:** Stellen Sie sicher, dass Sie das richtige Kennwort eingeben. Wenn Sie das falsche Kennwort speichern, wird der ATA-Dienst auf den ATA-Gatewayservern nicht mehr ausgeführt.|
    |**Domäne** (erforderlich)|Geben Sie die Domäne für den schreibgeschützten Benutzer ein, z. B. **contoso.com**. **Hinweis:** Es ist wichtig, dass Sie den vollqualifizierten Domänennamen (FQDN) der Domäne eingeben, in der sich das Benutzerkonto befindet. Wenn sich das Konto des Benutzers beispielsweise in der Domäne „corp.contoso.com“ befindet, müssen Sie `corp.contoso.com` und nicht „contoso.com“ eingeben.|
    |Alle ATA-Gateways automatisch aktualisieren |Wenn Sie diese Einstellung aktivieren, werden bei künftigen Versionen während des Updates von ATA Center alle ATA-Gateways automatisch aktualisiert.|

    ![Abbildung ATA-Domänenverbindungseinstellungen](media/ata-domain-connectivity-user.jpg)



>[!div class="step-by-step"]
[« Schritt 1](install-ata-step1.md)
[Schritt 3 »](install-ata-step3.md)


## Siehe auch

- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Voraussetzungen für ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=Jul16_HO3-->


