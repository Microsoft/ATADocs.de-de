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
ms.openlocfilehash: 3f022f070bc924388bee2fb3a0dda250b59ce053
ms.sourcegitcommit: 5bf0c6a204b71126306a0c64108eaf9cb7fc042f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/18/2021
ms.locfileid: "101097506"
---
# <a name="install-ata---step-3"></a>Installieren von ATA – Schritt 3

[!INCLUDE [Banner for top of topics](includes/banner.md)]

> [!div class="step-by-step"]
> [« Schritt 2](install-ata-step2.md)
> [Schritt 4 »](install-ata-step4.md)

## <a name="step-3-download-the-ata-gateway-setup-package"></a>Schritt 3 Herunterladen des ATA-Gateway-Setuppakets

Nach dem Konfigurieren der Domänenverbindungseinstellungen können Sie das ATA-Gateway-Setuppaket herunterladen. Das ATA-Gateway kann auf einem dedizierten Server oder einem Domänencontroller installiert werden. Wenn Sie es auf einem Domänencontroller installieren, wird es als ATA-Lightweight-Gateway installiert. Weitere Informationen zum ATA-Lightweight-Gateway finden Sie unter [ATA-Architektur](ata-architecture.md). 

Klicken Sie in der Liste mit den Schritten am oberen Rand der Seite auf **gatewaysetup herunterladen** , um zur Seite **Gateways** zu wechseln.

![Einstellungen für ATA-Gateway-Konfiguration](media/ATA_1.7-welcome-download-gateway.PNG)

> [!NOTE] 
> Um den Konfigurationsbildschirm für das Gateway später zu erreichen, klicken Sie auf das **Servereinstellungs-Symbol** (in der oberen rechten Ecke), und wählen Sie **Konfiguration** aus. Klicken Sie anschließend unter **System** auf **Gateways**.  

1. Klicken Sie auf **Gatewaysetup**.
  ![ATA-Gatewaysetup herunterladen](media/download-gateway-setup.png)
1. Speichern Sie das Paket lokal.
1. Kopieren Sie das Paket auf den dedizierten Server oder Domänencontroller, auf dem das ATA-Gateway installiert werden soll. Alternativ können Sie die ATA-Konsole vom dedizierten Server oder vom Domänencontroller aus öffnen und diesen Schritt überspringen.

Die ZIP-Datei enthält die folgenden Dateien:

- Installationsprogramm für ATA-Gateway

- Konfigurationseinstellungsdatei mit den erforderlichen Informationen für die Verbindung mit ATA Center


> [!div class="step-by-step"]
> [« Schritt 2](install-ata-step2.md)
> [Schritt 4 »](install-ata-step4.md)


## <a name="related-videos"></a>Verwandte Videos
- [Übersicht über die ATA-Bereitstellung](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Auswählen des richtigen ATA-Gatewaytyps](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)

## <a name="see-also"></a>Siehe auch
- [Handbuch für die ATA POC-Bereitstellung](/samples/browse/?redirectedfrom=TechNet-Gallery)
- [Tool zur Bemessung von ATA-Gateways](https://aka.ms/atasizingtool)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [ATA-Voraussetzungen](ata-prerequisites.md)