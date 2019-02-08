---
title: Sicherheitswarnungen zur Reconnaissancephase in Azure ATP | Microsoft-Dokumentation
d|Description: This article explains the Azure ATP alerts issued when attacks typically part of reconnaissance phase efforts are detected against your organization.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 02/04/2019
ms.topic: tutorial
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: e9cf68d2-36bd-4b0d-b36e-7cf7ded2618e
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: c8e4d9fbc094e5bd1b58253b771cb5d693b7361c
ms.sourcegitcommit: 9236d279f5e01424b498ce23e9d84c407ebfcdf3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/04/2019
ms.locfileid: "55689301"
---
# <a name="tutorial-reconnaissance-alerts"></a>Tutorial: Warnungen zu Reconnaissance  

Cyberangriffe werden üblicherweise auf alle zugänglichen Entitäten wie etwa Benutzer mit geringen Rechten durchgeführt. Anschließend dringt der Angreifer schnell im internen Netzwerk vor (Lateral Movement), um Zugriff auf wertvolle Ressourcen zu erhalten. Dabei kann es sich um sensible Konten, Konten von Domänenadministratoren oder streng vertrauliche Daten handeln. Azure ATP identifiziert diese komplexen Bedrohungen an der Quelle über die gesamte Kette der Angriffsabwehr hinweg und ordnet sie in die folgenden Phasen ein

1. **Reconnaissance**
2. [Kompromittierte Anmeldeinformationen](atp-compromised-credentials-alerts.md)
3. [Lateral Movement-Aktivitäten](atp-lateral-movement-alerts.md)
4. [Warnungen zu Domänendominanz](atp-domain-dominance-alerts.md)
5. [Exfiltration](atp-exfiltration-alerts.md) 

Weitere Informationen zur Struktur und zu gängigen Komponenten der Azure ATP-Sicherheitswarnungen finden Sie unter [Grundlegendes zu Sicherheitswarnungen](understanding-security-alerts.md).

Die folgenden Sicherheitswarnungen unterstützen Sie dabei, verdächtige Aktivitäten zu identifizieren und zu unterbinden, die von Azure ATP in Ihrem Netzwerk erkannt werden und auf **Reconnaissance** hindeuten.

In diesem Tutorial machen Sie sich mit den folgenden Angriffstypen vertraut und erfahren, wie Sie diese klassifizieren, unterbinden und im Vorfeld verhindern:

> [!div class="checklist"]
> * Reconnaissance über Kontoenumeration (externe ID 2003)
> * Reconnaissance über Netzwerkzuordnungen (DNS) (externe ID 2007)
> * Reconnaissance über Benutzer und IP-Adressen (SMB) (externe ID 2012)
> * Reconnaissance über Benutzer und Gruppenmitgliedschaften (SAMR) (externe ID 2021)

## <a name="account-enumeration-reconnaissance-external-id-2003"></a>Reconnaissance über Kontoenumeration (externe ID 2003) 


*Vorheriger Name*: Reconnaissance mithilfe von Kontoenumeration

**Beschreibung**

Bei Reconnaissancemaßnahmen über Kontoenumerationen verwendet ein Angreifer ein Wörterbuch mit Tausenden von Benutzernamen oder Tools wie KrbGuess, um Benutzernamen in Ihrer Domäne zu erraten.

**Kerberos**: Der Angreifer führt Kerberos-Anforderungen mit diesen Namen durch, um einen gültigen Benutzernamen in der Domäne aufzuspüren. Wenn dadurch ein Benutzername bestimmt wird, erhält der Angreifer die Kerberos-Fehlermeldung **Preauthentication required** (Vorauthentifizierung erforderlich) statt der Meldung **Security principal unknown** (Unbekannter Sicherheitsprinzipal).

**NTLM**: Der Angreifer führt NLTM-Authentifizierungsanforderungen mit diesem Wörterbuch mit Namen durch, um einen gültigen Benutzernamen in der Domäne aufzuspüren. Wenn dadurch ein Benutzername bestimmt wird, erhält der Angreifer die NTLM-Fehlermeldung **WrongPassword (0xc000006a)** statt der Meldung **NoSuchUser (0xc0000064)**.

Bei Erkennung dieser Warnung ermittelt Azure ATP den Ursprung des Kontoenumerationsangriffs, die Gesamtzahl der Versuche zum Erraten des Namens und die Anzahl der gefundenen Übereinstimmungen. Wenn es zu viele unbekannte Benutzer gibt, erkennt Azure ATP dies als verdächtige Aktivität.

**TP, B-TP oder FP**

Einige Server und Anwendungen fragen Domänencontroller ab, um festzustellen, ob Konten in zulässigen Verwendungsszenarios zum Einsatz kommen.

