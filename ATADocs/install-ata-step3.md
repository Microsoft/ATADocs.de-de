---
title: "Installieren von Advanced Threat Analytics – Schritt 3 | Microsoft-Dokumentation"
description: Im dritten Schritt beim Installieren von ATA laden Sie das ATA-Gateway-Setuppaket herunter.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 06/12/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 7fb024e6-297a-4ad9-b962-481bb75a0ba3
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 68c169ffd0f42bd8b030dc12f4711cbde2718a99
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/30/2017
---
*Gilt für: Advanced Threat Analytics Version 1.8*



# Installieren von ATA – Schritt 3
<a id="install-ata---step-3" class="xliff"></a>

>[!div class="step-by-step"]
[« Schritt 2](install-ata-step2.md)
[Schritt 4 »](install-ata-step4.md)

## Schritt 3: Herunterladen des ATA-Gateway-Setuppakets
<a id="step-3-download-the-ata-gateway-setup-package" class="xliff"></a>
Nach dem Konfigurieren der Domänenverbindungseinstellungen können Sie das ATA-Gateway-Setuppaket herunterladen. Das ATA-Gateway kann auf einem dedizierten Server oder einem Domänencontroller installiert werden. Wenn Sie es auf einem Domänencontroller installieren, wird es als ATA-Lightweight-Gateway installiert. Weitere Informationen zum ATA-Lightweight-Gateway finden Sie unter [ATA-Architektur](ata-architecture.md). 

Klicken Sie in der Liste mit den Schritten am Anfang der Seite auf „Gatewaysetup herunterladen“, um zu der Seite mit den Gateways zu gelangen:

![Einstellungen für ATA-Gateway-Konfiguration](media/ATA_1.7-welcome-download-gateway.PNG)

> [!NOTE] 
> Um den Konfigurationsbildschirm für das Gateway später zu erreichen, klicken Sie auf das **Servereinstellungs-Symbol** (in der oberen rechten Ecke), und wählen Sie **Konfiguration** aus. Klicken Sie anschließend unter **System** auf **Gateways**.  

1.  Klicken Sie auf **Gatewaysetup**.
  ![ATA-Gatewaysetup herunterladen](media/download-gateway-setup.png)
2.  Speichern Sie das Paket lokal.
3.  Kopieren Sie das Paket auf den dedizierten Server oder Domänencontroller, auf dem das ATA-Gateway installiert werden soll. Alternativ können Sie die ATA-Konsole vom dedizierten Server oder vom Domänencontroller aus öffnen und diesen Schritt überspringen.

Die ZIP-Datei enthält Folgendes:

-   Installationsprogramm für ATA-Gateway

-   Konfigurationseinstellungsdatei mit den erforderlichen Informationen für die Verbindung mit ATA Center


>[!div class="step-by-step"]
[« Schritt 2](install-ata-step2.md)
[Schritt 4 »](install-ata-step4.md)

## Weitere Informationen
<a id="see-also" class="xliff"></a>

- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Voraussetzungen für ATA](ata-prerequisites.md)
