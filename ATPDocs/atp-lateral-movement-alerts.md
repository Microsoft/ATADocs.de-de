---
title: Lateral Movement-Sicherheitswarnungen in Azure ATP| Microsoft-Dokumentation
d|Description: This article explains the Azure ATP alerts issued when attacks typically part of lateral movement phase efforts are detected against your organization.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 1/15/2019
ms.topic: tutorial
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 2257eb00-8614-4577-b6a1-5c65085371f2
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7816dba02c2fea07afc080c7aed5ede073c88fac
ms.sourcegitcommit: e2daa0f93d97d552cfbf1577fbd05a547b63e95b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/15/2019
ms.locfileid: "54314311"
---
# <a name="tutorial-lateral-movement-alerts"></a>Tutorial: Lateral Movement-Warnungen  

Cyberangriffe werden üblicherweise auf alle zugänglichen Entitäten wie etwa Benutzer mit geringen Rechten durchgeführt. Anschließend dringt der Angreifer schnell im internen Netzwerk vor (Lateral Movement), um Zugriff auf wertvolle Ressourcen zu erhalten. Dabei kann es sich um sensible Konten, Konten von Domänenadministratoren oder streng vertrauliche Daten handeln. Azure ATP identifiziert diese komplexen Bedrohungen an der Quelle über die gesamte Kette der Angriffsabwehr hinweg und ordnet sie in die folgenden Phasen ein

1. [Reconnaissance](atp-reconnaissance-alerts.md)
2. [Kompromittierte Anmeldeinformationen](atp-compromised-credentials-alerts.md)
3. **Lateral Movements**
4. [Warnungen zu Domänendominanz](atp-domain-dominance-alerts.md)
5. [Exfiltration](atp-exfiltration-alerts.md)

Weitere Informationen zur Struktur und zu gängigen Komponenten der Azure ATP-Sicherheitswarnungen finden Sie unter [Understanding security alerts (Grundlegendes zu Sicherheitswarnungen)](understanding-security-alerts.md).

Die folgenden Sicherheitswarnungen unterstützen Sie dabei, verdächtige Aktivitäten zu identifizieren und zu unterbinden, die von Azure ATP in Ihrem Netzwerk erkannt werden und auf **Lateral Movement** hindeuten. In diesem Tutorial erfahren Sie, wie die folgenden Angriffstypen klassifiziert, behoben und unterbunden werden:

> [!div class="checklist"]
> * Suspected identity theft (pass-the-hash) (Verdacht auf Identitätsdiebstahl (Pass-the-Hash)) (externalid 2017)
> * Suspected identity theft (pass-the-ticket) (Verdacht auf Identitätsdiebstahl (Pass-the-Ticket)) (externalid 2018)
> * Suspected over-pass-the-hash attack (encryption downgrade) (Verdacht auf Over-Pass-the-Hash-Angriff (Herabstufung der Verschlüsselung)) (externalid 2008)
> * Suspected overpass-the-hash attack (Kerberos) (Verdacht auf einen Overpass-the-Hash-Angriff (Kerberos)) (externalid 2002)

## <a name="suspected-identity-theft-pass-the-hash-external-id-2017"></a>Suspected identity theft (pass-the-hash) (Verdacht auf Identitätsdiebstahl (Pass-the-Hash)) (externalid 2017)

*Vorheriger Name*: Identitätsdiebstahl mithilfe eines Pass-the-Hash-Angriffs

**Beschreibung**

Pass-the-Hash ist eine Technik mit seitlicher Bewegung, bei der Angreifer den NTLM-Hash eines Benutzers von einem Computer stehlen und diesen verwenden, um Zugriff auf einen anderen Computer zu erlangen.

**TP, B-TP oder FP?**
1. Wurde der Hash auf Computern verwendet, die der Benutzer regelmäßig verwendet? 
    - Wenn der Hash regelmäßig auf Computern verwendet wurde, **Schließen** Sie die Warnung als **FP**-Aktivität (falsch positiv).  
 
