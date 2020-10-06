---
title: Azure ATP-Sicherheitswarnungen zur Phase „Kompromittierte Anmeldeinformationen“
description: In diesem Artikel werden die Azure ATP-Warnungen erläutert, die ausgegeben werden, wenn Angriffe in Ihrer Organisation erkannt werden, die typisch für die Phase der kompromittierten Anmeldeinformationen sind.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/01/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: e9cf68d2-36bd-4b0d-b36e-7cf7ded2618e
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 5ba78ddacfed1993a4c5f4b6c4407e4af45826f8
ms.sourcegitcommit: dd8435ba20f76a6fc4590980c040c6fc7ec6c62b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/29/2020
ms.locfileid: "91451784"
---
# <a name="tutorial-compromised-credential-alerts"></a>Tutorial: Warnungen zu kompromittierten Anmeldeinformationen

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Cyberangriffe werden in der Regel gegen eine beliebige zugängliche Entität gestartet, wie z.B. einen Benutzer mit geringfügigen Berechtigungen, und verschieben sich anschließend schnell seitwärts, bis der Angreifer Zugriff auf wertvolle Objekte erhält (z.B. sensible Konten, Domänenadministratoren und streng vertrauliche Daten). Azure ATP identifiziert diese komplexen Bedrohungen an der Quelle über die gesamte Kette der Angriffsabwehr hinweg und ordnet sie in die folgenden Phasen ein

1. [Reconnaissance](reconnaissance-alerts.md)
2. **Kompromittierte Anmeldeinformationen**
3. [Seitliche Verschiebung](lateral-movement-alerts.md)
4. [Warnungen zu Domänendominanz](domain-dominance-alerts.md)
5. [Exfiltration](exfiltration-alerts.md)

