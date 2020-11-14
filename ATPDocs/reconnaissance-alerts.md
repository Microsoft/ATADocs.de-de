---
title: Microsoft Defender for Identity-Sicherheitswarnungen für die Reconnaissance-Phase
description: In diesem Artikel werden die Microsoft Defender for Identity-Warnungen erläutert, die ausgegeben werden, wenn Angriffe in Ihrer Organisation erkannt werden, die in der Regel Teil der Maßnahmen der Reconnaissance-Phase sind.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/27/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 1a21762351400d298154e7dbf7503fd7d820e0a2
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93275367"
---
# <a name="tutorial-reconnaissance-alerts"></a>Tutorial: Warnungen zu Reconnaissance

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Cyberangriffe werden üblicherweise auf alle zugänglichen Entitäten wie etwa Benutzer mit geringen Rechten durchgeführt. Anschließend dringt der Angreifer schnell im internen Netzwerk vor (Lateral Movement), um Zugriff auf wertvolle Ressourcen zu erhalten. Dabei kann es sich um sensible Konten, Konten von Domänenadministratoren oder streng vertrauliche Daten handeln. [!INCLUDE [Product long](includes/product-long.md)] identifiziert diese komplexen Bedrohungen an der Quelle über die gesamte Kette der Angriffsabwehr hinweg und ordnet sie in die folgenden Phasen ein:

1. **Reconnaissance**
1. [Kompromittierte Anmeldeinformationen](compromised-credentials-alerts.md)
1. [Seitliche Verschiebung](lateral-movement-alerts.md)
1. [Warnungen zu Domänendominanz](domain-dominance-alerts.md)
1. [Exfiltration](exfiltration-alerts.md)