**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie die [Quell- und Zielcomputer](investigate-a-computer.md) weiter.  
2. Untersuchen Sie den [kompromittierten Benutzer](investigate-a-computer.md).
 
**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

1. Setzen Sie die Kennwörter des Quellbenutzers zurück, und aktivieren Sie die mehrstufige Authentifizierung (MFA).
2. Isolieren Sie die Quell- und Zielcomputer.
3. Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
4. Finden Sie heraus, ob sich ungefähr gleichzeitig mit der Aktivität Benutzer angemeldet haben, da auch sie kompromittiert sein könnten. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA.

## <a name="suspected-identity-theft-pass-the-ticket-external-id-2018"></a>Suspected identity theft (pass-the-ticket) (Verdacht auf Identitätsdiebstahl (Pass-the-Ticket)) (externalid 2018)

*Vorheriger Name*: Identitätsdiebstahl mithilfe eines Pass-the-Ticket-Angriffs

**Beschreibung**

Pass-the-Ticket ist eine Technik mit seitlicher Bewegung, bei der die Angreifer ein Kerberos-Ticket von einem Computer stehlen und dieses verwenden, um Zugriff auf einen anderen Computer zu erlangen, indem sie das gestohlene Ticket wiederverwenden. In dieser Erkennung wird ein Kerberos-Ticket auf zwei (oder mehr) verschiedenen Computern verwendet.

**TP, B-TP oder FP?**

Das erfolgreiche Auflösen von IP-Adressen für Computer in der Organisation ist wichtig, um Pass-The-Ticket-Angriffe von einem Computer auf einen anderen zu identifizieren. 

1. Überprüfen Sie, ob die IP-Adresse von einem oder beiden Computern zu einem Subnetz gehört, das aus einem zu kleinen DHCP-Pool (z. B. VPN, VDI oder WiFi) zugewiesen wird. 
2. Wurde die IP-Adresse freigegeben (z. B. durch ein NAT-Gerät)?  
3. Werden eine oder mehrere Ziel-IP-Adressen vom Sensor nicht aufgelöst? Wenn eine Ziel-IP-Adresse nicht aufgelöst wird, kann dies bedeuten, dass die richtigen Ports zwischen dem Sensor und den Geräten nicht ordnungsgemäß geöffnet sind. 

    Wenn die Antwort auf eine der vorausgegangenen Fragen **Ja** lautet, überprüfen Sie, ob Quell- und Zielcomputer identisch sind. Sind sie identisch, handelt es sich um eine **FP**-Aktivität (falsch positiv), und es haben keine echten **Pass-the-Ticket**-Versuche stattgefunden. 

Es gibt benutzerdefinierte Anwendungen, die Tickets im Auftrag des Benutzers weiterleiten. Diese Anwendungen verfügen über Delegierungsberechtigungen für Benutzertickets.

1. Gibt es eine benutzerdefinierte Anwendung wie die zuvor beschriebene derzeit auf den Zielcomputern? Welche Dienste werden von der Anwendung ausgeführt? Werden die Dienste durch Anweisung der Benutzer ausgeführt, beispielsweise zum Zugreifen auf Datenbanken?
    - Wenn ja, **schließen** Sie die Sicherheitswarnung, da es sich um eine **B-TP**-Aktivität (unbedenklich richtig positiv) handelt.
2. Ist der Zielcomputer ein Delegierungsserver?
    - Wenn ja, **schließen** Sie die Sicherheitswarnung, und schließen Sie diesen Computer als **B-TP**-Aktivität (unbedenklich richtig positiv) aus.
 
**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie die [Quell- und Zielcomputer](investigate-a-computer.md).  
2. Untersuchen Sie den [kompromittierten Benutzer](investigate-a-computer.md). 

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

1. Setzen Sie das Kennwort des Quellbenutzers zurück, und aktivieren Sie die mehrstufige Authentifizierung (MFA).
2. Isolieren Sie die Quell- und Zielcomputer.
3. Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
4. Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA.
5. Wenn Windows Defender ATP installiert ist, nutzen Sie **klist.exe purge**, um alle Tickets der angegebenen Anmeldesitzung endgültig zu löschen und zu verhindern, dass die Tickets in Zukunft verwendet werden.