Um festzustellen, ob es sich bei der Abfrage um den Typ **TP**, **B-TP** oder **FP** handelt, klicken Sie auf die Warnung, um die zugehörige Detailseite aufzurufen:

1. Überprüfen Sie, ob der Quellcomputer diese Abfrage tatsächlich ausführen sollte. Beispiele für **B-TP** könnten in diesem Fall Microsoft Exchange-Server oder Systeme der Personalverwaltung sein.

2. Überprüfen Sie die Kontodomänen.
   - Werden zusätzliche Benutzer angezeigt, die zu einer anderen Domäne gehören? 
     <br>Eine Fehlkonfigurationen der Server kann z. B. bei Exchange/Skype oder ADSF dazu führen, dass zusätzliche Benutzer vorhanden sind, die verschiedenen Domänen angehören.
   - Sehen Sie sich die Konfiguration des problematischen Diensts an, um die Fehlkonfiguration zu beheben.

     Wenn Sie die obigen Fragen mit **Ja** beantwortet haben, handelt es sich um eine **B-TP**-Aktivität. *Schließen* Sie die Sicherheitswarnung.<br>

Betrachten Sie im nächsten Schritt den Quellcomputer: 

1. Wird auf dem Quellcomputer ein Skript oder eine Anwendung ausgeführt, die dieses Verhalten verursachen könnten?  
   - Ist das Skript schon älter und wird es mit alten Anmeldeinformationen ausgeführt? <br>Wenn ja, beenden und bearbeiten Sie das Skript, oder löschen Sie es. 
   - Handelt es sich um ein Verwaltungs- oder Sicherheitsskript bzw. um eine entsprechende Anwendung, die tatsächlich in der Umgebung ausgeführt werden soll?
 
     Wenn Sie die vorherige Frage mit **Ja** beantwortet haben, *schließen* Sie die Sicherheitswarnung, und schließen Sie diesen Computer aus. Vermutlich handelt es sich um eine **B-TP**-Aktivität.

Betrachten Sie nun die Konten:<br>
<br>Angreifer verwenden häufig ein Wörterbuch mit zufälligen Kontonamen, um vorhandene Kontonamen in einer Organisation zu finden.

1. Kommen Ihnen die nicht vorhandenen Konten vertraut vor?  
   - Wenn ja, sind diese Konten möglicherweise deaktiviert, oder sie gehören Mitarbeitern, die das Unternehmen verlassen haben.
   - Überprüfen Sie, ob eine Anwendung oder ein Skript vorhanden ist, mit dem überprüft wird, welche Konten in Active Directory Domain Services noch vorhanden sind.

     Wenn Sie eine der vorherigen Fragen mit **Ja** beantwortet haben, *schließen* Sie die Sicherheitswarnung. Es handelt sich vermutlich um eine **B-TP**-Aktivität.

2. Wenn einer der Rateversuche mit einem vorhandenen Kontonamen übereinstimmt, kennt der Angreifer vorhandene Konten in Ihrer Umgebung und kann mit Brute-Force-Angriffen und gefundenen Benutzernamen versuchen, Zugriff auf Ihre Domäne zu erhalten. 
    - Überprüfen Sie die erratenen Kontonamen auf weitere verdächtige Aktivitäten. 
    - Überprüfen Sie, ob es sich bei den Konten um sensible Konten handelt.

### <a name="understand-the-scope-of-the-breach"></a>Ermitteln des Umfangs der Sicherheitsverletzung

1. Untersuchen Sie den Quellcomputer.
2. Wenn bei einem Rateversuch eine Übereinstimmung mit einem vorhandenen Kontonamen gefunden wird, kennt der Angreifer vorhandene Konten in Ihrer Umgebung und kann mit den gefundenen Benutzernamen Brute-Force-Angriffe ausführen, um Zugriff auf Ihre Domäne zu erhalten. Untersuchen Sie vorhandene Konten mithilfe des [Leitfadens für die Untersuchung von Benutzern](investigate-a-user.md). 

### <a name="suggested-remediation-and-steps-for-prevention"></a>Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung

1. Isolieren Sie den [Quellcomputer](investigate-a-computer.md). 
    1. Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
    2. Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch kompromittiert sind. 
    3. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA.
2. Erzwingen Sie [komplexe und lange Kennwörter](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) in der Organisation. Komplexe und lange Kennwörter stellen die erste Sicherheitsstufe zum Schutz vor Brute-Force-Angriffen dar. Diese sind nach der Enumeration normalerweise der nächste Schritt in der Kill Chain des Cyberangriffs. 

