---
title: "Installieren von ATA – Schritt 3 | Microsoft Advanced Threat Analytics"
description: Im dritten Schritt beim Installieren von ATA laden Sie das ATA-Gateway-Setuppaket herunter.
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 7fb024e6-297a-4ad9-b962-481bb75a0ba3
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: 0209d8352704fef6caf059d152d6bde6127d3d55


---

# Installieren von ATA – Schritt 3

>[!div class="step-by-step"]
[« Schritt 2](install-ata-step2.md)
[Schritt 4 »](install-ata-step4.md)

## Schritt 3: Herunterladen des ATA-Gateway-Setuppakets
Nach dem Konfigurieren der Domänenverbindungseinstellungen können Sie das ATA-Gateway-Setuppaket herunterladen. Das ATA-Gateway kann auf einem dedizierten Server oder einem Domänencontroller installiert werden. Wenn Sie es auf einem Domänencontroller installieren, wird es als ATA-Lightweight-Gateway installiert. Weitere Informationen zum ATA-Lightweight-Gateway finden Sie unter [ATA-Architektur](/advanced-threat-analytics/plan-design/ata-architecture). 

So laden Sie das ATA-Gateway-Paket herunter

1.  Klicken Sie in der ATA-Konsole auf das Symbol „Einstellungen“, und wählen Sie **Konfiguration** aus.

    ![Einstellungen für ATA-Gateway-Konfiguration](media/ATA-config-icon.JPG)

2.  Klicken Sie auf der Registerkarte **ATA-Gateways** auf **ATA-Gatewaysetup herunterladen**.

3.  Speichern Sie das Paket lokal.
4.  Kopieren Sie das Paket auf den dedizierten Server oder Domänencontroller, auf dem das ATA-Gateway installiert werden soll. Alternativ können Sie die ATA-Konsole vom dedizierten Server oder vom Domänencontroller aus öffnen und diesen Schritt überspringen.

Die ZIP-Datei enthält Folgendes:

-   Installationsprogramm für ATA-Gateway

-   Konfigurationseinstellungsdatei mit den erforderlichen Informationen für die Verbindung mit ATA Center


>[!div class="step-by-step"]
[« Schritt 2](install-ata-step2.md)
[Schritt 4 »](install-ata-step4.md)

## Siehe auch

- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Voraussetzungen für ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=Jun16_HO4-->