## <a name="suspected-overpass-the-hash-attack-encryption-downgrade-external-id-2008"></a>Suspected over-pass-the-hash attack (encryption downgrade) (Verdacht auf Over-Pass-the-Hash-Angriff (Herabstufung der Verschlüsselung)) (externalid 2008) 

*Vorheriger Name*: Aktivität zur Herabstufung der Verschlüsselung

**Beschreibung**

Die Herabstufung der Verschlüsselung ist eine Methode, die dazu dient, Kerberos zu schwächen, indem die Verschlüsselung von unterschiedlichen Feldern des Protokolls, die normalerweise mit der höchsten Verschlüsselungsstufe verschlüsselt werden, herabgestuft wird. Ein abgeschwächtes verschlüsseltes Feld ist ein leichteres Ziel für versuchte Brute-Force-Angriffe offline. Verschiedene Angriffsmethoden nutzen schwache Kerberos-Verschlüsselungsverfahren. Bei dieser Erkennung lernt Azure ATP die Kerberos-Verschlüsselungsverfahren, die von Computern und Benutzern verwendet werden, und benachrichtigt Sie, wenn ein schwächeres Verschlüsselungsverfahren verwendet wird, das unüblich für den Quellcomputer und/oder den Benutzer ist und mit bekannten Angriffstechniken übereinstimmt. 

Bei einem Overpass-the-Hash-Angriff kann ein Angreifer zusammen mit einer Kerberos-AS-Anforderung einen schwachen gestohlenen Hash zur Erstellung eines starken Tickets verwenden. In dieser Erkennung werden Instanzen erkannt, bei denen der AS_REQ-Nachrichtenverschlüsselungstyp des Quellcomputers im Vergleich zu dem zuvor gelernten Verhalten (der Computer hat AES verwendet) heruntergestuft wird.

**TP, B-TP oder FP?**
1. Finden Sie heraus, ob die Smartcardkonfiguration kürzlich geändert worden ist. 
    - Sind bei den beteiligten Konten kürzlich Smartcardkonfigurationen geändert worden?  
    
    Wenn ja, **schließen** Sie die Sicherheitswarnung, da es sich um eine **B-TP**-Aktivität (unbedenklich richtig positiv) handelt. 

Einige unbedenkliche Ressourcen unterstützen keine starken Verschlüsselungsverfahren und können diese Warnung auslösen. 

2. Ist für alle Quellbenutzer etwas bestimmtes freigegeben? 
    1. Beispielsweise können Sie überprüfen, ob alle Mitarbeiter des Marketingteams auf eine bestimmte Ressource zugreifen und dadurch eine Warnung auslösen.
    2. Überprüfen Sie die Ressourcen, auf die mit diesen Tickets zugegriffen wurde. 
        - Verwenden Sie dafür das *msDS-SupportedEncryptionTypes*-Attribut des Ressourcendienstkontos in Azure Active Directory.
    3. Wenn es nur eine Ressource gibt, auf die zugegriffen worden ist, überprüfen Sie, ob es sich um eine für diese Benutzer gültige Ressource handelt, auf die sie zugreifen dürfen.   

    Wenn die Antwort auf eine der vorherigen Fragen **Ja** lautet, handelt es sich vermutlich um eine **B-TP**-Aktivität. Überprüfen Sie, ob von der Ressource ein starkes Verschlüsselungsverfahren unterstützt wird, implementieren Sie es nach Möglichkeit, und **schließen** Sie die Sicherheitswarnung.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie den [Quellcomputer](investigate-a-computer.md).  
2. Untersuchen Sie den [kompromittierten Benutzer](investigate-a-computer.md). 

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung** 

**Wartung**
1. Setzen Sie das Kennwort des Quellbenutzers zurück, und aktivieren Sie die mehrstufige Authentifizierung (MFA). 
2. Kontrollieren Sie den Quellcomputer. 
3. Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es. 
4. Suchen Sie nach Benutzern, die zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA.  

