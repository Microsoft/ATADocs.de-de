---
title: Tutorial für das Playbook zu Azure ATP-Reconnaissance | Microsoft-Dokumentation
description: Im Tutorial für das Playbook zu Azure ATP-Reconnaissance wird das Simulieren von Reconnaissancebedrohungen für die Erkennung durch Azure ATP beschrieben.
ms.service: azure-advanced-threat-protection
ms.topic: tutorial
author: mlottner
ms.author: mlottner
ms.date: 03/03/2019
ms.reviewer: itargoet
ms.openlocfilehash: 20e91bc710dc184fa710cf7fd59cb9bd9d625d20
ms.sourcegitcommit: 929f28783110c7e114ab36d4cccd50563f4030df
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/04/2019
ms.locfileid: "57253962"
---
# <a name="tutorial-reconnaissance-playbook"></a>Tutorial: Playbook zu Reconnaissance

Das zweite Tutorial in dieser vierteiligen Reihe zu Azure ATP-Sicherheitswarnungen ist ein Playbook zu Reconnaissance. Die Azure ATP-Sicherheitswarnungsumgebung soll die Funktionen von **Azure ATP** zum Identifizieren und Erkennen verdächtiger Aktivitäten und potenzieller Angriffe auf Ihr Netzwerk veranschaulichen. Das Playbook erläutert das Testen der *diskreten* Erkennungen von Azure ATP und konzentriert sich auf die *signaturbasierten* Funktionen von Azure ATP. Dieses Playbook enthält keine Warnungen oder Verhaltenserkennungen auf Basis des erweiterten Machine Learning, auf Benutzer- oder Entitätsbasis, da sie eine Lernphase mit echtem Netzwerkverkehr von bis zu 30 Tagen erfordern. Weitere Informationen über jedes Tutorial dieser Reihe finden Sie unter [Tutorialübersicht: ATP-Sicherheitswarnungsumgebung](atp-playbook-lab-overview.md).

Dieses Playbook veranschaulicht die Bedrohungserkennungen und Sicherheitswarnungen von Azure ATP für simulierte Angriffe durch allgemeine, reale, öffentlich verfügbare Hacker- und Angriffstools vor.

Inhalt des Tutorials:
> [!div class="checklist"]
> * Simulieren der Netzwerkzuordnungs-Reconnaissance
> * Simulieren der Verzeichnisdienstreconnaissance
> * Simulieren von Benutzer- und IP-Adressenreconnaissance (SMB)
> * Überprüfen der Sicherheitswarnungen von der simulierten Reconnaissance in Azure ATP

## <a name="prerequisites"></a>Voraussetzungen

[Eine vollständige ATP-Sicherheitswarnungsumgebung](atp-playbook-setup-lab.md)
  - Sie sollten die Setupanweisungen für die Testumgebung genau einhalten. Je mehr Ihre Testumgebung dem vorgeschlagenen Testumgebungssetup entspricht, desto einfacher können Sie die Azure ATP-Testverfahren befolgen.

## <a name="simulate-a-reconnaissance-attack"></a>Simulieren eines Reconnaissanceangriffs

Wenn ein Angreifer die Präsenz in Ihrer Umgebung erlangt, beginnt die Reconnaissancekampagne. In dieser Phase wird der Angreifer in der Regel Zeit mit Nachforschungen verbringen. Er versucht, den gewünschten Computer zu entdecken, Benutzer und Gruppen aufzulisten, wichtige IP-Adressen zu sammeln und die Ressourcen und Schwächen Ihrer Organisation einzuschätzen. Mit Reconnaissanceaktivitäten können Angreifer umfassende Kenntnisse und eine vollständige Zuordnung Ihrer Umgebung für die spätere Verwendung erzielen.

Testverfahren für Reconnaissanceangriffe:

* Reconnaissance über Netzwerkzuordnung
* Verzeichnisdienstreconnaissance
* Benutzer- und IP-Adressenreconnaissance (SMB)

## <a name="network-mapping-reconnaissance-dns"></a>Network-mapping reconnaissance (DNS) (Reconnaissance über Netzwerkzuordnung (DNS))

Zuerst wird ein Angreifer u.a. versuchen, eine Kopie aller DNS-Informationen zu erhalten. Bei erfolgreicher Ausführung erhält der Angreifer umfangreiche Informationen über Ihre Umgebung, die möglicherweise ähnliche Informationen zu Ihren sonstigen Umgebungen oder Netzwerken umfassen.

### <a name="run-nslookup-from-victimpc"></a>Ausführen von nslookup auf VictimPC

