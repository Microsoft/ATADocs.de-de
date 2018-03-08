---
title: "Installieren von Azure Advanced Threat Protection – Schritt 4 | Microsoft-Dokumentation"
description: "Im vierten Schritt der Azure ATP-Installation erhalten Sie Hilfe zur Installation des eigenständigen Azure ATP-Sensors."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 51911e39-76c7-4dcd-bc0b-ec6235d0403f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7b003882f21f22b3427fb95534ca2bde255b14e6
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/21/2018
---
*Gilt für: Azure Advanced Threat Protection*



# <a name="install-azure-atp---step-4"></a>Installieren von Azure ATP – Schritt 4

>[!div class="step-by-step"]
[« Schritt 3](install-atp-step3.md)
[Schritt 5 »](install-atp-step5.md)

## <a name="step-4-install-the-azure-atp-sensor"></a>Schritt 4: Installieren des Azure ATP-Sensors

Überprüfen Sie vor der Installation des eigenständigen Azure ATP-Sensors auf einem dedizierten Server, ob die Portspiegelung ordnungsgemäß konfiguriert ist und ob der eigenständige Azure ATP-Sensor Datenverkehr zu und von den Domänencontrollern anzeigen kann. 


> [!IMPORTANT]
>Stellen Sie sicher, dass .NET Framework 4.7 auf dem Computer installiert ist. Wenn .NET Framework 4.7 nicht installiert ist, wird es vom Azure ATP-Sensorsetuppaket installiert, wodurch ein Neustart des Servers erforderlich ist. Stellen Sie sicher, dass der Computer mit dem Endpunkt des Azure ATP-Clouddiensts verbunden ist: https://triprd1wceuw1sensorapi.atp.azure.com (für Europa) oder https://triprd1wcuse1sensorapi.atp.azure.com (für die USA).

Führen Sie die folgenden Schritte auf dem Azure ATP-Sensorserver oder -Domänencontroller aus.

1.  Extrahieren Sie die Dateien aus der ZIP-Datei. 
> [!NOTE] 
> Eine Installation direkt aus der ZIP-Datei verursacht einen Fehler.

2.  Führen Sie **Azure ATP sensor setup.exe** aus, und befolgen Sie die Anweisungen des Setup-Assistenten.

3.  Wählen Sie auf der Seite **Willkommen** Ihre Sprache aus, und klicken Sie auf **Weiter**.

     ![Sprache der Installation des eigenständigen Azure ATP-Sensors](media/sensor-install-language.png)


4.  Der Installations-Assistent überprüft automatisch, ob der Server ein Domänencontroller oder ein dedizierter Server ist. Wenn es sich um einen Domänencontroller handelt, wird der Azure ATP-Sensor installiert. Wenn es sich um einen dedizierten Server handelt, wird der eigenständige Azure ATP-Sensor installiert. 
    
    Beispielsweise wird im Falle eines eigenständigen Azure ATP-Sensors der folgende Bildschirm angezeigt, um Sie darüber zu informieren, dass ein eigenständiger Azure ATP-Sensor auf Ihrem dedizierten Server installiert wird:
    
    ![Installation des eigenständigen Azure ATP-Sensors](media/sensor-install-deployment-type.png)

    Klicken Sie auf **Weiter**.

    > [!NOTE] 
    > Wenn der Domänencontroller oder der dedizierte Server nicht den Mindestanforderungen der Hardware für die Installation entspricht, erhalten Sie eine Warnung. Dies verhindert nicht, dass Sie auf **Weiter** klicken können und mit der Installation fortfahren können. Dies ist möglicherweise die richtige Option für die Installation von Azure ATP in einer Testumgebung für ein kleines Labor, in der Sie nicht so viel Platz für die Datenspeicherung benötigen. Für Produktionsumgebungen wird dringend empfohlen, mit dem Handbuch zur [Kapazitätsplanung](atp-capacity-planning.md) von Azure ATP zu arbeiten, um sicherzustellen, dass Ihre Domänencontroller oder dedizierten Server den nötigen Anforderungen entsprechen.

4.  Geben Sie basierend auf Ihrer Umgebung unter **Configure the sensor** (Sensor konfigurieren) den Installationspfad und den Zugriffsschlüssel ein, die Sie im vorherigen Schritt kopiert haben:

    ![Bild: Konfiguration des eigenständigen Azure ATP-Sensors](media/sensor-install-config.png)

      - Installationspfad: Dies ist der Speicherort, an dem der eigenständige Azure ATP-Sensor installiert wird. Bei der Standardeinstellung ist dies folgender Pfad: %programfiles%\Azure Advanced Threat Protection sensor. Behalten Sie den Standardwert bei.

      - Zugriffsschlüssel: Dieser wird vom Arbeitsbereichsportal im vorherigen Schritt abgerufen.
    
5. Klicken Sie auf **Installieren**. Bei der Installation des Azure ATP-Sensors werden die folgenden Komponenten installiert und konfiguriert:

    -   KB 3047154 (nur für Windows Server 2012 R2)

        > [!IMPORTANT]
        > -   Installieren Sie KB 3047154 nicht auf einem Virtualisierungshost (der Host, auf dem die Virtualisierung ausgeführt wird; die Ausführung auf einem virtuellen Computer ist möglich). Dies kann dazu führen, dass die Portspiegelung nicht mehr ordnungsgemäß ausgeführt wird. 
        > -   Wenn Wireshark auf Computer mit dem ATP-Sensor installiert ist, müssen Sie den ATP-Sensor neu starten, nachdem Sie Wireshark ausgeführt haben, da beide die gleichen Treiber verwenden.

    -   Azure ATP-Sensordienst und Azure ATP-Sensorupdatedienst
    -   Microsoft Visual C++ 2013 Redistributable

5.  Klicken Sie nach Abschluss der Installation auf **Starten**, um den Browser zu öffnen und sich beim Azure ATP-Arbeitsbereichsportal anzumelden.


>[!div class="step-by-step"]
[« Schritt 3](install-atp-step3.md)
[Schritt 5 »](install-atp-step5.md)


## <a name="see-also"></a>Weitere Informationen

- [Azure ATP sizing tool (Azure ATP-Tool zur Größenanpassung)](http://aka.ms/aatpsizingtool)

- [Konfigurieren der Ereignissammlung](configure-event-collection.md)

- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)

- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)