**Prävention**
 
1. Konfigurieren Sie Ihre Domäne so, dass starke Verschlüsselungsverfahren unterstützt werden, und entfernen Sie *Use Kerberos DES encryption types* (Kerberos DES-Verschlüsselungstypen verwenden). Erfahren Sie mehr über [Verschlüsselungstypen und Kerberos](https://blogs.msdn.microsoft.com/openspecification/2011/05/30/windows-configurations-for-kerberos-supported-encryption-type/). 
2. Stellen Sie sicher, dass für die Domänenfunktionsebene die Unterstützung starker Verschlüsselungsverfahren eingestellt ist.  
3. Verwenden Sie bevorzugt Anwendungen, die starke Verschlüsselungsverfahren unterstützen.

## <a name="suspected-overpass-the-hash-attack-kerberos-external-id-2002"></a>Suspected overpass-the-hash attack (Kerberos) (Verdacht auf einen Overpass-the-Hash-Angriff (Kerberos)) (externalid 2002) 

*Vorheriger Name*: Ungewöhnliche Kerberos-Protokollimplementierung (potenzieller Overpass-the-Hash-Angriff)

**Beschreibung**

Angreifer verwenden Tools, die verschiedene Protokolle wie Kerberos und SMB auf nicht standardmäßige Arten implementieren. Während diese Art des Netzwerkdatenverkehrs von Microsoft Windows ohne Warnungen akzeptiert wird, kann Azure ATP potenziell böswillige Absichten erkennen. Das Verhalten weist auf Techniken hin, wie sie beispielsweise für Overpass-the-Hash, Brute-Force oder erweiterte Ransomware-Exploits, z. B. WannaCry, verwendet werden.

**TP, B-TP oder FP?**

Zuweilen implementieren Anwendungen einen eigenen Kerberos-Stapel, der nicht der Kerberos-RFC-Dokumentation entspricht. 

1. Überprüfen Sie, ob auf dem Quellcomputer eine Anwendung mit ihrem eigenen Kerberos-Stapel ausgeführt wird, und dies im Widerspruch zur Kerberos-RFC steht.  
2. Führt der Quellcomputer eine solche Anwendung aus, obwohl er dies **nicht** tun sollte, korrigieren Sie die Anwendungskonfiguration. **Schließen** Sie die Sicherheitswarnung als **B-TP**-Aktivität (unbedenklich richtig positiv).  
3. Führt der Quellcomputer eine solche Anwendung aus, und soll er das auch weiterhin tun, **schließen** Sie die Sicherheitswarnung als **B-TP**-Aktivität (unbedenklich richtig positiv), und schließen Sie diesen Computer aus. 

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie den [Quellcomputer](investigate-a-computer.md).  
2. Wenn ein [Quellbenutzer](investigate-a-user.md) vorhanden ist, untersuchen Sie diesen. 

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung** 

1. Setzen Sie die Kennwörter der kompromittierten Benutzer zurück, und aktivieren Sie die mehrstufige Authentifizierung (MFA).
2. Kontrollieren Sie den Quellcomputer.
3. Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
4. Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der verdächtigen Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA.  
5. Setzen Sie die Kennwörter des Quellbenutzers zurück, und aktivieren Sie die mehrstufige Authentifizierung (MFA).

> [!div class="nextstepaction"]
> [Tutorial: Warnung zu Domänendominanz](atp-domain-dominance-alerts.md)

## <a name="see-also"></a>Weitere Informationen

- [Untersuchen eines Computers](investigate-a-computer.md)
- [Arbeiten mit Sicherheitswarnungen](working-with-suspicious-activities.md)
- [Arbeiten mit Lateral Movement-Pfaden](use-case-lateral-movement-path.md)
- [Warnungen zu Reconnaissance](atp-reconnaissance-alerts.md)
- [Warnungen zu kompromittierten Anmeldeinformationen](atp-compromised-credentials-alerts.md)
- [Warnungen zu Domänendominanz](atp-domain-dominance-alerts.md)
- [Warnungen zu Exfiltration](atp-exfiltration-alerts.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
