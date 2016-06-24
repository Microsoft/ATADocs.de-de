---
# required metadata

title: Installieren von ATA – Schritt 2 | Microsoft Advanced Threat Analytics
description: Im zweiten Schritt beim Installieren von ATA konfigurieren Sie die Domänenverbindungseinstellungen auf dem ATA Center-Server.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Installieren von ATA – Schritt 2

>[!div class="step-by-step"]
[« Schritt 1](install-ata-step1.md)
[Schritt 3 »](install-ata-step3.md)

## Schritt 2. Konfigurieren der ATA-Gateway-Domänenverbindungseinstellungen
Die Einstellungen im Bereich „Domänenverbindungseinstellungen“ gelten für alle über ATA Center verwalteten ATA-Gateways.

Führen Sie zum Konfigurieren der Domänenverbindungseinstellungen die folgenden Schritte auf dem ATA Center-Server aus.

1.  Öffnen Sie die ATA-Konsole, und melden Sie sich an. Entsprechende Anweisungen finden Sie unter [Arbeiten mit der ATA-Konsole](/advanced-threat-analytics/understand/working-with-ata-console).

2.  Bei Ihrer ersten Anmeldung in der ATA-Konsole nach dem Installieren von ATA Center werden Sie automatisch zur Konfigurationsseite für ATA-Gateways weitergeleitet. Wenn Sie die Einstellungen später ändern möchten, klicken Sie auf das Symbol „Einstellungen“, und wählen Sie **Konfiguration** aus.

    ![Einstellungen für ATA-Gateway-Konfiguration](media/ATA-config-icon.JPG)

3.  Klicken Sie auf der Seite **Gateways** auf **Domänenverbindungseinstellungen**, geben Sie die folgenden Informationen ein, und klicken Sie auf **Speichern**.

    |Feld|Kommentare|
    |---------|------------|
    |**Benutzername** (erforderlich)|Geben Sie den schreibgeschützten Benutzernamen ein, z. B. **user1**.|
    |**Kennwort** (erforderlich)|Geben Sie das Kennwort für den schreibgeschützten Benutzer ein, z. B. **Pencil1**. **Hinweis:** Stellen Sie sicher, dass Sie das richtige Kennwort eingeben. Wenn Sie das falsche Kennwort speichern, wird der ATA-Dienst auf den ATA-Gatewayservern nicht mehr ausgeführt.|
    |**Domäne** (erforderlich)|Geben Sie die Domäne für den schreibgeschützten Benutzer ein, z. B. **contoso.com**. **Hinweis:** Es ist wichtig, dass Sie den vollqualifizierten Domänennamen (FQDN) der Domäne eingeben, in der sich das Benutzerkonto befindet. Wenn sich das Konto des Benutzers beispielsweise in der Domäne „corp.contoso.com“ befindet, müssen Sie `corp.contoso.com` und nicht „contoso.com“ eingeben.|
    ![Abbildung ATA-Domänenverbindungseinstellungen](media/ATA-Domain-Connectivity-User.JPG)


>[!div class="step-by-step"]
[« Schritt 1](install-ata-step1.md)
[Schritt 3 »](install-ata-step3.md)


## Siehe auch

- [Unterstützung finden Sie in unserem Forum.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Konfigurieren der Ereignissammlung](/advanced-threat-analytics/plandesign/configure-event-collection)
- [Voraussetzungen für ATA](/advanced-threat-analytics/plandesign/ata-prerequisites)


<!--HONumber=Apr16_HO2-->


