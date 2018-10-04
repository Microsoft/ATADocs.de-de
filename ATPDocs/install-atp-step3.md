---
title: 'Installieren von Azure Advanced Threat Protection: Schritt 3 | Microsoft-Dokumentation'
description: Im dritten Schritt der Azure ATP-Installation erhalten Sie Hilfe zum Download des Setuppakets des eigenständigen Azure ATP-Sensors.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 95bb4ec1-841f-41b7-92fe-fbd144085724
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 96d459bd00d39bb21ce363d079b5b24ceca4ace7
ms.sourcegitcommit: b283bf66e63d76e6dba4564a229e804792794c6d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/29/2018
ms.locfileid: "47454019"
---
*Gilt für: Azure Advanced Threat Protection*



# <a name="install-azure-atp---step-3"></a>Installieren von Azure ATP: Schritt 3

> [!div class="step-by-step"]
> [« Schritt 2](install-atp-step2.md)
> [Schritt 4 »](install-atp-step4.md)

## <a name="step-3-download-the-azure-atp-sensor-setup-package"></a>Schritt 3: Herunterladen des Setuppakets für den Azure ATP-Sensor
Nach dem Konfigurieren der Verbindungseinstellungen der Domäne können Sie das Setuppaket für den Azure ATP-Sensor herunterladen. Das Setuppaket für den Azure ATP-Sensor kann auf einem dedizierten Server oder einem Domänencontroller installiert werden. Wenn Sie die Installation direkt auf einem Domänencontroller durchführen, erfolgt die Installation als Azure ATP-Sensor. Wenn Sie auf einem dedizierten Server installieren und Portspiegelung verwenden, wird ein eigenständiger Azure ATP-Sensor installiert. Weitere Informationen zum Azure ATP-Sensor finden Sie unter [Azure ATP-Architektur](atp-architecture.md). 

Klicken Sie in der Liste mit den Schritten am Anfang der Seite auf **Download**, um zur Seite **Sensor** zu gelangen.

![Azure ATP-Sensorkonfigurationseinstellungen](media/atp-sensor-config.png)

> [!NOTE] 
> Um den Sensorkonfigurationsbildschirm später zu erreichen, klicken Sie auf das **Symbol für Einstellungen** (in der oberen rechten Ecke), und wählen Sie **Konfiguration** aus. Klicken Sie anschließend unter **System** auf **Sensor**.  

1.  Klicken Sie auf **Sensor**.
2.  Speichern Sie das Paket lokal.
3.  Kopieren Sie den **Zugriffsschlüssel**. Der Azure ATP-Sensor benötigt den Zugriffsschlüssel, um eine Verbindung mit Ihrem Azure ATP-Arbeitsbereich herzustellen. Der Zugriffsschlüssel ist ein Einmalkennwort für die Sensorbereitstellung. Danach wird die gesamte Kommunikation mittels Zertifikaten für die Authentifizierung und TLS-Verschlüsselung ausgeführt. Klicken Sie auf die Schaltfläche **Erneut generieren**, wenn Sie den neuen Zugriffsschlüssel erneut generieren müssen. Dies ist möglich und wirkt sich nicht auf zuvor bereitgestellte Sensoren aus, da der Zugriffsschlüssel nur für die erste Registrierung des Sensors verwendet wird.
4.  Kopieren Sie das Paket auf den dedizierten Server oder Domänencontroller, auf dem der Azure ATP-Sensor installiert werden soll. Alternativ können Sie das Azure ATP-Arbeitsbereichsportal vom dedizierten Server oder vom Domänencontroller aus öffnen und diesen Schritt überspringen.

Die ZIP-Datei enthält die folgenden Dateien:

-   Installieren des Azure ATP-Sensors

-   Konfigurationseinstellungsdatei mit den erforderlichen Informationen für die Verbindung mit dem Azure ATP-Clouddienst


> [!div class="step-by-step"]
> [« Schritt 2](install-atp-step2.md)
> [Schritt 4 »](install-atp-step4.md)


## <a name="see-also"></a>Weitere Informationen

- [Azure ATP sizing tool (Azure ATP-Tool zur Größenanpassung)](http://aka.ms/aatpsizingtool)

- [Konfigurieren der Ereignissammlung](configure-event-collection.md)

- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)

- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)