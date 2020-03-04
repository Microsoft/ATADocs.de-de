---
title: Lateral Movement-Sicherheitswarnungen in Azure ATP| Microsoft-Dokumentation
d|Description: This article explains the Azure ATP alerts issued when attacks typically part of lateral movement phase efforts are detected against your organization.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 03/01/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2257eb00-8614-4577-b6a1-5c65085371f2
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b815ea0cb5e9276f280ce2164cf97b4fe3daadbf
ms.sourcegitcommit: 4381148c0487b473e23fe9b425b133c42acde881
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2020
ms.locfileid: "78208032"
---
# <a name="tutorial-lateral-movement-alerts"></a>Tutorial: Lateral Movement-Warnungen

Cyberangriffe werden üblicherweise auf alle zugänglichen Entitäten wie etwa Benutzer mit geringen Rechten durchgeführt. Anschließend dringt der Angreifer schnell im internen Netzwerk vor (Lateral Movement), um Zugriff auf wertvolle Ressourcen zu erhalten. Dabei kann es sich um sensible Konten, Konten von Domänenadministratoren oder streng vertrauliche Daten handeln. Azure ATP identifiziert diese komplexen Bedrohungen an der Quelle über die gesamte Kette der Angriffsabwehr hinweg und ordnet sie in die folgenden Phasen ein

1. [Reconnaissance](atp-reconnaissance-alerts.md)
2. [Kompromittierte Anmeldeinformationen](atp-compromised-credentials-alerts.md)
3. **Seitliche Verschiebung**
4. [Warnungen zu Domänendominanz](atp-domain-dominance-alerts.md)
5. [Exfiltration](atp-exfiltration-alerts.md)

Weitere Informationen zur Struktur und zu gängigen Komponenten der Azure ATP-Sicherheitswarnungen finden Sie unter [Understanding security alerts (Grundlegendes zu Sicherheitswarnungen)](understanding-security-alerts.md).

Die folgenden Sicherheitswarnungen unterstützen Sie dabei, verdächtige Aktivitäten zu identifizieren und zu unterbinden, die von Azure ATP in Ihrem Netzwerk erkannt werden und auf **Lateral Movement** hindeuten. In diesem Tutorial erfahren Sie, wie die folgenden Angriffstypen klassifiziert, behoben und unterbunden werden:

> [!div class="checklist"]
>
> * Remotecodeausführung über DNS (externe ID 2036)
> * Suspected identity theft (pass-the-hash) (Verdacht auf Identitätsdiebstahl (Pass-the-Hash)) (externalid 2017)
> * Suspected identity theft (pass-the-ticket) (Verdacht auf Identitätsdiebstahl (Pass-the-Ticket)) (externalid 2018)
> * Suspected NTLM authentication tampering (external ID 2039) (Vermutete Manipulation der NTLM-Authentifizierung [Externe ID 2039])
> * Vermuteter NTLM-Relaisangriff (Exchange-Konto) (externe ID 2037)
> * Suspected over-pass-the-hash attack (encryption downgrade) (Verdacht auf Over-Pass-the-Hash-Angriff (Herabstufung der Verschlüsselung)) (externalid 2008)
> * Suspected overpass-the-hash attack (Kerberos) (Verdacht auf einen Overpass-the-Hash-Angriff (Kerberos)) (externalid 2002)

## <a name="remote-code-execution-over-dns-external-id-2036"></a>Remotecodeausführung über DNS (externe ID 2036)

**Beschreibung**

Am 11.12.2018 hat Microsoft [CVE-2018-8626](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2018-8626) veröffentlicht und gibt bekannt, dass bei Windows DNS-Servern (Domain Name System) ein neues Sicherheitsrisiko bei der Remotecodeausführung erkannt wurde. Bei diesem Sicherheitsrisiko können Server Anforderungen nicht mehr ordnungsgemäß verarbeiten. Ein Angreifer, der dieses Sicherheitsrisiko erfolgreich ausnutzt, kann im Kontext des lokalen Systemkontos beliebigen Code ausführen. Derzeit als DNS-Server konfigurierte Windows-Server sind von diesem Sicherheitsrisiko betroffen.

Bei dieser Erkennung wird eine Azure ATP-Sicherheitswarnung ausgelöst, wenn DNS-Abfragen an einen Domänencontroller im Netzwerk gerichtet werden, die im Verdacht stehen, die Sicherheitslücke CVE-2018-8626 auszunutzen.

**TP, B-TP oder FP**

1. Sind Sie die Zielcomputer auf dem neuesten Stand und für CVE-2018-8626 gepatcht?
    - Wenn die Computer auf dem neuesten Stand und gepatcht sind, **schließen** Sie die Sicherheitswarnung als **FP**.
2. Wurde ungefähr zum Zeitpunkt des Angriffs ein Dienst erstellt oder ein unbekannter Prozess ausgeführt?
    - Wenn Sie keinen neuen Dienst oder einen unbekannten Prozess finden, **schließen** Sie die Sicherheitswarnung als **FP**.
