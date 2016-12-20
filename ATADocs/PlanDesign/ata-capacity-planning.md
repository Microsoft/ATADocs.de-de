---
title: Planen Ihrer ATA-Bereitstellung | Microsoft Docs
description: "Hilft bei der Planung Ihrer Bereitstellung und der Entscheidung, wie viele ATA-Server für Ihr Netzwerk erforderlich sind."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/6/2016
ms.topic: get-started-article
ms.service: advanced-threat-analytics
ms.prod: 
ms.assetid: 279d79f2-962c-4c6f-9702-29744a5d50e2
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 56eff27ffdd988d5cc9e67352859ddfedebb2144
ms.openlocfilehash: 93ec7373a166529332d7c4809c756ab3ba240868


---

*Gilt für: Advanced Threat Analytics Version 1.7*



# <a name="ata-capacity-planning"></a>ATA-Kapazitätsplanung
Dieses Thema hilft Ihnen zu ermitteln, wie viele ATA-Server zur Überwachung Ihres Netzwerks erforderlich sind. Es wird erläutert, wie viele ATA-Gateways und/oder ATA-Lightweight-Gateways benötigt werden und welche Serverkapazität für ATA Center und die ATA-Gateways erforderlich ist.

##<a name="using-the-sizing-tool"></a>Verwenden das Tools zur Größenanpassung
Die empfohlene und einfachste Methode zum Ermitteln der Kapazität für die ATA-Bereitstellung besteht in der Verwendung des [ATA-Tools zur Größenanpassung](http://aka.ms/atasizingtool). Führen Sie das ATA-Tool zur Größenanpassung aus, und verwenden Sie aus den Excel-Dateiergebnissen heraus die folgenden Felder zum Ermitteln der benötigten ATA-Kapazität:

- ATA Center-CPU und -Arbeitsspeicher: Gleichen Sie das Feld **Busy Packets/sec** in der ATA Center-Tabelle in der Ergebnisdatei mit dem Feld **PACKETS PER SECOND** in der [ATA Center-Tabelle](#ata-center-sizing) ab.

- ATA Center-Speicher: Gleichen Sie das Feld **Avg Packets/sec** in der ATA Center-Tabelle in der Ergebnisdatei mit dem Feld **PACKETS PER SECOND** in der [ATA Center-Tabelle](#ata-center-sizing) ab.
- ATA-Gateway: Gleichen Sie das Feld **Busy Packets/sec** in der ATA-Gateway-Tabelle in der Ergebnisdatei mit dem Feld **PACKETS PER SECOND** in der [ATA Gateway-Tabelle](#ata-gateway-sizing) oder der [ATA Lightweight Gateway-Tabelle](#ata-lightweight-gateway-sizing) ab, je nach [ausgewähltem Gateway](#choosing-the-right-gateway-type-for-your-deployment).


![Beispiel für das Kapazitätsplanungstool](media/capacity tool.png)



Wenn Sie das ATA-Tool zur Größenanpassung aus irgendeinem Grund nicht verwenden können, müssen Sie die Informationen zum Pakete/Sek.-Leistungsindikator manuell von allen Domänencontrollern über einen Zeitraum von 24 Stunden mit einem sehr niedrigen Erfassungsintervall (etwa 5 Sekunden) sammeln. Anschließend müssen Sie für jeden Domänencontroller den Tagesdurchschnitt und den Durchschnitt der Zeitspanne (15 Minuten) mit der höchsten Auslastung berechnen.
Die folgenden Abschnitte enthalten Anweisungen dazu, wie Sie Informationen zum Pakete/Sek.-Leistungsindikator für einen Domänencontroller sammeln.



### <a name="ata-center-sizing"></a>Größenzuteilung für ATA Center
Für die Analyse des Benutzerverhaltens benötigt das ATA Center die Daten von mindestens 30 Tagen.
 

|Pakete pro Sekunde von allen Domänencontrollern|CPU (Kerne&#42;)|Arbeitsspeicher (GB)|Datenbankspeicher pro Tag (GB)|Datenbankspeicher pro Monat (GB)|IOPS&#42;&#42;|
|---------------------------|-------------------------|-------------------|---------------------------------|-----------------------------------|-----------------------------------|
|1,000|2|32|0.3|9|30 (100)
|10.000|4|48|3|90|200 (300)
|40.000|8|64|12|360|500 (1.000)
|100.000|12|96|30|900|1.000 (1.500)
|400.000|40|128|120|1.800|2.000 (2.500)

&#42;Dies umfasst physische Kerne, keine Hyperthreadingkerne.

&#42;&#42;Durchschnittliche Werte (Spitzenwerte)
> [!NOTE]
> -   ATA Center kann in der Summe aller überwachten Domänencontroller maximal 400.000 Frames pro Sekunde behandeln.
> -   Die hier vorgegebenen Speichermengen sind Nennwerte und sollten stets im Hinblick auf künftiges Wachstum angepasst werden. Das Laufwerk, auf dem sich die Datenbank befindet, sollte mindestens 20 % freien Speicherplatz aufweisen.
> -   Wenn der freie Speicherplatz auf 20 % oder 100 GB fällt, werden die Daten der ältesten Sammlung gelöscht. Dieser Vorgang wird weiter ausgeführt, bis nur noch 5% oder 50 GB an freiem Speicherplatz übrig bleiben. Sobald dies der Fall ist, wird die Datensammlung abgebrochen.
> -   Die Speicherlatenz für Lese- und Schreibvorgänge sollte unter 10 ms betragen.
> -   Das Verhältnis zwischen Schreib- und Lesevorgängen beträgt unterhalb von 100.000 Paketen pro Sekunde etwa 1:3 und oberhalb dieser Grenze etwa 1:6.
> -   Bei Ausführung als virtueller Computer wird kein dynamischer Arbeitsspeicher und keine andere Speichererweiterungsfunktion unterstützt.
> -   Um eine optimale Leistung zu erzielen, legen Sie die **Energieoption** von ATA Center auf **Hohe Leistung** fest.<br>
> -   Wenn Sie auf einem physischen Server arbeiten, erfordert die ATA-Datenbank, dass Sie den nicht einheitlichen Speicherzugriff (Non-Uniform Memory Access, NUMA) im BIOS **deaktivieren**. Das System bezieht sich möglicherweise als Knotenüberlappung auf NUMA. In diesem Fall müssen Sie die Knotenüberlappung **aktivieren**, um NUMA zu deaktivieren. Weitere Informationen finden Sie in der BIOS-Dokumentation. Beachten Sie, dass dies nicht relevant ist, wenn ATA Center auf einem virtuellen Server ausgeführt wird.


## <a name="choosing-the-right-gateway-type-for-your-deployment"></a>Auswählen des richtigen Gatewaytyps für die Bereitstellung
In einer ATA-Umgebung wird jede Kombination der ATA-Gatewaytypen unterstützt:

- Ausschließlich ATA-Gateways
- Ausschließlich ATA-Lightweight-Gateways
- Eine Kombination aus beiden Typen

Berücksichtigen Sie Folgendes bei der Entscheidung für den Bereitstellungstyp für das Gateway:

|Gatewaytyp|Vorteile|Kosten|Bereitstellungstopologie|Domänencontrollerverwendung|
|----|----|----|----|-----|
|ATA-Gateway|Eine Out-of-Band-Bereitstellung erschwert es Angreifern, herauszufinden, ob ATA vorhanden ist.|Höher|Neben dem Domänencontroller installiert (out-of-band).|Unterstützt bis zu 50.000 Pakete pro Sekunde.|
|ATA-Lightweight-Gateway|Erfordert keinen dedizierten Server und keine Konfiguration der Portspiegelung.|Kleinschreibung|Auf dem Domänencontroller installiert.|Unterstützt bis zu 10.000 Pakete pro Sekunde.|

Es folgen Beispiele für Szenarien, in denen Domänencontroller durch das ATA-Lightweight-Gateway abgedeckt werden sollten:


- Filialstandorte

- Virtuelle Domänencontroller, die in der Cloud bereitgestellt wurden (IaaS).


Es folgen Beispiele für Szenarien, in denen Domänencontroller durch das ATA-Gateway abgedeckt werden sollten:


- Rechenzentren an Hauptstandorten (mit Domänencontrollern mit mehr als 10.000 Paketen pro Sekunde).


### <a name="ata-lightweight-gateway-sizing"></a>Dimensionierung von ATA-Lightweight-Gateways

Ein ATA-Lightweight-Gateway kann die Überwachung eines Domänencontrollers basierend auf der Menge des vom Domänencontroller erzeugten Netzwerkverkehrs unterstützen. 


|Pakete pro Sekunde&#42;|CPU (Kerne&#42;&#42;)|Arbeitsspeicher (GB)&#42;&#42;&#42;|
|---------------------------|-------------------------|---------------|
|1,000|2|6|
|5,000|6|16|
    |10.000|10|24|

&#42;Gesamtanzahl der Pakete pro Sekunde auf dem von dem betreffenden ATA-Lightweight-Gateway überwachten Domänencontroller.

&#42;&#42;Gesamtmenge der Kerne ohne Hyperthreading, die auf diesem Domänencontroller installiert sind.<br>Hyperthreading ist zwar für das ATA-Lightweight-Gateway akzeptabel, bei der Kapazitätsplanung sollten Sie aber die tatsächlichen Kernen und nicht die Kerne mit Hyperthreading zählen.

&#42;&#42;&#42;Gesamtgröße des auf diesem Domänencontroller installierten Arbeitsspeichers.

> [!NOTE]   
> -   Wenn der Domänencontroller nicht über die für das ATA-Lightweight-Gateway erforderlichen Ressourcen verfügt, wird die Leistung des Domänencontrollers zwar nicht beeinträchtigt, aber das ATA-Lightweight-Gateway funktioniert möglicherweise nicht wie erwartet.
> -   Bei Ausführung als virtueller Computer wird kein dynamischer Arbeitsspeicher und keine andere Speichererweiterungsfunktion unterstützt.
> -   Um eine optimale Leistung zu erzielen, legen Sie die **Energieoption** des ATA-Lightweight-Gateways auf **Hohe Leistung** fest.
> -   Mindestens 5 GB Speicherplatz wird benötigt, 10 GB wird empfohlen. Dies umfasst den Speicherplatz, der für die ATA-Binärdateien, [ATA-Protokolle](/advanced-threat-analytics/troubleshoot/troubleshooting-ata-using-logs) und [Leistungsprotokolle](/advanced-threat-analytics/troubleshoot/troubleshooting-ata-using-perf-counters) benötigt wird.


### <a name="ata-gateway-sizing"></a>Bemessung von ATA-Gateways

Berücksichtigen Sie Folgendes bei der Entscheidung, wie viele ATA-Gateways bereitgestellt werden sollen.

-   **Active Directory-Gesamtstrukturen und -Domänen**<br>
    ATA kann den Datenverkehr aus mehreren Domänen einer einzigen Active Directory-Gesamtstruktur überwachen. Die Überwachung mehrerer Active Directory-Gesamtstrukturen erfordert separate ATA-Bereitstellungen. Für die Überwachung des Netzwerkdatenverkehrs von Domänencontrollern in unterschiedlichen Gesamtstrukturen sollte keine einzelne ATA-Bereitstellung konfiguriert werden.

-   **Portspiegelung**<br>
Überlegungen zur Portspiegelung machen möglicherweise die Bereitstellung mehrerer ATA-Gateways pro Rechenzentrum oder Filialstandort erforderlich.

-   **Kapazität**<br>
    Ein ATA-Gateway kann die Überwachung von mehreren Domänencontrollern unterstützen, abhängig vom Umfang des Netzwerkverkehrs der überwachten Domänencontroller. 
<br>



|Pakete pro Sekunde&#42;|CPU (Kerne&#42;&#42;)|Arbeitsspeicher (GB)|
|---------------------------|-------------------------|---------------|
|1,000|1|6|
|5,000|2|10|
|10.000|3|12|
|20.000|6|24|
|50.000|16|48|
&#42;Durchschnittliche Gesamtanzahl der Pakete pro Sekunde von allen Domänencontrollern, die von dem betreffenden ATA-Gateway überwacht werden, und zwar zum Zeitpunkt der höchsten Nutzung.

&#42;Die Gesamtmenge des per Portspiegelung verarbeiteten Domänencontroller-Datenverkehrs darf die Kapazität der für das Sammeln verwendeten NIC auf dem ATA-Gateway nicht überschreiten.

&#42;&#42;Hyperthreading muss deaktiviert sein.

> [!NOTE] 
> -   Dynamischer Arbeitsspeicher wird nicht unterstützt.
> -   Um eine optimale Leistung zu erzielen, legen Sie die **Energieoption** des ATA-Gateways auf **Hohe Leistung** fest.
> -   Mindestens 5 GB Speicherplatz wird benötigt, 10 GB wird empfohlen. Dies umfasst den Speicherplatz, der für die ATA-Binärdateien, [ATA-Protokolle](/advanced-threat-analytics/troubleshoot/troubleshooting-ata-using-logs) und [Leistungsprotokolle](/advanced-threat-analytics/troubleshoot/troubleshooting-ata-using-perf-counters) benötigt wird.


## <a name="domain-controller-traffic-estimation"></a>Abschätzung des Datenverkehrs für Domänencontroller
Es gibt verschiedene Tools, die Sie verwenden können, um die durchschnittliche Anzahl der Pakete pro Sekunde eines Domänencontrollers zu ermitteln. Auch ohne den Einsatz solcher Werkzeuge können Sie diesen Leistungsindikator mit dem Systemmonitor ermitteln.

Um die Pakete pro Sekunde zu ermitteln, gehen Sie auf jedem Domänencontroller wie folgt vor:

1.  Öffnen Sie den Systemmonitor.

    ![Abbildung des Systemmonitors](media/ATA-traffic-estimation-1.png)

2.  Erweitern Sie **Datensammlersätze**.

    ![Abbildung der Datensammlersätze](media/ATA-traffic-estimation-2.png)

3.  Klicken Sie mit der rechten Maustaste auf **Benutzerdefiniert**, und wählen Sie **Neu** &gt; **Datensammlersatz** aus.

    ![Abbildung eines neuen Datensammlersatzes](media/ATA-traffic-estimation-3.png)

4.  Geben Sie einen Namen für den Sammlersatz ein, und wählen Sie **Manuell erstellen (Erweitert)** aus.

5.  Wählen Sie unter **Welcher Datentyp soll eingeschlossen werden?** die Option **Datenprotokolle und Leistungsindikator erstellen** aus.

    ![Abbildung für Datentyp des neuen Sammlersatzes](media/ATA-traffic-estimation-5.png)

6.  Klicken Sie unter **Welche Leistungsindikatoren möchten Sie protokollieren?** auf **Hinzufügen**.

7.  Erweitern Sie **Netzwerkadapter**, wählen Sie **Pakete/Sek.** aus, und wählen Sie die richtige Instanz aus. Wenn Sie sich dabei nicht sicher sind, können Sie **&lt;Alle Instanzen&gt;** auswählen und auf **Hinzufügen** und **OK** klicken.

    > [!NOTE]
    > Führen Sie die Befehlszeile `ipconfig /all` aus, um den Namen des Adapters und die Konfiguration zu ermitteln.

    ![Abbildung – Hinzufügen von Leistungsindikatoren](media/ATA-traffic-estimation-7.png)

8.  Ändern Sie das **Abtastintervall** auf **1 Sekunde**.

9. Legen Sie den Speicherort fest, an dem die Daten gespeichert werden sollen.

10. Wählen Sie unter **Neuen Datensammlersatz erstellen** die Option **Diesen Datensammlersatz jetzt starten** aus, und klicken Sie auf **Fertig stellen**.

    Jetzt sollte der gerade erstellte Datensammlersatz mit einem grünen Dreieck als Zeichen der Funktion dargestellt werden.

11. Beenden Sie nach 24 Stunden den Datensammlersatz, indem Sie mit der rechten Maustaste auf das zugehörige Symbol klicken und die Option **Beenden** auswählen.

    ![Abbildung für das Beenden des Datensammlersatzes](media/ATA-traffic-estimation-12.png)

12. Wechseln Sie im Datei-Explorer zu dem Ordner, in dem die BLG-Datei gespeichert wurde, und doppelklicken Sie darauf, um sie im Systemmonitor zu öffnen.

13. Wählen Sie den Leistungsindikator für Pakete/Sekunde aus, und notieren Sie die durchschnittlichen und maximalen Werte.

    ![Abbildung Leistungsindikator für Pakete pro Sekunde](media/ATA-traffic-estimation-14.png)

## <a name="see-also"></a>Siehe auch
- [Voraussetzungen für ATA](ata-prerequisites.md)
- [ATA-Architektur](ata-architecture.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Dec16_HO2-->