Weitere Informationen zur Struktur und zu gängigen Komponenten aller [!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnungen finden Sie unter [Grundlegendes zu Sicherheitswarnungen](understanding-security-alerts.md). Weitere Informationen zu **True Positive (TP)** , **Benign True Positive (B-TP)** (unschädlich richtig positiv) und **False Positive (FP)** finden Sie unter [Klassifizierungen der Sicherheitswarnungen](understanding-security-alerts.md#security-alert-classifications).

Mit den folgenden Sicherheitswarnungen können Sie verdächtige Aktivitäten der Phase **Reconnaissance** identifizieren und beheben, die von [!INCLUDE [Product short](includes/product-short.md)] in Ihrem Netzwerk erkannt wurden.

In diesem Tutorial machen Sie sich mit den folgenden Angriffstypen vertraut und erfahren, wie Sie diese klassifizieren, unterbinden und im Vorfeld verhindern:

> [!div class="checklist"]
>
> - Reconnaissance über Kontoenumeration (externe ID 2003)
> - Active Directory-Attributreconnaissance (LDAP) (externe ID 2210)
> - Reconnaissance über Netzwerkzuordnungen (DNS) (externe ID 2007)
> - Sicherheitsprinzipalreconnaissance (LDAP) (externe ID 2038)
> - Reconnaissance über Benutzer und Gruppenmitgliedschaften (SAMR) (externe ID 2021)
> - Reconnaissance über Benutzer und IP-Adressen (SMB) (externe ID 2012)

## <a name="account-enumeration-reconnaissance-external-id-2003"></a>Reconnaissance über Kontoenumeration (externe ID 2003)

*Vorheriger Name* : Reconnaissance mithilfe von Kontoenumeration

**Beschreibung**

Bei Reconnaissancemaßnahmen über Kontoenumerationen verwendet ein Angreifer ein Wörterbuch mit Tausenden von Benutzernamen oder Tools wie KrbGuess, um Benutzernamen in Ihrer Domäne zu erraten.

**Kerberos** : Der Angreifer führt Kerberos-Anforderungen mit diesen Namen durch, um einen gültigen Benutzernamen in der Domäne aufzuspüren. Wenn dadurch ein Benutzername bestimmt wird, erhält der Angreifer die Kerberos-Fehlermeldung **Preauthentication required** (Vorauthentifizierung erforderlich) statt der Meldung **Security principal unknown** (Unbekannter Sicherheitsprinzipal).

**NTLM** : Der Angreifer führt NLTM-Authentifizierungsanforderungen mit diesem Wörterbuch mit Namen durch, um einen gültigen Benutzernamen in der Domäne aufzuspüren. Wenn dadurch ein Benutzername bestimmt wird, erhält der Angreifer die NTLM-Fehlermeldung **WrongPassword (0xc000006a)** statt der Meldung **NoSuchUser (0xc0000064)** .

Bei Erkennung dieser Warnung ermittelt [!INCLUDE [Product short](includes/product-short.md)] den Ursprung des Kontoenumerationsangriffs, die Gesamtzahl der Versuche zum Erraten des Namens und die Anzahl der gefundenen Übereinstimmungen. Wenn es zu viele unbekannte Benutzer gibt, erkennt [!INCLUDE [Product short](includes/product-short.md)] dies als verdächtige Aktivität.

**Lernphase**

Nicht zutreffend

**TP, B-TP oder FP?**

Einige Server und Anwendungen fragen Domänencontroller ab, um festzustellen, ob Konten in zulässigen Verwendungsszenarios zum Einsatz kommen.

Um festzustellen, ob es sich bei der Abfrage um den Typ **TP** , **B-TP** oder **FP** handelt, klicken Sie auf die Warnung, um die zugehörige Detailseite aufzurufen:

1. Überprüfen Sie, ob der Quellcomputer diese Abfrage tatsächlich ausführen sollte. Beispiele für **B-TP** könnten in diesem Fall Microsoft Exchange-Server oder Systeme der Personalverwaltung sein.

1. Überprüfen Sie die Kontodomänen.
    - Werden zusätzliche Benutzer angezeigt, die zu einer anderen Domäne gehören?  
     Eine Fehlkonfigurationen der Server kann z. B. bei Exchange/Skype oder ADSF dazu führen, dass zusätzliche Benutzer vorhanden sind, die verschiedenen Domänen angehören.
    - Sehen Sie sich die Konfiguration des problematischen Diensts an, um die Fehlkonfiguration zu beheben.

    Wenn Sie die obigen Fragen mit **Ja** beantwortet haben, handelt es sich um eine **B-TP** -Aktivität. *Schließen* Sie die Sicherheitswarnung.

Betrachten Sie im nächsten Schritt den Quellcomputer:

1. Wird auf dem Quellcomputer ein Skript oder eine Anwendung ausgeführt, die dieses Verhalten verursachen könnten?
    - Ist das Skript schon älter und wird es mit alten Anmeldeinformationen ausgeführt?  
    Wenn ja, beenden und bearbeiten Sie das Skript, oder löschen Sie es.
    - Handelt es sich um ein Verwaltungs- oder Sicherheitsskript bzw. um eine entsprechende Anwendung, die tatsächlich in der Umgebung ausgeführt werden soll?

      Wenn Sie die vorherige Frage mit **Ja** beantwortet haben, *schließen* Sie die Sicherheitswarnung, und schließen Sie diesen Computer aus. Vermutlich handelt es sich um eine **B-TP** -Aktivität.

Betrachten Sie nun die Konten:

Angreifer verwenden häufig ein Wörterbuch mit zufälligen Kontonamen, um vorhandene Kontonamen in einer Organisation zu finden.

1. Kommen Ihnen die nicht vorhandenen Konten vertraut vor?
    - Wenn ja, sind diese Konten möglicherweise deaktiviert, oder sie gehören Mitarbeitern, die das Unternehmen verlassen haben.
    - Überprüfen Sie, ob eine Anwendung oder ein Skript vorhanden ist, mit dem überprüft wird, welche Konten in Active Directory Domain Services noch vorhanden sind.

      Wenn Sie eine der vorherigen Fragen mit **Ja** beantwortet haben, *schließen* Sie die Sicherheitswarnung. Es handelt sich vermutlich um eine **B-TP** -Aktivität.

1. Wenn einer der Rateversuche mit einem vorhandenen Kontonamen übereinstimmt, kennt der Angreifer vorhandene Konten in Ihrer Umgebung und kann mit Brute-Force-Angriffen und gefundenen Benutzernamen versuchen, Zugriff auf Ihre Domäne zu erhalten.
    - Überprüfen Sie die erratenen Kontonamen auf weitere verdächtige Aktivitäten.
    - Überprüfen Sie, ob es sich bei den Konten um sensible Konten handelt.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie den Quellcomputer.
1. Wenn bei einem Rateversuch eine Übereinstimmung mit einem vorhandenen Kontonamen gefunden wird, kennt der Angreifer vorhandene Konten in Ihrer Umgebung und kann mit den gefundenen Benutzernamen Brute-Force-Angriffe ausführen, um Zugriff auf Ihre Domäne zu erhalten. Untersuchen Sie vorhandene Konten mithilfe des [Leitfadens für die Untersuchung von Benutzern](investigate-a-user.md).
    > [!NOTE]
    > Überprüfen Sie die Beweise, um das verwendete Authentifizierungsprotokoll zu ermitteln. Wenn die NTLM-Authentifizierung verwendet wurde, aktivieren Sie die NTLM-Überwachung des Windows-Ereignisses 8004 auf dem Domänencontroller, um den Ressourcenserver zu ermitteln, auf den die Benutzer zugreifen wollten.  
    > Windows-Ereignis 8004 ist das NTLM-Authentifizierungsereignis, das Informationen zum Quellcomputer, Benutzerkonto und Server enthält, auf die das Quellbenutzerkonto zugreifen wollte.  
    > [!INCLUDE [Product short](includes/product-short.md)] erfasst die auf Windows-Ereignis 4776 basierenden Daten des Quellcomputers, die den computerdefinierten Namen des Quellcomputers enthalten. Wenn Sie Windows-Ereignis 4776 verwenden, um diese Informationen zu erfassen, wird das Quellfeld der Informationen gelegentlich von dem Gerät oder der Software überschrieben, und es wird nur „Arbeitsstation“ oder „MSTSC“ als Informationsquelle angezeigt. Darüber hinaus ist der Quellcomputer möglicherweise nicht tatsächlich in Ihrem Netzwerk vorhanden. Dies ist möglich, da Angreifer in der Regel offene, über das Internet zugängliche Server außerhalb des Netzwerks zum Ziel haben und dies dann zum Auflisten Ihrer Benutzer verwenden. Wenn Sie häufig Geräte verwenden, die als „Arbeitsstation“ oder „MSTSC“ angezeigt werden, vergewissern Sie sich, dass die NTLM-Überwachung auf den Domänencontrollern aktiviert ist, um den Namen des Ressourcenservers zu erhalten, auf den zugegriffen wurde. Sie sollten diesen Server ebenfalls untersuchen und überprüfen, ob er zum Internet geöffnet ist, und ihn ggf. schließen.

1. Wenn Sie wissen, welcher Server die Authentifizierungsüberprüfung gesendet hat, untersuchen Sie den Server, indem Sie Ereignisse wie das Windows-Ereignis 4624 überprüfen, um den Authentifizierungsprozess besser nachvollziehen zu können.

1. Überprüfen Sie, ob dieser Server mithilfe von offenen Ports eine Verbindung mit dem Internet herstellt. Verwendet der Server beispielsweise RDP für die Verbindung mit dem Internet?

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

1. Isolieren Sie den [Quellcomputer](investigate-a-computer.md).
    1. Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
    1. Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch kompromittiert sind.
    1. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Erzwingen Sie [komplexe und lange Kennwörter](/windows/device-security/security-policy-settings/password-policy) in der Organisation. Komplexe und lange Kennwörter stellen die erste Sicherheitsstufe zum Schutz vor Brute-Force-Angriffen dar. Diese sind nach der Enumeration normalerweise der nächste Schritt in der Kill Chain des Cyberangriffs.

## <a name="active-directory-attributes-reconnaissance-ldap-external-id-2210"></a>Active Directory-Attributreconnaissance (LDAP) (externe ID 2210)

**Beschreibung**

Die Active Directory-LDAP-Reconnaissance wird von Angreifern verwendet, um wichtige Informationen über die Domänenumgebung zu erhalten. Diese Informationen können Angreifern helfen, die Domänenstruktur zu erfassen und auch privilegierte Konten für die Verwendung in späteren Schritten in ihrer Angriffsabwehrkette zu identifizieren. Lightweight Directory Access Protocol (LDAP) ist eine der sowohl für zulässige als auch böswillige Zwecke am häufigsten verwendeten Methoden zum Abfragen von Active Directory.

**Lernphase**

Nicht zutreffend

**TP, B-TP oder FP?**

1. Klicken Sie auf die Warnung, um die ausgeführten Abfragen anzuzeigen.
    - Überprüfen Sie, ob der Quellcomputer diese Abfragen ausführen soll.
        - Falls ja, schließen Sie die Sicherheitswarnung als **FP** -Aktivität. Wenn es sich um eine laufende Aktivität handelt, schließen Sie die verdächtige Aktivität aus.
1. Klicken Sie auf den Quellcomputer, und rufen Sie seine Profilseite auf.
    - Suchen Sie nach ungewöhnlichen Aktivitäten, die zum Zeitpunkt der Abfrage aufgetreten sind. Beispiele für Suchtypen sind angemeldete Benutzer, Ressourcen, auf die zugegriffen wurde und andere Überprüfungsabfragen.
    - Wenn die Microsoft Defender für Endpunkt-Integration aktiviert ist, klicken Sie auf das Symbol, um den Computer genauer zu untersuchen.
        - Suchen Sie nach ungewöhnlichen Prozessen und Warnungen, die zum Zeitpunkt der Abfrage aufgetreten sind.
1. Überprüfen Sie offengelegte Konten.
    - Suchen Sie nach ungewöhnlichen Aktivitäten.

Wenn Sie Frage 2 oder 3 mit „Ja“ beantwortet haben, betrachten Sie diese Warnung als **TP** , und führen Sie die unter **Ermitteln des Umfangs der Sicherheitsverletzung** beschriebenen Anweisungen aus.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie den [Quellcomputer](investigate-a-computer.md).
1. Führt der Computer ein Scantool aus, das mehrere LDAP-Abfragen ausführt?
    - Überprüfen Sie, ob die im Angriff abgefragten Benutzer und Gruppen über hohe Berechtigungen verfügen oder anderweitig wichtig sind (d. h. CEO, CFO, IT-Abteilung usw.). Falls dies der Fall ist, überprüfen Sie auch andere Aktivitäten auf diesem Endpunkt, und überwachen Sie Computer, auf denen die abgefragten Konten angemeldet sind, da diese für Lateral Movement-Methoden verwendet werden können.
1. Überprüfen Sie die Abfragen und deren Attribute, und ermitteln Sie, ob diese erfolgreich waren. Untersuchen Sie jede gefährdete Gruppe, und suchen Sie nach verdächtigen Aktivitäten im Zusammenhang mit der Gruppe oder Gruppenmitgliedern.
1. Erkennen Sie ein SAM-R-, DNS- oder SMB-Reconnaissanceverhalten auf dem Quellcomputer?

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

1. Kontrollieren Sie den Quellcomputer.
    1. Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
    1. Wenn auf dem Computer ein Überprüfungstool ausgeführt wird, das eine Vielzahl von LDAP-Abfragen ausführt, suchen Sie nach den Benutzern, die zum Zeitpunkt der Aktivität angemeldet waren, da diese Benutzer möglicherweise ebenfalls betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Setzen Sie das Kennwort zurück, wenn der Zugriff auf eine SPN-Ressource erfolgte, die unter einem Benutzerkonto (kein Computerkonto) ausgeführt wird.

## <a name="network-mapping-reconnaissance-dns-external-id-2007"></a>Reconnaissance über Netzwerkzuordnungen (DNS) (externe ID 2007)

*Vorheriger Name* : Reconnaissance über DNS

**Beschreibung**

Ihr DNS-Server enthält eine Struktur aller Computer, IP-Adressen und Dienste in Ihrem Netzwerk. Diese Informationen werden von Angreifern verwendet, um Ihre Netzwerkstruktur auszukundschaften und um interessante Zielcomputer zu bestimmten, die sie in den nächsten Schritten des Angriffs benötigen.

Es gibt mehrere Abfragetypen im DNS-Protokoll. Diese [!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnung erkennt verdächtige Anforderungen, entweder AXFR-Anforderungen (Übertragung) von Nicht-DNS-Servern oder solche, die eine übermäßige Anzahl von Anforderungen verwenden.

**Lernphase**

Für diese Warnung gilt eine Lernphase von 8 Tagen ab dem Start der Domänencontrollerüberwachung.

**TP, B-TP oder FP?**

1. Überprüfen Sie, ob der Quellcomputer ein DNS-Server ist.

    - Wenn der Quellcomputer **tatsächlich** ein DNS-Server ist, schließen Sie die Sicherheitswarnung als **FP** -Aktivität.
    - Achten Sie darauf, dass der UDP-Port 53 für die Verbindung zwischen dem [!INCLUDE [Product short](includes/product-short.md)]-Sensor und dem Quellcomputer **offen** ist, um zukünftige **FP** -Aktivitäten zu verhindern.

Sicherheitsscanner und zulässige Anwendungen können DNS-Abfragen erstellen.

1. Überprüfen Sie, ob diese Aktivitäten tatsächlich vom Quellcomputer ausgeführt werden sollen.

    - Wenn ja, **schließen** Sie die Sicherheitswarnung als **B-TP** -Aktivität, und schließen Sie den Computer aus.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie den [Quellcomputer](investigate-a-computer.md).

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

**Abhilfemaßnahmen:**

- Kontrollieren Sie den Quellcomputer.
  - Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
  - Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch kompromittiert sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.

**Vorbeugung:**

Zukünftige Angriffe über AXFR-Abfragen vermeiden Sie, indem Sie Ihren internen DNS-Server sichern.

- Dadurch verhindern Sie Reconnaissance über DNS. Deaktivieren Sie hierzu Zonenübertragungen, oder [schränken Sie diese auf bestimmte IP-Adressen ein](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee649273(v=ws.10)). Das Bearbeiten von Zonenübertragungen ist eine Aufgabe innerhalb einer Prüfliste, die für das [Sichern des DNS-Servers gegen interne und externe Angriffe](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee649273(v=ws.10)) gelten sollte.

## <a name="security-principal-reconnaissance-ldap-external-id-2038"></a>Sicherheitsprinzipalreconnaissance (LDAP) (externe ID 2038)

**Beschreibung**

Mit Sicherheitsprinzipalreconnaissance erlangen Angreifer wichtige Informationen über die Domänenumgebung. Informationen, die sowohl Angreifern helfen, die Domänenstruktur zu erfassen, als auch privilegierte Konten für die Verwendung in späteren Schritten in ihrer Angriffsabwehrkette zu identifizieren. Lightweight Directory Access Protocol (LDAP) ist eine der sowohl für zulässige als auch böswillige Zwecke am häufigsten verwendeten Methoden zum Abfragen von Active Directory. LDAP-fokussierte Sicherheitsprinzipalreconnaissance wird häufig als erste Phase eines Kerberoasting-Angriffs verwendet. Mit Kerberoasting-Angriffen wird eine Zielliste von Sicherheitsprinzipalnamen (Security Principal Names, SPNs) abgerufen, für die Angreifer dann versuchen, Ticket Granting Server-Tickets (TGS) zu erhalten.

Damit [!INCLUDE [Product short](includes/product-short.md)] berechtigte Benutzer kennenlernen und präzise Profile für diese kann, werden in den ersten 10 Tagen nach der Bereitstellung von [!INCLUDE [Product short](includes/product-short.md)] keine Warnungen dieses Typs ausgelöst. Sobald die anfängliche Lernphase von [!INCLUDE [Product short](includes/product-short.md)] abgeschlossen ist, werden Warnungen auf Computern generiert, die mithilfe von zuvor nicht beobachteten Methoden verdächtige LDAP-Enumerationsabfragen durchführen, bzw. Abfragen, die auf sensible Gruppen zielen.

**Lernphase**

15 Tage pro Computer, ab dem Tag, an dem das erste Ereignis auf dem Computer beobachtet wurde.

**TP, B-TP oder FP?**

1. Klicken Sie auf den Quellcomputer, und rufen Sie seine Profilseite auf.
    1. Wird von diesem Quellcomputer erwartet, dass er diese Aktivität generiert?
    1. Wenn diese Aktivität von diesem Computer erwartet wird, **schließen** Sie die Sicherheitswarnung, und schließen Sie diesen Computer als **B-TP** -Aktivität aus.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Überprüfen Sie die Abfragen, die ausgeführt wurden (z.B. als Domänenadministratoren oder alle Benutzer in einer Domäne), und bestimmen Sie, ob die Abfragen erfolgreich ausgeführt wurden. Untersuchen Sie bei jeder gefährdeten Gruppe, ob die Gruppe oder der Gruppe angehörende Benutzer betreffende verdächtige Aktivitäten aufgetreten sind.
1. Untersuchen Sie den [Quellcomputer](investigate-a-computer.md).
    - Überprüfen Sie mit den LDAP-Abfragen, ob bei einem der gefährdeten SPNs Ressourcenzugriffsaktivität aufgetreten ist.

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

1. Kontrollieren Sie den Quellcomputer.
    1. Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
    1. Führt der Computer ein Scantool aus, das eine Vielzahl von LDAP-Abfragen ausführt?
    1. Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Setzen Sie das Kennwort zurück, wenn der Zugriff auf eine SPN-Ressource erfolgte, die unter einem Benutzerkonto (kein Computerkonto) ausgeführt wird.

**Kerberoasting-spezifische vorgeschlagene Schritte zur Vorbeugung und Wiederherstellung**

1. Setzen Sie die Kennwörter der kompromittierten Benutzer zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Die Verwendung von [langen und komplexen Kennwörtern für Benutzer Dienstprinzipalkonten](/windows/security/threat-protection/security-policy-settings/minimum-password-length) ist erforderlich.
1. [Ersetzen Sie das Benutzerkonto durch ein gruppenverwaltetes Dienstkonto (GMSA)](/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview).

> [!NOTE]
> Warnungen zu Reconnaissance über Sicherheitsprinzipal (LDAP) werden nur von [!INCLUDE [Product short](includes/product-short.md)]-Sensoren unterstützt.

## <a name="user-and-group-membership-reconnaissance-samr-external-id-2021"></a>Reconnaissance über Benutzer und Gruppenmitgliedschaften (SAMR) (externe ID 2021)

*Vorheriger Name* : Reconnaissance mithilfe von Verzeichnisdienstabfragen

**Beschreibung**

Die Reconnaissance über Benutzer und Gruppenmitgliedschaften wird von Angreifern verwendet, um die Verzeichnisstruktur und Zielkonten mit weitreichenden Rechten für die weiteren Schritte eines Angriffs auszukundschaften. Das Protokoll Security Account Manager Remote (SAM-R) ist eine Methode, die zum Abfragen des Verzeichnisses verwendet wird, um diese Art der Zuordnung vorzunehmen.
In dieser Erkennung werden im ersten Monat nach der Bereitstellung von [!INCLUDE [Product short](includes/product-short.md)] keine Warnungen ausgelöst (Lernphase). Während der Lernphase erfasst [!INCLUDE [Product short](includes/product-short.md)], welche SAM-R-Abfragen (Enumerationsabfragen und einzelne Abfragen von sensiblen Konten) von welchen Computern gestellt werden.

**Lernphase**

Vier Wochen pro Domänencontroller, beginnend mit der ersten Netzwerkaktivität von SAMR für den festgelegten DC.

**TP, B-TP oder FP?**

1. Klicken Sie auf den Quellcomputer, um die entsprechende Profilseite aufzurufen.
    - Sollen diese Aktivitäten tatsächlich vom Quellcomputer ausgeführt werden?
      - Wenn ja, *schließen* Sie die Sicherheitswarnung als **B-TP** -Aktivität, und schließen Sie diesen Computer aus.
    - Überprüfen Sie die Benutzer, die den Vorgang ausgeführt haben.
      - Melden sich diese normalerweise bei diesem Quellcomputer an, oder sind sie Administratoren, die diese Aktionen durchführen sollten?
    - Überprüfen Sie das Benutzerprofil und die damit verbundenen Benutzeraktivitäten. Analysieren Sie ihr normales Verhalten, und suchen Sie nach zusätzlichen verdächtigen Aktivitäten mithilfe des [Leitfadens zur Untersuchung von Benutzern](investigate-a-user.md).

      Wenn Sie die vorherige Frage mit **Ja** beantwortet haben, *schließen* Sie die Sicherheitswarnung als **B-TP** -Aktivität.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Überprüfen Sie, welche Abfragen gestellt wurden (z. B. von Unternehmensadministratoren oder Administratoren), und ermitteln Sie, ob diese erfolgreich waren.
1. Untersuchen Sie jeden verfügbar gemachten Benutzer anhand des Leitfadens zur Untersuchung von Benutzern.
1. Untersuchen Sie den Quellcomputer.

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

1. Kontrollieren Sie den Quellcomputer.
1. Suchen Sie das Tool, mit dem der Angriff ausgeführt wurde, und entfernen Sie es.
1. Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Setzen Sie das Kennwort des Quellbenutzers zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Wenden Sie die Netzwerkzugriffssteuerung an, und schränken Sie die Zahl der Clients ein, die Remoteaufrufe der SAM-Gruppenrichtlinie durchführen dürfen.

## <a name="user-and-ip-address-reconnaissance-smb-external-id-2012"></a>Reconnaissance über Benutzer und IP-Adressen (SMB) (externe ID 2012)

*Vorheriger Name* : Reconnaissance mithilfe der SMB-Sitzungsenumeration

### <a name="description"></a>Beschreibung

Eine Enumeration mithilfe des SMB-Protokolls (Server Message Block) ermöglicht es Angreifern, Informationen darüber zu erhalten, wo Benutzer sich zuletzt angemeldet haben. Sobald Angreifer diese Informationen besitzen, können sie sich seitlich im Netzwerk bewegen, um zu einem bestimmten sensiblen Konto zu gelangen.

In dieser Erkennung wird eine Warnung ausgelöst, wenn eine SMB-Sitzungsenumeration auf einem Domänencontroller ausgeführt wird.

**TP, B-TP oder FP?**

Sicherheitsscanner und Anwendungen können möglicherweise zulässige Abfragen an Domänencontroller senden, um offene SMB-Sitzungen zu ermitteln.

1. Sollen diese Aktivitäten tatsächlich vom Quellcomputer ausgeführt werden?
1. Wird auf dem Quellcomputer eine Art Sicherheitsscanner ausgeführt?
    Wenn die Antwort „Ja“ lautet, handelt es sich wahrscheinlich um eine B-TP-Aktivität. *Schließen* Sie die Sicherheitswarnung, und schließen Sie diesen Computer aus.
1. Überprüfen Sie die Benutzer, die den Vorgang ausgeführt haben.
    Sollen diese Aktionen tatsächlich von diesen Benutzern ausgeführt werden?
    Wenn die Antwort „Ja“ lautet, *schließen* Sie die Sicherheitswarnung als B-TP-Aktivität.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie den Quellcomputer.
1. Überprüfen Sie auf der Warnungsseite, ob kompromittierte Benutzer angezeigt werden. Überprüfen Sie anschließend ihre jeweiligen Profile, um weitere Untersuchungen durchzuführen. Es wird empfohlen, zuerst sensible Benutzerkonten sowie Konten mit hoher Priorität zu untersuchen.

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

Verwenden Sie das [Net Cease-Tool](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b), um den Schutz Ihrer Umgebung gegen diese Attacken zu erhöhen.

> [!NOTE]
> Wenn Sie eine [!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnung deaktivieren möchten, wenden Sie sich an den Support.

> [!div class="nextstepaction"]
> [Tutorial: Warnungen zu kompromittierten Anmeldeinformationen](compromised-credentials-alerts.md)

## <a name="see-also"></a>Weitere Informationen

- [Untersuchen eines Computers](investigate-a-computer.md)
- [Untersuchen eines Benutzers](investigate-a-user.md)
- [Arbeiten mit Sicherheitswarnungen](working-with-suspicious-activities.md)
- [Warnungen zu kompromittierten Anmeldeinformationen](compromised-credentials-alerts.md)
- [Lateral Movement-Warnungen](lateral-movement-alerts.md)
- [Warnungen zu Domänendominanz](domain-dominance-alerts.md)
- [Warnungen zu Exfiltration](exfiltration-alerts.md)
- [Referenz zum SIEM-Protokoll für [!INCLUDE [Product short](includes/product-short.md)]](cef-format-sa.md)
- [Arbeiten mit Lateral Movement-Pfaden](use-case-lateral-movement-path.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