3. Diese Art von Angriff kann den DNS-Dienst zum Absturz bringen, bevor die Codeausführung erfolgreich veranlasst wurde.
    - Überprüfen Sie, ob der DNS-Dienst ungefähr zum Zeitpunkt des Angriffs mehrmals neu gestartet wurde.
    - Wenn der DNS-Dienst neu gestartet wurde, handelte es sich wahrscheinlich um einen Versuch, CVE-2018-8626 auszunutzen. Betrachten Sie diese Warnung als **TP**, und führen Sie die unter **Ermitteln des Umfangs der Sicherheitsverletzung** beschriebenen Anweisungen aus.

**Ermitteln des Umfangs der Sicherheitsverletzung**

- Untersuchen Sie die [Quell- und Zielcomputer](investigate-a-computer.md).

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

**Wartung**

1. Isolieren Sie die Domänencontroller.
    1. Unterbinden Sie die versuchte Remotecodeausführung.
    2. Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der verdächtigen Aktivität ebenfalls angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
2. Kontrollieren Sie den Quellcomputer.
    1. Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
    2. Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der verdächtigen Aktivität ebenfalls angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.

**Vorbeugung**

- Stellen Sie sicher, dass alle DNS-Server in der Umgebung auf dem aktuellen Stand und für [CVE-2018-8626](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2018-8626) gepatcht sind.

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

1. Setzen Sie das Kennwort des Quellbenutzers zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
2. Isolieren Sie die Quell- und Zielcomputer.
3. Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
4. Finden Sie heraus, ob sich ungefähr gleichzeitig mit der Aktivität Benutzer angemeldet haben, da auch sie kompromittiert sein könnten. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.

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

