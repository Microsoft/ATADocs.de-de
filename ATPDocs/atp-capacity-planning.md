---
title: 'Schnellstart: Planen der Azure Advanced Threat Protection-Bereitstellung'
description: Hilft bei der Planung Ihrer Bereitstellung und der Entscheidung, wie viele Azure ATP-Server für Ihr Netzwerk erforderlich sind.
author: shsagir
ms.author: shsagir
ms.date: 05/20/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.openlocfilehash: 11b895e4d18df33bb220dc806246fec6ddfa6877
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88956770"
---
# <a name="quickstart-plan-capacity-for-azure-atp"></a>Schnellstart: Planen der Kapazität für Azure ATP

In diesem Schnellstart erfahren Sie, wie viele Azure ATP-Sensoren Sie benötigen.

## <a name="prerequisites"></a>Voraussetzungen

- Laden Sie das [Tool zur Azure ATP-Größenanpassung](https://aka.ms/aatpsizingtool) herunter.
- Lesen Sie den Artikel [Azure ATP-Architektur](atp-architecture.md).
- Lesen Sie den Artikel [Voraussetzungen für Azure ATP](atp-prerequisites.md).

## <a name="use-the-sizing-tool"></a>Verwenden des Tools zur Größenanpassung

Die empfohlene und einfachste Methode zum Bestimmen der Kapazität für die Azure ATP-Bereitstellung besteht in der Verwendung des Tools zur Azure ATP-Größenanpassung. Mit diesem Tool können Sie manuell Informationen zum Datenverkehr erfassen. Weitere Informationen zur manuellen Methode finden Sie im Abschnitt [Datenverkehrsschätzung für Domänencontroller](#manual-sizing) am Ende dieses Artikels.

1. Führen Sie das Tool zur Azure ATP-Größenanpassung (**TriSizingTool.exe**) aus der ZIP-Datei aus, die Sie heruntergeladen haben.
1. Öffnen Sie nach Abschluss der Toolausführung die Excel-Datei mit den Ergebnissen.
1. Suchen Sie in der Excel-Datei nach dem Blatt **Azure ATP Summary** (Azure ATP-Zusammenfassung). Das zweite Blatt wird nicht benötigt, da es für die ATA-Planung vorgesehen ist.
    ![Beispiel für das Kapazitätsplanungstool](media/capacity-tool.png)

1. Suchen Sie in der Excel-Ergebnisdatei in der Azure ATP-Sensortabelle nach dem Feld **Busy Packets/sec** (Aktive Pakete/s), und notieren Sie den Wert.
1. Gleichen Sie Ihren Wert für **Busy Packets/sec** (Aktive Pakete/s) an den Wert im Feld **PACKETS PER SECOND** (PAKETE PRO SEKUNDE) im Abschnitt [Azure ATP-Sensortabelle](#sizing) in diesem Artikel an. Verwenden Sie die Felder, um die vom Sensor verwendeten Arbeitsspeicher- und CPU-Ressourcen zu bestimmen.

## <a name="azure-atp-sensor-sizing"></a><a name="sizing"></a> Dimensionierung von Azure ATP-Sensoren

Ein Azure ATP-Sensor kann die Überwachung eines Domänencontrollers basierend auf der Menge des vom Domänencontroller erzeugten Datenverkehrs unterstützen. Die folgende Tabelle enthält Schätzungen. Die tatsächlich vom Sensor analysierte Menge ist abhängig vom Umfang des Datenverkehrs und dessen Verteilung.

Die folgende CPU- und RAM-Kapazität (Random Access Memory) bezieht sich auf den **Verbrauch des Sensors selbst** und nicht auf die Domänencontrollerkapazität.

|Pakete pro Sekunde|CPU (Kerne)\*|Arbeitsspeicher\*\* (GB)|
|----|----|-----|
|0 – 1.000|0,25|2,50|
|1\.000 – 5.000|0,75|6,00|
|5\.000 – 10.000|1,00|6,50|
|10.000 – 20.000|2,00|9,00|
|20.000 – 50.000|3,50|9,50|
|50.000 – 75.000 |3,50|9,50|
|75.000 – 100.000|3,50|9,50|

\* Dies umfasst physische Kerne, keine Hyperthreadingkerne.  
\*\* Arbeitsspeicher (RAM)

Beachten Sie bei der Größenanpassung Folgendes:

- Gesamtanzahl der vom Sensordienst verwendeten Kerne  
Es wird empfohlen, nicht mit Hyperthreadingkernen zu arbeiten. Der Einsatz von Hyperthreadkernen kann zu Problemen mit der Integrität von Azure ATP-Sensoren führen.
- Gesamtarbeitsspeicher, der vom Sensordienst verwendet wird
- Wenn der Domänencontroller nicht über die für den Azure ATP-Sensor erforderlichen Ressourcen verfügt, wird die Leistung des Domänencontrollers zwar nicht beeinträchtigt, aber der Azure ATP-Sensor funktioniert möglicherweise nicht wie erwartet.
- Bei Ausführung als virtueller Computer muss der gesamte Arbeitsspeicher zu jedem Zeitpunkt dem virtuellen Computer zugewiesen sein.
- Um eine optimale Leistung zu erzielen, legen Sie die **Energieoption** des Azure ATP-Sensors auf **Hohe Leistung** fest.
- Es sind mindestens 2 Kerne erforderlich.
- Es wird mindestens 6 GB Festplattenspeicher benötigt (10 GB empfohlen), einschließlich des Speicherplatzes, der für die Azure ATP-Binärdateien und -Protokolle benötigt wird.

### <a name="dynamic-memory"></a>Dynamischer Arbeitsspeicher

> [!NOTE]
> Bei Ausführung als virtueller Computer (VM) muss der gesamte Arbeitsspeicher zu jedem Zeitpunkt dem virtuellen Computer zugewiesen sein.

|VM-Host|Beschreibung|
|------------|-------------|
|Hyper-V|Stellen Sie sicher, dass **Dynamischen Arbeitsspeicher aktivieren** für den virtuellen Computer nicht aktiviert ist.|
|VMWare|Stellen Sie sicher, dass die konfigurierte und die reservierte Arbeitsspeichermenge gleich sind, oder wählen Sie in den VM-Einstellungen die folgende Option aus: **Gesamten Gastarbeitsspeicher reservieren (alle gesperrt)** .|
|Anderer Virtualisierungshost|Informieren Sie sich in der Dokumentation des Herstellers, wie Sie sicherstellen, dass der Arbeitsspeicher zu jedem Zeitpunkt vollständig dem virtuellen Computer zugewiesen ist. |

## <a name="domain-controller-traffic-estimation"></a><a name="manual-sizing"></a> Datenverkehrsschätzung für Domänencontroller

Wenn Sie das Azure ATP-Tool zur Größenanpassung nicht verwenden können, sammeln Sie die Informationen zum Leistungsindikator für die Paketanzahl pro Sekunde manuell von allen Domänencontrollern. Sammeln Sie hierbei Daten über einen Zeitraum von 24 Stunden mit einem niedrigen Erfassungsintervall (etwa 5 Sekunden). Anschließend müssen Sie für jeden Domänencontroller den Tagesdurchschnitt und den Durchschnitt für die Zeitspanne (15 Minuten) mit der höchsten Auslastung berechnen. Die folgenden Abschnitte enthalten Anweisungen dazu, wie Sie Informationen zum Pakete/Sek.-Leistungsindikator für einen Domänencontroller sammeln.

Es gibt verschiedene Tools, die Sie verwenden können, um die durchschnittliche Anzahl der Pakete pro Sekunde eines Domänencontrollers zu ermitteln. Auch ohne den Einsatz solcher Werkzeuge können Sie diesen Leistungsindikator mit dem Systemmonitor ermitteln.

Um die Pakete pro Sekunde zu ermitteln, gehen Sie auf jedem Domänencontroller wie folgt vor:

1. Öffnen Sie den Systemmonitor.

    ![Abbildung des Systemmonitors](media/atp-traffic-estimation-1.png)

1. Erweitern Sie **Datensammlersätze**.

    ![Abbildung der Datensammlersätze](media/atp-traffic-estimation-2.png)

1. Klicken Sie mit der rechten Maustaste auf **Benutzerdefiniert**, und wählen Sie **Neu** &gt; **Datensammlersatz** aus.

    ![Abbildung eines neuen Datensammlersatzes](media/atp-traffic-estimation-3.png)

1. Geben Sie einen Namen für den Sammlersatz ein, und wählen Sie **Manuell erstellen (Erweitert)** aus.

1. Wählen Sie unter **Welcher Datentyp soll eingeschlossen werden?** die Option **Datenprotokolle und Leistungsindikator erstellen** aus.

    ![Abbildung für Datentyp des neuen Sammlersatzes](media/atp-traffic-estimation-5.png)

1. Klicken Sie unter **Welche Leistungsindikatoren möchten Sie protokollieren?** auf **Hinzufügen**.

1. Erweitern Sie **Netzwerkadapter**, wählen Sie **Pakete/Sek.** aus, und wählen Sie die richtige Instanz aus. Wenn Sie sich dabei nicht sicher sind, können Sie **&lt;Alle Instanzen&gt;** auswählen und auf **Hinzufügen** und **OK** klicken.

    > [!NOTE]
    > Um diesen Vorgang auf einer Befehlszeile auszuführen, führen Sie `ipconfig /all` aus, um den Namen des Adapters und die Konfiguration zu ermitteln.

    ![Abbildung – Hinzufügen von Leistungsindikatoren](media/atp-traffic-estimation-7.png)

1. Ändern Sie das **Stichprobenintervall** auf **5 Sekunden**.

1. Legen Sie den Speicherort fest, an dem die Daten gespeichert werden sollen.

1. Wählen Sie unter **Neuen Datensammlersatz erstellen** die Option **Diesen Datensammlersatz jetzt starten** aus, und klicken Sie auf **Fertig stellen**.

    Jetzt sollte der erstellte Datensammlersatz mit einem grünen Dreieck als Zeichen der Funktion dargestellt werden.

1. Beenden Sie nach 24 Stunden den Datensammlersatz, indem Sie mit der rechten Maustaste auf das zugehörige Symbol klicken und die Option **Beenden** auswählen.

    ![Abbildung für das Beenden des Datensammlersatzes](media/atp-traffic-estimation-12.png)

1. Wechseln Sie im Datei-Explorer zu dem Ordner, in dem die BLG-Datei gespeichert wurde, und doppelklicken Sie darauf, um sie im Systemmonitor zu öffnen.

1. Wählen Sie den Leistungsindikator für Pakete/Sekunde aus, und notieren Sie die durchschnittlichen und maximalen Werte.

    ![Abbildung Leistungsindikator für Pakete pro Sekunde](media/atp-traffic-estimation-14.png)

## <a name="next-steps"></a>Nächste Schritte

In diesem Schnellstart haben Sie ermittelt, wie viele Azure ATP-Sensoren Sie benötigen. Außerdem haben Sie die Größe für die Sensoren bestimmt. Fahren Sie mit dem nächsten Schnellstart fort, um eine Azure ATP-Instanz zu erstellen.

> [!div class="nextstepaction"]
> [Erstellen einer Azure ATP-Instanz](install-atp-step1.md)

## <a name="join-the-community"></a>Beitritt zur Community

Haben Sie weitere Fragen, oder möchten Sie mit anderen über Azure ATP und damit verbundene Sicherheitsaspekte diskutieren? Treten Sie noch heute der [Azure ATP-Community](https://aka.ms/azureatpcommunity) bei!