Um die DNS-Reconnaissance zu testen, verwenden wir das native Befehlszeilentool *nslookup*, um eine DNS-Zonenübertragung zu initiieren. DNS-Server mit der richtigen Konfiguration verweigern Abfragen dieses Typs und gestatten den Versuch der Zonenübertragung nicht.  

Melden Sie sich mit den kompromittierten JeffL-Anmeldeinformationen bei **VictimPC** an. Führen Sie den folgenden Befehl aus:

``` cmd
nslookup
```

Geben Sie **server** und anschließend den FQDN oder die IP-Adresse des DC ein, auf dem der ATP-Sensor installiert ist.

```nslookup
server contosodc.contoso.azure
```

Probieren Sie, die Domäne zu übertragen.

```nslookup
ls -d contoso.azure
```

- Ersetzen Sie contosodc.contoso.azure und contoso.azure durch den FQDN Ihres Azure ATP-Sensors bzw. durch den Domänennamen.

 ![nslookup-Befehlsversuch zum Kopieren des DNS-Serversfehlers](media/playbook-recon-nslookup.png)

Wenn **ContsoDC** Ihr erster bereitgestellter Sensor ist, warten Sie 15 Minuten, bis das Datenbank-Back-End das Bereitstellen der erforderlichen Microservices beendet hat.

### <a name="network-mapping-reconnaissance-dns-detected-in-azure-atp"></a>Reconnaissance über Netzwerkzuordnung (DNS) in Azure ATP erkannt

Das Abrufen der Sichtbarkeit dieses Versuchstyps (fehlerhaft oder erfolgreich) ist entscheidend für den Domänenbedrohungsschutz. Da wir gerade die Umgebung installiert haben, müssen wir die Aktivität auf der Zeitachse logischer Aktivitäten beobachten. 

Geben Sie in der Azure ATP-Suche **VictimPC** ein, und klicken Sie dann darauf, um die Zeitachse anzuzeigen.

![DNS-Reconnaissance von AATP erkannt, Übersicht](media/playbook-recon-nslookupdetection1.png)

Suchen Sie nach der Aktivität „AXFR query“. Azure ATP erkennt diese Art von Reconnaissance gegen Ihr DNS. 
  - Klicken Sie bei einer großen Anzahl von Aktivitäten auf **Filtern nach**, und deaktivieren Sie alle Typen außer „DNS-Abfrage“.

![Detaillierte Ansicht der DNS-Reconnaissanceerkennung in AATP](media/playbook-recon-nslookupdetection2.png)

Wenn Ihr Sicherheitsanalyst festgestellt hat, dass diese Aktivität von einem Sicherheitsscanner stammt, kann dieses Gerät von weiteren Erkennungswarnungen ausgeschlossen werden. Klicken Sie im oberen rechten Bereich der Warnung auf die drei Punkte. Wählen Sie dann **MySecurityScanner schließen und ausschließen** aus. Stellen Sie sicher, dass diese Warnung nicht wieder bei Erkennung von „MySecurityScanner“ angezeigt wird.

Das Erkennen von Fehlern kann genauso aufschlussreich sein wie das Erkennen erfolgreicher Angriffe auf eine Umgebung. Das Azure ATP-Portal zeigt uns das genaue Ergebnis der Aktionen eines potenziellen Angreifers. In unserem simulierten DNS-Reconnaissanceangriffsszenario wurden wir – als Angreifer agierend – daran gehindert, die DNS-Einträge der Domäne zu speichern. Ihr SecOps-Team wurde von der Azure ATP-Sicherheitswarnung auf unseren Angriffsversuch aufmerksam gemacht, und auf den Computer, den wir in unserem Versuch verwendeten.

## <a name="directory-service-reconnaissance"></a>Verzeichnisdienstreconnaissance

Das nächste Reconnaissanceziel eines Angreifers ist der Versuch, alle Benutzer und Gruppen in der Gesamtstruktur aufzulisten. Azure ATP unterdrückt Verzeichnisdienstenumerations-Aktivität von Ihrer Zeitachse für verdächtige Aktivitäten, bis ein Lernzeitraum von 30 Tagen abgeschlossen ist. In der Lernphase lernt Azure ATP, was in Ihrem Netzwerk normal und ungewöhnlich ist. Nach Ablauf des Lernzeitraums von 30 Tagen rufen ungewöhnliche Verzeichnisdienstenumerations-Ereignisse eine Sicherheitswarnung auf. Während des Lernzeitraums von 30 Tagen können Sie Azure ATP-Erkennungen dieser Aktivitäten mithilfe der Aktivitätszeitachse einer Entität in Ihrem Netzwerk sehen. Der Azure ATP-Erkennungen dieser Aktivitäten werden in dieser Testumgebung angezeigt.