Das Feature [Remote Credential Guard](https://docs.microsoft.com/windows/security/identity-protection/remote-credential-guard) der RDP-Verbindungen kann zu **B-TP**-Warnungen führen, wenn es mit Windows 10 auf Windows Server 2016 und höher verwendet wird.
Überprüfen Sie mithilfe der Warnungsbeweisen, ob der Benutzer eine Remotedesktopverbindung vom Quellcomputer zum Zielcomputer hergestellt hat.

1. Suchen Sie nach entsprechenden Beweisen.
2. Wenn Sie Beweise gefunden haben, überprüfen Sie, ob die Verbindung mithilfe von Remote Credential Guard hergestellt wurde.
3. Wenn ja, **schließen** Sie die Sicherheitswarnung, da es sich um eine **B-TP**-Aktivität (unbedenklich richtig positiv) handelt.

Es gibt benutzerdefinierte Anwendungen, die Tickets im Auftrag des Benutzers weiterleiten. Diese Anwendungen verfügen über Delegierungsberechtigungen für Benutzertickets.

1. Gibt es eine benutzerdefinierte Anwendung wie die zuvor beschriebene derzeit auf den Zielcomputern? Welche Dienste werden von der Anwendung ausgeführt? Werden die Dienste durch Anweisung der Benutzer ausgeführt, beispielsweise zum Zugreifen auf Datenbanken?
    - Wenn ja, **schließen** Sie die Sicherheitswarnung, da es sich um eine **B-TP**-Aktivität (unbedenklich richtig positiv) handelt.
2. Ist der Zielcomputer ein Delegierungsserver?
    - Wenn ja, **schließen** Sie die Sicherheitswarnung, und schließen Sie diesen Computer als **B-TP**-Aktivität (unbedenklich richtig positiv) aus.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie die [Quell- und Zielcomputer](investigate-a-computer.md).
2. Untersuchen Sie den [kompromittierten Benutzer](investigate-a-computer.md).

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

1. Setzen Sie das Kennwort des Quellbenutzers zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
2. Isolieren Sie die Quell- und Zielcomputer.
3. Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
4. Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
5. Wenn Windows Defender ATP installiert ist, nutzen Sie **klist.exe purge**, um alle Tickets der angegebenen Anmeldesitzung endgültig zu löschen und zu verhindern, dass die Tickets in Zukunft verwendet werden.

## <a name="suspected-ntlm-authentication-tampering-external-id-2039"></a>Suspected NTLM authentication tampering (external ID 2039) (Vermutete Manipulation der NTLM-Authentifizierung [Externe ID 2039])

Im Juni 2019 hat Microsoft das [Sicherheitsrisiko CVE-2019-1040](https://portal.msrc.microsoft.com/security-guidance/advisory/CVE-2019-1040) veröffentlicht und die Ermittlung einer neuen Manipulationsrisikos in Microsoft Windows angekündigt, wenn ein Man-in-the-Middle-Angriff die NTLM-MIC (Message Integrity Check) erfolgreich umgehen kann.

Böswillige Akteure, die dieses Sicherheitsrisiko erfolgreich ausnutzen, können NTLM-Sicherheitsfeatures herabstufen und erfolgreich authentifizierte Sitzungen im Namen anderer Konten erstellen. Nicht gepatchte Windows-Server sind durch dieses Sicherheitsrisiko gefährdet.

Bei dieser Erkennung wird eine Azure ATP-Sicherheitswarnung ausgelöst, wenn NTLM-Authentifizierungsanforderungen an einen Domänencontroller im Netzwerk gerichtet werden, die im Verdacht stehen, die Sicherheitslücke [CVE-2019-1040](https://portal.msrc.microsoft.com/security-guidance/advisory/CVE-2019-1040) auszunutzen.

**TP, B-TP oder FP?**

1. Handelt es sich bei den beteiligten Computern, einschließlich Domänencontroller, um aktuelle und für [CVE-2019-1040](https://portal.msrc.microsoft.com/security-guidance/advisory/CVE-2019-1040) gepatchte Computer? Wenn die Computer aktuell und gepatcht sind, wird erwartet, dass die Authentifizierung fehlschlägt. Wenn die Authentifizierung fehlgeschlagen ist, **schließen** Sie die Sicherheitswarnung als fehlgeschlagenen Versuch.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie die [Quellcomputer](investigate-a-computer.md).
2. Untersuchen Sie das [Quellkonto](investigate-a-user.md).

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

**Wartung**

1. Isolieren Sie die Quellcomputer.
2. Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
3. Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
4. Erzwingen Sie die Verwendung der versiegelten NTLMv2-Authentifizierung in der Domäne, indem Sie die Gruppenrichtlinie **Netzwerksicherheit: LAN Manager-Authentifizierungsebene** verwenden. Weitere Informationen zum Festlegen von Gruppenrichtlinien für Domänencontroller finden Sie unter [Network security: LAN Manager authentication level (Netzwerksicherheit: LAN Manager-Authentifizierungsebene)](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-lan-manager-authentication-level).

**Vorbeugung**

• Stellen Sie sicher, dass alle Geräte in der Umgebung auf dem aktuellen Stand und für [CVE-2019-1040](https://portal.msrc.microsoft.com/security-guidance/advisory/CVE-2019-1040) gepatcht sind.

## <a name="suspected-ntlm-relay-attack-exchange-account-external-id-2037"></a>Vermuteter NTLM-Relaisangriff (Exchange-Konto) (externe ID 2037)

**Beschreibung**

Ein Exchange-Server kann so konfiguriert werden, dass die NTLM-Authentifizierung mit dem Exchange-Server-Konto bei einem HTTP-Remoteserver ausgelöst wird, der von einem Angreifer betrieben wird. Dieser Server wartet darauf, dass die Kommunikation des Exchange-Servers die eigene vertrauliche Authentifizierung auf einen anderen Server oder über LDAP auf Active Directory überträgt, und greift dann die Authentifizierungsinformationen ab.

Sobald der Relaisserver die NTLM-Authentifizierung empfängt, wird eine Abfrage durchgeführt, die vom Zielserver erstellt wurde. Der Client antwortet auf dieser Abfrage und verhindert so, dass der Angreifer antworten kann. Auf diese Weise kann der NTLM-Vorgang mit dem Zieldomänencontroller fortgesetzt werden.

Hierbei wird eine Warnung ausgelöst, wenn Azure ATP ermittelt, dass die Anmeldeinformationen eines Exchange-Kontos von einer verdächtigen Quelle verwendet werden.

**TP, B-TP oder FP?**

1. Überprüfen Sie die zur IP-Adresse gehörigen Quellcomputer.
    1. Wenn der Quellcomputer ein Exchange-Server ist, **schließen** Sie die Sicherheitswarnung als **FP-Aktivität**.
    2. Legen Sie fest, ob das Quellkonto sich von diesen Computern aus über NTLM authentifizieren muss. Wenn das der Fall ist, **schließen** Sie die Sicherheitswarnung, und schließen Sie diese Computer als **B-TP-Aktivität** aus.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Setzen Sie die [Untersuchung der Quellcomputer](investigate-a-computer.md) mit den entsprechenden IP-Adressen fort.
2. Untersuchen Sie das [Quellkonto](investigate-a-user.md).

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

1. Isolieren Sie die Quellcomputer.
    1. Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
    2. Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
2. Erzwingen Sie die Verwendung der versiegelten NTLMv2-Authentifizierung in der Domäne, indem Sie die Gruppenrichtlinie **Netzwerksicherheit: LAN Manager-Authentifizierungsebene** verwenden. Weitere Informationen zum Festlegen von Gruppenrichtlinien für Domänencontroller finden Sie unter [Network security: LAN Manager authentication level (Netzwerksicherheit: LAN Manager-Authentifizierungsebene)](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-lan-manager-authentication-level).

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

1. Setzen Sie das Kennwort des Quellbenutzers zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
2. Kontrollieren Sie den Quellcomputer.
3. Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
4. Suchen Sie nach Benutzern, die zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.

**Vorbeugung**

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

1. Setzen Sie die Kennwörter der kompromittierten Benutzer zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
2. Kontrollieren Sie den Quellcomputer.
3. Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
4. Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der verdächtigen Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
5. Setzen Sie die Kennwörter des Quellbenutzers zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.

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