## <a name="network-mapping-reconnaissance-dns-external-id-2007"></a>Reconnaissance über Netzwerkzuordnungen (DNS) (externe ID 2007) 


*Vorheriger Name*: Reconnaissance über DNS

**Beschreibung**

Ihr DNS-Server enthält eine Struktur aller Computer, IP-Adressen und Dienste in Ihrem Netzwerk. Diese Informationen werden von Angreifern verwendet, um Ihre Netzwerkstruktur auszukundschaften und um interessante Zielcomputer zu bestimmten, die sie in den nächsten Schritten des Angriffs benötigen. 
 
Es gibt mehrere Abfragetypen im DNS-Protokoll. Diese Azure ATP-Sicherheitswarnung erkennt AXFR-Übertragungsanforderungen, die von Nicht-DNS-Servern stammen.

**Lernphase**

Für diese Warnung gilt eine Lernphase von 8 Tagen ab dem Start der Domänencontrollerüberwachung. 

**TP, B-TP oder FP?**

1. Überprüfen Sie, ob der Quellcomputer ein DNS-Server ist.

    - Wenn der Quellcomputer **tatsächlich** ein DNS-Server ist, schließen Sie die Sicherheitswarnung als **FP**-Aktivität. 
    - Achten Sie darauf, dass der UDP-Port 53 für die Verbindung zwischen dem Azure ATP-Sensor und dem Quellcomputer **offen** ist, um zukünftige **FP**-Aktivitäten zu verhindern.

Sicherheitsscanner und zulässige Anwendungen können DNS-Abfragen erstellen. 

1. Überprüfen Sie, ob diese Aktivitäten tatsächlich vom Quellcomputer ausgeführt werden sollen.

    - Wenn ja, **schließen** Sie die Sicherheitswarnung als **B-TP**-Aktivität, und schließen Sie den Computer aus.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie den [Quellcomputer](investigate-a-computer.md). 

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

**Abhilfemaßnahmen:**
1. Kontrollieren Sie den Quellcomputer. 
    - Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
    - Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch kompromittiert sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA.

**Vorbeugung:** Zukünftige Angriffe über AXFR-Abfragen vermeiden Sie, indem Sie Ihren internen DNS-Server sichern.

1. Dadurch verhindern Sie Reconnaissance über DNS. Deaktivieren Sie hierzu Zonenübertragungen, oder [schränken Sie diese auf bestimmte IP-Adressen ein](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee649273(v=ws.10)). Das Bearbeiten von Zonenübertragungen ist eine Aufgabe innerhalb einer Prüfliste, die für das [Sichern des DNS-Servers gegen interne und externe Angriffe](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee649273(v=ws.10)) gelten sollte.

## <a name="user-and-ip-address-reconnaissance-smb-external-id-2012"></a>Reconnaissance über Benutzer und IP-Adressen (SMB) (externe ID 2012) 


*Vorheriger Name*: Reconnaissance mithilfe der SMB-Sitzungsenumeration

### <a name="description"></a>Beschreibung

Eine Enumeration mithilfe des SMB-Protokolls (Server Message Block) ermöglicht es Angreifern, Informationen darüber zu erhalten, wo Benutzer sich zuletzt angemeldet haben. Sobald Angreifer diese Informationen besitzen, können sie sich seitlich im Netzwerk bewegen, um zu einem bestimmten sensiblen Konto zu gelangen.

In dieser Erkennung wird eine Warnung ausgelöst, wenn eine SMB-Sitzungsenumeration auf einem Domänencontroller ausgeführt wird. 

**TP, B-TP oder FP**

Sicherheitsscanner und Anwendungen können möglicherweise zulässige Abfragen an Domänencontroller senden, um offene SMB-Sitzungen zu ermitteln.

1. Sollen diese Aktivitäten tatsächlich vom Quellcomputer ausgeführt werden?
2. Wird auf dem Quellcomputer eine Art Sicherheitsscanner ausgeführt?  
    Wenn die Antwort „Ja“ lautet, handelt es sich wahrscheinlich um eine B-TP-Aktivität. *Schließen* Sie die Sicherheitswarnung, und schließen Sie diesen Computer aus.
3. Überprüfen Sie die Benutzer, die den Vorgang ausgeführt haben.
   Sollen diese Aktionen tatsächlich von diesen Benutzern ausgeführt werden?  
    Wenn die Antwort „Ja“ lautet, *schließen* Sie die Sicherheitswarnung als B-TP-Aktivität.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie den Quellcomputer.  
2. Überprüfen Sie auf der Warnungsseite, ob kompromittierte Benutzer angezeigt werden. Überprüfen Sie anschließend ihre jeweiligen Profile, um weitere Untersuchungen durchzuführen. Es wird empfohlen, zuerst sensible Benutzerkonten sowie Konten mit hoher Priorität zu untersuchen.

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

