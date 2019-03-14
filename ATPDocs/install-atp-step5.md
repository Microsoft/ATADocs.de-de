---
title: 'Schnellstart: Konfigurieren von Azure ATP-Einstellungen | Microsoft-Dokumentation'
description: Im fünften Schritt der Installation von Azure ATP konfigurieren Sie Einstellungen für Ihren eigenständigen Azure ATP-Sensor.
author: mlottner
ms.author: mlottner
ms.date: 03/03/2018
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 9b51c781cee16d4f158cc0e0528d4f80683aabad
ms.sourcegitcommit: 929f28783110c7e114ab36d4cccd50563f4030df
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/04/2019
ms.locfileid: "57253945"
---
# <a name="quickstart-configure-azure-atp-sensor-settings"></a>Schnellstart: Konfigurieren der Einstellungen des Azure ATP-Sensors

In diesem Schnellstart konfigurieren Sie die Einstellungen für den Azure ATP-Sensor, damit Daten angezeigt werden. Sie müssen zusätzliche Konfigurations- und Integrationsschritte vornehmen, um die Funktionen von Azure ATP nutzen zu können.  

## <a name="prerequisites"></a>Voraussetzungen

- Eine [Azure ATP](install-atp-step1.md)-Instanz, die mit [Active Directory verbunden ist](install-atp-step2.md).
- Eine heruntergeladene Kopie des [Setuppakets für Ihren ATP-Sensor](install-atp-step3.md) und den Zugriffsschlüssel.

## <a name="configure-sensor-settings"></a>Konfigurieren von Sensoreinstellungen

Gehen Sie nach der Installation des Azure ATP-Sensors folgendermaßen vor, um die Einstellungen des Azure ATP-Sensors zu konfigurieren.

1. Klicken Sie auf **Starten**, um Ihren Browser zu öffnen und sich beim Azure ATP-Portal anzumelden.

2.  Öffnen Sie die **Konfiguration** im Azure ATP-Portal, und wählen Sie **Sensoren** im Abschnitt **System** aus.
   
    ![Abbildung der Konfiguration der Sensoreinstellungen](media/atp-sensor-config.png)


