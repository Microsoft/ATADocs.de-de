---
title: Planen von Microsoft Defender für die Identitäts Bereitstellung
description: Hilft Ihnen bei der Planung der Bereitstellung und der Entscheidung, wie viele Microsoft Defender für Identitäts Server für die Unterstützung Ihres Netzwerks benötigt werden.
author: shsagir
ms.author: shsagir
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2fa0a70299b897a2c8b29e01ebb97e9740b0eb66
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2020
ms.locfileid: "94848617"
---
# <a name="plan-capacity-for-product-long"></a>Planen der Kapazität für [!INCLUDE [Product long](includes/product-long.md)]

In dieser Anleitung legen Sie fest, wie viele [!INCLUDE [Product long](includes/product-long.md)] Sensoren Sie benötigen.

## <a name="prerequisites"></a>Voraussetzungen

- Das [ [!INCLUDE [Product short](includes/product-short.md)] Tool zur Größen](https://aka.ms/aatpsizingtool)Anpassung herunterladen.
- Lesen Sie den Artikel [[!INCLUDE [Product short](includes/product-short.md)]-Architektur](architecture.md).
- Lesen Sie den Artikel [[!INCLUDE [Product short](includes/product-short.md)]-Voraussetzungen](prerequisites.md).

## <a name="use-the-sizing-tool"></a>Verwenden des Tools zur Größenanpassung

Die empfohlene und einfachste Methode zum Ermitteln der Kapazität für Ihre [!INCLUDE [Product short](includes/product-short.md)] Bereitstellung ist die Verwendung des [!INCLUDE [Product short](includes/product-short.md)] Tools zur Größenanpassung. Mit diesem Tool können Sie manuell Informationen zum Datenverkehr erfassen. Weitere Informationen zur manuellen Methode finden Sie im Abschnitt [Datenverkehrsschätzung für Domänencontroller](#manual-sizing) am Ende dieses Artikels.

1. Führen [!INCLUDE [Product short](includes/product-short.md)] Sie das Tool zur Größenanpassung aus der heruntergeladenen ZIP-Datei **TriSizingTool.exe** aus.
1. Öffnen Sie nach Abschluss der Toolausführung die Excel-Datei mit den Ergebnissen.
1. Suchen Sie in der Excel-Datei nach dem Blatt **Azure ATP Summary** (Azure ATP-Zusammenfassung). Das zweite Blatt wird nicht benötigt, da es für die ATA-Planung vorgesehen ist.
    ![Beispiel für das Kapazitätsplanungstool](media/capacity-tool.png)

1. Suchen Sie in der Excel-Ergebnisdatei in der Azure ATP-Sensortabelle nach dem Feld **Busy Packets/sec** (Aktive Pakete/s), und notieren Sie den Wert.
1. Vergleichen Sie das Feld " **ausgelastete Pakete/** s" mit dem Feld " **Pakete pro Sekunde** " im Abschnitt " [ [!INCLUDE [Product short](includes/product-short.md)] Sensor Tabelle](#sizing) " in diesem Artikel. Verwenden Sie die Felder, um die vom Sensor verwendeten Arbeitsspeicher- und CPU-Ressourcen zu bestimmen.

## <a name="product-short-sensor-sizing"></a><a name="sizing"></a>[!INCLUDE [Product short](includes/product-short.md)]Sensorgröße

Ein [!INCLUDE [Product short](includes/product-short.md)] Sensor kann die Überwachung eines Domänen Controllers basierend auf der Menge des vom Domänen Controller generierten Netzwerkverkehrs unterstützen. Die folgende Tabelle enthält Schätzungen. Die tatsächlich vom Sensor analysierte Menge ist abhängig vom Umfang des Datenverkehrs und dessen Verteilung.

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
Es wird empfohlen, nicht mit Hyperthreadingkernen zu arbeiten. Das Arbeiten mit hyperthreadkernen kann zu Problemen mit der Sensor Integrität führen [!INCLUDE [Product short](includes/product-short.md)] .
- Gesamtarbeitsspeicher, der vom Sensordienst verwendet wird
- Wenn der Domänen Controller nicht über die für den Sensor benötigten Ressourcen verfügt [!INCLUDE [Product short](includes/product-short.md)] , ist die Leistung des Domänen Controllers nicht beeinträchtigt. Der [!INCLUDE [Product short](includes/product-short.md)] Sensor funktioniert jedoch möglicherweise nicht erwartungsgemäß.
- Bei Ausführung als virtueller Computer muss der gesamte Arbeitsspeicher zu jedem Zeitpunkt dem virtuellen Computer zugewiesen sein.
- Legen Sie die **Energie Option** des [!INCLUDE [Product short](includes/product-short.md)] Sensors auf **hohe Leistung** fest, um eine optimale Leistung zu erzielen.
- Es sind mindestens 2 Kerne erforderlich.
- Mindestens 6 GB Festplatten Speicherplatz sind erforderlich, 10 GB wird empfohlen, einschließlich des Speicherplatzes, der für die [!INCLUDE [Product short](includes/product-short.md)] Binärdateien und Protokolle benötigt wird.

### <a name="dynamic-memory"></a>Dynamischer Arbeitsspeicher

> [!NOTE]
> Bei Ausführung als virtueller Computer (VM) muss der gesamte Arbeitsspeicher zu jedem Zeitpunkt dem virtuellen Computer zugewiesen sein.

|VM-Host|Beschreibung|
|------------|-------------|
|Hyper-V|Stellen Sie sicher, dass **Dynamischen Arbeitsspeicher aktivieren** für den virtuellen Computer nicht aktiviert ist.|
|VMWare|Stellen Sie sicher, dass die konfigurierte und die reservierte Arbeitsspeichermenge gleich sind, oder wählen Sie in den VM-Einstellungen die folgende Option aus: **Gesamten Gastarbeitsspeicher reservieren (alle gesperrt)** .|
|Anderer Virtualisierungshost|Informieren Sie sich in der Dokumentation des Herstellers, wie Sie sicherstellen, dass der Arbeitsspeicher zu jedem Zeitpunkt vollständig dem virtuellen Computer zugewiesen ist. |

## <a name="domain-controller-traffic-estimation"></a><a name="manual-sizing"></a> Datenverkehrsschätzung für Domänencontroller

Wenn Sie das Tool zur Größenanpassung aus irgendeinem Grund nicht verwenden können [!INCLUDE [Product short](includes/product-short.md)] , sammeln Sie die Informationen zum Paket/Sek. manuell von allen Domänen Controllern. Sammeln Sie hierbei Daten über einen Zeitraum von 24 Stunden mit einem niedrigen Erfassungsintervall (etwa 5 Sekunden). Anschließend müssen Sie für jeden Domänencontroller den Tagesdurchschnitt und den Durchschnitt für die Zeitspanne (15 Minuten) mit der höchsten Auslastung berechnen. Die folgenden Abschnitte enthalten Anweisungen dazu, wie Sie Informationen zum Pakete/Sek.-Leistungsindikator für einen Domänencontroller sammeln.

Es gibt verschiedene Tools, die Sie verwenden können, um die durchschnittliche Anzahl der Pakete pro Sekunde eines Domänencontrollers zu ermitteln. Auch ohne den Einsatz solcher Werkzeuge können Sie diesen Leistungsindikator mit dem Systemmonitor ermitteln.

Um die Pakete pro Sekunde zu ermitteln, gehen Sie auf jedem Domänencontroller wie folgt vor:

1. Öffnen Sie den Systemmonitor.

    ![Abbildung des Systemmonitors](media/traffic-estimation-1.png)

1. Erweitern Sie **Datensammlersätze**.

    ![Abbildung der Datensammlersätze](media/traffic-estimation-2.png)

1. Klicken Sie mit der rechten Maustaste auf **Benutzerdefiniert**, und wählen Sie **Neu** &gt; **Datensammlersatz** aus.

    ![Abbildung eines neuen Datensammlersatzes](media/traffic-estimation-3.png)

1. Geben Sie einen Namen für den Sammlersatz ein, und wählen Sie **Manuell erstellen (Erweitert)** aus.

1. Wählen Sie unter **Welcher Datentyp soll eingeschlossen werden?** die Option **Datenprotokolle und Leistungsindikator erstellen** aus.

    ![Abbildung für Datentyp des neuen Sammlersatzes](media/traffic-estimation-5.png)

1. Klicken Sie unter **Welche Leistungsindikatoren möchten Sie protokollieren?** auf **Hinzufügen**.

1. Erweitern Sie **Netzwerkadapter**, wählen Sie **Pakete/Sek.** aus, und wählen Sie die richtige Instanz aus. Wenn Sie sich dabei nicht sicher sind, können Sie **&lt;Alle Instanzen&gt;** auswählen und auf **Hinzufügen** und **OK** klicken.

    > [!NOTE]
    > Um diesen Vorgang auf einer Befehlszeile auszuführen, führen Sie `ipconfig /all` aus, um den Namen des Adapters und die Konfiguration zu ermitteln.

    ![Abbildung – Hinzufügen von Leistungsindikatoren](media/traffic-estimation-7.png)

1. Ändern Sie das **Stichprobenintervall** auf **5 Sekunden**.

1. Legen Sie den Speicherort fest, an dem die Daten gespeichert werden sollen.

1. Wählen Sie unter **Neuen Datensammlersatz erstellen** die Option **Diesen Datensammlersatz jetzt starten** aus, und klicken Sie auf **Fertig stellen**.

    Jetzt sollte der erstellte Datensammlersatz mit einem grünen Dreieck als Zeichen der Funktion dargestellt werden.

1. Beenden Sie nach 24 Stunden den Datensammlersatz, indem Sie mit der rechten Maustaste auf das zugehörige Symbol klicken und die Option **Beenden** auswählen.

    ![Abbildung für das Beenden des Datensammlersatzes](media/traffic-estimation-12.png)

1. Wechseln Sie im Datei-Explorer zu dem Ordner, in dem die BLG-Datei gespeichert wurde, und doppelklicken Sie darauf, um sie im Systemmonitor zu öffnen.

1. Wählen Sie den Leistungsindikator für Pakete/Sekunde aus, und notieren Sie die durchschnittlichen und maximalen Werte.

    ![Abbildung Leistungsindikator für Pakete pro Sekunde](media/traffic-estimation-14.png)

## <a name="next-steps"></a>Nächste Schritte

In dieser Anleitung haben Sie festgelegt, wie viele [!INCLUDE [Product short](includes/product-short.md)] Sensoren Sie benötigen. Außerdem haben Sie die Größe für die Sensoren bestimmt. Fahren Sie mit dem [!INCLUDE [Product short](includes/product-short.md)] Schnellstart Handbuch zum Erstellen einer Instanz fort.

> [!div class="nextstepaction"]
> [Erstellen der [!INCLUDE [Product short](includes/product-short.md)] Instanz](install-step1.md)

## <a name="join-the-community"></a>Beitritt zur Community

Haben Sie weitere Fragen, oder möchten Sie mit anderen über [!INCLUDE [Product short](includes/product-short.md)] und damit verbundene Sicherheitsaspekte diskutieren? Treten Sie noch heute der [[!INCLUDE [Product short](includes/product-short.md)]Community](https://aka.ms/MDIcommunity) bei.
