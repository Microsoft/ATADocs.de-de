---
title: "Installieren von ATA – Schritt 3 | Microsoft Docs"
description: Im dritten Schritt beim Installieren von ATA laden Sie das ATA-Gateway-Setuppaket herunter.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 7fb024e6-297a-4ad9-b962-481bb75a0ba3
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 85e285c5d88e5916e0bf0eb7dd327cb4cb45b4cb
ms.openlocfilehash: c8f3f5453757fbc7a95aa2377a84c3a133d38181


---

*Gilt für: Advanced Threat Analytics Version 1.7*



# <a name="install-ata---step-3"></a>Installieren von ATA – Schritt 3

>[!div class="step-by-step"]
[« Schritt 2](install-ata-step2.md)
[Schritt 4 »](install-ata-step4.md)

## <a name="step-3-download-the-ata-gateway-setup-package"></a>Schritt 3: Herunterladen des ATA-Gateway-Setuppakets
Nach dem Konfigurieren der Domänenverbindungseinstellungen können Sie das ATA-Gateway-Setuppaket herunterladen. Das ATA-Gateway kann auf einem dedizierten Server oder einem Domänencontroller installiert werden. Wenn Sie es auf einem Domänencontroller installieren, wird es als ATA-Lightweight-Gateway installiert. Weitere Informationen zum ATA-Lightweight-Gateway finden Sie unter [ATA-Architektur](/advanced-threat-analytics/plan-design/ata-architecture). 

Wenn Sie zum ersten Mal einen ATA-Gateway herunterladen, erscheint folgender Bildschirm:

![Einstellungen für ATA-Gateway-Konfiguration](media/ATA_1.7-welcome-download-gateway.PNG)

Wenn Sie nicht zum ersten Mal ein ATA-Gateway herunterladen, erscheint diese Willkommensnachricht nicht.

> [!NOTE] 
> Um den Konfigurationsbildschirm später zu erreichen, klicken Sie auf das **Servereinstellungs-Symbol** (in der oberen rechten Ecke), und wählen Sie **Konfiguration** aus. Klicken Sie anschließend unter **System** auf **Gateways**.  

1.  Klicken Sie auf **Gatewaysetup herunterladen**.
2.  Speichern Sie das Paket lokal.
3.  Kopieren Sie das Paket auf den dedizierten Server oder Domänencontroller, auf dem das ATA-Gateway installiert werden soll. Alternativ können Sie die ATA-Konsole vom dedizierten Server oder vom Domänencontroller aus öffnen und diesen Schritt überspringen.

Die ZIP-Datei enthält Folgendes:

-   Installationsprogramm für ATA-Gateway

-   Konfigurationseinstellungsdatei mit den erforderlichen Informationen für die Verbindung mit ATA Center


>[!div class="step-by-step"]
[« Schritt 2](install-ata-step2.md)
[Schritt 4 »](install-ata-step4.md)

## <a name="see-also"></a>Weitere Informationen

- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Voraussetzungen für ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=Jan17_HO1-->


