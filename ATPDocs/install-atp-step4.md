---
title: Installieren von Azure Advanced Threat Protection | Microsoft-Dokumentation
description: Im vierten Schritt der Azure ATP-Installation erhalten Sie Hilfe zur Installation des Azure ATP-Sensors.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 1/27/2019
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 51911e39-76c7-4dcd-bc0b-ec6235d0403f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 5c357ea537c9fe9a23fc426670d47bf85d53f316
ms.sourcegitcommit: 19ff0ed88e450506b5725bbcbb0d0bd2f0c5e4bb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/27/2019
ms.locfileid: "55085247"
---
# <a name="install-azure-atp---step-4"></a>Installieren von Azure ATP – Schritt 4

> [!div class="step-by-step"]
> [« Schritt 3](install-atp-step3.md)
> [Schritt 5 »](install-atp-step5.md)

## <a name="install-the-azure-atp-sensor"></a>Installieren des Azure ATP-Sensors

> [!IMPORTANT]
>Stellen Sie sicher, dass Microsoft .NET Framework 4.7 auf dem Computer installiert ist. Wenn .NET Framework 4.7 nicht installiert ist, wird es vom Azure ATP-Sensorsetuppaket installiert. Dadurch ist möglicherweise ein Neustart des Servers erforderlich.

Führen Sie auf dem Domänencontroller folgende Schritte aus.

1. Stellen Sie sicher, dass der Computer mit den relevanten Azure ATP-Clouddienst-Endpunkten verbunden ist:
   - [https://triprd1wceuw1sensorapi.atp.azure.com](https://triprd1wceuw1sensorapi.atp.azure.com) 
   - [https://triprd1wceun1sensorapi.atp.azure.com](https://triprd1wceun1sensorapi.atp.azure.com)
   <br>(für Europa)  
   - [https://triprd1wcuse1sensorapi.atp.azure.com](https://triprd1wcuse1sensorapi.atp.azure.com)
   - [https://triprd1wcusw1sensorapi.atp.azure.com](https://triprd1wcusw1sensorapi.atp.azure.com)
   - [https://triprd1wcuswb1sensorapi.atp.azure.com](https://triprd1wcuswb1sensorapi.atp.azure.com)
   <br>(für die USA)
   - [https://triprd1wcasse1sensorapi.atp.azure.com](https://triprd1wcasse1sensorapi.atp.azure.com)<br>(für Asien)

2. Extrahieren Sie die Installationsdateien aus der ZIP-Datei. 
   > [!NOTE] 
   > Eine Installation direkt aus der ZIP-Datei verursacht einen Fehler.

3. Führen Sie **Azure ATP sensor setup.exe** aus, und befolgen Sie die Anweisungen des Setup-Assistenten.

4. Wählen Sie auf der Seite **Willkommen** Ihre Sprache aus, und klicken Sie auf **Weiter**.

    ![Sprache der Installation des eigenständigen Azure ATP-Sensors](media/sensor-install-language.png)


5. Der Installations-Assistent überprüft automatisch, ob der Server ein Domänencontroller oder ein dedizierter Server ist. Wenn es sich um einen Domänencontroller handelt, wird der Azure ATP-Sensor installiert. Wenn es sich um einen dedizierten Server handelt, wird der eigenständige Azure ATP-Sensor installiert. 
    
    Beispielsweise wird im Falle eines Azure ATP-Sensors die folgende Anzeige angezeigt, um Sie darüber zu informieren, dass ein Azure ATP-Sensor auf Ihrem dedizierten Server installiert wird:
    
    ![Installation des Azure ATP-Sensors](media/sensor-install-deployment-type.png)

   Klicken Sie auf **Weiter**.

    > [!NOTE] 
    > Wenn der Domänencontroller oder der dedizierte Server nicht den Mindestanforderungen der Hardware für die Installation entspricht, wird eine Warnung ausgegeben. Die Warnung verhindert nicht, dass Sie auf **Weiter** klicken und mit der Installation fortfahren können. Dies kann dennoch die richtige Option für die Installation von Azure ATP in einer kleinen Labtestumgebung sein, für die nicht viel Platz für die Datenspeicherung erforderlich ist. Für Produktionsumgebungen wird dringend empfohlen, mit dem Handbuch zur [Kapazitätsplanung](atp-capacity-planning.md) von Azure ATP zu arbeiten, um sicherzustellen, dass Ihre Domänencontroller oder dedizierten Server den nötigen Anforderungen entsprechen.

6. Geben Sie basierend auf Ihrer Umgebung unter **Configure the sensor** (Sensor konfigurieren) den Installationspfad und den Zugriffsschlüssel ein, die Sie im vorherigen Schritt kopiert haben:

    ![Bild der Azure ATP-Sensorkonfiguration](media/sensor-install-config.png)

      - Installationspfad: An diesem Speicherort wird der eigenständige Azure ATP-Sensor installiert. Bei der Standardeinstellung ist dies folgender Pfad: %programfiles%\Azure Advanced Threat Protection sensor. Behalten Sie den Standardwert bei.

     - Zugriffsschlüssel: Dieser wird vom Azure ATP-Portal im vorherigen Schritt abgerufen.
    
7. Klicken Sie auf **Installieren**. Bei der Installation des Azure ATP-Sensors werden die folgenden Komponenten installiert und konfiguriert:

    -   KB 3047154 (nur für Windows Server 2012 R2)

        > [!IMPORTANT]
        > -   Installieren Sie KB 3047154 nicht auf einem Virtualisierungshost (der Host, auf dem die Virtualisierung ausgeführt wird; die Ausführung auf einem virtuellen Computer ist möglich). Dies kann dazu führen, dass die Portspiegelung nicht mehr ordnungsgemäß ausgeführt wird. 
        > -   Wenn Wireshark auf Computer mit dem ATP-Sensor installiert ist, müssen Sie den ATP-Sensor neu starten, nachdem Sie Wireshark ausgeführt haben, da beide die gleichen Treiber verwenden.

    -   Azure ATP-Sensordienst und Azure ATP-Sensorupdatedienst
    -   Microsoft Visual C++ 2013 Redistributable

8. Klicken Sie nach Abschluss der Installation auf **Starten**, um den Browser zu öffnen und sich beim Azure ATP-Portal anzumelden.


> [!div class="step-by-step"]
> [« Schritt 3](install-atp-step3.md)
> [Schritt 5 »](install-atp-step5.md)


## <a name="see-also"></a>Weitere Informationen

- [Azure ATP sizing tool (Azure ATP-Tool zur Größenanpassung)](http://aka.ms/aatpsizingtool)

- [Konfigurieren der Ereignissammlung](configure-event-collection.md)

- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)

- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
