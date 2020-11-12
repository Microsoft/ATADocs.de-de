---
title: Microsoft Defender for Identity-Sicherheitswarnungen zu Lateral Movement
description: In diesem Artikel werden die Microsoft Defender for Identity-Warnungen erläutert, die ausgegeben werden, wenn Angriffe in Ihrer Organisation erkannt werden, die in der Regel Teil der Maßnahmen der Lateral Movement-Phase sind.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 774f8f3f560b52d5a39a96aacc9b145d1ca2d445
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93275801"
---
# <a name="tutorial-lateral-movement-alerts"></a>Tutorial: Lateral Movement-Warnungen

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Cyberangriffe werden üblicherweise auf alle zugänglichen Entitäten wie etwa Benutzer mit geringen Rechten durchgeführt. Anschließend dringt der Angreifer schnell im internen Netzwerk vor (Lateral Movement), um Zugriff auf wertvolle Ressourcen zu erhalten. Dabei kann es sich um sensible Konten, Konten von Domänenadministratoren oder streng vertrauliche Daten handeln. [!INCLUDE [Product long](includes/product-long.md)] identifiziert diese komplexen Bedrohungen an der Quelle über die gesamte Kette der Angriffsabwehr hinweg und ordnet sie in die folgenden Phasen ein:

1. [Reconnaissance](reconnaissance-alerts.md)
1. [Kompromittierte Anmeldeinformationen](compromised-credentials-alerts.md)
1. **Seitliche Verschiebung**
1. [Warnungen zu Domänendominanz](domain-dominance-alerts.md)
1. [Exfiltration](exfiltration-alerts.md)