3. Klicken Sie auf den Sensor, den Sie konfigurieren möchten, und geben Sie die folgenden Informationen ein:

   ![Abbildung der Konfiguration der Sensoreinstellungen](media/atp-sensor-config-2.png)

   - **Beschreibung**: Geben Sie eine Beschreibung für den Azure ATP-Sensor ein (optional).
   - **Domänencontroller (FQDN)** (für den eigenständigen Azure ATP-Sensor erforderlich; kann für den Azure ATP-Sensor nicht geändert werden): Geben Sie den vollqualifizierten Domänennamen (FQDN) des Domänencontrollers ein, und klicken Sie auf das Pluszeichen, um ihn der Liste hinzuzufügen, z. B. **dc01.contoso.com**.

     Die folgenden Informationen gelten für die Server, die Sie in der Liste **Domänencontroller** eingeben.
     - Alle Domänencontroller, deren Datenverkehr vom eigenständigen Azure ATP-Sensor mittels Portspiegelung überwacht wird, müssen in der Liste **Domänencontroller** aufgeführt sein. Wenn ein Domänencontroller nicht in der Liste **Domänencontroller** aufgeführt wird, werden verdächtige Aktivitäten möglicherweise nicht wie erwartet erkannt.
     - Mindestens ein Domänencontroller in der Liste sollte ein globaler Katalog sein. Dadurch kann Azure ATP Computer- und Benutzerobjekte in anderen Domänen in der Gesamtstruktur auflösen.

   - **Netzwerkadapter für Erfassung** (erforderlich):
   
    - Für Azure ATP-Sensoren sind alle Netzwerkadapter erforderlich, die für die Kommunikation mit anderen Computern in Ihrer Organisation verwendet werden.
    - Wählen Sie für eigenständige Azure ATP-Sensoren auf einem dedizierten Server die Netzwerkadapter aus, die als Zielspiegelport konfiguriert sind. Diese Netzwerkadapter empfangen den Datenverkehr des gespiegelten Domänencontrollers.

  - **Kandidat für die Domänensynchronisierung**: 
    
    - Der Domänensynchronizer ist für die Synchronisierung zwischen Azure ATP und Ihrer Active Directory-Domäne verantwortlich. Je nach Größe der Domäne ist die erste Synchronisierung ressourcenintensiv und kann einige Zeit dauern. Für Azure ATP wird empfohlen, dass pro Domäne mindestens ein Domänencontroller als Domänensynchronizerkandidat festgelegt wird. Wenn kein Domänencontroller als Domänensynchronizerkandidat ausgewählt wird, überprüft Azure ATP Ihr Netzwerk nur passiv und erfasst möglicherweise nicht alle Änderungen und Entitätsdetails von Active Directory. Mit mindestens einem **Domänensynchronizerkandidat** pro Domäne wird sichergestellt, dass Azure ATP Ihr Netzwerk jederzeit aktiv überprüft und alle Änderungen und Entitätswerte von Active Directory erfasst.
  
    - Azure ATP-Sensoren kommen standardmäßig nicht als Domänensynchronizer in Frage, eigenständige Azure ATP-Sensoren hingegen schon. Schalten Sie die Umschaltoption **Domänensynchronizerkandidat** im Konfigurationsbildschirm auf **EIN**, um einen Azure ATP-Sensor manuell als Domänensynchronizerkandidat festzulegen.
        
    - Es wird empfohlen, alle Azure ATP-Sensoren an Remotestandorten als mögliche Domänensynchronizer zu deaktivieren.
   
    - Legen Sie keine schreibgeschützten Domänencontroller als möglichen Domänensynchronizer fest. Weitere Informationen zur Azure ATP-Domänensynchronisierung finden Sie unter [Azure ATP-Architektur](atp-architecture.md#azure-atp-sensor-features).
  
3. Klicken Sie auf **Speichern**.


## <a name="validate-installations"></a>Überprüfen von Installationen
Überprüfen Sie folgendermaßen, ob der Azure ATP-Sensor erfolgreich bereitgestellt wurde:

1. Überprüfen Sie, ob der Dienst mit dem Namen **Azure Advanced Threat Protection-Sensor** ausgeführt wird. Es kann einige Sekunden dauern, bis der Dienst nach dem Speichern der Einstellungen für den Azure ATP-Sensor gestartet wird.

2. Wenn der Dienst nicht gestartet wird, überprüfen Sie die Datei „Microsoft.Tri.sensor-Errors.log“ im Standardordner „%programfiles%\Azure Advanced Threat Protection sensor\Version X\Logs“.
 
   >[!NOTE]
   > Es werden regelmäßig Versionsupdates für Azure ATP ausgeführt. Wenn Sie die neuste Version im Azure ATP-Portal überprüfen möchten, navigieren Sie zur **Konfiguration**, und klicken Sie dann auf **Info**. 

3. Rufen Sie Ihre Azure ATP-Instanz auf. Suchen Sie im Azure ATP-Portal über die Suchleiste nach einem bestimmten Objekt, z.B. einem Benutzer oder einer Gruppe in Ihrer Domäne.

4. Überprüfen Sie die ATP-Konnektivität für alle Domänengeräte anhand der folgenden Schritte:
    1. Öffnen Sie eine Eingabeaufforderung.
    2. Geben Sie Folgendes ein: ```nslookup```
    3. Geben Sie **server** und anschließend den FQDN oder die IP-Adresse des Domänencontrollers ein, auf dem der ATP-Sensor installiert ist. Beispiel: ```server contosodc.contoso.azure```
        - Stellen Sie sicher, dass Sie contosodc.contoso.azure und contoso.azure durch den FQDN Ihres Azure ATP-Sensors bzw. durch den Domänennamen ersetzen.
    4. Geben Sie Folgendes ein: ```ls -d contoso.azure```
    5. Wiederholen Sie die Schritte 3 und 4 für jeden Sensor, den Sie testen möchten.  
    6. Öffnen Sie von der Azure ATP-Konsole aus das Entitätsprofil für den Computer, von dem aus Sie den Konnektivitätstest durchgeführt haben. 
    7. Überprüfen Sie die zugehörige logische Aktivität, und bestätigen Sie die Konnektivität. 

    > [!NOTE] 
    >Wenn der zu testende Domänencontroller der erste bereitgestellte Sensor ist, warten Sie mindestens 15 Minuten, damit das Datenbank-Back-End die erste Bereitstellung der erforderlichen Microservices abschließen kann. Versuchen Sie erst anschließend, die zugehörige logische Aktivität für diesen Domänencontroller zu überprüfen.

## <a name="next-steps"></a>Nächste Schritte

- [Proxykonfiguration](configure-proxy.md)
- [Überprüfung der erweiterten Überwachungsrichtlinie von Azure ATP](atp-advanced-audit-policy.md)
- [Konfigurieren von Azure ATP für das Ausführen von Remoteaufrufen an SAM](install-atp-step8-samr.md)


## <a name="join-the-community"></a>Beitritt zur Community

Haben Sie weitere Fragen, oder möchten Sie mit anderen über Azure ATP und damit verbundene Sicherheitsaspekte diskutieren? Treten Sie noch heute der [Azure ATP-Community](https://aka.ms/azureatpcommunity) bei!