Um eine gängige Verzeichnisdienst-Reconnaissancemethode zu demonstrieren, verwenden wir die native Binärdatei *net* von Microsoft. Nach unserem Versuch ist auf der Aktivitätszeitachse unseres gefährdeten Benutzers JeffL zu erkennen, dass Azure ATP diese Aktivität erkannt hat.

### <a name="directory-service-enumeration-via-net-from-victimpc"></a>Verzeichnisdienstenumeration über *net* von VictimPC aus

Alle authentifizierten Benutzer oder Computer können potenziell andere Benutzer und Gruppen in einer Domäne auflisten. Diese Enumerationsfähigkeit ist erforderlich, damit die meisten Anwendungen ordnungsgemäß funktionieren. Unser gefährdeter Benutzer JeffL ist ein Domänenkonto ohne Privilegien. Bei diesem simulierten Angriff sehen wir genau, wie auch ein nicht privilegiertes Domänenkonto einem Angreifer immer noch wertvolle Datenpunkte liefern kann.

1. Führen Sie auf **VictimPC** den folgenden Befehl aus:

    ``` cmd
    net user /domain
    ```

   Die Ausgabe zeigt alle Benutzer in der Domäne Contoso.Azure.

   ![Auflisten aller Benutzer in der Domäne](media/playbook-recon-dsenumeration-netusers.png)

2. Probieren Sie, alle Gruppen in der Domäne aufzulisten. Führen Sie den folgenden Befehl aus:

    ``` cmd
    net group /domain
    ```

   Die Ausgabe zeigt alle Gruppen in der Domäne Contoso.Azure. Beachten Sie die eine Sicherheitsgruppe, die keine Standardgruppe ist: **Helpdesk**.

   ![Auflisten aller Gruppen in der Domäne](media/playbook-recon-dsenumeration-netgroups.png)

3. Versuchen Sie nun, nur die Domänen-Admins-Gruppe aufzulisten. Führen Sie den folgenden Befehl aus:

    ``` cmd
    net group "Domain Admins" /domain
    ```

   ![Auflisten aller Mitglieder der Gruppe „Domänen-Admins“](media/playbook-recon-dsenumeration-netdomainadmins.png)

    Als Angreifer haben wir gelernt, dass es zwei Mitglieder der Gruppe „Domänen-Admins“ gibt: **SamiraA** und **ContosoAdmin** (integrierter Administrator für den Domänencontroller). Wissend, dass keine Sicherheitsgrenze zwischen unserer Domäne und der Gesamtstruktur vorhanden ist, versuchen Sie im nächsten Schritt, die Organisations-Admins aufzulisten.

4. Um zu versuchen, Organisations-Admins aufzulisten, führen Sie den folgenden Befehl aus:

    ``` cmd
   net group "Enterprise Admins" /domain
   ```

   Wir haben gelernt, dass es nur einen Organisations-Admin gibt, und zwar ContosoAdmin. Diese Information war nicht wichtig, da wir bereits wussten, dass es keine Sicherheitsbegrenzung zwischen unserer Domäne und der Gesamtstruktur gibt.

   ![Organisations-Admins in der Domäne aufgelistet](media/playbook-recon-dsenumeration-netenterpriseadmins.png)

Dank der im Rahmen unserer Reconnaissance gesammelten Informationen kennen wir nun die Sicherheitsgruppe „Helpdesk“. Diese Information ist *noch* nicht interessant. Wir wissen auch, dass **SamiraA** Mitglied der Gruppe „Domänen-Admins“ ist. Wenn wir die Anmeldeinformationen von SamiraA stehlen können, können wir auf den Domänencontroller selbst zugreifen.

### <a name="directory-service-enumeration-detected-in-azure-atp"></a>Verzeichnisdienstenumeration in Azure ATP erkannt

Wenn in unserer Testumgebung *echte Liveaktivität für 30 Tage mit Azure ATP-Installation* stattfände, würde die Aktivität, die wir eben als JeffL durchgeführt haben, möglicherweise als nicht ordnungsgemäß klassifiziert werden. Ungewöhnliche Aktivitäten würden in der Zeitachse für verdächtige Aktivitäten angezeigt. Da wir jedoch gerade die Umgebung installiert haben, müssen wir die Zeitachse logischer Aktivitäten beobachten.

Über die Azure ATP-Suche rufen wir die Zeitachse logischer Aktivitäten von JeffL auf:

![Suchen der Zeitachse logischer Aktivitäten für eine bestimmte Entität](media/playbook-recon-dsenumeration-searchlogicalactivity.png)

