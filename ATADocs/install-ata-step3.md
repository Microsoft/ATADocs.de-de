---
title: Installieren von Advanced Threat Analytics (Schritt 3)
description: Im dritten Schritt beim Installieren von ATA laden Sie das ATA-Gateway-Setuppaket herunter.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 7fb024e6-297a-4ad9-b962-481bb75a0ba3
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 2649e5ece9a1613c8c0f396c7fc906219c178046
ms.sourcegitcommit: fbb0768c392f9bccdd7e4adf0e9a0303c8d1922c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2020
ms.locfileid: "84775215"
---
# <a name="install-ata---step-3"></a>Installieren von ATA – Schritt 3

*Gilt für: Advanced Threat Analytics Version 1.9*

> [!div class="step-by-step"]
> [« Schritt 2](install-ata-step2.md)
> [Schritt 4 »](install-ata-step4.md)

## <a name="step-3-download-the-ata-gateway-setup-package"></a>Schritt 3: Herunterladen des ATA-Gateway-Setuppakets

Nach dem Konfigurieren der Domänenverbindungseinstellungen können Sie das ATA-Gateway-Setuppaket herunterladen. Das ATA-Gateway kann auf einem dedizierten Server oder einem Domänencontroller installiert werden. Wenn Sie es auf einem Domänencontroller installieren, wird es als ATA-Lightweight-Gateway installiert. Weitere Informationen zum ATA-Lightweight-Gateway finden Sie unter [ATA-Architektur](ata-architecture.md). 

Klicken Sie in der Liste mit den Schritten am oberen Rand der Seite auf **gatewaysetup herunterladen** , um zur Seite **Gateways** zu wechseln.

![Einstellungen für ATA-Gateway-Konfiguration](media/ATA_1.7-welcome-download-gateway.PNG)

> [!NOTE] 
> Um den Konfigurationsbildschirm für das Gateway später zu erreichen, klicken Sie auf das **Servereinstellungs-Symbol** (in der oberen rechten Ecke), und wählen Sie **Konfiguration** aus. Klicken Sie anschließend unter **System** auf **Gateways**.  

1.  Klicken Sie auf **Gatewaysetup**.
  ![ATA-Gatewaysetup herunterladen](media/download-gateway-setup.png)
2.  Speichern Sie das Paket lokal.
3.  Kopieren Sie das Paket auf den dedizierten Server oder Domänencontroller, auf dem das ATA-Gateway installiert werden soll. Alternativ können Sie die ATA-Konsole vom dedizierten Server oder vom Domänencontroller aus öffnen und diesen Schritt überspringen.

Die ZIP-Datei enthält die folgenden Dateien:

-   Installationsprogramm für ATA-Gateway

-   Konfigurationseinstellungsdatei mit den erforderlichen Informationen für die Verbindung mit ATA Center


> [!div class="step-by-step"]
> [« Schritt 2](install-ata-step2.md)
> [Schritt 4 »](install-ata-step4.md)


## <a name="related-videos"></a>Verwandte Videos
- [Übersicht über die ATA-Bereitstellung](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Auswählen des richtigen ATA-Gatewaytyps](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)

## <a name="see-also"></a>Weitere Informationen
- [Handbuch für die ATA POC-Bereitstellung](https://aka.ms/atapoc)
- [Tool zur Bemessung von ATA-Gateways](https://aka.ms/atasizingtool)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Voraussetzungen für ATA](ata-prerequisites.md)
