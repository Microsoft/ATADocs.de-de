---
title: Schnellstart zum Herunterladen des Setuppakets für den Azure ATP-Sensor | Microsoft-Dokumentation
description: Im dritten Schritt der Azure ATP-Installation erhalten Sie Hilfe zum Download des Setuppakets für den Azure ATP-Sensor.
keywords: ''
author: mlottner
ms.author: mlottner
ms.date: 02/05/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 95bb4ec1-841f-41b7-92fe-fbd144085724
ms.openlocfilehash: 538053c1033c1e6fc04fd80a6d6a009a6fe5347f
ms.sourcegitcommit: 38b68d96fbf04fe40e1f9a62a1af3d1d00e63614
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/02/2019
ms.locfileid: "58808154"
---
# <a name="quickstart-download-the-azure-atp-sensor-setup-package"></a>Schnellstart: Herunterladen des Setuppakets für den Azure ATP-Sensor

In diesem Schnellstart laden Sie das Setuppaket für den Azure ATP-Sensor aus dem Portal herunter.

## <a name="prerequisites"></a>Voraussetzungen

- Eine [Azure ATP](install-atp-step1.md)-Instanz, die mit [Active Directory verbunden ist](install-atp-step2.md).

## <a name="download-the-setup-package"></a>Herunterladen des Setuppakets

Nach dem Konfigurieren der Verbindungseinstellungen der Domäne können Sie das Setuppaket für den Azure ATP-Sensor herunterladen. Das Setuppaket für den Azure ATP-Sensor kann auf einem dedizierten Server oder einem Domänencontroller installiert werden. Wenn Sie die Installation direkt auf einem Domänencontroller durchführen, erfolgt die Installation als Azure ATP-Sensor. Wenn Sie sie auf einem dedizierten Server durchführen und die Portspiegelung verwenden, wird ein eigenständiger Azure ATP-Sensor installiert. Weitere Informationen zum Azure ATP-Sensor finden Sie unter [Azure ATP-Architektur](atp-architecture.md). 

Klicken Sie in der Liste mit den Schritten am Anfang der Seite auf **Download**, um zur Seite **Sensor** zu gelangen.

![Azure ATP-Sensorkonfigurationseinstellungen](media/atp-sensor-config.png)

 Sie können den Sensorkonfigurationsbildschirm später aufrufen, indem Sie auf das **Symbol für Einstellungen** klicken (in der oberen rechten Ecke) und **Konfiguration** auswählen. Klicken Sie anschließend unter **System** auf **Sensor**.  

1. Klicken Sie auf **Sensor**.
2. Speichern Sie das Paket lokal.
3. Kopieren Sie den **Zugriffs** **schlüssel**. Der Azure ATP-Sensor benötigt den Zugriffsschlüssel, um eine Verbindung mit Ihrer Azure ATP-Instanz herzustellen. Der Zugriffsschlüssel ist ein Einmalkennwort für die Sensorbereitstellung. Danach wird die gesamte Kommunikation mittels Zertifikaten für die Authentifizierung und TLS-Verschlüsselung ausgeführt. Klicken Sie auf die Schaltfläche **Erneut generieren**, wenn Sie den neuen Zugriffsschlüssel erneut generieren müssen. Dieser Vorgang wirkt sich nicht auf zuvor bereitgestellte Sensoren aus, da der Zugriffsschlüssel nur für die erste Registrierung des Sensors verwendet wird.
4. Kopieren Sie das Paket auf den dedizierten Server oder Domänencontroller, auf dem der Azure ATP-Sensor installiert werden soll. Alternativ können Sie das Azure ATP-Portal vom dedizierten Server oder vom Domänencontroller aus öffnen und diesen Schritt überspringen.

Die ZIP-Datei enthält die folgenden Dateien:

- Installieren des Azure ATP-Sensors

- Konfigurationseinstellungsdatei mit den erforderlichen Informationen für die Verbindung mit dem Azure ATP-Clouddienst

## <a name="next-steps"></a>Nächste Schritte

> [!div class="step-by-step"]
> [« Installieren von Azure ATP: Schritt 2](install-atp-step2.md)
> [Installieren von Azure ATP – Schritt 4 »](install-atp-step4.md)

## <a name="join-the-community"></a>Beitritt zur Community

Haben Sie weitere Fragen, oder möchten Sie mit anderen über Azure ATP und damit verbundene Sicherheitsaspekte diskutieren? Treten Sie noch heute der [Azure ATP-Community](https://aka.ms/azureatpcommunity) bei!