Weitere Informationen zur Struktur und zu gängigen Komponenten aller [!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnungen finden Sie unter [Grundlegendes zu Sicherheitswarnungen](understanding-security-alerts.md). Weitere Informationen zu **True Positive (TP)** , **Benign True Positive (B-TP)** (unschädlich richtig positiv) und **False Positive (FP)** finden Sie unter [Klassifizierungen der Sicherheitswarnungen](understanding-security-alerts.md#security-alert-classifications).

Die folgenden Sicherheitswarnungen unterstützen Sie dabei, verdächtige Aktivitäten zu identifizieren und zu unterbinden, die von [!INCLUDE [Product short](includes/product-short.md)] in Ihrem Netzwerk erkannt werden und auf **Lateral Movement** hindeuten. In diesem Tutorial erfahren Sie, wie die folgenden Angriffstypen klassifiziert, behoben und unterbunden werden:

> [!div class="checklist"]
>
> - Remotecodeausführung über DNS (externe ID 2036)
> - Suspected identity theft (pass-the-hash) (Verdacht auf Identitätsdiebstahl (Pass-the-Hash)) (externalid 2017)
> - Suspected identity theft (pass-the-ticket) (Verdacht auf Identitätsdiebstahl (Pass-the-Ticket)) (externalid 2018)
> - Suspected NTLM authentication tampering (external ID 2039) (Vermutete Manipulation der NTLM-Authentifizierung [Externe ID 2039])
> - Vermuteter NTLM-Relaisangriff (Exchange-Konto) (externe ID 2037)
> - Suspected overpass-the-hash attack (Kerberos) (Verdacht auf einen Overpass-the-Hash-Angriff (Kerberos)) (externalid 2002)
> - Mutmaßliche Verwendung von Rogue-Kerberos-Zertifikat (externe ID 2047)
> - Mutmaßliche Manipulation von SMB-Paketen (Exploit von CVE-2020-0796) (Vorschau) (externe ID 2406)

<!-- * Suspected overpass-the-hash attack (encryption downgrade) (external ID 2008)-->

## <a name="remote-code-execution-over-dns-external-id-2036"></a>Remotecodeausführung über DNS (externe ID 2036)

**Beschreibung**

Am 11.12.2018 hat Microsoft [CVE-2018-8626](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2018-8626) veröffentlicht und gibt bekannt, dass bei Windows DNS-Servern (Domain Name System) ein neues Sicherheitsrisiko bei der Remotecodeausführung erkannt wurde. Bei diesem Sicherheitsrisiko können Server Anforderungen nicht mehr ordnungsgemäß verarbeiten. Ein Angreifer, der dieses Sicherheitsrisiko erfolgreich ausnutzt, kann im Kontext des lokalen Systemkontos beliebigen Code ausführen. Derzeit als DNS-Server konfigurierte Windows-Server sind von diesem Sicherheitsrisiko betroffen.

Bei dieser Erkennung wird eine [!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnung ausgelöst, wenn DNS-Abfragen an einen Domänencontroller im Netzwerk gerichtet werden, die im Verdacht stehen, die Sicherheitslücke CVE-2018-8626 auszunutzen.

**Lernphase**

Nicht zutreffend

**TP, B-TP oder FP**

1. Sind Sie die Zielcomputer auf dem neuesten Stand und für CVE-2018-8626 gepatcht?
    - Wenn die Computer auf dem neuesten Stand und gepatcht sind, **schließen** Sie die Sicherheitswarnung als **FP**.
1. Wurde ungefähr zum Zeitpunkt des Angriffs ein Dienst erstellt oder ein unbekannter Prozess ausgeführt?
    - Wenn Sie keinen neuen Dienst oder einen unbekannten Prozess finden, **schließen** Sie die Sicherheitswarnung als **FP**.
1. Diese Art von Angriff kann den DNS-Dienst zum Absturz bringen, bevor die Codeausführung erfolgreich veranlasst wurde.
    - Überprüfen Sie, ob der DNS-Dienst ungefähr zum Zeitpunkt des Angriffs mehrmals neu gestartet wurde.
    - Wenn der DNS-Dienst neu gestartet wurde, handelte es sich wahrscheinlich um einen Versuch, CVE-2018-8626 auszunutzen. Betrachten Sie diese Warnung als **TP** , und führen Sie die unter **Ermitteln des Umfangs der Sicherheitsverletzung** beschriebenen Anweisungen aus.

**Ermitteln des Umfangs der Sicherheitsverletzung**

- Untersuchen Sie die [Quell- und Zielcomputer](investigate-a-computer.md).

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

**Wartung**

1. Isolieren Sie die Domänencontroller.
    1. Unterbinden Sie die versuchte Remotecodeausführung.
    1. Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der verdächtigen Aktivität ebenfalls angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Kontrollieren Sie den Quellcomputer.
    1. Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
    1. Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der verdächtigen Aktivität ebenfalls angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.

**Vorbeugung**

- Stellen Sie sicher, dass alle DNS-Server in der Umgebung auf dem aktuellen Stand und für [CVE-2018-8626](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2018-8626) gepatcht sind.

## <a name="suspected-identity-theft-pass-the-hash-external-id-2017"></a>Suspected identity theft (pass-the-hash) (Verdacht auf Identitätsdiebstahl (Pass-the-Hash)) (externalid 2017)

*Vorheriger Name* : Identitätsdiebstahl mithilfe eines Pass-the-Hash-Angriffs

**Beschreibung**

Pass-the-Hash ist eine Technik mit seitlicher Bewegung, bei der Angreifer den NTLM-Hash eines Benutzers von einem Computer stehlen und diesen verwenden, um Zugriff auf einen anderen Computer zu erlangen.

**Lernphase**

Nicht zutreffend

**TP, B-TP oder FP?**
1. Wurde der Hash auf Computern verwendet, die der Benutzer regelmäßig verwendet?
    - Wenn der Hash regelmäßig auf Computern verwendet wurde, **Schließen** Sie die Warnung als **FP** -Aktivität (falsch positiv).

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie die [Quell- und Zielcomputer](investigate-a-computer.md) weiter.
1. Untersuchen Sie den [kompromittierten Benutzer](investigate-a-computer.md).

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

1. Setzen Sie das Kennwort des Quellbenutzers zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Isolieren Sie die Quell- und Zielcomputer.
1. Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
1. Finden Sie heraus, ob sich ungefähr gleichzeitig mit der Aktivität Benutzer angemeldet haben, da auch sie kompromittiert sein könnten. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.

## <a name="suspected-identity-theft-pass-the-ticket-external-id-2018"></a>Suspected identity theft (pass-the-ticket) (Verdacht auf Identitätsdiebstahl (Pass-the-Ticket)) (externalid 2018)

*Vorheriger Name* : Identitätsdiebstahl mithilfe eines Pass-the-Ticket-Angriffs

**Beschreibung**

Pass-the-Ticket ist eine Technik mit seitlicher Bewegung, bei der die Angreifer ein Kerberos-Ticket von einem Computer stehlen und dieses verwenden, um Zugriff auf einen anderen Computer zu erlangen, indem sie das gestohlene Ticket wiederverwenden. In dieser Erkennung wird ein Kerberos-Ticket auf zwei (oder mehr) verschiedenen Computern verwendet.

**Lernphase**

Nicht zutreffend

**TP, B-TP oder FP?**

Das erfolgreiche Auflösen von IP-Adressen für Computer in der Organisation ist wichtig, um Pass-The-Ticket-Angriffe von einem Computer auf einen anderen zu identifizieren.

1. Überprüfen Sie, ob die IP-Adresse von einem oder beiden Computern zu einem Subnetz gehört, das aus einem zu kleinen DHCP-Pool (z. B. VPN, VDI oder WiFi) zugewiesen wird.
1. Wurde die IP-Adresse freigegeben (z. B. durch ein NAT-Gerät)?
1. Werden eine oder mehrere Ziel-IP-Adressen vom Sensor nicht aufgelöst? Wenn eine Ziel-IP-Adresse nicht aufgelöst wird, kann dies bedeuten, dass die richtigen Ports zwischen dem Sensor und den Geräten nicht ordnungsgemäß geöffnet sind.

    Wenn die Antwort auf eine der vorausgegangenen Fragen **Ja** lautet, überprüfen Sie, ob Quell- und Zielcomputer identisch sind. Sind sie identisch, handelt es sich um eine **FP** -Aktivität (falsch positiv), und es haben keine echten **Pass-the-Ticket** -Versuche stattgefunden.

Das Feature [Remote Credential Guard](/windows/security/identity-protection/remote-credential-guard) der RDP-Verbindungen kann zu **B-TP** -Warnungen führen, wenn es mit Windows 10 auf Windows Server 2016 und höher verwendet wird.
Überprüfen Sie mithilfe der Warnungsbeweisen, ob der Benutzer eine Remotedesktopverbindung vom Quellcomputer zum Zielcomputer hergestellt hat.

1. Suchen Sie nach entsprechenden Beweisen.
1. Wenn Sie Beweise gefunden haben, überprüfen Sie, ob die Verbindung mithilfe von Remote Credential Guard hergestellt wurde.
1. Wenn ja, **schließen** Sie die Sicherheitswarnung, da es sich um eine **B-TP** -Aktivität (unbedenklich richtig positiv) handelt.

Es gibt benutzerdefinierte Anwendungen, die Tickets im Auftrag des Benutzers weiterleiten. Diese Anwendungen verfügen über Delegierungsberechtigungen für Benutzertickets.

1. Gibt es eine benutzerdefinierte Anwendung wie die zuvor beschriebene derzeit auf den Zielcomputern? Welche Dienste werden von der Anwendung ausgeführt? Werden die Dienste durch Anweisung der Benutzer ausgeführt, beispielsweise zum Zugreifen auf Datenbanken?
    - Wenn ja, **schließen** Sie die Sicherheitswarnung, da es sich um eine **B-TP** -Aktivität (unbedenklich richtig positiv) handelt.
1. Ist der Zielcomputer ein Delegierungsserver?
    - Wenn ja, **schließen** Sie die Sicherheitswarnung, und schließen Sie diesen Computer als **B-TP** -Aktivität (unbedenklich richtig positiv) aus.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie die [Quell- und Zielcomputer](investigate-a-computer.md).
1. Untersuchen Sie den [kompromittierten Benutzer](investigate-a-computer.md).

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

1. Setzen Sie das Kennwort des Quellbenutzers zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Isolieren Sie die Quell- und Zielcomputer.
1. Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
1. Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Wenn Microsoft Defender for Endpoint installiert ist, nutzen Sie **klist.exe purge** , um alle Tickets der angegebenen Anmeldesitzung endgültig zu löschen und zu verhindern, dass die Tickets in Zukunft verwendet werden.

## <a name="suspected-ntlm-authentication-tampering-external-id-2039"></a>Suspected NTLM authentication tampering (external ID 2039) (Vermutete Manipulation der NTLM-Authentifizierung [Externe ID 2039])

Im Juni 2019 hat Microsoft das [Sicherheitsrisiko CVE-2019-1040](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2019-1040) veröffentlicht und die Ermittlung einer neuen Manipulationsrisikos in Microsoft Windows angekündigt, wenn ein Man-in-the-Middle-Angriff die NTLM-MIC (Message Integrity Check) erfolgreich umgehen kann.

Böswillige Akteure, die dieses Sicherheitsrisiko erfolgreich ausnutzen, können NTLM-Sicherheitsfeatures herabstufen und erfolgreich authentifizierte Sitzungen im Namen anderer Konten erstellen. Nicht gepatchte Windows-Server sind durch dieses Sicherheitsrisiko gefährdet.

Bei dieser Erkennung wird eine [!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnung ausgelöst, wenn NTLM-Authentifizierungsanforderungen an einen Domänencontroller im Netzwerk gerichtet werden, die im Verdacht stehen, die Sicherheitslücke [CVE-2019-1040](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2019-1040) auszunutzen.

**Lernphase**

Nicht zutreffend

**TP, B-TP oder FP?**

1. Sind die beteiligten Computer, einschließlich Domänencontrollern, auf dem neuesten Stand und für [CVE-2019-1040](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2019-1040) gepatcht?
    - Wenn die Computer auf dem neuesten Stand und gepatcht sind, gehen wir davon aus, dass die Authentifizierung fehlschlägt. Wenn die Authentifizierung fehlgeschlagen ist, **schließen** Sie die Sicherheitswarnung als fehlgeschlagenen Versuch.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie die [Quellcomputer](investigate-a-computer.md).
1. Untersuchen Sie das [Quellkonto](investigate-a-user.md).

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

**Wartung**

1. Isolieren Sie die Quellcomputer.
1. Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
1. Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Erzwingen Sie die Verwendung der versiegelten NTLMv2-Authentifizierung in der Domäne, indem Sie die Gruppenrichtlinie **Netzwerksicherheit: LAN Manager-Authentifizierungsebene** verwenden. Weitere Informationen zum Festlegen von Gruppenrichtlinien für Domänencontroller finden Sie unter [Network security: LAN Manager authentication level (Netzwerksicherheit: LAN Manager-Authentifizierungsebene)](/windows/security/threat-protection/security-policy-settings/network-security-lan-manager-authentication-level).

**Vorbeugung**

- Stellen Sie sicher, dass alle Geräte in der Umgebung auf dem aktuellen Stand und für [CVE-2019-1040](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2019-1040) gepatcht sind.

## <a name="suspected-ntlm-relay-attack-exchange-account-external-id-2037"></a>Vermuteter NTLM-Relaisangriff (Exchange-Konto) (externe ID 2037)

**Beschreibung**

Ein Exchange-Server kann so konfiguriert werden, dass die NTLM-Authentifizierung mit dem Exchange-Server-Konto bei einem HTTP-Remoteserver ausgelöst wird, der von einem Angreifer betrieben wird. Dieser Server wartet darauf, dass die Kommunikation des Exchange-Servers die eigene vertrauliche Authentifizierung auf einen anderen Server oder über LDAP auf Active Directory überträgt, und greift dann die Authentifizierungsinformationen ab.

Sobald der Relaisserver die NTLM-Authentifizierung empfängt, wird eine Abfrage durchgeführt, die vom Zielserver erstellt wurde. Der Client antwortet auf dieser Abfrage und verhindert so, dass der Angreifer antworten kann. Auf diese Weise kann der NTLM-Vorgang mit dem Zieldomänencontroller fortgesetzt werden.

Hierbei wird eine Warnung ausgelöst, wenn [!INCLUDE [Product short](includes/product-short.md)] ermittelt, dass die Anmeldeinformationen eines Exchange-Kontos von einer verdächtigen Quelle verwendet werden.

**Lernphase**

Nicht zutreffend

**TP, B-TP oder FP?**

1. Überprüfen Sie die zur IP-Adresse gehörigen Quellcomputer.
    1. Wenn der Quellcomputer ein Exchange-Server ist, **schließen** Sie die Sicherheitswarnung als **FP-Aktivität**.
    1. Legen Sie fest, ob das Quellkonto sich von diesen Computern aus über NTLM authentifizieren muss. Wenn das der Fall ist, **schließen** Sie die Sicherheitswarnung, und schließen Sie diese Computer als **B-TP-Aktivität** aus.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Setzen Sie die [Untersuchung der Quellcomputer](investigate-a-computer.md) mit den entsprechenden IP-Adressen fort.
1. Untersuchen Sie das [Quellkonto](investigate-a-user.md).

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

1. Isolieren Sie die Quellcomputer.
    1. Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
    1. Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Erzwingen Sie die Verwendung der versiegelten NTLMv2-Authentifizierung in der Domäne, indem Sie die Gruppenrichtlinie **Netzwerksicherheit: LAN Manager-Authentifizierungsebene** verwenden. Weitere Informationen zum Festlegen von Gruppenrichtlinien für Domänencontroller finden Sie unter [Network security: LAN Manager authentication level (Netzwerksicherheit: LAN Manager-Authentifizierungsebene)](/windows/security/threat-protection/security-policy-settings/network-security-lan-manager-authentication-level).

<!--
## Suspected overpass-the-hash attack (encryption downgrade) (external ID 2008)

*Previous name:* Encryption downgrade activity

**Description**

Encryption downgrade is a method of weakening Kerberos using encryption downgrade of different fields of the protocol, normally encrypted using the highest levels of encryption. A weakened encrypted field can be an easier target to offline brute force attempts. Various attack methods utilize weak Kerberos encryption cyphers. In this detection, [!INCLUDE [Product short](includes/product-short.md)] learns the Kerberos encryption types used by computers and users, and alerts you when a weaker cypher is used that is unusual for the source computer, and/or user, and matches known attack techniques.

In an over-pass-the-hash attack, an attacker can use a weak stolen hash to create a strong ticket, with a Kerberos AS request. In this detection,  instances are detected where the AS_REQ message encryption type from the source computer is downgraded, when compared to the previously learned behavior (the computer used AES).

**Learning period**

Not applicable

**TP, B-TP, or FP?**

1. Determine if the smartcard configuration recently changed.
    - Did the accounts involved recently have smartcard configurations changes?

      If the answer is yes, **Close** the security alert as a **T-BP** activity.

Some legitimate resources don't support strong encryption ciphers and may trigger this alert.

1. Do all source users share something?
    1. For example, are all of your marketing personnel accessing a specific resource that could cause the alert to be triggered?
    1. Check the resources accessed by those tickets.
       - Check this in Active Directory by checking the attribute *msDS-SupportedEncryptionTypes*, of the resource service account.
    1. If there is only one accessed resource, check if it is a valid resource for these users to access.

      If the answer to one of the previous questions is **yes**, it is likely to be a **T-BP** activity. Check if the resource can support a strong encryption cipher, implement a stronger encryption cipher where possible, and **Close** the security alert.

**Understand the scope of the breach**

1. Investigate the [source computer](investigate-a-computer.md).
1. Investigate the [compromised user](investigate-a-computer.md).

**Suggested remediation and steps for prevention**

**Remediation**

1. Reset the password of the source user and enable MFA or, if you have configured the relevant high-risk user policies in Azure Active Directory Identity Protection, you can use the [**Confirm user compromised**](/cloud-app-security/accounts#governance-actions) action in the Cloud App Security portal.
1. Contain the source computer.
1. Find the tool that performed the attack and remove it.
1. Look for users logged on around the time of the activity, as they may also be compromised. Reset their passwords and enable MFA or, if you have configured the relevant high-risk user policies in Azure Active Directory Identity Protection, you can use the [**Confirm user compromised**](/cloud-app-security/accounts#governance-actions) action in the Cloud App Security portal.

**Prevention**

1. Configure your domain to support strong encryption cyphers, and remove *Use Kerberos DES encryption types*. Learn more about [encryption types and Kerberos](/archive/blogs/openspecification/windows-configurations-for-kerberos-supported-encryption-type).
1. Make sure the domain functional level is set to support strong encryption cyphers.
1. Give preference to using applications that support strong encryption cyphers.
-->

## <a name="suspected-overpass-the-hash-attack-kerberos-external-id-2002"></a>Suspected overpass-the-hash attack (Kerberos) (Verdacht auf einen Overpass-the-Hash-Angriff (Kerberos)) (externalid 2002)

*Vorheriger Name* : Ungewöhnliche Kerberos-Protokollimplementierung (potenzieller Overpass-the-Hash-Angriff)

**Beschreibung**

Angreifer verwenden Tools, die verschiedene Protokolle wie Kerberos und SMB auf nicht standardmäßige Arten implementieren. Während diese Art des Netzwerkdatenverkehrs von Microsoft Windows ohne Warnungen akzeptiert wird, kann [!INCLUDE [Product short](includes/product-short.md)] potenziell böswillige Absichten erkennen. Das Verhalten weist auf Techniken hin, wie sie beispielsweise für Overpass-the-Hash, Brute-Force oder erweiterte Ransomware-Exploits, z. B. WannaCry, verwendet werden.

**Lernphase**

Nicht zutreffend

**TP, B-TP oder FP?**

Zuweilen implementieren Anwendungen einen eigenen Kerberos-Stapel, der nicht der Kerberos-RFC-Dokumentation entspricht.

1. Überprüfen Sie, ob auf dem Quellcomputer eine Anwendung mit ihrem eigenen Kerberos-Stapel ausgeführt wird, und dies im Widerspruch zur Kerberos-RFC steht.
1. Führt der Quellcomputer eine solche Anwendung aus, obwohl er dies **nicht** tun sollte, korrigieren Sie die Anwendungskonfiguration. **Schließen** Sie die Sicherheitswarnung als **B-TP** -Aktivität (unbedenklich richtig positiv).
1. Führt der Quellcomputer eine solche Anwendung aus, und soll er das auch weiterhin tun, **schließen** Sie die Sicherheitswarnung als **B-TP** -Aktivität (unbedenklich richtig positiv), und schließen Sie diesen Computer aus.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie den [Quellcomputer](investigate-a-computer.md).
1. Wenn ein [Quellbenutzer](investigate-a-user.md) vorhanden ist, untersuchen Sie diesen.

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

1. Setzen Sie die Kennwörter der kompromittierten Benutzer zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Kontrollieren Sie den Quellcomputer.
1. Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
1. Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der verdächtigen Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Setzen Sie die Kennwörter des Quellbenutzers zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.

<!-- REMOVE BOOKMARK FROM TITLE WHEN PREVIEW REMOVED -->

<a name="suspected-smb-packet-manipulation-cve-2020-0796-exploitation-external-id-2406"></a>

## <a name="suspected-rogue-kerberos-certificate-usage-external-id-2047"></a>Mutmaßliche Verwendung von Rogue-Kerberos-Zertifikat (externe ID 2047)

**Beschreibung**

Ein Rogue-Zertifikatsangriff ist eine Persistenztechnik, die von Angreifern verwendet wird, nachdem sie die Kontrolle über die Organisation erlangt haben. Angreifer kompromittieren den Zertifizierungsstellenserver (CA) und generieren Zertifikate, die in zukünftigen Angriffen als Hintertürkonten verwendet werden können.

**Lernphase**

Nicht zutreffend

**TP, B-TP oder FP?**

- Wird dieses Konto regelmäßig für die Anmeldung beim Computer verwendet?
  - Wenn das Zertifikat regelmäßig vom Computer verwendet wird, **schließen** Sie die Warnung als **FP** -Aktivität.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie den [Quellcomputer](investigate-a-computer.md).
2. Untersuchen Sie den [Quellbenutzer](investigate-a-user.md).
3. Überprüfen Sie, auf welche Ressourcen erfolgreich zugegriffen wurde, und [untersuchen](investigate-a-computer.md) Sie diese.

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

1. Setzen Sie das Kennwort des Quellbenutzers zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Kontrollieren Sie den Quellcomputer.
    - Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
    - Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Suchen Sie das Zertifikat, das auf dem Zertifizierungsstellenserver verwendet wird, und widerrufen Sie es, indem Sie die TLS und SSL vor dem geplanten Ablaufdatum ungültig machen.

## <a name="suspected-smb-packet-manipulation-cve-2020-0796-exploitation---preview-external-id-2406"></a>Mutmaßliche Manipulation von SMB-Paketen (Exploit von CVE-2020-0796) (Vorschau) (externe ID 2406)

**Beschreibung**

12.3.2020 Microsoft hat [CVE-2020-0796](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2020-0796) veröffentlicht und dabei angekündigt, dass ein neues Sicherheitsrisiko bei der Remotecodeausführung vorliegt, in der das Protokoll von Microsoft Server Message Block 3.1.1 (SMBv3) bestimmte Anforderungen verarbeitet. Ein Angreifer, der das Sicherheitsrisiko erfolgreich ausgenutzt hat, könnte die Möglichkeit erhalten, Code auf dem Zielserver oder -client auszuführen. Nicht gepatchte Windows-Server sind durch dieses Sicherheitsrisiko gefährdet.

Bei dieser Erkennung wird eine [!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnung ausgelöst, wenn das SMBv3-Paket an einen Domänencontroller im Netzwerk gerichtet wird, der im Verdacht steht, die Sicherheitslücke CVE-2020-0796 auszunutzen.

**Lernphase**

Nicht zutreffend

**TP, B-TP oder FP?**

1. Sind die beteiligten Domänencontroller auf dem neuesten Stand und für CVE-2020-0796 gepatcht?
    - Wenn die Computer auf dem neuesten Stand und gepatcht sind, schlägt der Angriff höchstwahrscheinlich fehl. **Schließen** Sie die Sicherheitswarnung daher als fehlgeschlagener Versuch.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie den [Quellcomputer](investigate-a-computer.md).
1. Untersuchen Sie den Zieldomänencontroller.

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

**Wartung**

1. Kontrollieren Sie den Quellcomputer.
1. Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
1. Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der verdächtigen Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Wenn Sie über Computer mit Betriebssystemen verfügen, die [KB4551762](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4551762) nicht unterstützen, wird empfohlen, das SMBv3-Kompressionsfeature wie im Abschnitt zu [Problemumgehungen](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2020-0796) beschrieben in der Umgebung zu deaktivieren.

**Vorbeugung**

1. Stellen Sie sicher, dass alle Geräte in der Umgebung auf dem aktuellen Stand und für [CVE-2020-0796](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2020-0796) gepatcht sind.

> [!div class="nextstepaction"]
> [Tutorial: Warnung zu Domänendominanz](domain-dominance-alerts.md)

## <a name="see-also"></a>Weitere Informationen

- [Untersuchen eines Computers](investigate-a-computer.md)
- [Arbeiten mit Sicherheitswarnungen](working-with-suspicious-activities.md)
- [Arbeiten mit Lateral Movement-Pfaden](use-case-lateral-movement-path.md)
- [Warnungen zu Reconnaissance](reconnaissance-alerts.md)
- [Warnungen zu kompromittierten Anmeldeinformationen](compromised-credentials-alerts.md)
- [Warnungen zu Domänendominanz](domain-dominance-alerts.md)
- [Warnungen zu Exfiltration](exfiltration-alerts.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