Weitere Informationen zur Struktur und zu gängigen Komponenten der Azure ATP-Sicherheitswarnungen finden Sie unter [Understanding security alerts (Grundlegendes zu Sicherheitswarnungen)](understanding-security-alerts.md). Weitere Informationen zu **True Positive (TP)** , **Benign True Positive (B-TP)** (unschädlich richtig positiv) und **False Positive (FP)** finden Sie unter [Klassifizierungen der Sicherheitswarnungen](understanding-security-alerts.md#security-alert-classifications).

Mit den folgenden Sicherheitswarnungen können Sie verdächtige Aktivitäten der Phase **Kompromittierte Anmeldeinformationen** identifizieren und beheben, die von Azure ATP in Ihrem Netzwerk erkannt wurden. In diesem Tutorial erfahren Sie, wie die folgenden Angriffstypen klassifiziert, behoben und unterbunden werden:

> [!div class="checklist"]
>
> * Honeytoken-Aktivität (externe ID 2014)
> * Vermuteter Brute-Force-Angriff (Kerberos, NTLM) (externe ID 2023)
> * Vermuteter Brute-Force-Angriff (LDAP) (externe ID 2004)
> * Vermuteter Brute-Force-Angriff (SMB) (externe ID 2033)
> * Verdächtigter Netlogon-Rechteerweiterungsversuch (externe ID 2411)
> * Vermuteter WannaCry-Ransomware-Angriff (externe ID 2035)
> * Vermutete Verwendung des Metasploit-Hackerframeworks (externe ID 2034)
> * Verdächtige VPN-Verbindung (externe ID 2025)

## <a name="honeytoken-activity-external-id-2014"></a>Honeytoken-Aktivität (externe ID 2014)

*Alter Name:* Honeytokenaktivität

**Beschreibung**

Honeytoken-Konten sind Köderkonten, die eingerichtet werden, um schädliche Aktivitäten, die versuchen, diese Konten zu verwenden, zu erkennen und zu verfolgen. Honeytoken-Konten sollten nicht verwendet werden, aber einen attraktiven Namen besitzen, um Angreifer anzulocken (z.B. SQL-Admin). Jede von diesen ausgehende Aktivität kann auf böswilliges Verhalten hinweisen.

Weitere Informationen zu Honeytokenkonten finden Sie unter [Konfigurieren von Ausschlüssen von Erkennungen und Honeytokenkonten](install-step7.md).

**TP, B-TP oder FP?**

1. Überprüfen Sie, ob der Besitzer des Quellcomputers das Honeytokenkonto für die Authentifizierung verwendet hat. Verwenden Sie dazu die auf der Seite zu verdächtigen Aktivitäten beschriebene Methode (z.B. Kerberos, LDAP, NTLM).

    Sollte der Besitzer des Quellcomputers das Honeytokenkonto für die Authentifizierung verwendet haben, verwenden Sie genau die in der Warnung beschriebene Methode, und *Schließen* Sie die Sicherheitswarnung als **B-TP**-Aktivität.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie den [Quellbenutzer](investigate-a-user.md).
1. Untersuchen Sie den [Quellcomputer](investigate-a-computer.md).

    > [!NOTE]
    > Wenn die Authentifizierung mithilfe von NTLM erfolgt ist, sind in einigen Szenarios möglicherweise nicht genügend Informationen zum Server verfügbar, auf die der Quellcomputer zugreifen wollte. Azure ATP erfasst die auf Windows-Ereignis 4776 basierenden Daten des Quellcomputers, die den computerdefinierten Namen des Quellcomputers enthalten.
    > Wenn Sie Windows-Ereignis 4776 verwenden, um diese Informationen zu erfassen, wird das Quellfeld für diese Informationen gelegentlich von dem Gerät oder der Software überschrieben, und zeigt nur „Arbeitsstation“ oder „MSTSC“ an. Wenn Sie häufig Geräte verwenden, die als „Arbeitsstation“ oder „MSTSC“ angezeigt werden, vergewissern Sie sich, dass die NTLM-Überwachung auf den entsprechenden Domänencontrollern aktiviert ist, um den richtigen Quellcomputernamen zu erhalten.
    > Aktivieren Sie dazu das Windows-Ereignis 8004 (NTLM-Authentifizierungsereignis, das Informationen zum Quellcomputer, Benutzerkonto und Server enthält, auf die der Quellcomputer zugreifen wollte).

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

1. Kontrollieren Sie den Quellcomputer.
    * Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
    * Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch kompromittiert sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.

## <a name="suspected-brute-force-attack-kerberos-ntlm-external-id-2023"></a>Vermuteter Brute-Force-Angriff (Kerberos, NTLM) (externe ID 2023)

*Alter Name:* Verdächtige Authentifizierungsfehler

**Beschreibung**

Bei einem Brute-Force-Angriff versucht der Angreifer, sich mit mehreren Kennwörtern bei verschiedenen Konten zu authentifizieren, bis ein korrektes Kennwort gefunden wird. Oder der Angreifer verwendet ein Kennwort im Rahmen eines umfangreichen Kennwort-Spray-Angriffs, das bei mindestens einem Konto funktioniert. Sobald eines gefunden wurde, meldet sich der Angreifer mit dem authentifizierten Konto an.

Bei diesem Erkennungsvorgang wird eine Warnung ausgelöst, wenn viele Authentifizierungsfehler bei der Verwendung von Kerberos oder NTLM auftreten oder die Ausführung eines Kennwort-Spray-Angriffs erkannt wurde. Bei Kerberos oder NTLM wird dieser Angriffstyp üblicherweise entweder *horizontal* mit wenigen Kennwörtern für viele Benutzer oder *vertikal* mit einer Vielzahl von Kennwörtern für wenige Benutzer ausgeführt. Auch eine beliebige Kombination dieser beiden Optionen ist möglich.

Bei einem Kennwort-Spray-Angriff testen Angreifer nach erfolgreichem Durchzählen einer Liste von gültigen Benutzern aus dem Domänencontroller EIN sorgfältig erstelltes Kennwort für ALLE bekannten Benutzerkonten (ein Kennwort für n Konten). Wenn beim ersten Kennwort-Spray-Angriff ein Fehler auftritt, wiederholen sie den Vorgang mit einem anderen sorgfältig erstellten Kennwort – normalerweise nach einer Wartezeit von 30 Minuten zwischen den Versuchen. Durch die Wartezeit verhindern Angreifer, dass meist zeitbasierte Schwellenwerte für die Kontosperre ausgelöst werden. Kennwort-Spray-Angriffe haben sich rasch zu einer beliebten Methode unter Angreifern und Pen-Testern entwickelt. Kennwort-Spray-Angriffe haben sich als effektiv erwiesen, um innerhalb einer Organisation einen Ankerpunkt zu finden und infolgedessen weitere Schwachstellen auszunutzen, um Berechtigungen auszuweiten. Der Mindestzeitraum, bevor eine Warnung ausgelöst werden kann, beträgt eine Woche.

**Lernphase**

1 Woche

**TP, B-TP oder FP?**

Überprüfen Sie auf jeden Fall, ob Anmeldeversuche mit einer erfolgreichen Authentifizierung beendet wurden.

1. Wurde ein Anmeldeversuch erfolgreich beendet, überprüfen Sie, ob eines der **erratenen Konten** normalerweise von diesem Quellcomputer verwendet wird.
    * Besteht die Möglichkeit, dass bei diesen Konten wegen der Verwendung eines falschen Kennworts ein Fehler aufgetreten ist?
    * Überprüfen Sie zusammen mit dem Benutzer/den Benutzern, ob die Aktivität von ihm/ihnen generiert wurde (durch erfolgreiches Anmelden nach einigen fehlerhaften Anmeldeversuchen).

      Lautet die Antwort **Ja**, **Schließen** Sie die Sicherheitswarnung als B-TP-Aktivität.

1. Wenn es keine **Erratenen Konten** gibt, überprüfen Sie, ob eines der **Angegriffenen Konten** normalerweise vom Quellcomputer verwendet wird.
    * Überprüfen Sie, ob auf dem Quellcomputer ein Skript mit falschen/veralteten Anmeldeinformationen ausgeführt wird.
    * Lautet die Antwort **Ja**, beenden und bearbeiten Sie das Skript, oder löschen Sie es. **Schließen** Sie die Sicherheitswarnung als B-TP-Aktivität.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie den Quellcomputer.
1. Überprüfen Sie auf der Seite für Warnungen, ob und gegebenenfalls welche Benutzer erfolgreich erraten wurden.
    * Überprüfen Sie für jeden erfolgreich erratenen Benutzer [dessen Profil](investigate-a-user.md), um weitere Informationen zu erhalten.

    > [!NOTE]
    > Überprüfen Sie die Beweise, um das verwendete Authentifizierungsprotokoll zu ermitteln. Wenn die NTLM-Authentifizierung verwendet wurde, aktivieren Sie die NTLM-Überwachung des Windows-Ereignisses 8004 auf dem Domänencontroller, um den Ressourcenserver zu ermitteln, auf den die Benutzer zugreifen wollten. Windows-Ereignis 8004 ist das NTLM-Authentifizierungsereignis, das Informationen zum Quellcomputer, Benutzerkonto und Server enthält, auf die das Quellbenutzerkonto zugreifen wollte.
    > Azure ATP erfasst die auf Windows-Ereignis 4776 basierenden Daten des Quellcomputers, die den computerdefinierten Namen des Quellcomputers enthalten. Wenn Sie Windows-Ereignis 4776 verwenden, um diese Informationen zu erfassen, wird das Quellfeld der Informationen gelegentlich von dem Gerät oder der Software überschrieben, und es wird nur „Arbeitsstation“ oder „MSTSC“ als Informationsquelle angezeigt. Darüber hinaus ist der Quellcomputer möglicherweise nicht tatsächlich in Ihrem Netzwerk vorhanden. Dies ist möglich, da Angreifer in der Regel offene, über das Internet zugängliche Server außerhalb des Netzwerks zum Ziel haben und dies dann zum Auflisten Ihrer Benutzer verwenden. Wenn Sie häufig Geräte verwenden, die als „Arbeitsstation“ oder „MSTSC“ angezeigt werden, vergewissern Sie sich, dass die NTLM-Überwachung auf den Domänencontrollern aktiviert ist, um den Namen des Ressourcenservers zu erhalten, auf den zugegriffen wurde. Sie sollten diesen Server ebenfalls untersuchen und überprüfen, ob er zum Internet geöffnet ist, und ihn ggf. schließen.

1. Wenn Sie wissen, welcher Server die Authentifizierungsüberprüfung gesendet hat, untersuchen Sie den Server, indem Sie Ereignisse wie das Windows-Ereignis 4624 überprüfen, um den Authentifizierungsprozess besser nachvollziehen zu können.
1. Überprüfen Sie, ob dieser Server mithilfe von offenen Ports eine Verbindung mit dem Internet herstellt.
    Verwendet der Server beispielsweise RDP für die Verbindung mit dem Internet?

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

1. Setzen Sie die Kennwörter der erratenen Benutzer zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Kontrollieren Sie den Quellcomputer.
    * Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
    * Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch kompromittiert sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Setzen Sie die Kennwörter des Quellbenutzers zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Erzwingen Sie in der Organisation [komplexe und lange Kennwörter](/windows/device-security/security-policy-settings/password-policy), und stellen Sie damit die notwendige erste Sicherheitsstufe zum Schutz vor zukünftigen Brute-Force-Angriffen zur Verfügung.

## <a name="suspected-brute-force-attack-ldap-external-id-2004"></a>Vermuteter Brute-Force-Angriff (LDAP) (externe ID 2004)

*Alter Name:* Brute-Force-Angriff mithilfe einer einfachen LDAP-Bindung

**Beschreibung**

Bei einem Brute-Force-Angriff versucht der Angreifer, sich mit vielen verschiedenen Kennwörtern für verschiedene Konten anzumelden, bis ein korrektes Kennwort für mindestens ein Konto gefunden wird. Sobald eines gefunden wurde, kann sich der Angreifer mit diesem Konto anmelden.

In dieser Erkennung wird eine Warnung ausgelöst, wenn Azure ATP eine signifikante Anzahl von Authentifizierungen mit einfacher Bindung erkennt. Diese Warnung erkennt Brute-Force-Angriffe, die entweder *horizontal* mit wenigen Kennwörtern für viele Benutzer oder *vertikal* mit einer Vielzahl von Kennwörtern für wenige Benutzer ausgeführt werden. Auch eine beliebige Kombination dieser beiden Optionen ist möglich.

**TP, B-TP oder FP?**

Überprüfen Sie auf jeden Fall, ob Anmeldeversuche mit einer erfolgreichen Authentifizierung beendet wurden.

1. Wurde ein Anmeldeversuch erfolgreich beendet, überprüfen Sie, ob eines der **Erratenen Konten** normalerweise von diesem Quellcomputer verwendet wird.
    * Besteht die Möglichkeit, dass bei diesen Konten wegen der Verwendung eines falschen Kennworts ein Fehler aufgetreten ist?
    * Überprüfen Sie zusammen mit dem Benutzer/den Benutzern, ob die Aktivität von ihm/ihnen generiert wurde (durch erfolgreiches Anmelden nach einigen fehlerhaften Anmeldeversuchen).

     Lautet die Antwort **Ja**, **Schließen** Sie die Sicherheitswarnung als B-TP-Aktivität.

1. Wenn es keine **Erratenen Konten** gibt, überprüfen Sie, ob eines der **Angegriffenen Konten** normalerweise vom Quellcomputer verwendet wird.
    * Überprüfen Sie, ob auf dem Quellcomputer ein Skript mit falschen/veralteten Anmeldeinformationen ausgeführt wird.

      Lautet die Antwort **Ja**, beenden und bearbeiten Sie das Skript, oder löschen Sie es. **Schließen** Sie die Sicherheitswarnung als B-TP-Aktivität.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie den [Quellcomputer](investigate-a-computer.md).
1. Überprüfen Sie auf der Seite für Warnungen, ob und gegebenenfalls welche Benutzer erfolgreich erraten wurden. Überprüfen Sie für jeden erfolgreich erratenen Benutzer [dessen Profil](investigate-a-user.md), um weitere Informationen zu erhalten.

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

1. Setzen Sie die Kennwörter der erratenen Benutzer zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Kontrollieren Sie den Quellcomputer.
    * Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
    * Suchen Sie nach Benutzern, die ungefähr zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch kompromittiert sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Setzen Sie die Kennwörter des Quellbenutzers zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Erzwingen Sie in der Organisation [komplexe und lange Kennwörter](/windows/device-security/security-policy-settings/password-policy), und stellen Sie damit die notwendige erste Sicherheitsstufe zum Schutz vor zukünftigen Brute-Force-Angriffen zur Verfügung.
1. Unterbinden Sie in Ihrer Organisation künftig die Verwendung von LDAP-Klartextprotokoll.

## <a name="suspected-brute-force-attack-smb-external-id-2033"></a>Vermuteter Brute-Force-Angriff (SMB) (externe ID 2033)

*Vorheriger Name*: Ungewöhnliche Protokollimplementierung (potenzielle Verwendung schädlicher Tools wie Hydra)

**Beschreibung**

Angreifer verwenden Tools, die verschiedene Protokolle wie SMB, Kerberos und NTLM auf nicht standardmäßige Arten implementieren. Während diese Art des Netzwerkdatenverkehrs von Windows ohne Warnungen akzeptiert wird, kann Azure ATP potenziell böswillige Absichten erkennen. Das Verhalten weist auf Brute-Force-Techniken hin.

**TP, B-TP oder FP?**

1. Überprüfen Sie, ob auf dem Quellcomputer ein Angriffstool wie Hydra ausgeführt wird.
    1. Wird auf dem Quellcomputer ein Angriffstool ausgeführt, stellt diese Warnung eine **TP**-Aktivität dar. Befolgen Sie die Anweisungen im Abschnitt **Ermitteln des Umfangs der Sicherheitsverletzung** oben.

Anwendungen implementieren gelegentlich einen eigenen NTLM- oder SMB-Stapel.

1. Überprüfen Sie, ob auf dem Quellcomputer dessen eigener NTLM- oder SMB-Anwendungstyp im Stapel ausgeführt wird.
    1. Führt der Quellcomputer diesen Anwendungstyp aus, obwohl er das nicht sollte, korrigieren Sie entsprechend die Anwendungskonfiguration. **Schließen** Sie die Sicherheitswarnung als **B-TP**-Aktivität (unbedenklich richtig positiv).
    2. **Schließen** Sie die Sicherheitswarnung als **B-TP**-Aktivität, und schließen Sie diesen Computer aus, wenn der Quellcomputer diesen Anwendungstyp ausführt und dies auch weiterhin tun soll.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie den [Quellcomputer](investigate-a-computer.md).
1. Untersuchen Sie den [Quellbenutzer](investigate-a-user.md) (sofern vorhanden).

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

1. Setzen Sie die Kennwörter der erratenen Benutzer zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Kontrollieren Sie den Quellcomputer.
    1. Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
    2. Suchen Sie nach Benutzern, die zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind.
    3. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Erzwingen Sie [komplexe und lange Kennwörter](/windows/security/threat-protection/security-policy-settings/password-policy) in der Organisation. Komplexe und lange Kennwörter stellen die notwendige erste Sicherheitsstufe zum Schutz vor zukünftigen Brute-Force-Angriffen dar.
1. [Deaktivieren von SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)

<a name="suspected-netlogon-priv-elev-2411"></a>
## <a name="suspected-netlogon-privilege-elevation-attempt-cve-2020-1472-exploitationexternalid2411"></a>Verdächtigter Netlogon-Rechteerweiterungsversuch (CVE-2020-1472-Ausnutzung) (externe ID 2411)

Microsoft hat [CVE-2020-1472](https://portal.msrc.microsoft.com/security-guidance/advisory/CVE-2020-1472) veröffentlicht mit der Ankündigung, dass ein neues Sicherheitsrisiko vorliegt, das die Rechteerweiterung für den Domänencontroller ermöglicht.

Ein Rechteerweiterungs-Sicherheitsrisiko liegt vor, wenn ein Angreifer eine gefährdete Netlogon-Verbindung über einen sicheren Kanal mit einem Domänencontroller herstellt und dabei das Netlogon Remote Protocol ([MS-NRPC](/openspecs/windows_protocols/ms-nrpc/ff8f970f-3e37-40f7-bd4b-af7336e4792f)) verwendet. Dies ist auch als *Netlogon-Rechteerweiterungs-Sicherheitsrisiko* bekannt.

**Lernphase**

Keine

**TP, B-TP oder FP**

Wenn der Quellcomputer ein Domänencontroller (DC) ist, wird Azure ATP möglicherweise aufgrund fehlender Entscheidungssicherheit an dessen Identifikation gehindert.

1. Wenn der Quellcomputer ein Domänencontroller ist, **Schließen** Sie die Warnung als **B-TP** -Aktivität.

1. Wenn dieser Quellcomputer diesen Aktivitätstyp erzeugen und zukünftig weiterhin erzeugen soll, **Schließen** Sie die Sicherheitswarnung als **B-TP** -Aktivität, und schließen Sie den Computer aus, um zusätzliche gutartige Warnungen zu vermeiden.

Betrachten Sie diese Warnung andernfalls als  **TP** , und führen Sie die unter  **Ermitteln des Umfangs der Sicherheitsverletzung** beschriebenen Anweisungen aus.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie den [Quellcomputer](investigate-a-computer.md), und überprüfen Sie, ob bösartige Skripts oder Tools die Verbindung mit dem Domänencontroller hergestellt haben.

1. Untersuchen Sie den Ziel-DC nach verdächtigen Aktivitäten, die nach der Verwendung des Sicherheitsrisikos aufgetreten sind.

**Abhilfemaßnahmen:**

1. Patchen Sie alle Computer, und stellen Sie sicher, dass Sicherheitsupdates angewendet werden.
1. In [unserem Leitfaden](https://support.microsoft.com/help/4557222/how-to-manage-the-changes-in-netlogon-secure-channel-connections-assoc) erfahren Sie, wie Sie Änderungen an einer Netlogon-Verbindung über einen sicheren Kanal verwalten, die sich auf dieses Sicherheitsrisiko beziehen und es verhindern können.
1. Kontrollieren Sie den Quellcomputer.
    * Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.

## <a name="suspected-wannacry-ransomware-attack-external-id-2035"></a>Vermuteter WannaCry-Ransomware-Angriff (externe ID 2035)

*Vorheriger Name*: Ungewöhnliche Protokollimplementierung (potenzieller WannaCry-Ransomwareangriff)

**Beschreibung**

Angreifer verwenden Tools, die verschiedene Protokolle auf nicht standardmäßige Arten implementieren. Während diese Art des Netzwerkdatenverkehrs von Windows ohne Warnungen akzeptiert wird, kann Azure ATP potenziell böswillige Absichten erkennen. Das Verhalten weist auf Techniken hin, die von erweiterter Ransomware, z.B. WannaCry, verwendet werden.

**TP, B-TP oder FP?**

1. Überprüfen Sie, ob WannaCry auf dem Quellcomputer ausgeführt wird.

    * Wird WannaCry ausgeführt, stellt diese Warnung eine **TP**-Aktivität dar. Befolgen Sie die Anweisungen im Abschnitt **Ermitteln des Umfangs der Sicherheitsverletzung** oben.

Anwendungen implementieren gelegentlich einen eigenen NTLM- oder SMB-Stapel.

1. Überprüfen Sie, ob auf dem Quellcomputer dessen eigener NTLM- oder SMB-Anwendungstyp im Stapel ausgeführt wird.
    1. Führt der Quellcomputer diesen Anwendungstyp aus, obwohl er das nicht sollte, korrigieren Sie entsprechend die Anwendungskonfiguration. **Schließen** Sie die Sicherheitswarnung als **B-TP**-Aktivität (unbedenklich richtig positiv).
    2. Führt der Quellcomputer diesen Anwendungstyp aus und soll das auch weiterhin tun, **Schließen** Sie die Sicherheitswarnung als **B-TP**-Aktivität, und schließen Sie diesen Computer aus.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie den [Quellcomputer](investigate-a-computer.md).
1. Untersuchen Sie den [kompromittierten Benutzer](investigate-a-user.md).

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

1. Kontrollieren Sie den Quellcomputer.
    * [Entfernen von WannaCry](https://support.microsoft.com/help/890830/remove-specific-prevalent-malware-with-windows-malicious-software-remo)
    * WanaKiwi kann für einige Ransomwares die Daten in deren Besitz entschlüsseln. Dies ist aber nur möglich, wenn der Benutzer den Computer nicht neu gestartet oder ausgeschaltet hat. Weitere Informationen finden Sie unter [WannaCry-Ransomware](https://answers.microsoft.com/windows/forum/windows_10-security/wanna-cry-ransomware/5afdb045-8f36-4f55-a992-53398d21ed07?auth=1).
    * Suchen Sie nach Benutzern, die zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Patchen Sie alle Computer, und stellen Sie sicher, dass Sicherheitsupdates angewendet werden.
    * [Deaktivieren von SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)

## <a name="suspected-use-of-metasploit-hacking-framework-external-id-2034"></a>Vermutete Verwendung des Metasploit-Hackerframeworks (externe ID 2034)

*Vorheriger Name*: Ungewöhnliche Protokollimplementierung (potenzielle Verwendung schädlicher Hackertools wie Metasploit)

**Beschreibung**

Angreifer verwenden Tools, die verschiedene Protokolle (SMB, Kerberos, NTLM) auf nicht standardmäßige Arten implementieren. Während diese Art des Netzwerkdatenverkehrs von Windows ohne Warnungen akzeptiert wird, kann Azure ATP potenziell böswillige Absichten erkennen. Das Verhalten weist auf Techniken wie z.B. die Verwendung des Metasploit-Hackerframeworks hin.

**TP, B-TP oder FP?**

1. Überprüfen Sie, ob auf dem Quellcomputer ein Angriffstool wie Metasploit oder Medusa ausgeführt wird.

1. Wenn dies der Fall ist, handelt es sich um ein richtig positives Ereignis. Befolgen Sie die Anweisungen im Abschnitt **Ermitteln des Umfangs der Sicherheitsverletzung** oben.

Anwendungen implementieren gelegentlich einen eigenen NTLM- oder SMB-Stapel.

 1. Überprüfen Sie, ob auf dem Quellcomputer dessen eigener NTLM- oder SMB-Anwendungstyp im Stapel ausgeführt wird.
    1. Führt der Quellcomputer diesen Anwendungstyp aus, obwohl er das nicht sollte, korrigieren Sie entsprechend die Anwendungskonfiguration. **Schließen** Sie die Sicherheitswarnung als **B-TP**-Aktivität (unbedenklich richtig positiv).
    2. Führt der Quellcomputer diesen Anwendungstyp aus und soll das auch weiterhin tun, **Schließen** Sie die Sicherheitswarnung als **B-TP**-Aktivität, und schließen Sie diesen Computer aus.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie den [Quellcomputer](investigate-a-computer.md).
1. Wenn ein Quellbenutzer vorhanden ist, [untersuchen Sie diesen Benutzer](investigate-a-user.md).

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

1. Setzen Sie die Kennwörter der erratenen Benutzer zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Kontrollieren Sie den Quellcomputer.
    1. Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
    2. Suchen Sie nach Benutzern, die zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Setzen Sie die Kennwörter des Quellbenutzers zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
4. [Deaktivieren von SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)

## <a name="suspicious-vpn-connection-external-id-2025"></a>Verdächtige VPN-Verbindung (externe ID 2025)

*Alter Name:* Verdächtige VPN-Verbindung

**Beschreibung**

Azure ATP speichert Informationen zum Entitätsverhalten für VPN-Verbindungen von Benutzern für einen gleitenden Zeitraum von einem Monat.

Das Modell für das VPN-Verhalten basiert auf den Computern, auf denen sich Benutzer anmelden und den Standorten, von denen Benutzer eine Verbindung herstellen.

Es wird eine Warnung ausgelöst, wenn basierend auf einem Machine-Learning-Algorithmus eine Abweichung des Benutzerverhaltens vorliegt.

**Lernphase**

30 Tage ab der ersten VPN-Verbindung und mindestens fünf VPN-Verbindungen während der letzten 30 Tage pro Benutzer.

**TP, B-TP oder FP?**

1. Soll der verdächtige Benutzer diese Vorgänge ausführen?
    1. Hat der Benutzer vor Kurzem seinen Standort geändert?
    2. Gab es einen Ortswechsel, und stellte der Benutzer eine Verbindung von einem neuen Gerät aus her?

Lautet die Antwort auf diese Fragen „Ja“, **Schließen** Sie die Sicherheitswarnung als **B-TP**-Aktivität.

**Ermitteln des Umfangs der Sicherheitsverletzung**

1. Untersuchen Sie den [Quellcomputer](investigate-a-computer.md).
1. Wenn ein Quellbenutzer vorhanden ist, [untersuchen Sie diesen Benutzer](investigate-a-user.md).

**Empfohlene Abhilfemaßnahmen und Schritte zur Vorbeugung**

1. Setzen Sie das Kennwort des Benutzers zurück, und aktivieren Sie MFA. Wenn Sie in Azure Active Directory Identity Protection die relevanten Richtlinien für Benutzer mit hohem Risiko konfiguriert haben, können Sie auch im Cloud App Security-Portal die Aktion [**Benutzergefährdung bestätigen**](/cloud-app-security/accounts#governance-actions) verwenden.
1. Blockieren Sie für diesen Benutzer ggf. die Möglichkeit, über VPN eine Verbindung herzustellen.
1. Blockieren Sie für diesen Computer ggf. die Möglichkeit, über VPN eine Verbindung herzustellen.
1. Überprüfen Sie, ob von diesen Standorten weitere Benutzer eine Verbindung über VPN hergestellt haben und ob sie kompromittiert sind.

> [!div class="nextstepaction"]
> [Lateral Movement Alert tutorial (Tutorial zu Lateral Movement-Warnungen)](lateral-movement-alerts.md)

## <a name="see-also"></a>Weitere Informationen

- [Untersuchen eines Computers](investigate-a-computer.md)
- [Untersuchen eines Benutzers](investigate-a-user.md)
- [Arbeiten mit Sicherheitswarnungen](working-with-suspicious-activities.md)
- [Arbeiten mit Lateral Movement-Pfaden](use-case-lateral-movement-path.md)
- [Warnungen zu Reconnaissance](reconnaissance-alerts.md)
- [Lateral Movement-Warnungen](lateral-movement-alerts.md)
- [Warnungen zu Domänendominanz](domain-dominance-alerts.md)
- [Warnungen zu Exfiltration](exfiltration-alerts.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)