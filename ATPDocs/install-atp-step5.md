---
title: 'Installieren von Azure Advanced Threat Protection: Schritt 5 | Microsoft-Dokumentation'
description: Im fünften Schritt der Installation von Azure ATP konfigurieren Sie Einstellungen für Ihren eigenständigen Azure ATP-Sensor.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: d7c95f8c-04f8-4946-9bae-c27ed362fcb0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a2e61758e06aedfe607afc0d3365227af872fe20
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/21/2018
ms.locfileid: "29444926"
---
*Gilt für: Azure Advanced Threat Protection*



# <a name="install-azure-atp---step-5"></a>Installieren von Azure ATP: Schritt 5

>[!div class="step-by-step"]
[« Schritt 4](install-atp-step4.md)
[Schritt 6 »](install-atp-step6-vpn.md)


## <a name="step-5-configure-the-azure-atp-sensor-settings"></a>Schritt 5: Konfigurieren der Einstellungen des Azure ATP-Sensors
Führen Sie nach der Installation des Azure ATP-Sensors die folgenden Schritte aus, um die Einstellungen für den Azure ATP-Sensor zu konfigurieren.

1.  Gehen Sie im Azure ATP-Arbeitsbereichsportal auf **Konfiguration**, und klicken Sie unter **System** auf **Sensor**.
   
     ![Abbildung der Konfiguration der Sensoreinstellungen](media/atp-sensor-config.png)


2.  Klicken Sie auf den Sensor, den Sie konfigurieren möchten, und geben Sie die folgenden Informationen ein:

    ![Abbildung der Konfiguration der Sensoreinstellungen](media/atp-sensor-config-2.png)

  - **Beschreibung:**: Geben Sie eine Beschreibung für den Azure ATP-Sensor ein (optional).
  - **Domänencontroller (FQDN)** (erforderlich für den eigenständigen Azure ATP-Sensor; kann nicht für den Azure ATP-Sensor geändert werden): Geben Sie den vollqualifizierten Domänennamen (FQDN) Ihres Domänencontrollers ein, und klicken Sie auf das Pluszeichen, um ihn der Liste hinzuzufügen. z. B. **dc01.contoso.com**.

      Die folgenden Informationen gelten für die Server, die Sie in der Liste **Domänencontroller** eingeben.
      - Alle Domänencontroller, deren Datenverkehr vom eigenständigen Azure ATP-Sensor mittels Portspiegelung überwacht wird, müssen in der Liste **Domänencontroller** aufgeführt sein. Wenn ein Domänencontroller nicht in der Liste **Domänencontroller** aufgeführt ist, werden verdächtige Aktivitäten möglicherweise nicht wie erwartet erkannt.
      - Mindestens ein Domänencontroller in der Liste sollte ein globaler Katalog sein. Dadurch kann Azure ATP Computer- und Benutzerobjekte in anderen Domänen in der Gesamtstruktur auflösen.

  - **Netzwerkadapter für Erfassung** (erforderlich):
     - Wählen Sie für einen eigenständigen Azure ATP-Sensor auf einem dedizierten Server die Netzwerkadapter aus, die als Zielspiegelport konfiguriert sind. Diese empfangen den Datenverkehr des gespiegelten Domänencontrollers.
     - Für einen Azure ATP-Sensor sollten dies alle Netzwerkadapter sein, die für die Kommunikation mit anderen Computern in Ihrer Organisation verwendet werden.


  - **Kandidat für die Domänensynchronisierung**: Alle eigenständigen Azure ATP-Sensoren, die als Kandidat für die Domänensynchronisierung festgelegt sind, können die Synchronisierung zwischen Azure ATP und Ihrer Active Directory-Domäne übernehmen. Je nach Größe der Domäne ist die erste Synchronisierung ressourcenintensiv und kann einige Zeit dauern. Standardmäßig sind nur eigenständige Azure ATP-Sensoren als Kandidaten für die Domänensynchronisierung festgelegt.
   Es empfiehlt sich, alle Azure ATP-Sensoren an Remotestandorten als Kandidaten für die Domänensynchronisierung zu deaktivieren.
   Wenn Ihr Domänencontroller schreibgeschützt ist, verwenden Sie ihn nicht als Kandidat für die Domänensynchronisierung. Weitere Informationen finden Sie unter [Azure ATP architecture (Azure ATP-Architektur](atp-architecture.md#azure-atp-sensor-features).
  
4. Klicken Sie auf **Speichern**.


## <a name="validate-installations"></a>Überprüfen von Installationen
Gehen Sie wie folgt vor, um zu überprüfen, ob der Azure ATP-Sensor erfolgreich bereitgestellt wurde:

1.  Überprüfen Sie, ob der Dienst mit dem Namen **Azure Advanced Threat Protection-Sensor** ausgeführt wird. Es kann einige Sekunden dauern, bis der Dienst nach dem Speichern der Einstellungen für den Azure ATP-Sensor gestartet wird.

2.  Wenn der Dienst nicht gestartet wird, überprüfen Sie die Datei „Microsoft.Tri.sensor-Errors.log“ im Standardordner „%programfiles%\Azure Advanced Threat Protection sensor\Version X\Logs“.
 
 >[!NOTE]
 > Es werden regelmäßig Versionsupdates für Azure ATP ausgeführt. Wenn Sie die neuste Version im Azure ATP-Arbeitsbereichsportal überprüfen möchten, gehen Sie auf **Konfiguration** > **About** (Info). 

3.  Rufen Sie die URL Ihres Arbeitsbereichs auf. Suchen Sie im Arbeitsbereichsportal auf der Suchleiste nach einem bestimmten Objekt, z.B. einem Benutzer oder einer Gruppe in Ihrer Domäne.



>[!div class="step-by-step"]
[« Schritt 4](install-atp-step4.md)
[Schritt 6 »](install-atp-step6-vpn.md)


## <a name="see-also"></a>Weitere Informationen

- [Azure ATP sizing tool (Azure ATP-Tool zur Größenanpassung)](http://aka.ms/aatpsizingtool)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)
