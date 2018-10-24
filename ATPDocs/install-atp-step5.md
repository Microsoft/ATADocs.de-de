---
title: Installieren von Azure Advanced Threat Protection | Microsoft-Dokumentation
description: Im fünften Schritt der Installation von Azure ATP konfigurieren Sie Einstellungen für Ihren eigenständigen Azure ATP-Sensor.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: d7c95f8c-04f8-4946-9bae-c27ed362fcb0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6f65b3af56e683a385f7128a989170c8c4073b3e
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/04/2018
ms.locfileid: "48783864"
---
*Gilt für: Azure Advanced Threat Protection*



# <a name="install-azure-atp---step-5"></a>Installieren von Azure ATP: Schritt 5

> [!div class="step-by-step"]
> [« Schritt 4](install-atp-step4.md)



## <a name="step-5-configure-the-azure-atp-sensor-settings"></a>Schritt 5: Konfigurieren der Einstellungen des Azure ATP-Sensors
Führen Sie die folgenden Schritte nach der Installation des Azure ATP-Sensors aus, um die Azure ATP-Sensor-Einstellungen zu konfigurieren.

1.  Gehen Sie im Azure ATP-Portal auf **Konfiguration**, und klicken Sie unter **System** auf **Sensor**.
   
     ![Abbildung der Konfiguration der Sensoreinstellungen](media/atp-sensor-config.png)


2.  Klicken Sie auf den Sensor, den Sie konfigurieren möchten, und geben Sie die folgenden Informationen ein:

    ![Abbildung der Konfiguration der Sensoreinstellungen](media/atp-sensor-config-2.png)

  - **Beschreibung:**: Geben Sie eine Beschreibung für den Azure ATP-Sensor ein (optional).
  - **Domänencontroller (FQDN)** (erforderlich für den eigenständigen Azure ATP-Sensor; kann nicht für den Azure ATP-Sensor geändert werden): Geben Sie den vollqualifizierten Domänennamen (FQDN) Ihres Domänencontrollers ein, und klicken Sie auf das Pluszeichen, um ihn der Liste hinzuzufügen. z. B. **dc01.contoso.com**.

      Die folgenden Informationen gelten für die Server, die Sie in der Liste **Domänencontroller** eingeben.
      - Alle Domänencontroller, deren Datenverkehr vom eigenständigen Azure ATP-Sensor mittels Portspiegelung überwacht wird, müssen in der Liste **Domänencontroller** aufgeführt sein. Wenn ein Domänencontroller nicht in der Liste **Domänencontroller** aufgeführt ist, werden verdächtige Aktivitäten möglicherweise nicht wie erwartet erkannt.
      - Mindestens ein Domänencontroller in der Liste sollte ein globaler Katalog sein. Dadurch kann Azure ATP Computer- und Benutzerobjekte in anderen Domänen in der Gesamtstruktur auflösen.

  - **Netzwerkadapter für Erfassung** (erforderlich):
   
     - Für einen Azure ATP-Sensor sollten dies alle Netzwerkadapter sein, die für die Kommunikation mit anderen Computern in Ihrer Organisation verwendet werden.
    - Wählen Sie für einen eigenständigen Azure ATP-Sensor auf einem dedizierten Server die Netzwerkadapter aus, die als Zielspiegelport konfiguriert sind. Diese empfangen den Datenverkehr des gespiegelten Domänencontrollers.

    - **Kandidat für die Domänensynchronisierung:** Azure ATP-Sensoren sind standardmäßig keine Kandidaten für die Domänensynchronisierung, eigenständige Azure ATP-Sensoren hingegen sind es. Um einen Azure ATP-Sensor als Kandidat für die Domänensynchronisierung auszuwählen, schalten Sie die Umschaltoption **Kandidat für die Domänensynchronisierung** im Konfigurationsbildschirm auf **EIN**. 
    
        Der Domänensynchronizer ist für die Synchronisierung zwischen Azure ATP und Ihrer Active Directory-Domäne verantwortlich. Je nach Größe der Domäne ist die erste Synchronisierung ressourcenintensiv und kann einige Zeit dauern. 
   Es wird empfohlen, alle Azure ATP-Sensoren an Remotestandorten als Kandidaten für die Domänensynchronisierung zu deaktivieren.
   Wenn Ihr Domänencontroller schreibgeschützt ist, verwenden Sie ihn nicht als Kandidat für die Domänensynchronisierung. Weitere Informationen zur Azure ATP-Domänensynchronisierung finden Sie unter [Azure ATP-Architektur](atp-architecture.md#azure-atp-sensor-features).
  
4. Klicken Sie auf **Speichern**.


## <a name="validate-installations"></a>Überprüfen von Installationen
Gehen Sie wie folgt vor, um zu überprüfen, ob der Azure ATP-Sensor erfolgreich bereitgestellt wurde:

1.  Überprüfen Sie, ob der Dienst mit dem Namen **Azure Advanced Threat Protection-Sensor** ausgeführt wird. Es kann einige Sekunden dauern, bis der Dienst nach dem Speichern der Einstellungen für den Azure ATP-Sensor gestartet wird.

2.  Wenn der Dienst nicht gestartet wird, überprüfen Sie die Datei „Microsoft.Tri.sensor-Errors.log“ im Standardordner „%programfiles%\Azure Advanced Threat Protection sensor\Version X\Logs“.
 
 >[!NOTE]
 > Es werden regelmäßig Versionsupdates für Azure ATP ausgeführt. Wenn Sie die neuste Version im Azure ATP-Portal überprüfen möchten, navigieren Sie zur **Konfiguration**, und klicken Sie dann auf **Info**. 

3.  Rufen Sie die URL Ihres Arbeitsbereichs auf. Suchen Sie im Azure ATP-Portal über die Suchleiste nach einem bestimmten Objekt, z.B. einem Benutzer oder einer Gruppe in Ihrer Domäne.



> [!div class="step-by-step"]
> [« Schritt 4](install-atp-step4.md)



## <a name="see-also"></a>Weitere Informationen

- [Azure ATP sizing tool (Azure ATP-Tool zur Größenanpassung)](http://aka.ms/aatpsizingtool)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
