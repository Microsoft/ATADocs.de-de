---
title: 'Schnellstart: Herunterladen des Setuppakets für den Azure ATP-Sensor'
description: Im dritten Schritt der Azure ATP-Installation erhalten Sie Hilfe zum Download des Setuppakets für den Azure ATP-Sensor.
keywords: ''
author: shsagir
ms.author: shsagir
ms.date: 02/19/2020
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 95bb4ec1-841f-41b7-92fe-fbd144085724
ms.openlocfilehash: 08b561bb3021181ab9217c8ab6c4a44947af1e78
ms.sourcegitcommit: 0c356b0860ae8663254e0cf6f04001bcc91ce207
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/21/2020
ms.locfileid: "90826867"
---
# <a name="quickstart-download-the-azure-atp-sensor-setup-package"></a>Schnellstart: Herunterladen des Setuppakets für den Azure ATP-Sensor

In diesem Schnellstart laden Sie das Setuppaket für den Azure ATP-Sensor aus dem Portal herunter.

## <a name="prerequisites"></a>Voraussetzungen

- Eine [Azure ATP](install-step1.md)-Instanz, die mit [Active Directory verbunden ist](install-step2.md).

## <a name="download-the-setup-package"></a>Herunterladen des Setuppakets

Nach dem Konfigurieren der Verbindungseinstellungen der Domäne können Sie das Setuppaket für den Azure ATP-Sensor herunterladen. Weitere Informationen zum Azure ATP-Sensor finden Sie unter [Azure ATP-Architektur](architecture.md).

Klicken Sie in der Liste mit den Schritten am Anfang der Seite auf **Download**, um zur Seite **Sensor** zu gelangen.

![Azure ATP-Sensorkonfigurationseinstellungen](media/atp-sensor-config.png)

 Sie können den Sensorkonfigurationsbildschirm später aufrufen, indem Sie auf das **Symbol für Einstellungen** klicken (in der oberen rechten Ecke) und **Konfiguration** auswählen. Klicken Sie anschließend unter **System** auf **Sensor**.  

1. Klicken Sie auf **Sensor**.
1. Speichern Sie das Paket lokal.
1. Kopieren Sie den **** Zugriffsschlüssel****. Der Azure ATP-Sensor benötigt den Zugriffsschlüssel, um eine Verbindung mit Ihrer Azure ATP-Instanz herzustellen. Der Zugriffsschlüssel ist ein Einmalkennwort für die Sensorbereitstellung. Danach wird die gesamte Kommunikation mittels Zertifikaten für die Authentifizierung und TLS-Verschlüsselung ausgeführt. Klicken Sie auf die Schaltfläche **Erneut generieren**, wenn Sie den neuen Zugriffsschlüssel erneut generieren müssen. Dieser Vorgang wirkt sich nicht auf zuvor bereitgestellte Sensoren aus, da der Zugriffsschlüssel nur für die erste Registrierung des Sensors verwendet wird.
1. Kopieren Sie das Paket auf den dedizierten Server oder Domänencontroller, auf dem der Azure ATP-Sensor installiert werden soll. Alternativ können Sie das Azure ATP-Portal vom dedizierten Server oder vom Domänencontroller aus öffnen und diesen Schritt überspringen.

Die ZIP-Datei enthält die folgenden Dateien:

- Installieren des Azure ATP-Sensors

- Konfigurationseinstellungsdatei mit den erforderlichen Informationen für die Verbindung mit dem Azure ATP-Clouddienst

## <a name="next-steps"></a>Nächste Schritte

> [!div class="step-by-step"]
> [« Installieren von Azure ATP: Schritt 2](install-step2.md)
> [Installieren von Azure ATP – Schritt 4 »](install-step4.md)

## <a name="join-the-community"></a>Beitritt zur Community

Haben Sie weitere Fragen, oder möchten Sie mit anderen über Azure ATP und damit verbundene Sicherheitsaspekte diskutieren? Treten Sie noch heute der [Azure ATP-Community](https://aka.ms/azureatpcommunity) bei!
