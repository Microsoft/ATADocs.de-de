---
title: 'Tutorial: Playbook zur Microsoft Defender for Identity-Reconnaissance'
description: Das Playbook zur Microsoft Defender for Identity-Reconnaissance beschreibt, wie Sie Reconnaissancebedrohungen zur Erkennung durch Defender for Identity simulieren.
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 25f21451a61f3d41b5694e3b594769e4f8b1614b
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93275770"
---
# <a name="tutorial-reconnaissance-playbook"></a>Tutorial: Playbook zu Reconnaissance

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Das zweite Tutorial in dieser vierteiligen Reihe zu [!INCLUDE [Product long](includes/product-long.md)]-Sicherheitswarnungen ist ein Playbook zur Reconnaissance. Das Lab zu [!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnungen soll die Funktionen von **[!INCLUDE [Product short](includes/product-short.md)]** zum Identifizieren und Erkennen verdächtiger Aktivitäten und potenzieller Angriffe auf Ihr Netzwerk veranschaulichen. In diesem Playbook wird das Testen der *diskreten* Erkennungen von [!INCLUDE [Product short](includes/product-short.md)] erläutert. Der Fokus liegt dabei auf den *signaturbasierten* Funktionen von [!INCLUDE [Product short](includes/product-short.md)]. Dieses Playbook enthält keine Warnungen oder Verhaltenserkennungen auf Basis des erweiterten Machine Learning, auf Benutzer- oder Entitätsbasis, da sie eine Lernphase mit echtem Netzwerkverkehr von bis zu 30 Tagen erfordern. Weitere Informationen zu den einzelnen Tutorials dieser Reihe finden Sie unter [Tutorialübersicht: [!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnungsumgebung](playbook-lab-overview.md).

Dieses Playbook veranschaulicht die Dienste von [!INCLUDE [Product short](includes/product-short.md)] für Bedrohungserkennungen und Sicherheitswarnungen anhand von simulierten Angriffen durch allgemeine, reale und öffentlich verfügbare Hacker- und Angriffstools.

Inhalt des Tutorials:

> [!div class="checklist"]
>
> - Simulieren der Netzwerkzuordnungs-Reconnaissance
> - Simulieren der Verzeichnisdienstreconnaissance
> - Simulieren von Benutzer- und IP-Adressenreconnaissance (SMB)
> - Überprüfen der Sicherheitswarnungen aus der simulierten Reconnaissance in [!INCLUDE [Product short](includes/product-short.md)]

## <a name="prerequisites"></a>Voraussetzungen

[Ein vollständiges [!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnungslab](playbook-setup-lab.md)

- Sie sollten die Setupanweisungen für die Testumgebung genau einhalten. Je genauer Ihr Lab dem vorgeschlagenen Labsetup entspricht, desto einfacher können Sie die [!INCLUDE [Product short](includes/product-short.md)]-Testverfahren befolgen.

## <a name="simulate-a-reconnaissance-attack"></a>Simulieren eines Reconnaissanceangriffs

Wenn ein Angreifer die Präsenz in Ihrer Umgebung erlangt, beginnt die Reconnaissancekampagne. In dieser Phase wird der Angreifer in der Regel Zeit mit Nachforschungen verbringen. Er versucht, den gewünschten Computer zu entdecken, Benutzer und Gruppen aufzulisten, wichtige IP-Adressen zu sammeln und die Ressourcen und Schwächen Ihrer Organisation einzuschätzen. Mit Reconnaissanceaktivitäten können Angreifer umfassende Kenntnisse und eine vollständige Zuordnung Ihrer Umgebung für die spätere Verwendung erzielen.

Testverfahren für Reconnaissanceangriffe:

- Reconnaissance über Netzwerkzuordnung
- Verzeichnisdienstreconnaissance
- Benutzer- und IP-Adressenreconnaissance (SMB)

## <a name="network-mapping-reconnaissance-dns"></a>Network-mapping reconnaissance (DNS) (Reconnaissance über Netzwerkzuordnung (DNS))

Zuerst wird ein Angreifer u.a. versuchen, eine Kopie aller DNS-Informationen zu erhalten. Bei erfolgreicher Ausführung erhält der Angreifer umfangreiche Informationen über Ihre Umgebung, die möglicherweise ähnliche Informationen zu Ihren sonstigen Umgebungen oder Netzwerken umfassen.

[!INCLUDE [Product short](includes/product-short.md)] unterdrückt Aktivitäten zur Netzwerkzuordnungs-Reconnaissance auf Ihrer **Zeitachse für verdächtige Aktivitäten** , bis eine Lernphase von acht Tagen abgeschlossen ist. In der Lernphase lernt [!INCLUDE [Product short](includes/product-short.md)], was in Ihrem Netzwerk normal und was ungewöhnlich ist. Nach der achttägigen Lernphase lösen ungewöhnliche Ereignisse der Netzwerkzuordnungs-Reconnaissance die entsprechende Sicherheitswarnung aus.

### <a name="run-nslookup-from-victimpc"></a>Ausführen von nslookup auf VictimPC

Um die DNS-Reconnaissance zu testen, verwenden wir das native Befehlszeilentool *nslookup* , um eine DNS-Zonenübertragung zu initiieren. DNS-Server mit der richtigen Konfiguration verweigern Abfragen dieses Typs und gestatten den Versuch der Zonenübertragung nicht.

Melden Sie sich mit den kompromittierten JeffL-Anmeldeinformationen bei **VictimPC** an. Führen Sie den folgenden Befehl aus:

```dos
nslookup
```

Geben Sie **server** und anschließend den vollqualifizierten Domänenname oder die IP-Adresse des Domänencontrollers ein, auf dem der [!INCLUDE [Product short](includes/product-short.md)]-Sensor installiert ist.

```nslookup
server contosodc.contoso.azure
```

Probieren Sie, die Domäne zu übertragen.

```nslookup
ls -d contoso.azure
```

- Ersetzen Sie „contosodc.contoso.azure“ und „contoso.azure“ durch den vollqualifizierten Domänenname Ihres [!INCLUDE [Product short](includes/product-short.md)]-Sensors bzw. durch den Domänennamen.

 ![nslookup-Befehlsversuch zum Kopieren des DNS-Serversfehlers](media/playbook-recon-nslookup.png)

Wenn **ContosoDC** Ihr erster bereitgestellter Sensor ist, warten Sie 15 Minuten, bis das Datenbank-Back-End die Bereitstellung der erforderlichen Microservices beendet hat.

### <a name="network-mapping-reconnaissance-dns-detected-in-product-short"></a>Reconnaissance über Netzwerkzuordnung (DNS) in [!INCLUDE [Product short](includes/product-short.md)] erkannt

Das Abrufen der Sichtbarkeit dieses Versuchstyps (fehlerhaft oder erfolgreich) ist entscheidend für den Domänenbedrohungsschutz. Nachdem Sie die Umgebung installiert haben, müssen Sie zur Zeitachse **Logische Aktivitäten** wechseln, um die erkannte Aktivität anzuzeigen.

Geben Sie in der [!INCLUDE [Product short](includes/product-short.md)]-Suche den Suchbegriff **VictimPC** ein, und klicken Sie dann darauf, um die Zeitachse anzuzeigen.

![Von [!INCLUDE [Product short](includes/product-short.md)] erkannte DNS-Reconnaissance, allgemeine Ansicht](media/playbook-recon-nslookupdetection1.png)

Suchen Sie nach der Aktivität „AXFR query“. [!INCLUDE [Product short](includes/product-short.md)] erkennt diese Art von Reconnaissanceangriffen auf Ihr DNS.

- Wenn viele Aktivitäten vorhanden sind, klicken Sie auf **Filtern nach** , und deaktivieren Sie alle Typen außer **DNS-Abfrage**.

![Detailansicht der Erkennung der DNS-Reconnaissance in [!INCLUDE [Product short](includes/product-short.md)]](media/playbook-recon-nslookupdetection2.png)

Wenn Ihr Sicherheitsanalyst festgestellt hat, dass diese Aktivität von einem Sicherheitsscanner stammt, kann dieses Gerät von weiteren Erkennungswarnungen ausgeschlossen werden. Klicken Sie im oberen rechten Bereich der Warnung auf die drei Punkte. Wählen Sie dann **MySecurityScanner schließen und ausschließen** aus. Stellen Sie sicher, dass diese Warnung nicht wieder bei Erkennung von „MySecurityScanner“ angezeigt wird.

Das Erkennen von Fehlern kann genauso aufschlussreich sein wie das Erkennen erfolgreicher Angriffe auf eine Umgebung. Das [!INCLUDE [Product short](includes/product-short.md)]-Portal zeigt uns das genaue Ergebnis der Aktionen eines potenziellen Angreifers. In unserem simulierten DNS-Reconnaissanceangriffsszenario wurden wir – als Angreifer agierend – daran gehindert, die DNS-Einträge der Domäne zu speichern. Ihr SecOps-Team wurde von der [!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnung auf unseren Angriffsversuch und den Computer aufmerksam gemacht, den wir in unserem Versuch verwendet haben.

## <a name="directory-service-reconnaissance"></a>Verzeichnisdienstreconnaissance

Das nächste Reconnaissanceziel eines Angreifers ist der Versuch, alle Benutzer und Gruppen in der Gesamtstruktur aufzulisten. [!INCLUDE [Product short](includes/product-short.md)] unterdrückt Enumerationsaktivitäten des Verzeichnisdiensts auf Ihrer Zeitachse für verdächtige Aktivitäten, bis eine Lernzeitphase von 30 Tagen abgeschlossen ist. In der Lernphase lernt [!INCLUDE [Product short](includes/product-short.md)], was in Ihrem Netzwerk normal und was ungewöhnlich ist. Nach Ablauf des Lernzeitraums von 30 Tagen rufen ungewöhnliche Verzeichnisdienstenumerations-Ereignisse eine Sicherheitswarnung auf. Während der 30-tägigen Lernphase können Sie [!INCLUDE [Product short](includes/product-short.md)]-Erkennungen dieser Aktivitäten mithilfe der Aktivitätszeitachse einer Entität in Ihrem Netzwerk sehen. Die [!INCLUDE [Product short](includes/product-short.md)]-Erkennungen solcher Aktivitäten werden in diesem Lab gezeigt.

Um eine gängige Verzeichnisdienst-Reconnaissancemethode zu demonstrieren, verwenden wir die native Binärdatei *net* von Microsoft. Nach unserem Versuch ist auf der Aktivitätszeitachse unseres gefährdeten Benutzers JeffL zu erkennen, dass [!INCLUDE [Product short](includes/product-short.md)] diese Aktivität erkannt hat.

### <a name="directory-service-enumeration-via-net-from-victimpc"></a>Verzeichnisdienstenumeration über *net* von VictimPC aus

Alle authentifizierten Benutzer oder Computer können potenziell andere Benutzer und Gruppen in einer Domäne auflisten. Diese Enumerationsfähigkeit ist erforderlich, damit die meisten Anwendungen ordnungsgemäß funktionieren. Unser gefährdeter Benutzer JeffL ist ein Domänenkonto ohne Privilegien. Bei diesem simulierten Angriff sehen wir genau, wie auch ein nicht privilegiertes Domänenkonto einem Angreifer immer noch wertvolle Datenpunkte liefern kann.

1. Führen Sie auf **VictimPC** den folgenden Befehl aus:

    ```dos
    net user /domain
    ```

    Die Ausgabe zeigt alle Benutzer in der Domäne Contoso.Azure.

    ![Auflisten aller Benutzer in der Domäne](media/playbook-recon-dsenumeration-netusers.png)

1. Probieren Sie, alle Gruppen in der Domäne aufzulisten. Führen Sie den folgenden Befehl aus:

    ```dos
    net group /domain
    ```

    Die Ausgabe zeigt alle Gruppen in der Domäne Contoso.Azure. Beachten Sie die eine Sicherheitsgruppe, die keine Standardgruppe ist: **Helpdesk**.

    ![Auflisten aller Gruppen in der Domäne](media/playbook-recon-dsenumeration-netgroups.png)

1. Versuchen Sie nun, nur die Domänen-Admins-Gruppe aufzulisten. Führen Sie den folgenden Befehl aus:

    ```dos
    net group "Domain Admins" /domain
    ```

    ![Auflisten aller Mitglieder der Gruppe „Domänen-Admins“](media/playbook-recon-dsenumeration-netdomainadmins.png)

    Als Angreifer haben wir gelernt, dass es zwei Mitglieder der Gruppe „Domänen-Admins“ gibt: **SamiraA** und **ContosoAdmin** (integrierter Administrator für den Domänencontroller). Wissend, dass keine Sicherheitsgrenze zwischen unserer Domäne und der Gesamtstruktur vorhanden ist, versuchen Sie im nächsten Schritt, die Organisations-Admins aufzulisten.

1. Um zu versuchen, Organisations-Admins aufzulisten, führen Sie den folgenden Befehl aus:

    ```dos
    net group "Enterprise Admins" /domain
    ```

    Wir haben gelernt, dass es nur einen Organisations-Admin gibt, und zwar ContosoAdmin. Diese Information war nicht wichtig, da wir bereits wussten, dass es keine Sicherheitsbegrenzung zwischen unserer Domäne und der Gesamtstruktur gibt.

    ![Organisations-Admins in der Domäne aufgelistet](media/playbook-recon-dsenumeration-netenterpriseadmins.png)

Dank der im Rahmen unserer Reconnaissance gesammelten Informationen kennen wir nun die Sicherheitsgruppe „Helpdesk“. Diese Information ist *noch* nicht interessant. Wir wissen auch, dass **SamiraA** Mitglied der Gruppe „Domänen-Admins“ ist. Wenn wir die Anmeldeinformationen von SamiraA stehlen können, können wir auf den Domänencontroller selbst zugreifen.

### <a name="directory-service-enumeration-detected-in-product-short"></a>Verzeichnisdienstenumeration in [!INCLUDE [Product short](includes/product-short.md)] erkannt

Wenn in unserem Lab *bei installiertem [!INCLUDE [Product short](includes/product-short.md)] 30 Tage lang echte Aktivitäten* stattfänden, würde die Aktivität, die wir eben als JeffL durchgeführt haben, wahrscheinlich als nicht ordnungsgemäß klassifiziert. Ungewöhnliche Aktivitäten würden in der Zeitachse für verdächtige Aktivitäten angezeigt. Da wir jedoch gerade die Umgebung installiert haben, müssen wir die Zeitachse logischer Aktivitäten beobachten.

Über die [!INCLUDE [Product short](includes/product-short.md)]-Suche rufen wir die Zeitachse der logischen Aktivitäten von JeffL auf:

![Suchen der Zeitachse logischer Aktivitäten für eine bestimmte Entität](media/playbook-recon-dsenumeration-searchlogicalactivity.png)

Wir können sehen, wann JeffL sich bei VictimPC mithilfe des Kerberos-Protokolls angemeldet hat. Darüber hinaus sehen wir, dass JeffL von VictimPC aus alle Benutzer in der Domäne aufgelistet hat.

![Die Zeitachse logischer Aktivitäten von JeffL](media/playbook-recon-dsenumeration-jeffvlogicalactivity.png)

Viele Aktivitäten werden in der Zeitachse logischer Aktivitäten protokolliert, sodass ihr eine wichtige Funktion bei der DFIR-Ausführung (Digital Forensics and Incident Response) zukommt. Sie können sogar Aktivitäten anzeigen, deren erste Erkennung nicht durch [!INCLUDE [Product short](includes/product-short.md)], sondern durch Microsoft Defender ATP, Microsoft 365 und andere Dienste erfolgte.

Bei einem Blick auf die **ContosoDC-Seite** sehen wir auch die Computer, bei denen JeffL angemeldet ist.

![Computer, bei denen JeffL angemeldet ist](media/playbook-recon-dsenumeration-jeffvloggedin.png)

Wir können aus [!INCLUDE [Product short](includes/product-short.md)] auch Verzeichnisdaten abrufen, einschließlich der Mitgliedschaften und Zugriffssteuerungen von JeffL.

![Verzeichnisdaten von JeffL in [!INCLUDE [Product short](includes/product-short.md)]](media/playbook-recon-dsenumeration-jeffvdirectorydata.png)

Nun richtet sich unsere Aufmerksamkeit auf die SMB-Sitzungsenumeration.

## <a name="user-and-ip-address-reconnaissance-smb"></a>Reconnaissance über Benutzer und IP-Adressen (SMB)

Der Active Directory-Ordner **sysvol** ist eine sehr wichtige Netzwerkfreigaben in der Umgebung – wenn nicht sogar die *wichtigste*. Alle Computer und Benutzer müssen auf diese bestimmte Netzwerkfreigabe zugreifen können, um Gruppenrichtlinien zu pullen. Für einen Angreifer kann die Auflistung, wer aktive Sitzungen mit dem Ordner „sysvol“ hat, eine wahre Goldmine an Informationen sein.

Im nächsten Schritt führen wir die SMB-Sitzungsenumeration für die ContosoDC-Ressource durch. Wir möchten erfahren, welche weiteren Personen Sitzungen mit der SMB-Freigabe haben, und *über welche IP*.

### <a name="use-joewares-netsessexe-from-victimpc"></a>Verwenden von „NetSess.exe“ von JoeWare auf VictimPC

Führen Sie das Tool **NetSess** von JoeWare für ContosoDC im Kontext eines authentifizierten Benutzers aus, in diesem Fall ContosoDC:

```dos
NetSess.exe ContosoDC
```

![Angreifer verwenden SMB-Reconnaissance, um Benutzer und ihre IP-Adressen zu identifizieren](media/playbook-recon-smbrecon.png)

Wir wissen bereits, dass SamiraA Domänenadministratorin ist. Dieser Angriff lieferte uns die IP-Adresse von SamiraA – 10.0.24.6. Als Angreifer haben wir genau erfahren, wenn wir gefährden müssen. Wir haben auch den Netzwerkspeicherort erfahren, wo die Anmeldung mit diesen Anmeldeinformationen erfolgt.

### <a name="user-and-ip-address-reconnaissance-smb-detected-in-product-short"></a>Reconnaissance von Benutzern und IP-Adressen (SMB) in [!INCLUDE [Product short](includes/product-short.md)] erkannt

Jetzt sehen wir, was [!INCLUDE [Product short](includes/product-short.md)] für uns erkannt hat:

![[!INCLUDE [Product short](includes/product-short.md)] bei der Erkennung der SMB-Reconnaissance](media/playbook-recon-smbrecon-detection1.png)

Wir werden nicht nur vor dieser Aktivität gewarnt, sondern auch bezüglich der offengelegten Konten und der entsprechenden IP-Adressen *zu diesem Zeitpunkt*. Als Security Operations Center (SOC) möchten wir nicht nur über den Versuch und seinen Status informiert werden, sondern auch darüber, was an den Angreifer zurückgesendet wurde. Diese Informationen unterstützen unsere Untersuchung.

## <a name="next-steps"></a>Nächste Schritte

Die nächste Phase in der Kette der Angriffsabwehr ist in der Regel Lateral Movement.

> [!div class="nextstepaction"]
> [[!INCLUDE [Product short](includes/product-short.md)]-Playbook zu Lateral Movement](playbook-lateral-movement.md)

## <a name="join-the-community"></a>Beitritt zur Community

Haben Sie weitere Fragen, oder möchten Sie mit anderen über [!INCLUDE [Product short](includes/product-short.md)] und damit verbundene Sicherheitsaspekte diskutieren? Werden Sie Teil der [[!INCLUDE [Product short](includes/product-short.md)]Community](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection)!
