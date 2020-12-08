---
title: 'Schnellstart: Herunterladen des Microsoft Defender for Identity-Sensorsetuppakets'
description: Im dritten Schritt der Installation von Microsoft Defender for Identity laden Sie das Defender for Identity-Sensorsetuppaket herunter.
ms.date: 10/26/2020
ms.topic: quickstart
ms.openlocfilehash: f0eb884a7367ae50e076e0298f720a94def7da8c
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/03/2020
ms.locfileid: "96543126"
---
# <a name="quickstart-download-the-product-long-sensor-setup-package"></a>Schnellstart: Herunterladen des [!INCLUDE [Product long](includes/product-long.md)]-Sensorsetuppakets

In diesem Schnellstart laden Sie das Setuppaket für den [!INCLUDE [Product long](includes/product-long.md)]-Sensor aus dem Portal herunter.

## <a name="prerequisites"></a>Voraussetzungen

- Eine [[!INCLUDE [Product short](includes/product-short.md)]-Instanz](install-step1.md), die [mit Active Directory verbunden](install-step2.md) ist

## <a name="download-the-setup-package"></a>Herunterladen des Setuppakets

Nach dem Konfigurieren der Verbindungseinstellungen der Domäne können Sie das Setuppaket für den [!INCLUDE [Product short](includes/product-short.md)]-Sensor herunterladen. Weitere Informationen über den [!INCLUDE [Product short](includes/product-short.md)]-Sensor finden Sie unter [[!INCLUDE [Product short](includes/product-short.md)]-Architektur](architecture.md).

Klicken Sie in der Liste mit den Schritten am Anfang der Seite auf **Download**, um zur Seite **Sensor** zu gelangen.

![Symbol für die [!INCLUDE [Product short](includes/product-short.md)]-Sensorkonfigurationseinstellungen](media/sensor-config.png)

Sie können den Sensorkonfigurationsbildschirm später aufrufen, indem Sie auf **Konfiguration** und dann unter **System** auf **Sensoren** klicken.  

1. Klicken Sie auf **Download**, um das Paket lokal zu speichern.
1. Kopieren Sie den Zugriffsschlüssel. Der [!INCLUDE [Product short](includes/product-short.md)]-Sensor benötigt den Zugriffsschlüssel, um eine Verbindung mit Ihrer [!INCLUDE [Product short](includes/product-short.md)]-Instanz herzustellen. Der Zugriffsschlüssel ist ein Einmalkennwort für die Sensorbereitstellung. Danach wird die gesamte Kommunikation mittels Zertifikaten für die Authentifizierung und TLS-Verschlüsselung ausgeführt. Klicken Sie auf die Schaltfläche **Erneut generieren**, wenn Sie den neuen Zugriffsschlüssel erneut generieren müssen. Dieser Vorgang wirkt sich nicht auf zuvor bereitgestellte Sensoren aus, da der Zugriffsschlüssel nur für die erste Registrierung des Sensors verwendet wird.
1. Kopieren Sie das Paket auf den dedizierten Server oder Domänencontroller, auf dem der [!INCLUDE [Product short](includes/product-short.md)]-Sensor installiert werden soll. Alternativ können Sie das [!INCLUDE [Product short](includes/product-short.md)]-Portal vom dedizierten Server oder vom Domänencontroller aus öffnen und diesen Schritt überspringen.

Die ZIP-Datei enthält die folgenden Dateien:

- Das Installationsprogramm für den [!INCLUDE [Product short](includes/product-short.md)]-Sensor

- Die Konfigurationseinstellungsdatei mit den erforderlichen Informationen für die Verbindung mit dem [!INCLUDE [Product short](includes/product-short.md)]-Clouddienst

## <a name="next-steps"></a>Nächste Schritte

> [!div class="step-by-step"]
> [« Schritt 2: Herstellen einer Verbindung mit Active Directory](install-step2.md)
> [Schritt 4: Installieren des [!INCLUDE [Product short](includes/product-short.md)]-Sensors »](install-step4.md)

## <a name="join-the-community"></a>Beitritt zur Community

Haben Sie weitere Fragen, oder möchten Sie mit anderen über [!INCLUDE [Product short](includes/product-short.md)] und damit verbundene Sicherheitsaspekte diskutieren? Treten Sie noch heute der [[!INCLUDE [Product short](includes/product-short.md)]Community](https://aka.ms/MDIcommunity) bei.
