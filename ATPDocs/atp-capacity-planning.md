---
title: 'Planen der Azure Advanced Threat Protection-Bereitstellung: Schnellstart | Microsoft-Dokumentation'
description: Hilft bei der Planung Ihrer Bereitstellung und der Entscheidung, wie viele Azure ATP-Server für Ihr Netzwerk erforderlich sind.
author: mlottner
ms.author: mlottner
ms.date: 11/05/2019
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.openlocfilehash: 0d149b74724ecddcce88bc932626d6bd395d4202
ms.sourcegitcommit: ef68a774d2756719bce8747e65f8bde2b9afdd5d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/05/2019
ms.locfileid: "73618492"
---
# <a name="quickstart-plan-capacity-for-azure-atp"></a>Schnellstart: Planen der Kapazität für Azure ATP

In diesem Schnellstart erfahren Sie, wie viele Azure ATP-Sensoren und eigenständige Sensoren Sie benötigen.

## <a name="prerequisites"></a>Voraussetzungen

- Laden Sie das [Tool zur Azure ATP-Größenanpassung](https://aka.ms/aatpsizingtool) herunter.
- Lesen Sie den Artikel [Azure ATP-Architektur](atp-architecture.md).
- Lesen Sie den Artikel [Voraussetzungen für Azure ATP](atp-prerequisites.md). 


## <a name="use-the-sizing-tool"></a>Verwenden des Tools zur Größenanpassung

Die empfohlene und einfachste Methode zum Bestimmen der Kapazität für die Azure ATP-Bereitstellung besteht in der Verwendung des Tools zur Azure ATP-Größenanpassung. Mit diesem Tool können Sie manuell Informationen zum Datenverkehr erfassen. Weitere Informationen zur manuellen Methode finden Sie im Abschnitt [Datenverkehrsschätzung für Domänencontroller](#manual-sizing) am Ende dieses Artikels.

1. Führen Sie das Tool zur Azure ATP-Größenanpassung (**TriSizingTool.exe**) aus der ZIP-Datei aus, die Sie heruntergeladen haben. 
2. Öffnen Sie nach Abschluss der Toolausführung die Excel-Datei mit den Ergebnissen.
3. Suchen Sie in der Excel-Datei nach dem Blatt **Azure ATP Summary** (Azure ATP-Zusammenfassung). Das zweite Blatt wird nicht benötigt, da es für die Azure ATA-Planung vorgesehen ist.
   ![Beispiel für das Kapazitätsplanungstool](media/capacity-tool.png)

4. Suchen Sie in der Excel-Ergebnisdatei in der Azure ATP-Sensortabelle nach dem Feld **Busy Packets/sec** (Aktive Pakete/s), und notieren Sie den Wert.
5. Wählen Sie Ihren Sensortyp aus. Bestimmen Sie anhand der Informationen im Abschnitt [Auswählen des geeigneten Sensortyps](#choosing-the-right-sensor-type-for-your-deployment), welchen Sensor bzw. welche Sensoren Sie verwenden möchten. Berücksichtigen Sie bei der Auswahl des Sensortyps Ihren Wert für **Busy Packets/sec** (Aktive Pakete/s).
6. Gleichen Sie Ihren Wert für **Busy Packets/sec** (Aktive Pakete/s) an den Wert im Feld **PACKETS PER SECOND** (PAKETE PRO SEKUNDE) im Abschnitt [Azure ATP-Sensortabelle](#sizing) in diesem Artikel an. Verwenden Sie die Felder, um die vom Sensor verwendeten Arbeitsspeicher- und CPU-Ressourcen zu bestimmen.


## Auswählen des richtigen Sensortyps für die Bereitstellung<a name="choosing-the-right-sensor-type-for-your-deployment"></a>

In einer Azure ATP-Bereitstellung wird jede Kombination aus den Typen des Azure ATP-Sensors unterstützt:

- Nur Azure ATP-Sensoren
- Nur eigenständige Azure ATP-Sensoren
- Eine Kombination aus beiden Typen

Berücksichtigen Sie folgende Vorteile bei der Auswahl des Bereitstellungstyps des Sensors:

|Sensortyp|Vorteile|Kosten|Bereitstellungstopologie|Domänencontrollerverwendung|
|----|----|----|----|-----|
|Azure ATP-Sensor|Erfordert keinen dedizierten Server und keine Konfiguration der Portspiegelung.|Kleinschreibung|Auf dem Domänencontroller installiert.|Unterstützt bis zu 100.000 Pakete pro Sekunde.|
|Eigenständiger Azure ATP-Sensor|Die Out-of-Band-Bereitstellung erschwert es Angreifern, herauszufinden, ob Azure ATP vorhanden ist.|Höher|Neben dem Domänencontroller installiert (out-of-band).|Unterstützt bis zu 100.000 Pakete pro Sekunde.|


Berücksichtigen Sie die folgenden Punkte, wenn Sie entscheiden, wie viele eigenständige Azure ATP-Sensoren bereitgestellt werden sollen:

- **Active Directory-Gesamtstrukturen und -Domänen**: Azure ATP kann Datenverkehr aus mehreren Domänen innerhalb mehrerer Active Directory-Gesamtstrukturen für jede Azure ATP-Instanz überwachen, die Sie erstellen.

- **Portspiegelung**: Die Portspiegelung erfordert möglicherweise die Bereitstellung mehrerer eigenständiger Azure ATP-Sensoren pro Rechenzentrum oder Filialstandort.

- **Kapazität**: Ein eigenständiger Azure ATP-Sensor kann die Überwachung von mehreren Domänencontrollern unterstützen, abhängig vom Umfang des Datenverkehrs des überwachten Domänencontrollers.

## <a name="sizing"></a> Größenanpassung des Azure ATP-Sensors und des eigenständigen Azure ATP-Sensors 

Ein Azure ATP-Sensor kann die Überwachung eines Domänencontrollers basierend auf der Menge des vom Domänencontroller erzeugten Datenverkehrs unterstützen. Die folgende Tabelle enthält Schätzungen. Die tatsächlich vom Sensor analysierte Menge ist abhängig vom Umfang des Datenverkehrs und dessen Verteilung.

Die folgende CPU- und Arbeitsspeicherkapazität bezieht sich auf den **Verbrauch des Sensors selbst** und nicht auf die Domänencontrollerkapazität.

|Pakete pro Sekunde*|CPU (Kerne)**|Arbeitsspeicher (GB)|
|----|----|-----|
|0 – 1.000|0,25|2,50|
|1\.000 – 5.000|0,75|6,00|
|5\.000 – 10.000|1,00|6,50|
|10.000 – 20.000|2,00|9,00|
|20.000 – 50.000|3,50|9,50|
|50.000 – 75.000 |3,50|9,50|
|75.000 – 100.000|3,50 |9,50|
|
** Dies umfasst physische Kerne, keine Hyperthreadingkerne. 

Beachten Sie bei der Größenanpassung Folgendes: 

- Gesamtanzahl der vom Sensordienst verwendeten Kerne<br>Es wird empfohlen, nicht mit Hyperthreadingkernen zu arbeiten. Der Einsatz von Hyperthreadkernen kann zu Problemen mit der Integrität von Azure ATP-Sensoren führen. 
- Gesamtarbeitsspeicher, der vom Sensordienst verwendet wird
- Wenn der Domänencontroller nicht über die für den Azure ATP-Sensor erforderlichen Ressourcen verfügt, wird die Leistung des Domänencontrollers zwar nicht beeinträchtigt, aber der Azure ATP-Sensor funktioniert möglicherweise nicht wie erwartet.
- Bei Ausführung als virtueller Computer muss der gesamte Arbeitsspeicher zu jedem Zeitpunkt dem virtuellen Computer zugewiesen sein.
- Um eine optimale Leistung zu erzielen, legen Sie die **Energieoption** des Azure ATP-Sensors auf **Hohe Leistung** fest.
- Es sind mindestens 2 Kerne erforderlich. Es wird mindestens 6 GB Speicherplatz benötigt (10 GB empfohlen), einschließlich des Speicherplatzes, der für die Azure ATP-Binärdateien und -Protokolle benötigt wird.

### <a name="dynamic-memory"></a>Dynamischer Arbeitsspeicher

> [!NOTE] 
> Bei Ausführung als virtueller Computer (VM) muss der gesamte Arbeitsspeicher zu jedem Zeitpunkt dem virtuellen Computer zugewiesen sein. 

|VM-Host|Beschreibung|
|------------|-------------|
|Hyper-V|Stellen Sie sicher, dass **Dynamischen Arbeitsspeicher aktivieren** für den virtuellen Computer nicht aktiviert ist.|
|VMWare|Stellen Sie sicher, dass die konfigurierte und die reservierte Arbeitsspeichermenge gleich sind, oder wählen Sie in den VM-Einstellungen die folgende Option aus: **Gesamten Gastarbeitsspeicher reservieren (alle gesperrt)** .|
|Anderer Virtualisierungshost|Informieren Sie sich in der Dokumentation des Herstellers, wie Sie sicherstellen, dass der Arbeitsspeicher zu jedem Zeitpunkt vollständig dem virtuellen Computer zugewiesen ist. |
|

Fahren Sie bei Ausführung als virtueller Computer den Server herunter, bevor ein neuer Prüfpunkt erstellt wird, um eine mögliche Beschädigung der Datenbank zu verhindern.

## <a name="manual-sizing"></a> Datenverkehrsschätzung für Domänencontroller

Wenn Sie das Azure ATP-Tool zur Größenanpassung nicht verwenden können, sammeln Sie die Informationen zum Leistungsindikator für die Paketanzahl pro Sekunde manuell von allen Domänencontrollern. Sammeln Sie hierbei Daten über einen Zeitraum von 24 Stunden mit einem niedrigen Erfassungsintervall (etwa 5 Sekunden). Anschließend müssen Sie für jeden Domänencontroller den Tagesdurchschnitt und den Durchschnitt für die Zeitspanne (15 Minuten) mit der höchsten Auslastung berechnen. Die folgenden Abschnitte enthalten Anweisungen dazu, wie Sie Informationen zum Pakete/Sek.-Leistungsindikator für einen Domänencontroller sammeln.

Es gibt verschiedene Tools, die Sie verwenden können, um die durchschnittliche Anzahl der Pakete pro Sekunde eines Domänencontrollers zu ermitteln. Auch ohne den Einsatz solcher Werkzeuge können Sie diesen Leistungsindikator mit dem Systemmonitor ermitteln.

Um die Pakete pro Sekunde zu ermitteln, gehen Sie auf jedem Domänencontroller wie folgt vor:

1.  Öffnen Sie den Systemmonitor.

    ![Abbildung des Systemmonitors](media/atp-traffic-estimation-1.png)

2.  Erweitern Sie **Datensammlersätze**.

    ![Abbildung der Datensammlersätze](media/atp-traffic-estimation-2.png)

3.  Klicken Sie mit der rechten Maustaste auf **Benutzerdefiniert**, und wählen Sie **Neu** &gt; **Datensammlersatz** aus.

    ![Abbildung eines neuen Datensammlersatzes](media/atp-traffic-estimation-3.png)

4.  Geben Sie einen Namen für den Sammlersatz ein, und wählen Sie **Manuell erstellen (Erweitert)** aus.

5.  Wählen Sie unter **Welcher Datentyp soll eingeschlossen werden?** die Option **Datenprotokolle und Leistungsindikator erstellen** aus.

    ![Abbildung für Datentyp des neuen Sammlersatzes](media/atp-traffic-estimation-5.png)

6.  Klicken Sie unter **Welche Leistungsindikatoren möchten Sie protokollieren?** auf **Hinzufügen**.

7.  Erweitern Sie **Netzwerkadapter**, wählen Sie **Pakete/Sek.** aus, und wählen Sie die richtige Instanz aus. Wenn Sie sich dabei nicht sicher sind, können Sie **&lt;Alle Instanzen&gt;** auswählen und auf **Hinzufügen** und **OK** klicken.

    > [!NOTE]
    > Um diesen Vorgang auf einer Befehlszeile auszuführen, führen Sie `ipconfig /all` aus, um den Namen des Adapters und die Konfiguration zu ermitteln.

    ![Abbildung – Hinzufügen von Leistungsindikatoren](media/atp-traffic-estimation-7.png)

8.  Ändern Sie das **Stichprobenintervall** auf **5 Sekunden**.

9. Legen Sie den Speicherort fest, an dem die Daten gespeichert werden sollen.

10. Wählen Sie unter **Neuen Datensammlersatz erstellen** die Option **Diesen Datensammlersatz jetzt starten** aus, und klicken Sie auf **Fertig stellen**.

    Jetzt sollte der erstellte Datensammlersatz mit einem grünen Dreieck als Zeichen der Funktion dargestellt werden.

11. Beenden Sie nach 24 Stunden den Datensammlersatz, indem Sie mit der rechten Maustaste auf das zugehörige Symbol klicken und die Option **Beenden** auswählen.

    ![Abbildung für das Beenden des Datensammlersatzes](media/atp-traffic-estimation-12.png)

12. Wechseln Sie im Datei-Explorer zu dem Ordner, in dem die BLG-Datei gespeichert wurde, und doppelklicken Sie darauf, um sie im Systemmonitor zu öffnen.

13. Wählen Sie den Leistungsindikator für Pakete/Sekunde aus, und notieren Sie die durchschnittlichen und maximalen Werte.

    ![Abbildung Leistungsindikator für Pakete pro Sekunde](media/atp-traffic-estimation-14.png)



## <a name="next-steps"></a>Nächste Schritte

In diesem Schnellstart haben Sie erfahren, wie viele Azure ATP-Sensoren und eigenständige Sensoren Sie benötigen. Außerdem haben Sie die Größe für die Sensoren bestimmt. Fahren Sie mit dem nächsten Schnellstart fort, um eine Azure ATP-Instanz zu erstellen.

> [!div class="nextstepaction"]
> [Erstellen einer Azure ATP-Instanz](install-atp-step1.md)


## <a name="join-the-community"></a>Beitritt zur Community

Haben Sie weitere Fragen, oder möchten Sie mit anderen über Azure ATP und damit verbundene Sicherheitsaspekte diskutieren? Treten Sie noch heute der [Azure ATP-Community](https://aka.ms/azureatpcommunity) bei!