Verwenden Sie das [Net Cease-Tool](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b), um den Schutz Ihrer Umgebung gegen diese Attacken zu erhöhen.

## <a name="user-and-group-membership-reconnaissance-samr-external-id-2021"></a>Reconnaissance über Benutzer und Gruppenmitgliedschaften (SAMR) (externe ID 2021) 


*Vorheriger Name*: Reconnaissance mithilfe von Verzeichnisdienstabfragen 

**Beschreibung:** Die Reconnaissance über Benutzer und Gruppenmitgliedschaften wird von Angreifern verwendet, um die Verzeichnisstruktur und Zielkonten mit weitreichenden Rechten für die weiteren Schritte eines Angriffs auszukundschaften. Das Protokoll Security Account Manager Remote (SAM-R) ist eine Methode, die zum Abfragen des Verzeichnisses verwendet wird, um diese Art der Zuordnung vorzunehmen.  
In dieser Erkennung werden im ersten Monat nach der Bereitstellung von Azure ATP keine Warnungen ausgelöst (Lernphase). Während der Lernphase erfasst Azure ATP, welche SAM-R-Abfragen (Enumerationsabfragen und einzelne Abfragen von sensiblen Konten) von welchen Computern gestellt werden. 

**Lernphase**

Vier Wochen pro Domänencontroller, beginnend mit der ersten Netzwerkaktivität von SAMR für den festgelegten DC.

**TP, B-TP oder FP** 

1. Klicken Sie auf den Quellcomputer, um die entsprechende Profilseite aufzurufen.        
   - Sollen diese Aktivitäten tatsächlich vom Quellcomputer ausgeführt werden?
     - Wenn ja, *schließen* Sie die Sicherheitswarnung als **B-TP**-Aktivität, und schließen Sie diesen Computer aus. 
   - Überprüfen Sie die Benutzer, die den Vorgang ausgeführt haben.
     - Melden sich diese normalerweise bei diesem Quellcomputer an, oder sind sie Administratoren, die diese Aktionen durchführen sollten?   
     - Überprüfen Sie das Benutzerprofil und die damit verbundenen Benutzeraktivitäten. Analysieren Sie ihr normales Verhalten, und suchen Sie nach zusätzlichen verdächtigen Aktivitäten mithilfe des [Leitfadens zur Untersuchung von Benutzern](investigate-a-user.md). 
    
     Wenn Sie die vorherige Frage mit **Ja** beantwortet haben, *schließen* Sie die Sicherheitswarnung als **B-TP**-Aktivität. 
  
**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Überprüfen Sie, welche Abfragen gestellt wurden (z. B. von Unternehmensadministratoren oder Administratoren), und ermitteln Sie, ob diese erfolgreich waren.
2. Untersuchen Sie jeden verfügbar gemachten Benutzer anhand des Leitfadens zur Untersuchung von Benutzern.
3. Untersuchen Sie den Quellcomputer.  
  
**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

1. Kontrollieren Sie den Quellcomputer.
2. Suchen Sie das Tool, mit dem der Angriff ausgeführt wurde, und entfernen Sie es.
3. Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA.
4. Setzen Sie das Kennwort des Quellbenutzers zurück, und aktivieren Sie MFA.
5. Wenden Sie die Netzwerkzugriffssteuerung an, und schränken Sie die Zahl der Clients ein, die Remoteaufrufe der SAM-Gruppenrichtlinie durchführen dürfen.

> [!NOTE]
> Kontaktieren Sie den Support, wenn Sie Azure ATP-Sicherheitswarnungen deaktivieren möchten.

> [!div class="nextstepaction"]
> [Tutorial: Warnungen zu kompromittierten Anmeldeinformationen](atp-compromised-credentials-alerts.md)

## <a name="see-also"></a>Weitere Informationen

- [Untersuchen eines Computers](investigate-a-computer.md)
- [Untersuchen eines Benutzers](investigate-a-user.md)
- [Arbeiten mit Sicherheitswarnungen](working-with-suspicious-activities.md)
- [Warnungen zu kompromittierten Anmeldeinformationen](atp-compromised-credentials-alerts.md)
- [Lateral Movement-Warnungen](atp-lateral-movement-alerts.md)
- [Warnungen zu Domänendominanz](atp-domain-dominance-alerts.md)
- [Warnungen zu Exfiltration](atp-exfiltration-alerts.md)
- [Referenz zum Azure ATP-SIEM-Protokoll](cef-format-sa.md)
- [Arbeiten mit Lateral Movement-Pfaden](use-case-lateral-movement-path.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