Wir können sehen, wann JeffL sich bei VictimPC mithilfe des Kerberos-Protokolls angemeldet hat. Darüber hinaus sehen wir, dass JeffL von VictimPC aus alle Benutzer in der Domäne aufgelistet hat.

![Die Zeitachse logischer Aktivitäten von JeffL](media/playbook-recon-dsenumeration-jeffvlogicalactivity.png)

Viele Aktivitäten werden in der Zeitachse logischer Aktivitäten protokolliert, sodass ihr eine wichtige Funktion bei der DFIR-Ausführung (Digital Forensics and Incident Response) zukommt. Sie können auch Aktivitäten sehen, wenn die anfängliche Erkennung nicht durch Azure ATP, sondern Windows Defender ATP, Office 365 und andere erfolgte.

Bei einem Blick auf die **ContosoDC-Seite** sehen wir auch die Computer, bei denen JeffL angemeldet ist.

![Computer, bei denen JeffL angemeldet ist](media/playbook-recon-dsenumeration-jeffvloggedin.png)

Wir können auch Verzeichnisdaten, einschließlich der Mitgliedschaften und Zugriffssteuerungen von JeffL, von Azure ATP abrufen.

![Die Verzeichnisdaten von JeffL in AATP](media/playbook-recon-dsenumeration-jeffvdirectorydata.png)

Nun richtet sich unsere Aufmerksamkeit auf die SMB-Sitzungsenumeration.

## <a name="user-and-ip-address-reconnaissance-smb"></a>Reconnaissance über Benutzer und IP-Adressen (SMB)

Der Active Directory-Ordner „sysvol“ ist eine der wichtigsten Netzwerkfreigaben in der Umgebung – wenn nicht sogar die *wichtigste*. Alle Computer und Benutzer müssen auf diese bestimmte Netzwerkfreigabe zugreifen können, um Gruppenrichtlinien zu pullen. Für einen Angreifer kann die Auflistung, wer aktive Sitzungen mit dem Ordner „sysvol“ hat, eine wahre Goldmine an Informationen sein.

Im nächsten Schritt führen wir die SMB-Sitzungsenumeration für die ContosoDC-Ressource durch. Wir möchten erfahren, welche weiteren Personen Sitzungen mit der SMB-Freigabe haben, und *über welche IP*.

### <a name="use-joewares-netsessexe-from-victimpc"></a>Verwenden von „NetSess.exe“ von JoeWare auf VictimPC

Führen Sie das Tool **NetSess** von JoeWare für ContosoDC im Kontext eines authentifizierten Benutzers aus, in diesem Fall ContosoDC:

``` cmd
NetSess.exe ContosoDC
```

![Angreifer verwenden SMB-Reconnaissance, um Benutzer und ihre IP-Adressen zu identifizieren](media/playbook-recon-smbrecon.png)

Wir wissen bereits, dass SamiraA Domänenadministratorin ist. Dieser Angriff lieferte uns die IP-Adresse von SamiraA – 10.0.24.6. Als Angreifer haben wir genau erfahren, wenn wir gefährden müssen. Wir haben auch den Netzwerkspeicherort erfahren, wo die Anmeldung mit diesen Anmeldeinformationen erfolgt.

### <a name="user-and-ip-address-reconnaissance-smb-detected-in-azure-atp"></a>Reconnaissance von Benutzern und IP-Adressen (SMB) in Azure ATP erkannt

Jetzt sehen wir, was Azure ATP für uns erkannt hat:

![Erkennen der SMB-Reconnaissance durch AATP](media/playbook-recon-smbrecon-detection1.png)

Wir werden nicht nur vor dieser Aktivität gewarnt, sondern auch bezüglich der offengelegten Konten und der entsprechenden IP-Adressen *zu diesem Zeitpunkt*. Als Security Operations Center (SOC) möchten wir nicht nur über den Versuch und seinen Status informiert werden, sondern auch darüber, was an den Angreifer zurückgesendet wurde. Diese Informationen unterstützen unsere Untersuchung.


## <a name="next-steps"></a>Nächste Schritte

Die nächste Phase in der Kette der Angriffsabwehr ist in der Regel Lateral Movement.

> [!div class="nextstepaction"]
> [Playbook zu Azure ATP-Lateral Movement](atp-playbook-lateral-movement.md)

## <a name="join-the-community"></a>Beitritt zur Community

Haben Sie weitere Fragen, oder möchten Sie mit anderen über Azure ATP und damit verbundene Sicherheitsaspekte diskutieren? Treten Sie noch heute der [Azure ATP-Community](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) bei!

