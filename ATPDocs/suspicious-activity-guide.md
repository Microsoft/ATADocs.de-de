---
title: Azure ATP-Leitfaden zu Sicherheitswarnungen | Microsoft-Dokumentation
d|Description: This article provides a list of the security alerts issued by Azure ATP and steps for remediation.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 12/09/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ca5d1c7b-11a9-4df3-84a5-f53feaf6e561
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 8604e3cfead3b52fd9f0d1ed38bb7d806cf50f46
ms.sourcegitcommit: d1c9c3e69b196f6086a8f100e527553cf0d95aac
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/10/2018
ms.locfileid: "53125131"
---
*Gilt für: Azure Advanced Threat Protection*


# <a name="azure-advanced-threat-protection-security-alert-guide"></a>Azure Advanced Threat Protection – Leitfaden zu Sicherheitswarnungen

Nach einer gründlichen Untersuchung können alle Azure ATP-Sicherheitswarnungen wie folgt klassifiziert werden:

-   **Richtig positiv**: Eine von Azure ATP erkannte schädliche Aktion.

-   **Unbedenklich richtig positiv**: Eine von Azure ATP erkannte Aktion, die tatsächlich durchgeführt wurde, aber nicht schädlich ist, wie z.B. ein Penetrationstest.

-   **Falsch positiv**: Ein falscher Alarm, das heißt, die Aktivität wurde nicht ausgeführt.

Weitere Informationen zum Arbeiten mit Azure ATP-Sicherheitswarnungen finden Sie unter [Arbeiten mit Sicherheitswarnungen](working-with-suspicious-activities.md).

## <a name="security-alert-name-mapping-and-unique-externalid"></a>Zuordnen von Sicherheitswarnungsnamen und eindeutige externalId

In Version 2.56 wurden alle Sicherheitswarnungen für Azure ATP umbenannt. Die neuen Namen sind jetzt verständlicher. In der folgenden Tabelle sind die neuen und alten Namen sowie die eindeutigen externalIds nebeneinander aufgelistet. Microsoft empfiehlt die Verwendung von externalIds zur Warnung anstelle von Warnungsnamen für Skripts oder die Automatisierung, da nur externalIds dauerhaft für Sicherheitswarnungen verwendet und nicht geändert werden. 

> [!div class="mx-tableFixed"] 

|Neuer Sicherheitswarnungsname|Alter Sicherheitswarnungsname|Eindeutige externalId|
|---------|----------|---------|
|Reconnaissance mithilfe von Kontoenumeration|Reconnaissance mithilfe von Kontoenumeration|2003|
|Honeytoken-Aktivität|Honeytoken-Aktivität|2014|
|Malicious request of Data Protection API master key (Böswillige Anforderung eines Masterschlüssels zur Datenschutz-API)|Böswillige Anforderung privater Informationen im Rahmen der Datensicherheit|2020|
|Network-mapping reconnaissance (DNS) (Reconnaissance über Netzwerkzuordnung (DNS))|Reconnaissance über DNS|2007|
|Versuchte Remote-Codeausführung|Versuchte Remote-Codeausführung|2019|
|Suspected Brute Force attack (LDAP) (Verdacht auf einen Brute-Force-Angriff (LDAP))|Brute-Force-Angriff mithilfe einer einfachen LDAP-Bindung|2004|
|Suspected DCShadow attack (domain controller promotion) (Verdacht auf DCShadow-Angriff (Heraufstufung von Domänencontrollern))|Verdächtige Heraufstufung zu Domänencontrollern (potenzieller DcShadow-Angriff)|2028|
|Verdacht auf DCShadow-Angriff (Replikationsanforderung an Domänencontroller)|Verdächtige Replikationsanforderung von Domänencontroller (potenzieller DCShadow-Angriff)|2029|
|Suspected DCSync attack (replication of directory services) (Verdacht auf einen DCSync-Angriff (Replikation von Verzeichnisdiensten))|Böswillige Replikation von Verzeichnisdiensten|2006|
|Verdacht auf Verwendung eines Golden Ticket (Herabstufung der Verschlüsselung)|Aktivität zur Herabstufung der Verschlüsselung (potenzieller Golden Ticket-Angriff)|2009|
|Suspected Golden Ticket usage (forged authorization data) (Verdacht auf Verwendung eines Golden Ticket (gefälschte Autorisierungsdaten)) |Berechtigungsausweitung mithilfe von gefälschten Autorisierungsdaten|2013|
|Suspected golden ticket usage (nonexistent account) (Verdacht auf Verwendung eines Golden Ticket (nicht vorhandenes Konto))|Kerberos Golden Ticket: nicht vorhandenes Konto|2027|
|Verdacht auf Verwendung eines Golden Ticket (Ticketanomalie) |Kerberos Golden Ticket – Ticketanomalie|2022|
|Verdacht auf Verwendung eines Golden Ticket (Zeitanomalie) – Vorschauversion| –|2032|
|Suspected identity theft (pass-the-hash) (Verdacht auf Identitätsdiebstahl (Pass-the-Hash))|Identitätsdiebstahl mithilfe eines Pass-the-Hash-Angriffs|2017|
|Suspected identity theft (pass-the-ticket) (Verdacht auf Identitätsdiebstahl (Pass-the-Ticket))|Identitätsdiebstahl mithilfe eines Pass-the-Ticket-Angriffs|2018|
|Suspected over-pass-the-hash attack (encryption downgrade) (Verdacht auf Over-Pass-the-Hash-Angriff (Herabstufung der Verschlüsselung))|Aktivität zur Herabstufung der Verschlüsselung (potenzieller Overpass-the-Hash-Angriff)|2008|
|Suspected Skeleton Key attack (encryption downgrade) (Verdacht auf Skeleton-Key-Angriff (Herabstufung der Verschlüsselung))|Aktivität zur Herabstufung der Verschlüsselung (potenzieller Skeleton Key-Angriff)|2010|
|Verdächtige Kommunikation über DNS|Verdächtige Kommunikation über DNS|2031|
|Verdächtige Modifizierung von sensiblen Gruppen|Verdächtige Modifizierung von sensiblen Gruppen|2024|
|Erstellen eines verdächtigen Diensts|Erstellen eines verdächtigen Diensts|2026|
|Verdächtige VPN-Verbindung|Verdächtige VPN-Verbindung|2025|
|Suspected WannaCry ransomware attack (Verdacht auf einen WannaCry-Ransomangriff)|Ungewöhnliche Protokollimplementierung (potenzieller WannaCry-Ransomwareangriff)|2002|
|Suspected Brute Force attack (SMB) (Verdacht auf einen Brute-Force-Angriff (SMB))|Ungewöhnliche Protokollimplementierung (potenzielle Verwendung schädlicher Tools wie Hydra)|2002|
|Suspected use of Metasploit hacking framework (Verdacht auf Verwendung eines Hackerframeworks)|Ungewöhnliche Protokollimplementierung (potenzielle Verwendung schädlicher Hackertools wie Metasploit)|2002|
|Suspected overpass-the-hash attack (Kerberos) (Verdacht auf einen Overpass-the-Hash-Angriff (Kerberos))|Ungewöhnliche Kerberos-Protokollimplementierung (potenzieller Overpass-the-Hash-Angriff)|2002|
|User and group membership reconnaissance (SAMR) (Reconnaissance über Benutzer und Gruppenmitgliedschaften (SAMR))|Reconnaissance mithilfe von Verzeichnisdienstabfragen|2021|
|User and IP address reconnaissance (SMB) (Reconnaissance über Benutzer und IP-Adressen (SMB)) |Reconnaissance mithilfe der SMB-Sitzungsenumeration|2012|


## <a name="account-enumeration-reconnaissance"></a>Reconnaissance mithilfe von Kontoenumeration
<a name="reconnaissance-using-account-enumeration"></a>
*Vorheriger Name*: Reconnaissance mithilfe von Kontoenumeration

**Beschreibung**

Bei einer Reconnaissance zur Kontoenumeration verwendet ein Angreifer ein Wörterbuch mit tausenden von Benutzernamen oder Tools wie KrbGuess, um Benutzernamen in Ihrer Domäne zu erraten. Der Angreifer führt Kerberos-Anforderungen mit diesen Namen durch, um so auf einen gültigen Benutzernamen zu stoßen. Wenn dadurch ein Benutzername bestimmt wird, erhält der Angreifer die Kerberos-Fehlermeldung **Preauthentication required** (Vorauthentifizierung erforderlich) statt der Meldung **Security principal unknown** (Unbekannter Sicherheitsprinzipal). 

Bei dieser Erkennung kann Azure ATP erkennen, von wo der Angriff durchgeführt wurde, wie viele Versuche vorgenommen wurden und bei wie vielen dieser Versuche Übereinstimmungen gefunden wurden. Wenn es zu viele unbekannte Benutzer gibt, erkennt Azure ATP dies als verdächtige Aktivität. 

**Untersuchung**

1. Klicken Sie auf die Warnung, um auf die Seite „Details“ zu gelangen. 

2. Ist es zulässig, dass dieser Hostcomputer den Domänencontroller nach der Existenz von Konten abfragt (z.B. Exchange-Server)? <br></br>
Wird auf dem Host ein Skript oder eine Anwendung ausgeführt, die dieses Verhalten verursachen könnten? <br></br>
Wenn Sie eine dieser Fragen mit „ja“ beantworten können, **schließen Sie die verdächtige Aktivität** (dabei handelt es sich um ein harmloses richtig positives Ergebnis), und schließen Sie den Host aus der verdächtigen Aktivität aus.

3. Laden Sie die Warnungsdetails in einer Excel-Tabelle herunter, um sich eine nach vorhandenen und nicht vorhandenen Konten aufgeteilte Liste anzusehen. Wenn Sie sich das Arbeitsblatt mit den nicht vorhandenen Konten ansehen und Ihnen diese Konten bekannt vorkommen, handelt es sich dabei möglicherweise um deaktivierte Konten oder Angestellte, die nicht mehr in Ihrem Unternehmen arbeiten. In diesem Fall ist es unwahrscheinlich, dass es sich um einen Angriff mit einem Wörterbuch mit Benutzernamen handelt. Wahrscheinlich ging das Verhalten von einer Anwendung oder einem Skript aus, die überprüfen, welche Konten in Active Directory noch vorhanden sind. Dies bedeutet, dass es sich um ein harmloses richtig positives Ergebnis handelt.

3. Wenn Ihnen die Namen zum größten Teil unbekannt sind, fragen Sie sich Folgendes: Stimmt einer der geratenen Benutzernamen mit einem tatsächlichen Kontonamen in Active Directory überein? Wenn es keine Übereinstimmungen gibt, war der Versuch nicht erfolgreich. Dennoch sollten Sie diese Warnung im Blick behalten, falls Sie im Laufe der Zeit aktualisiert wird.

4. Wenn einer der Rateversuche mit einem vorhandenen Kontonamen übereinstimmt, kennt der Angreifer vorhandene Konten in Ihrer Umgebung und kann mit Brute-Force-Angriffen und gefundenen Benutzernamen versuchen, Zugriff auf Ihre Domäne zu erhalten. Überprüfen Sie die erratenen Kontonamen auf weitere verdächtige Aktivitäten. Überprüfen Sie, ob es sich bei den Konten um sensible Konten handelt.


**Wartung**

[Komplexe bzw. lange Kennwörter](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) stellen die erste Sicherheitsstufe zum Schutz gegen Brute-Force-Angriffe dar.

## <a name="honeytoken-activity"></a>Honeytoken-Aktivität
<a name="honeytoken-activity"></a>

*Vorheriger Name*: Honeytoken-Aktivität

**Beschreibung**

Honeytoken-Konten sind Köderkonten, die eingerichtet werden, um schädliche Aktivitäten, die versuchen, diese Konten zu verwenden, zu erkennen und zu verfolgen. Honeytoken-Konten sollten nicht verwendet werden, aber einen attraktiven Namen besitzen, um Angreifer anzulocken (z.B. SQL-Admin). Jede von diesen ausgehende Aktivität kann auf böswilliges Verhalten hinweisen.

Weitere Informationen zu Honeytokenkonten finden Sie unter [Konfigurieren von Erkennungsausschlüssen und Honeytokenkonten](install-atp-step7.md).

**Untersuchung**

1.  Überprüfen Sie, ob der Besitzer des Quellcomputers das Honeytoken-Konto für die Authentifizierung verwendet hat. Verwenden Sie dazu die auf der Seite „Verdächtige Aktivitäten“ beschriebene Methode (z.B. Kerberos, LDAP, NTLM).

2.  Navigieren Sie zu den Profilseiten des Quellcomputers, und überprüfen Sie, welche anderen Konten darüber authentifiziert wurden. Wenden Sie sich an die Besitzer dieser Konten, um festzustellen, ob Sie das Honeytoken-Konto verwendet haben.

3.  Dabei könnte es sich um eine nicht interaktive Anmeldung handeln. Überprüfen Sie deshalb Anwendungen oder Skripts, die auf dem Quellcomputer ausgeführt werden.

Wenn nach dem Ausführen von Schritt 1 bis 3 keine Beweise dafür vorliegen, dass es sich um eine harmlose Verwendung handelt, gehen Sie von einem böswilligen Ereignis aus.

**Wartung**

Stellen Sie sicher, dass Honeytoken-Konten nur für den beabsichtigten Zweck verwendet werden, andernfalls könnten sie viele Warnungen generieren.

## <a name="malicious-request-of-data-protection-api-master-key"></a>Malicious request of Data Protection API master key (Böswillige Anforderung eines Masterschlüssels zur Datenschutz-API)
<a name="malicious-data-protection-private-information-request"></a>

*Vorheriger Name*: Böswillige Anforderung privater Informationen im Rahmen der Datensicherheit

**Beschreibung**

Die Datenschutz-API (DPAPI) wird von Windows verwendet, um von Browsern gespeicherte Kennwörter, verschlüsselte Dateien und andere sensible Daten sicher zu schützen. Domänencontroller enthalten einen Hauptschlüssel zur Sicherung, der verwendet werden kann, um alle mit der DPAPI verschlüsselten Geheimnisse auf mit einer Domäne verbundenen Windows-Computern zu entschlüsseln. Angreifer können diesen Hauptschlüssel verwenden, um sämtliche von DPAPI geschützten Geheimnisse auf allen mit einer Domäne verbundenen Computern zu entschlüsseln.
In dieser Erkennung wird eine Warnung ausgelöst, wenn die DPAPI zum Abrufen des Sicherungshauptschlüssels verwendet wird.

**Untersuchung**

1. Wird auf dem Quellcomputer ein von der Organisation genehmigter Sicherheitsscanner für Active Directory ausgeführt?

2. Falls dies zutrifft und von Ihnen so gewünscht ist, können Sie die verdächtige Aktivität **schließen und ausschließen**.

3. Falls dies zutrifft und von Ihnen nicht so gewünscht ist, **schließen** Sie die verdächtige Aktivität.

**Wartung**

Ein Angreifer benötigt Domänenadministratorrechte zum Verwenden der DPAPI. Implementieren Sie  [Pass the hash recommendations (Empfehlungen zu Pass-the-Hash)](https://www.microsoft.com/download/details.aspx?id=36036).

## <a name="suspected-brute-force-attack-ldap"></a>Suspected Brute Force attack (LDAP) (Verdacht auf einen Brute-Force-Angriff (LDAP)) 
<a name="brute-force-attack-using-ldap-simple-bind"></a>
*Vorheriger Name*: Brute-Force-Angriff mithilfe einer einfachen LDAP-Bindung

**Beschreibung**

>[!NOTE]
> Der Hauptunterschied zwischen **verdächtigen Authentifizierungsfehlern** und dieser Erkennung ist der, dass in dieser Erkennung durch Azure ATP bestimmt werden kann, ob verschiedene Kennwörter verwendet wurden.

Bei einem Brute-Force-Angriff versucht ein Angreifer, sich mit vielen verschiedenen Kennwörtern für verschiedene Konten anzumelden, bis ein korrektes Kennwort für mindestens ein Konto gefunden wird. Sobald eines gefunden wurde, kann sich der Angreifer mit diesem Konto anmelden.

In dieser Erkennung wird eine Warnung ausgelöst, wenn Azure ATP eine signifikante Anzahl von Authentifizierungen mit einfacher Bindung erkennt. Dies kann entweder *horizontal* mit einem kleinen Satz von Kennwörtern für viele Benutzer oder *vertikal* mit einem großen Satz von Kennwörtern für wenige Benutzer geschehen. Auch eine beliebige Kombination dieser beiden Optionen ist möglich.

**Untersuchung**

1. Wenn viele Konten beteiligt sind, klicken Sie auf **Details herunterladen**, um die Liste in einem Excel-Arbeitsblatt anzuzeigen.

2. Klicken Sie auf die Warnung, um zu der dedizierten Seite zu gelangen. Überprüfen Sie, ob Anmeldeversuche mit einer erfolgreichen Authentifizierung beendet wurden. Die Versuche erscheinen als **Erratene Konten** auf der rechten Seite der Infografik. Falls ja, werden von den **erratenen Konten** einige normalerweise vom Quellcomputer verwendet? Falls ja, **unterdrücken** Sie die verdächtige Aktivität.

3. Wenn es keine **erratenen Konten** gibt, werden einige von den **angegriffenen Konten** normalerweise vom Quellcomputer verwendet? Falls ja, **unterdrücken** Sie die verdächtige Aktivität.

**Wartung**

[Komplexe bzw. lange Kennwörter](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) stellen die erste Sicherheitsstufe zum Schutz gegen Brute-Force-Angriffe dar.

## <a name="suspected-brute-force-attack-kerberos-ntlm"></a>Suspected Brute Force attack (Kerberos NTLM) (Verdacht auf einen Brute-Force-Angriff (Kerberos NTLM))
<a name="suspicious-authentication-failures"></a>

*Vorheriger Name*: Verdächtige Authentifizierungsfehler

**Beschreibung**

Bei einem Brute-Force-Angriff versucht der Angreifer, sich mit mehreren Kennwörtern bei verschiedenen Konten zu authentifizieren, bis er ein korrektes Kennwort findet, oder der Angreifer verwendet ein Kennwort im Rahmen eines umfangreichen Kennwort-Spray-Angriffs, das bei mindestens einem Konto funktioniert. Sobald eines gefunden wurde, meldet sich der Angreifer mit dem authentifizierten Konto an.

Bei diesem Erkennungsvorgang wird eine Warnung ausgelöst, wenn viele Authentifizierungsfehler bei der Verwendung von Kerberos oder NTLM auftreten oder die Ausführung eines Kennwort-Spray-Angriffs erkannt wurde. Bei Kerberos oder NTLM kann dieser Angriff üblicherweise entweder horizontal mit einem kleinen Satz von Kennwörtern für viele Benutzer oder vertikal mit einem großen Satz von Kennwörtern für wenige Benutzer geschehen. Auch eine beliebige Kombination dieser beiden Optionen ist möglich. Bei einem Kennwort-Spray-Angriff testen Angreifer nach erfolgreichem Durchzählen einer Liste von gültigen Benutzern aus dem Domänencontroller EIN sorgfältig erstelltes Kennwort für ALLE bekannten Benutzerkonten (ein Kennwort für n Konten). Wenn beim ersten Kennwort-Spray-Angriff ein Fehler auftritt, wiederholen sie den Vorgang mit einem anderen sorgfältig erstellten Kennwort – normalerweise nach einer Wartezeit von 30 Minuten zwischen den Versuchen. Durch die Wartezeit verhindern Angreifer, dass meist zeitbasierte Schwellenwerte für die Kontosperre ausgelöst werden. Kennwort-Spray-Angriffe haben sich rasch zu einer beliebten Methode unter Angreifern und Pen-Testern entwickelt. Kennwort-Spray-Angriffe haben sich als effektiv erwiesen, um innerhalb einer Organisation einen Ankerpunkt zu finden und infolgedessen weitere Schwachstellen auszunutzen, um Berechtigungen auszuweiten. 

**Lernphase** Der Mindestzeitraum, bevor eine Warnung dieses Typs ausgelöst werden kann, beträgt eine Woche.

**Untersuchung**

1.  Klicken Sie auf **Details herunterladen**, um die vollständigen Informationen in einem Excel-Arbeitsblatt anzuzeigen. Die folgenden Informationen sind verfügbar: 
   -    Liste der angegriffenen Konten
   -    Liste der erratenen Konten, bei denen Anmeldeversuche mit einer erfolgreichen Authentifizierung endeten
   -    Wenn die Authentifizierungsversuche über NTLM ausgeführt wurden, werden die relevanten Ereignisaktivitäten angezeigt. 
   -    Wenn die Authentifizierungsversuche über Kerberos ausgeführt wurden, werden die relevanten Netzwerkaktivitäten angezeigt.
   -  Wenn die Authentifizierungsversuche über einen Kennwort-Spray-Angriff ausgeführt wurden, werden die relevanten Netzwerkaktivitäten angezeigt.

2.  Klicken Sie auf den Quellcomputer, um die entsprechende Profilseite aufzurufen. Überprüfen Sie, was ungefähr zum Zeitpunkt dieser Versuche passiert ist. Suchen Sie nach ungewöhnlichen Aktivitäten wie z.B.: Wer war angemeldet, auf welche Ressourcen wurde zugegriffen. Wenn Sie die Windows Defender ATP-Integration aktiviert haben, klicken Sie auf das Windows Defender ATP-Badge, ![Windows Defender ATP-Badge](./media/wd-badge.png) um den Computer weiter zu untersuchen. In Windows Defender ATP können Sie sehen, welche Prozesse und Warnungen ungefähr gleichzeitig mit der Warnung aufgetreten sind. 

3.  Wenn die Authentifizierung mithilfe von NTLM durchgeführt wurde und Sie sehen, dass die Warnung mehrfach aufgetreten ist, aber keine ausreichenden Informationen zum Server verfügbar sind, auf den der Quellcomputer zugreifen wollte, aktivieren Sie die **NTLM-Überwachung** für die betroffenen Domänencontroller. Aktivieren Sie dazu Ereignis 8004. Dies ist das NTLM-Authentifizierungsereignis, das Informationen zum Quellcomputer, Benutzerkonto und **Server enthält, auf die der Quellcomputer zugreifen wollte. Wenn Sie wissen, welcher Server die Authentifizierungsüberprüfung gesendet hat, untersuchen Sie den Server, indem Sie seine Ereignisse, z.B. 4624, überprüfen, um den Authentifizierungsprozess besser nachvollziehen zu können. 

**Wartung**

[Komplexe bzw. lange Kennwörter](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) stellen die erste Sicherheitsstufe zum Schutz gegen Brute-Force-Angriffe dar.

## <a name="suspected-dcshadow-attack-dc-promotion"></a>Suspected DCShadow attack (DC promotion) (Verdacht auf DCShadow-Angriff (Heraufstufung von DC))
<a name="suspicious-domain-controller-promotion-potential-dcshadow-attack"></a>

*Vorheriger Name*: Verdächtige Heraufstufung zu Domänencontrollern (potenzieller DcShadow-Angriff)

**Beschreibung**

Bei einem DCShadow-Angriff (Domain Controller Shadow) handelt es sich um einen Angriff, bei dem mithilfe einer schädlichen Replikation Verzeichnisobjekte geändert werden sollen. Ein solcher Angriff kann von jedem Computer aus erfolgen, indem mithilfe eines Replikationsvorgangs ein nicht autorisierter Domänencontroller erstellt wird.
 
DCShadow verwendet RPC und LDAP zu folgenden Zwecken:
1. Das Computerkonto wird (unter Verwendung von Domänenadministratorrechten) als Domänencontroller registriert.
2. Die Replikation wird (unter Verwendung der gewährten Replikationsrechte) über DRSUAPI durchgeführt, und Änderungen werden an Verzeichnisobjekte gesendet.
 
Bei dieser Erkennungsfunktion wird eine Warnung ausgelöst, wenn ein Computer im Netzwerk versucht, sich als nicht autorisierter Domänencontroller zu registrieren. 

**Untersuchung**
 
1. Ist der fragliche Computer ein Domänencontroller? Beispielsweise ein neu hochgestufter Domänencontroller mit Replikationsproblemen. Falls ja, **schließen** Sie die verdächtige Aktivität.
2. Soll der fragliche Computer Daten von Active Directory replizieren? Beispielsweise Azure AD Connect. Falls ja, können Sie die verdächtige Aktivität **schließen und ausschließen**.
3. Klicken Sie auf den Quellcomputer oder das Konto, um die entsprechende Profilseite aufzurufen. Überprüfen Sie, was ungefähr zum Zeitpunkt der Replikation passiert ist. Suchen Sie nach ungewöhnlichen Aktivitäten wie z.B.: Wer war angemeldet, auf welche Ressourcen wurde zugegriffen, und um welches Computerbetriebssystem handelt es sich?
   1. Sollen alle Benutzer, die am Computer angemeldet waren, tatsächlich angemeldet sein? Welche Berechtigungen haben sie? Verfügen sie über die Berechtigung, einen Computer zum Domänencontroller hochzustufen? Handelt es sich um Domänenadministratoren?
   2. Sollen die Benutzer Zugriff auf diese Ressourcen haben?
   3. Wird auf dem Computer ein Windows Server-Betriebssystem (oder Windows/Linux) ausgeführt? Ein Computer, bei dem es sich nicht um einen Server handelt, darf keine Daten replizieren.
Wenn die Windows Defender ATP-Integration aktiviert ist, klicken Sie auf das Windows Defender ATP-Badge ![Windows Defender ATP-Badge](./media/wd-badge.png), um den Computer genauer zu untersuchen. In Windows Defender ATP können Sie sehen, welche Prozesse und Warnungen ungefähr gleichzeitig mit der Warnung aufgetreten sind.

4. Sehen Sie sich in der Ereignisanzeige [Active Directory-Ereignisse an, die im Protokoll der Verzeichnisdienste aufgezeichnet wurden](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961809(v=technet.10)/). Sie können das Protokoll verwenden, um Änderungen in Active Directory zu überwachen. Standardmäßig zeichnet Active Directory nur kritische Fehlerereignisse auf. Wenn diese Warnung aber wiederholt auftritt, aktivieren Sie diese Überwachung auf dem entsprechenden Domänencontroller, um eine weitere Untersuchung zu ermöglichen.

**Korrektur**

Überprüfen Sie, welche Benutzer in Ihrer Organisation über die folgenden Berechtigungen verfügen: 
- Replizieren von Verzeichnisänderungen 
- Replizieren von allen Verzeichnisänderungen 
 
 
Weitere Informationen finden Sie unter [Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013 (Erteilen von AD DS-Berechtigungen für die Profilsynchronisierung in SharePoint Server 2013)](https://technet.microsoft.com/library/hh296982.aspx). 

Nutzen Sie [AD ACL Scanner](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/), oder erstellen Sie ein Windows PowerShell-Skript, um festzustellen, wer in der Domäne über diese Berechtigungen verfügt.
 
> [!NOTE]
> Warnungen vor verdächtigen Heraufstufungen zu Domänencontrollern (potenzieller DCShadow-Angriff) werden nur von ATP-Sensoren unterstützt. 

## <a name="suspected-dcshadow-attack-dc-replication-request"></a>Suspected DCShadow attack (DC replication request) (Verdacht auf DCShadow-Angriff (DC-Replikationsanforderung))
<a name="suspicious-replication-request-potential-dcshadow-attack"></a>

*Vorheriger Name*: Verdächtige Replikationsanforderung (potenzieller DCShadow-Angriff) 

**Beschreibung** 

Bei der Active Directory-Replikation werden Änderungen, die auf einem Domänencontroller durchgeführt wurden, mit anderen Domänencontrollern synchronisiert. Wenn Angreifer über die erforderlichen Berechtigungen verfügen, können sie ihren Computerkonten Rechte gewähren, die es ihnen ermöglichen, die Identität eines Domänencontrollers anzunehmen. Die Angreifer werden versuchen, eine schädliche Replikationsanforderung zu initiieren, die es ihnen ermöglicht, Active Directory-Objekte auf einem echten Domänencontroller zu ändern und so in die Domäne einzudringen.
Bei dieser Erkennungsfunktion wird eine Warnung ausgelöst, wenn eine verdächtige Replikationsanforderung für einen echten Domänencontroller generiert wird, der durch Azure ATP geschützt ist. Dieses Verhalten weist auf Techniken hin, die bei DCShadow-Angriffen verwendet werden.

**Untersuchung** 
 
1. Ist der fragliche Computer ein Domänencontroller? Beispielsweise ein neu hochgestufter Domänencontroller mit Replikationsproblemen. Falls ja, **schließen** Sie die verdächtige Aktivität.
2. Soll der fragliche Computer Daten von Active Directory replizieren? Beispielsweise Azure AD Connect. Falls ja, können Sie die verdächtige Aktivität **schließen und ausschließen**.
3. Klicken Sie auf den Quellcomputer, um die entsprechende Profilseite aufzurufen. Überprüfen Sie, was **ungefähr zum Zeitpunkt** der Replikation passiert ist. Suchen Sie nach ungewöhnlichen Aktivitäten wie z.B.: Wer war angemeldet, welche Ressourcen wurden verwendet, und um welches Computerbetriebssystem handelt es sich?

   1.  Sollen alle Benutzer, die am Computer angemeldet waren, tatsächlich angemeldet sein? Welche Berechtigungen haben sie? Besitzen sie die Berechtigung, Replikationen auszuführen (sind sie Domänenadministratoren)?
   2.  Sollen die Benutzer Zugriff auf diese Ressourcen haben?
   3. Wird auf dem Computer ein Windows Server-Betriebssystem (oder Windows/Linux) ausgeführt? Ein Computer, bei dem es sich nicht um einen Server handelt, darf keine Daten replizieren.
Wenn die Windows Defender ATP-Integration aktiviert ist, klicken Sie auf das Windows Defender ATP-Badge ![Windows Defender ATP-Badge](./media/wd-badge.png), um den Computer genauer zu untersuchen. In Windows Defender ATP können Sie sehen, welche Prozesse und Warnungen ungefähr gleichzeitig mit der Warnung aufgetreten sind.
1. Sehen Sie sich in der Ereignisanzeige [Active Directory-Ereignisse an, die im Protokoll der Verzeichnisdienste aufgezeichnet wurden](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961809(v=technet.10)/). Sie können das Protokoll verwenden, um Änderungen in Active Directory zu überwachen. Standardmäßig zeichnet Active Directory nur kritische Fehlerereignisse auf. Wenn diese Warnung aber wiederholt auftritt, aktivieren Sie diese Überwachung auf dem entsprechenden Domänencontroller, um eine weitere Untersuchung zu ermöglichen.

**Wartung**

Überprüfen Sie, welche Benutzer in Ihrer Organisation über die folgenden Berechtigungen verfügen: 
- Replizieren von Verzeichnisänderungen 
- Replizieren von allen Verzeichnisänderungen 

Nutzen Sie zu diesem Zweck den [AD ACL Scanner](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/), oder erstellen Sie ein Windows PowerShell-Skript, um zu ermitteln, wer in der Domäne über diese Berechtigungen verfügt.

> [!NOTE]
> Warnungen vor verdächtigen Replikationsanforderungen (potenzieller DCShadow-Angriff) werden nur von ATP-Sensoren unterstützt. 

## <a name="suspected-dcsync-attack-replication-of-directory-services"></a>Suspected DCSync attack (replication of directory services) (Verdacht auf einen DCSync-Angriff (Replikation von Verzeichnisdiensten))
<a name="malicious-replication-of-directory-services"></a>

*Vorheriger Name*: Böswillige Replikation von Verzeichnisdiensten

**Beschreibung**

Bei der Replikation mit Active Directory werden Änderungen eines Domänencontrollers mit allen anderen Domänencontrollern synchronisiert. Mit den erforderlichen Berechtigungen können Angreifer eine Replikationsanforderung initiieren, die ihnen das Abrufen der in Active Directory gespeicherten Daten ermöglicht, einschließlich der Kennworthashes.

In dieser Erkennung wird eine Warnung ausgelöst, wenn eine Replikationsanforderung von einem Computer initiiert wird, der kein Domänencontroller ist.

**Untersuchung**

> [!NOTE]
> Falls Sie Domänencontroller haben, auf denen keine Azure ATP-Sensoren installiert sind, werden diese nicht von Azure ATP abgedeckt. Wenn Sie dann einen neuen Domänencontroller auf einem nicht registrierten oder ungeschützten Domänencontroller bereitstellen, wird dieser möglicherweise zunächst nicht von Azure ATP als Domänencontroller erkannt. Es wird dringend empfohlen, den Azure ATP-Sensor für eine vollständige Abdeckung auf jedem Domänencontroller zu installieren.

1. Ist der fragliche Computer ein Domänencontroller? Beispielsweise ein neu hochgestufter Domänencontroller mit Replikationsproblemen. Falls ja, **schließen** Sie die verdächtige Aktivität. 
2.  Soll der fragliche Computer Daten von Active Directory replizieren? Z. B. Azure AD Connect oder Geräte zur Netzwerkleistungsüberwachung. Falls ja, können Sie die verdächtige Aktivität **schließen und ausschließen**.
3. Wurde die IP-Adresse, von der die Replikationsanforderung gesendet wurde, über NAT oder Proxy übermittelt? Falls ja, überprüfen Sie, ob sich hinter dem Gerät ein neuer Domänencontroller befindet, oder ob andere verdächtige Aktivitäten für das Gerät aufgetreten sind. 

4. Klicken Sie auf den Quellcomputer oder das Konto, um die entsprechende Profilseite aufzurufen. Überprüfen Sie, was ungefähr zum Zeitpunkt der Replikation passiert ist. Suchen Sie nach ungewöhnlichen Aktivitäten wie z.B.: Wer war angemeldet, auf welche Ressourcen wurde zugegriffen. Wenn Sie die Windows Defender ATP-Integration aktiviert haben, klicken Sie auf das Windows Defender ATP-Badge, ![Windows Defender ATP-Badge](./media/wd-badge.png) um den Computer weiter zu untersuchen. In Windows Defender ATP können Sie sehen, welche Prozesse und Warnungen ungefähr gleichzeitig mit der Warnung aufgetreten sind. 


**Wartung**

Überprüfen Sie die folgenden Berechtigungen: 

- Replizieren von Verzeichnisänderungen   

- Replizieren von allen Verzeichnisänderungen  

Weitere Informationen finden Sie unter  [Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013 (Erteilen von AD DS-Berechtigungen für die Profilsynchronisierung in SharePoint Server 2013)](https://technet.microsoft.com/library/hh296982.aspx).
Nutzen Sie  [AD ACL Scanner](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) , oder erstellen Sie ein Windows PowerShell-Skript, um festzustellen, wer in der Domäne über diese Berechtigungen verfügt.

## <a name="suspected-golden-ticket-usage-encryption-downgrade"></a>Verdacht auf Verwendung eines Golden Ticket (Herabstufung der Verschlüsselung)
<a name="Encryption-downgrade-activity-potential-golden-ticket-attack"></a>

*Vorheriger Name*: Aktivität zur Herabstufung der Verschlüsselung

**Beschreibung:** Die Herabstufung der Verschlüsselung ist eine Methode, die dazu dient, Kerberos zu schwächen, indem für die Verschlüsselungsstufe von unterschiedlichen Feldern des Protokolls, die mit der höchsten Verschlüsselungsstufe verschlüsselt werden, ein Downgrade durchgeführt wird. Ein abgeschwächtes verschlüsseltes Feld ist ein leichteres Ziel für versuchte Brute-Force-Angriffe offline. Verschiedene Angriffsmethoden nutzen schwache Kerberos-Verschlüsselungsverfahren. In dieser Erkennung lernt Azure ATP die Kerberos-Verschlüsselungstypen, die von Computern und Benutzern verwendet werden, und benachrichtigt Sie, wenn ein schwächeres Verschlüsselungsverfahren verwendet wird, das (1) unüblich für den Quellcomputer und/oder den Benutzer ist und (2) mit bekannten Angriffstechniken übereinstimmt. 

Bei einer Golden Ticket-Warnung wurde die Verschlüsselungsmethode des TGT-Felds der TGS_REQ-Nachricht (Dienstanforderung) vom Quellcomputer im Vergleich zum zuvor gelernten Verhalten herabgestuft. Dies basiert nicht auf einer Zeitanomalie (wie bei der anderen Golden Ticket-Erkennung). Zusätzlich gab es keine Kerberos-Authentifizierungsanforderung, die der vorherigen von ATP erkannten Dienstanforderung zugeordnet ist.

**Untersuchung**
1. Einige Ressourcen unterstützten starke Verschlüsselungsmethoden nicht und lösen diese Warnung möglicherweise aus.
   1. Überprüfen Sie die Ressourcen, auf die mit diesen Tickets zugegriffen wurde. Verwenden Sie dafür das *msDS-SupportedEncryptionTypes*-Attribut des Ressourcendienstkontos in Azure Active Directory.
   2. Wenn Sie feststellen, dass auf eine Ressource zugegriffen wurde, überprüfen Sie diese. Vergewissern Sie sich, dass es sich um eine gültige Ressource handelt, auf die zugegriffen werden darf. 
2. Bei benutzerdefinierten Anwendungen wird möglicherweise eine niedrigere Verschlüsselungschiffre für die Authentifizierung verwendet.
   1. Überprüfen Sie, ob benutzerdefinierte Apps vorhanden sind, die auf dem Quellcomputer eine niedrigere Verschlüsselungschiffre für die Authentifizierung verwenden.
   2. Wenn es mehrere Benutzer gibt, überprüfen Sie diese auf Gemeinsamkeiten. <br>Beispielsweise könnten alle Marketingmitarbeiter eine bestimmte App verwenden, die die Warnung ausgelöst hat.
3. Klicken Sie auf den Quellcomputer oder das Konto, um die entsprechende Profilseite aufzurufen. Überprüfen Sie die Vorgänge zum Zeitpunkt der Replikation. Suchen Sie nach ungewöhnlichen Aktivitäten, z. B.: Wer war angemeldet und auf welche Ressourcen wurde zugegriffen? 

4. Wenn Sie die Windows Defender ATP-Integration aktiviert haben, klicken Sie auf das Windows Defender ATP-Badge, ![Windows Defender ATP-Badge](./media/wd-badge.png) um den Computer weiter zu untersuchen. In Windows Defender ATP können Sie sehen, welche Prozesse und Warnungen ungefähr gleichzeitig mit der Warnung aufgetreten sind.

**Wartung**

1. Setzen Sie das Kennwort für die gefährdeten Benutzer zurück.
2. Ändern Sie das Kennwort für das Kerberos Ticket Granting Ticket (KRBTGT) zweimal gemäß den Anweisungen unter [KRBTGT Account Password Reset Scripts now available for customers (Skripts zum Zurücksetzen von Kennwörtern des KRBTGT-Kontos stehen Kunden jetzt zur Verfügung)](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) mithilfe des [Reset the KRBTGT account password/keys tool (Tools zum Zurücksetzen des Kennworts/Schlüssels eines KRBTGT-Kontos)](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Durch das zweimalige Zurücksetzen von KRBTGT werden alle Kerberos-Tickets in dieser Domäne ungültig. Daher sollten Sie diesen Schritt im Voraus planen.

## <a name="suspected-golden-ticket-usage-forged-authorization-data"></a>Suspected Golden Ticket usage (forged authorization data) (Verdacht auf Verwendung eines Golden Ticket (gefälschte Autorisierungsdaten))
<a name="privilege-escalation-using-forged-authorization-data"></a>

*Vorheriger Name*: Berechtigungsausweitung mithilfe von gefälschten Autorisierungsdaten

**Beschreibung**

Über bekannte Sicherheitslücken in älteren Versionen von Windows Server können Angreifer das Privileged Attribute Certificate (PAC) manipulieren. PAC ist ein Feld im Kerberos-Ticket, das Benutzerdaten für die Autorisierung enthält (in Active Directory ist dies eine Gruppenmitgliedschaft), die Angreifern zusätzliche Berechtigungen gewähren.

**Untersuchung**

1. Klicken Sie auf die Warnung, um auf die Seite „Details“ zu gelangen.

2. Ist der Zielcomputer (in der Spalte **ACCESSED**) mit MS14-068 (Domänencontroller) oder MS11-013 (Server) gepatcht? Falls ja, **schließen** Sie die verdächtige Aktivität (diese ist falsch positiv).

3. Wenn nicht, wird auf dem Quellcomputer ausgeführt (in der Spalte **FROM**) ein Betriebssystem bzw. eine Anwendung ausgeführt, die dafür bekannt sind, das PAC zu ändern? Falls ja, **unterdrücken** Sie die verdächtige Aktivität (diese ist unbedenklich richtig positiv).

4. Wenn die Antwort auf die obigen zwei Fragen „nein“ ist, gehen Sie von einem böswilligen Ereignis aus.

**Wartung**

Stellen Sie sicher, dass alle Domänencontroller mit Betriebssystemen bis Windows Server 2012 R2 mit  [KB3011780](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privilege)  installiert sind und dass alle Memberserver und Domänencontroller bis 2012 R2 das aktuellste KB2496930 haben. Weitere Informationen finden Sie unter  [Silver PAC](https://technet.microsoft.com/library/security/ms11-013.aspx)  und  [Gefälschte PAC-Datei](https://technet.microsoft.com/library/security/ms14-068.aspx).

## <a name="suspected-golden-ticket-usage-nonexistant-account"></a>Verdacht auf Verwendung eines Golden Ticket (nicht vorhandenes Konto)
<a name="golden-ticket"></a>

Vorheriger Name: Kerberos Golden Ticket

**Beschreibung**

Angreifer, die Domänenadministratorrechte erlangen, können das KRBTGT-Konto beeinträchtigen. Angreifer können das KRBTGT-Konto verwenden, um ein Kerberos Ticket Granting Ticket (TGT) zu erstellen, das Autorisierung für jede beliebige Ressource bietet. Ein gefälschtes TGT dieses Typs wird als „Golden Ticket“ bezeichnet, da Angreifer damit dauerhafte Netzwerkpersistenz erlangen. Bei dieser Erkennung wird durch die Verwendung eines nicht vorhandenen Kontos eine Warnung ausgelöst.

**Untersuchung**

1. Untersuchen Sie die folgenden Fragen:
      - Ist der Benutzer ein bekannter und gültiger Domänenbenutzer? Falls ja, schließen Sie die Warnung (sie war falsch positiv).
      - Wurde der Benutzer kürzlich hinzugefügt? Falls Ja, schließen Sie die Warnung. Möglicherweise wurde die Änderung noch nicht synchronisiert.
      - Wurde der Benutzer kürzlich aus AD gelöscht? Falls ja, schließen Sie die Warnung.
2. Wenn die Antwort auf die obigen Fragen „nein“ ist, gehen Sie von einem böswilligen Ereignis aus.

3. Klicken Sie auf den Quellcomputer, um die entsprechende **Profilseite** aufzurufen. Überprüfen Sie, was ungefähr zum Zeitpunkt der Aktivität passiert ist. Achten Sie auf ungewöhnliche Aktivitäten, z. B. welcher Benutzer angemeldet war und auf welche Ressourcen zugegriffen wurde. 

4. Sollen alle Benutzer, die am Computer angemeldet waren, angemeldet sein? Welche Berechtigungen haben sie? 

5. Sollen die angemeldeten Benutzer Zugriff auf diese Ressourcen haben?<br>
Wenn Sie die Windows Defender ATP-Integration aktiviert haben, klicken Sie auf das Windows Defender ATP-Badge.
 
 1. Um den Computer weiter zu untersuchen, überprüfen Sie, welche Prozesse und Warnungen ungefähr dann aufgetreten sind, als die Warnung in Windows Defender ATP ausgelöst wurde.

**Wartung**


Ändern Sie das Kennwort für das Kerberos Ticket Granting Ticket (KRBTGT) zweimal gemäß den Anweisungen unter [KRBTGT Account Password Reset Scripts now available for customers (Skripts zum Zurücksetzen von Kennwörtern des KRBTGT-Kontos stehen Kunden jetzt zur Verfügung)](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) mithilfe des [Reset the KRBTGT account password/keys tool (Tools zum Zurücksetzen des Kennworts/Schlüssels eines KRBTGT-Kontos)](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Durch das zweimalige Zurücksetzen von KRBTGT werden alle Kerberos-Tickets in dieser Domäne ungültig. Daher sollten Sie diesen Schritt im Voraus planen. Implementieren Sie ebenfalls die [Pass the hash recommendations (Empfehlungen zu Pass-the-Hash)](https://www.microsoft.com/download/details.aspx?id=36036), da für das Erstellen eines Golden Tickets Domänenadministratorrechte erforderlich sind.

## <a name="suspected-golden-ticket-usage-time-anomaly"></a>Suspected golden ticket usage (time anomaly) (Verdacht auf Verwendung eines Golden Ticket (Zeitanomalie))

Vorheriger Name: Kerberos Golden Ticket

**Beschreibung**

Angreifer, die Domänenadministratorrechte erlangen, können das [KRBTGT-Konto](https://technet.microsoft.com/library/dn745899(v=ws.11).aspx#Sec_KRBTGT) beeinträchtigen. Über das KRBTGT-Konto können Angreifer ein Kerberos Ticket Granting Ticket (TGT) erstellen, das die Autorisierung für jede beliebige Ressource erteilen und den Ablaufzeitpunkt des Tickets auf einen beliebigen Zeitpunkt festlegen kann. Ein gefälschtes TGT dieses Typs wird als „Golden Ticket“ bezeichnet, da Angreifer damit dauerhafte Netzwerkpersistenz erlangen. In dieser Erkennung wird eine Warnung ausgelöst, wenn ein Kerberos Ticket Granting Ticket länger als erlaubt verwendet wird. Die zulässige Dauer ist in der Sicherheitsrichtlinie [Maximum lifetime for user ticket](https://technet.microsoft.com/library/jj852169(v=ws.11).aspx) (Max. Gültigkeitsdauer des Benutzertickets) angegeben.


**Untersuchung**

1. Wurden kürzlich (innerhalb der letzten Stunden) Änderungen an der Einstellung „Maximale Lebensdauer für Benutzertickets“ in der Gruppenrichtlinie vorgenommen? Überprüfen Sie, ob der spezifische Wert niedriger als der Zeitwert der Ticketnutzungsdauer ist. Falls ja, schließen Sie die Warnung (sie war falsch positiv).

2. Ist der Azure ATP-Sensor in dieser Warnung ein virtueller Computer? Falls ja, wurde dieser kürzlich aus einem gespeicherten Zustand fortgesetzt? Falls ja, schließen Sie diese Warnung.

3. Wenn die Antwort auf die obigen Fragen „nein“ ist, gehen Sie von einem böswilligen Ereignis aus.

**Wartung**


Ändern Sie das Kennwort für das Kerberos Ticket Granting Ticket (KRBTGT) zweimal gemäß den Anweisungen unter [KRBTGT Account Password Reset Scripts now available for customers (Skripts zum Zurücksetzen von Kennwörtern des KRBTGT-Kontos stehen Kunden jetzt zur Verfügung)](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) mithilfe des [Reset the KRBTGT account password/keys tool (Tools zum Zurücksetzen des Kennworts/Schlüssels eines KRBTGT-Kontos)](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Durch das zweimalige Zurücksetzen von KRBTGT werden alle Kerberos-Tickets in dieser Domäne ungültig. Daher sollten Sie diesen Schritt im Voraus planen. Implementieren Sie ebenfalls die [Pass the hash recommendations (Empfehlungen zu Pass-the-Hash)](https://www.microsoft.com/download/details.aspx?id=36036), da für das Erstellen eines Golden Tickets Domänenadministratorrechte erforderlich sind.

## <a name="suspected-golden-ticket-usage-ticket-anomaly---preview"></a>Verdacht auf Verwendung eines Golden Ticket (Ticketanomalie) – Vorschauversion
<a name="golden-ticket-usage-ticket-anomaly
"></a>

**Beschreibung**

Angreifer mit Domänenadministratorrechten können das KRBTGT-Konto beeinträchtigen. Angreifer können das KRBTGT-Konto verwenden, um ein Kerberos Ticket Granting Ticket (TGT) zu erstellen, das Autorisierung für jede beliebige Ressource bietet. Ein gefälschtes TGT dieses Typs wird als „Golden Ticket“ bezeichnet, da Angreifer damit dauerhafte Netzwerkpersistenz erlangen. Gefälschte Golden Tickets dieses Typs weisen eindeutige Merkmale auf, für deren Identifikation diese Erkennung konzipiert ist. 

**Untersuchung**
1. Verbunddienste generieren möglicherweise Tickets, die diese Warnung auslösen. Werden auf dem Quellcomputer derartige Dienste gehostet? Wenn dies der Fall ist, schließen Sie die Sicherheitswarnung.
2. Klicken Sie auf den Quellbenutzer, um dessen Profilseite aufzurufen. Überprüfen Sie die Vorgänge zum Zeitpunkt der Aktivität.
      1. Soll der Benutzer Zugriff auf diese Ressource haben (ist es erlaubt)? 
      2.  Wird erwartet, dass der Prinzipal auf den Dienst zugreifen kann? 
3. Klicken Sie auf den Quellcomputer, um die entsprechende Profilseite aufzurufen. Überprüfen Sie, was ungefähr zum Zeitpunkt der Aktivität passiert ist. Achten Sie auf ungewöhnliche Aktivitäten, z.B. welcher Benutzer angemeldet war und auf welche Ressourcen zugegriffen wurde. 
4. Sollen alle Benutzer, die am Computer angemeldet waren, tatsächlich bei diesem angemeldet sein? Welche Berechtigungen haben sie? 
5. Sollen die angemeldeten Benutzer Zugriff auf diese Ressourcen haben. bei denen sie angemeldet sind?
<br>Wenn Sie die Windows Defender ATP-Integration aktiviert haben, klicken Sie auf das Windows Defender ATP-Badge.
6. Um den Computer weiter zu untersuchen, überprüfen Sie, welche Prozesse und Warnungen ungefähr dann aufgetreten sind, als die Warnung in Windows Defender ATP ausgelöst wurde.


**Wartung**

Ändern Sie das Kennwort für das Kerberos Ticket Granting Ticket (KRBTGT) zweimal gemäß den Anweisungen unter [KRBTGT Account Password Reset Scripts now available for customers (Skripts zum Zurücksetzen von Kennwörtern des KRBTGT-Kontos stehen Kunden jetzt zur Verfügung)](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) mithilfe des [Reset the KRBTGT account password/keys tool (Tools zum Zurücksetzen des Kennworts/Schlüssels eines KRBTGT-Kontos)](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Durch das zweimalige Zurücksetzen von KRBTGT werden alle Kerberos-Tickets in dieser Domäne ungültig. Daher sollten Sie diesen Schritt im Voraus planen. Implementieren Sie ebenfalls die [Pass the hash recommendations (Empfehlungen zu Pass-the-Hash)](https://www.microsoft.com/download/details.aspx?id=36036), da für das Erstellen eines Golden Tickets Domänenadministratorrechte erforderlich sind.

## <a name="suspected-identity-theft-pass-the-hash"></a>Suspected identity theft (pass-the-hash) (Verdacht auf Identitätsdiebstahl (Pass-the-Hash)) 
<a name="identity-theft-using-pass-the-hash-attack"></a>

*Vorheriger Name*: Identitätsdiebstahl mithilfe eines Pass-the-Hash-Angriffs

**Beschreibung**

Pass-the-Hash ist eine Technik mit seitlicher Bewegung, bei der Angreifer den NTLM-Hash eines Benutzers von einem Computer stehlen und diesen verwenden, um Zugriff auf einen anderen Computer zu erlangen. 

**Untersuchung**

Stellen Sie fest, ob der verwendete Hash von einem Computer stammt, der dem Zielbenutzer gehört oder regelmäßig von diesem verwendet wird. Falls dies zutrifft, ist die Warnung falsch positiv, andernfalls ist sie wahrscheinlich richtig positiv.

**Wartung**

1. Wenn das beteiligte Konto nicht vertraulich ist, setzen Sie das Kennwort für dieses Konto zurück. Dies hindert den Angreifer daran, neue Kerberos-Tickets aus dem Kennworthash zu erstellen. Bestehende Tickets können jedoch weiterhin verwendet werden, bis sie ablaufen. 

2. Wenn es sich um ein vertrauliches Konto handelt, sollten Sie das KRBTGT-Konto zweimal zurücksetzen. Durch das zweimalige Zurücksetzen von KRBTGT werden alle Kerberos-Tickets in dieser Domäne ungültig. Daher sollten Sie diesen Schritt im Voraus planen. Siehe [KRBTGT Account Password Reset Scripts now available for customers (Skripts zum Zurücksetzen von Kennwörtern des KRBTGT-Kontos stehen Kunden jetzt zur Verfügung)](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/). Beachten Sie auch die Verwendung des  [Reset the KRBTGT account password/keys tool (Tool zum Zurücksetzen des Kennworts/Schlüssels eines KRBTGT-Kontos)](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Da es sich dabei um eine Technik mit seitlicher Bewegung handelt, führen Sie die bewährten Methoden der [Pass the hash recommendations (Empfehlungen zu Pass-the-Hash)](https://www.microsoft.com/download/details.aspx?id=36036) aus.

## <a name="suspected-identity-theft-pass-the-ticket"></a>Suspected identity theft (pass-the-ticket) (Verdacht auf Identitätsdiebstahl (Pass-the-Ticket)) 
<a name="identity-theft-using-pass-the-ticket-attack"></a>

*Vorheriger Name*: Identitätsdiebstahl mithilfe eines Pass-the-Ticket-Angriffs

**Beschreibung**

Pass-the-Ticket ist eine Technik mit seitlicher Bewegung, bei der die Angreifer ein Kerberos-Ticket von einem Computer stehlen und dieses verwenden, um Zugriff auf einen anderen Computer zu erlangen, indem sie das gestohlene Ticket wiederverwenden. In dieser Erkennung wird ein Kerberos-Ticket auf zwei (oder mehr) verschiedenen Computern verwendet.

**Untersuchung**

1. Klicken Sie auf die Schaltfläche **Details herunterladen**, um eine vollständige Liste der beteiligten IP-Adressen anzuzeigen. Gehört die IP-Adresse von einem oder beiden Computern zu einem Subnetz, das aus einem zu kleinen DHCP-Pool (z.B. VPN oder WiFi) zugewiesen wird? Ist die IP-Adresse freigegeben? Beispielsweise durch ein NAT-Gerät? Gibt es eine oder mehrere der Quell-IP-Adressen, die nicht vom Sensor aufgelöst werden? (Dies könnte darauf hinweisen, dass die richtigen Ports zwischen dem Sensor und den Geräten nicht ordnungsgemäß geöffnet sind.) Wenn die Antwort auf eine dieser Fragen „ja“ lautet, handelt es sich um ein falsch positives Ereignis.

2. Gibt es eine benutzerdefinierte Anwendung, die Tickets im Auftrag des Benutzers weiterleitet? Falls ja, handelt es sich um ein unbedenklich richtig positives Ereignis.

**Wartung**

1. Wenn das beteiligte Konto nicht vertraulich ist, setzen Sie das Kennwort für dieses Konto zurück. Dies hindert den Angreifer daran, neue Kerberos-Tickets aus dem Kennworthash zu erstellen. Bestehende Tickets können jedoch weiterhin verwendet werden, bis sie ablaufen.  

2. Wenn es sich um ein vertrauliches Konto handelt, sollten Sie das KRBTGT-Konto zweimal zurücksetzen. Durch das zweimalige Zurücksetzen von KRBTGT werden alle Kerberos-Tickets in dieser Domäne ungültig. Daher sollten Sie diesen Schritt im Voraus planen. Siehe [KRBTGT Account Password Reset Scripts now available for customers (Skripts zum Zurücksetzen von Kennwörtern des KRBTGT-Kontos stehen Kunden jetzt zur Verfügung)](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/). Beachten Sie auch die Verwendung des  [Reset the KRBTGT account password/keys tool (Tool zum Zurücksetzen des Kennworts/Schlüssels eines KRBTGT-Kontos)](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).  Da es sich dabei um eine Technik mit seitlicher Bewegung handelt, führen Sie die bewährten Methoden der [Pass the hash recommendations (Empfehlungen zu Pass-the-Hash)](https://www.microsoft.com/download/details.aspx?id=36036) aus.

## <a name="suspected-over-pass-the-hash-attack-encryption-downgrade"></a>Suspected over-pass-the-hash attack (encryption downgrade) (Verdacht auf Over-Pass-the-Hash-Angriff (Herabstufung der Verschlüsselung)) 
<a name="Encryption-downgrade-activity-potential-over-pass-the-hash"></a>

*Vorheriger Name*: Aktivität zur Herabstufung der Verschlüsselung

**Beschreibung**

Die Herabstufung der Verschlüsselung ist eine Methode, die dazu dient, Kerberos zu schwächen, indem für die Verschlüsselungsstufe von unterschiedlichen Feldern des Protokolls, die mit der höchsten Verschlüsselungsstufe verschlüsselt werden, ein Downgrade durchgeführt wird. Ein abgeschwächtes verschlüsseltes Feld ist ein leichteres Ziel für versuchte Brute-Force-Angriffe offline. Verschiedene Angriffsmethoden nutzen schwache Kerberos-Verschlüsselungsverfahren. In dieser Erkennung lernt Azure ATP die Kerberos-Verschlüsselungstypen, die von Computern und Benutzern verwendet werden, und benachrichtigt Sie, wenn ein schwächeres Verschlüsselungsverfahren verwendet wird, das (1) unüblich für den Quellcomputer und/oder den Benutzer ist und (2) mit bekannten Angriffstechniken übereinstimmt. 

Bei einem Overpass-the-Hash-Angriff kann ein Angreifer zusammen mit einer Kerberos-AS-Anforderung einen schwachen gestohlenen Hash zur Erstellung eines starken Tickets verwenden. In dieser Erkennung wurde der AS_REQ-Nachrichtenverschlüsselungstyp des Quellcomputers im Vergleich zum zuvor gelernten Verhalten heruntergestuft (der Computer hat also AES verwendet).

**Untersuchung**

1. Wurde die Smartcard-Konfiguration in letzter Zeit geändert? <br>Überprüfen Sie, ob solche Änderungen für die beteiligten Konten vorgenommen wurden. Falls ja, ist dies wahrscheinlich ein unbedenklich richtig positives Ereignis und kann unterdrückt werden.
2. Einige Ressourcen unterstützten starke Verschlüsselungsmethoden nicht. Diese Warnung kann von schwachen Verschlüsselungsmethoden ausgelöst werden.<br>Überprüfen Sie die Ressourcen, auf die mit diesen Tickets zugegriffen wurde. Verwenden Sie dafür das *msDS-SupportedEncryptionTypes*-Attribut des Ressourcendienstkontos in Azure Active Directory.<br>Wenn Sie feststellen, dass auf eine Ressource zugegriffen wurde, überprüfen Sie diese. Vergewissern Sie sich, dass es sich um eine gültige Ressource handelt, auf die zugegriffen werden darf. 
3. Klicken Sie auf den Quellcomputer oder das Konto, um die entsprechende Profilseite aufzurufen. Überprüfen Sie, was ungefähr zum Zeitpunkt der Replikation passiert ist. Suchen Sie nach ungewöhnlichen Aktivitäten, z.B.: Wer war angemeldet und auf welche Ressourcen wurde zugegriffen? <br> Wenn Sie die Windows Defender ATP-Integration aktiviert haben, klicken Sie auf das Windows Defender ATP-Badge, ![Windows Defender ATP-Badge](./media/wd-badge.png) um den Computer weiter zu untersuchen. In Windows Defender ATP können Sie sehen, welche Prozesse und Warnungen ungefähr gleichzeitig mit der Warnung aufgetreten sind.


**Wartung**
1. Wenn das Konto des gefährdeten Benutzers *nicht vertraulich* ist, setzen Sie das Kennwort für dieses Konto zurück. Dies hindert den Angreifer daran, neue Kerberos-Tickets aus dem Kennworthash zu erstellen. Bestehende Tickets können jedoch weiterhin verwendet werden, bis sie ablaufen. 
2. Wenn das Konto des gefährdeten Benutzers *vertraulich* ist, sollten Sie ggf. das KRBTGT-Konto zweimal zurücksetzen. Durch das zweimalige Zurücksetzen von KRBTGT werden alle Kerberos-Tickets in dieser Domäne ungültig. Daher sollten Sie diesen Schritt im Voraus planen. Weitere Informationen finden Sie im Leitfaden [KRBTGT Account Password Reset Scripts now available for customers (Skripts zum Zurücksetzen von Kennwörtern des KRBTGT-Kontos stehen Kunden jetzt zur Verfügung)](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/). Beachten Sie auch die Verwendung des [Reset the KRBTGT account password/keys tool (Tools zum Zurücksetzen des Kennworts/Schlüssels eines KRBTGT-Kontos)](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).

## <a name="suspected-skeleton-key-attack-encryption-downgrade"></a>Suspected Skeleton Key attack (encryption downgrade) (Verdacht auf Skeleton-Key-Angriff (Herabstufung der Verschlüsselung)) 
<a name="encryption-downgrade-activity-potential-skeleton-key-attack"></a>

*Vorheriger Name*: Aktivität zur Herabstufung der Verschlüsselung

**Beschreibung:** Die Herabstufung der Verschlüsselung ist eine Methode, die dazu dient, Kerberos zu schwächen, indem für die Verschlüsselungsstufe von unterschiedlichen Feldern des Protokolls, die mit der höchsten Verschlüsselungsstufe verschlüsselt werden, ein Downgrade durchgeführt wird. Ein abgeschwächtes verschlüsseltes Feld ist ein leichteres Ziel für versuchte Brute-Force-Angriffe offline. Verschiedene Angriffsmethoden nutzen schwache Kerberos-Verschlüsselungsverfahren. In dieser Erkennung lernt Azure ATP die Kerberos-Verschlüsselungstypen, die von Computern und Benutzern verwendet werden, und benachrichtigt Sie, wenn ein schwächeres Verschlüsselungsverfahren verwendet wird, das (1) unüblich für den Quellcomputer und/oder den Benutzer ist und (2) mit bekannten Angriffstechniken übereinstimmt. 

Skeleton Key ist eine Schadsoftware, die auf einem Domänencontroller ausgeführt wird und mit der eine Authentifizierung bei der Domäne mit jedem Konto ohne das passende Kennwort möglich ist. Diese Schadsoftware verwendet häufig schwächere Verschlüsselungsalgorithmen, um einen Hashwert für das Kennwort des Benutzers auf dem Domänencontroller zu erstellen. In dieser Erkennung wurde die Verschlüsselungsmethode der KRB_ERR-Nachricht vom Domänencontroller an das Konto, von dem aus ein Ticket erstellt wird, im Vergleich zum zuvor gelernten Verhalten heruntergestuft.

**Untersuchung**
1. Klicken Sie auf den Quellcomputer oder das Konto, um die entsprechende Profilseite aufzurufen. <br>Überprüfen Sie, was ungefähr zum Zeitpunkt der Replikation passiert ist. Suchen Sie nach ungewöhnlichen Aktivitäten wie: Wer war angemeldet und auf welche Ressourcen wurde zugegriffen. <br>Wenn Sie die Windows Defender ATP-Integration aktiviert haben, klicken Sie auf das Windows Defender ATP-Badge, ![Windows Defender ATP-Badge](./media/wd-badge.png) um den Computer weiter zu untersuchen. In Windows Defender ATP können Sie sehen, welche Prozesse und Warnungen ungefähr gleichzeitig mit der Warnung aufgetreten sind. 
2. Überprüfen Sie mithilfe des [vom Azure Advanced Threat Protection-Team entwickelten Scanners](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73), ob Ihre Domänencontroller von Skeleton Key betroffen sind.


**Wartung**
1. Entfernen Sie die Schadsoftware. Weitere Informationen zum Entfernen von Schadsoftware finden Sie in der [Skeleton Key Malware Analysis (Analyse der Skeleton Key-Schadsoftware)](https://www.virusbulletin.com/virusbulletin/2016/01/paper-digital-bian-lian-face-changing-skeleton-key-malware).


## <a name="network-mapping-reconnaissance-dns"></a>Network-mapping reconnaissance (DNS) (Reconnaissance über Netzwerkzuordnung (DNS))
<a name="reconnaissance-using-dns"></a>

Reconnaissance über DNS

**Beschreibung**

Ihr DNS-Server enthält eine Struktur aller Computer, IP-Adressen und Dienste in Ihrem Netzwerk. Diese Informationen werden von Angreifern verwendet, um Ihre Netzwerkstruktur auszukundschaften und um interessante Zielcomputer zu bestimmten, die sie in den nächsten Schritten des Angriffs benötigen.

Es gibt mehrere Abfragetypen im DNS-Protokoll. Azure ATP erkennt die AXFR-Anforderung (Transfer), die von Nicht-DNS-Servern stammt.

**Untersuchung**

1. Ist der Quellcomputer (**Stammt von...**) ein DNS-Server? Falls ja, ist dieses Ereignis wahrscheinlich falsch positiv. Klicken Sie zur Überprüfung auf die Warnung, um auf die Seite „Details“ zu gelangen. Überprüfen Sie in der Tabelle unter **Abfrage**, welche Domänen abgefragt wurden. Sind diese Domänen vorhanden? Falls ja, **schließen** Sie die verdächtige Aktivität (diese ist falsch positiv). Stellen Sie zusätzlich sicher, dass der UDP-Port 53 zwischen dem eigenständigen Azure ATP-Server und dem Quellcomputer geöffnet ist, um falsch positive Ereignisse zukünftig zu verhindern.

2. Wird auf dem Quellcomputer ein Sicherheitsscanner ausgeführt? Falls ja, **schließen Sie die Entitäten** in ATP aus, entweder direkt mit **Schließen und Ausschließen** oder über die Seite **Ausschluss** (unter **Konfiguration**, verfügbar für Azure ATP-Administratoren).

3. Falls die Antwort auf alle obigen Fragen „nein“ ist, setzen Sie die Untersuchung fort, und konzentrieren Sie sich dabei auf den Quellcomputer. Klicken Sie auf den Quellcomputer, um die entsprechende Profilseite aufzurufen. Überprüfen Sie, was ungefähr zum Zeitpunkt der Anforderung passiert ist. Suchen Sie nach ungewöhnlichen Aktivitäten wie z.B.: Wer war angemeldet, auf welche Ressourcen wurde zugegriffen. Wenn Sie die Windows Defender ATP-Integration aktiviert haben, klicken Sie auf das Windows Defender ATP-Badge, ![Windows Defender ATP-Badge](./media/wd-badge.png) um den Computer weiter zu untersuchen. In Windows Defender ATP können Sie sehen, welche Prozesse und Warnungen ungefähr gleichzeitig mit der Warnung aufgetreten sind. 

**Wartung**

Die Sicherung eines internen DNS-Servers, um zu verhindern, dass Reconnaissance mithilfe von DNS auftritt, kann von der Deaktivierung oder Einschränkung von Zonenübertragungen nur auf bestimmte IP-Adressen erreicht werden. Weitere Informationen zum Einschränken von Zonenübertragungen finden Sie unter [Restrict Zone Transfers (Einschränken von Zonenübertragungen)](https://technet.microsoft.com/library/ee649273(v=ws.10).aspx).
Das Bearbeiten von Zonenübertragungen ist eine Aufgabe innerhalb einer Prüfliste, die für das  [Sichern des DNS-Servers gegen interne und externe Angriffe](https://technet.microsoft.com/library/cc770432(v=ws.11).aspx) gelten sollte.

## <a name="remote-code-execution-attempt"></a>Versuchte Remote-Codeausführung
<a name="remote-code-execution-attempt"></a>
*Vorheriger Name*: Versuchte Remote-Codeausführung

**Beschreibung**

Angreifer, die Administratoranmeldeinformationen kompromittiert haben oder einen Zero-Day-Exploit verwenden, können Remotebefehle auf Ihrem Domänencontroller ausführen. Damit können sie Beständigkeit erhalten, Informationen sammeln, oder DOS-Attacken (Denial of Service) ausführen usw. Azure ATP erkennt PSexec-, Remote WMI- und PowerShell-Verbindungen.

**Untersuchung**

1. Dies tritt häufig bei administrativen Arbeitsstationen, IT-Teammitgliedern und Dienstkonten auf, die administrative Aufgaben auf den Domänencontrollern ausführen. Wenn dies der Fall ist und die Warnung aktualisiert wird, da die Aufgabe vom selben Administrator und/oder Computer ausgeführt wird, **unterdrücken** Sie die Warnung.

2. Ist der fragliche **Computer** berechtigt, diese Remoteausführung auf Ihrem Domänencontroller auszuführen?

 - Ist das fragliche **Konto** berechtigt, diese Remoteausführung auf Ihrem Domänencontroller auszuführen?

 - Wenn die Antwort auf beide Fragen *ja* ist, **schließen** Sie die Warnung.

3. Wenn Sie beide Fragen verneinen können, sollte dieses Ereignis als richtig positiv behandelt werden. Versuchen Sie, die Quelle des Versuchs zu ermitteln, indem Sie Computer- und Kontoprofile überprüfen. Klicken Sie auf den Quellcomputer oder das Konto, um die entsprechende Profilseite aufzurufen. Überprüfen Sie, was ungefähr zum Zeitpunkt dieser Versuche passiert ist. Suchen Sie nach ungewöhnlichen Aktivitäten wie z.B.: Wer war angemeldet, auf welche Ressourcen wurde zugegriffen. Wenn Sie die Windows Defender ATP-Integration aktiviert haben, klicken Sie auf das Windows Defender ATP-Badge, ![Windows Defender ATP-Badge](./media/wd-badge.png) um den Computer weiter zu untersuchen. In Windows Defender ATP können Sie sehen, welche Prozesse und Warnungen ungefähr gleichzeitig mit der Warnung aufgetreten sind. 

**Wartung**

1. Schränken Sie den Remotezugriff auf Domänencontroller von Computern ein, die nicht den Tier 0 aufweisen.

2. Implementieren Sie  [privilegierten Zugriff](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/securing-privileged-access) , damit nur abgesicherte Computer eine Verbindung für Administratoren mit dem Domänencontroller herstellen können.

> [!NOTE]
> Warnungen vor versuchter Remote-Codeausführung werden nur von ATP-Sensoren unterstützt. 

## <a name="suspicious-communication-over-dns"></a>Verdächtige Kommunikation über DNS
<a name="suspicious-communication-over-dns"></a>

*Vorheriger Name*: Verdächtige Kommunikation über DNS 

**Beschreibung**

In den meisten Organisationen wird das DNS-Protokoll nicht überwacht und nur selten wegen böswilliger Angriffe blockiert. Das gibt einem Angreifer auf einem kompromittierten Computer die Möglichkeit, das DNS-Protokoll zu missbrauchen. Schädliche Kommunikation über DNS kann für Datenexfiltration, Command-and-Control-Zugriff und/oder zur Umgehung von Einschränkungen des Unternehmensnetzwerks verwendet werden.

**Untersuchung**
> [!NOTE]
> *Verdächtige Kommunikation über DNS*: Diese Sicherheitswarnungen listen die vermutete Domäne auf. Neue Domänen, oder Domänen, die erst vor Kurzem hinzugefügt wurden, Azure ATP aber noch nicht bekannt sind und nicht erkannt werden, von denen aber feststeht, dass sie Teil Ihrer Organisation sind, können geschlossen werden. 


1.  In einigen legitimen Unternehmen wird DNS für die reguläre Kommunikation verwendet. Überprüfen Sie, ob die registrierte Abfragedomäne zu einer vertrauenswürdigen Quelle gehört, wie etwa Ihrem Virenschutzanbieter. Wenn die Domäne bekannt und vertrauenswürdig ist und DNS-Abfragen zulässig sind, kann die Warnung geschlossen werden und die Domäne für zukünftige Warnungen [ausgeschlossen](excluding-entities-from-detections.md) werden. 
2.   Wenn die registrierte Abfragedomäne nicht vertrauenswürdig ist, identifizieren Sie den Prozess, der die Anforderung erstellt hat, auf dem Quellcomputer. Verwenden Sie zur Unterstützung bei dieser Aufgabe den [Prozessmonitor](https://docs.microsoft.com/en-us/sysinternals/downloads/procmon).
3.  Bestimmen Sie, wann die verdächtige Aktivität begonnen hat. Wurden neue Programme (AV?) in der Organisation bereitgestellt oder installiert? Gibt es weitere Warnungen um die gleiche Uhrzeit?
4.  Klicken Sie auf den Quellcomputer, um auf dessen Profilseite zuzugreifen. Überprüfen Sie, was ungefähr zum Zeitpunkt der DNS-Abfrage passiert ist. Suchen Sie nach ungewöhnlichen Aktivitäten, z.B.: Wer war angemeldet, und welche Ressourcen wurden verwendet. Wenn Sie die Windows Defender ATP-Integration bereits aktiviert haben, klicken Sie auf das Windows Defender ATP-Badge, ![Windows Defender ATP-Badge](./media/wd-badge.png) um den Computer weiter zu untersuchen. Mithilfe von Windows Defender ATP können Sie sehen, welche Prozesse und Warnungen ungefähr gleichzeitig mit der Warnung aufgetreten sind.

**Wartung**

Wenn sich die registrierte Domäne nach Ihrer Untersuchung als nicht vertrauenswürdig erweist, empfehlen wir, die Zieldomäne zu blockieren, um zukünftig jede Kommunikation zu vermeiden. 

## <a name="suspicious-modification-of-sensitive-groups"></a>Verdächtige Modifizierung von sensiblen Gruppen
<a name="suspicious-midification-of-sensitive-groups"></a>

*Vorheriger Name*: Verdächtige Modifizierung von sensiblen Gruppen

**Beschreibung**

Angreifer fügen Benutzer zu sehr privilegierten Gruppen hinzu. Dadurch können Sie Zugriff auf weitere Ressourcen und Beständigkeit erhalten. Die Erkennung basiert auf dem Erfassen der Aktivitäten von Benutzern, die Gruppen ändern und den Warnungen, die bei nicht ordnungsgemäßen Ergänzungen zu einer sensiblen Gruppe angezeigt werden. Die Erfassung wird kontinuierlich von Azure ATP ausgeführt. Der Mindestzeitraum, bevor eine Warnung ausgelöst werden kann, beträgt einen Monat pro Domänencontroller.

Eine Definition von sensiblen Gruppen in Azure ATP finden Sie unter [Working with the sensitive accounts (Arbeiten mit sensiblen Konten)](sensitive-accounts.md).


Die Erkennung basiert auf [Ereignissen, die auf Domänencontrollern überwacht werden](configure-event-collection.md).
So stellen Sie sicher, dass Ihre Domänencontroller die benötigten Ereignisse überwachen.

**Untersuchung**

1. Ist das Ändern der Gruppe zulässig? </br>Zulässige Änderungen an Gruppen, die selten auftreten und nicht als „normal“ gelernt wurden, können eine Warnung auslösen. Dies würde als unbedenklich richtig positives Ereignis betrachtet werden.

2. Wenn es sich beim hinzugefügten Objekt um ein Benutzerkonto handelt, überprüfen Sie, welche Aktionen das Benutzerkonto durchgeführt hat, nachdem es zu der Administratorgruppe hinzugefügt wurde. Wechseln Sie für weiteren Kontext zu der Seite des Benutzers in Azure ATP. Gab es vor oder nach dem Hinzufügen andere verdächtige Aktivitäten im Zusammenhang mit dem Konto? Laden Sie den Bericht **Änderungen an sensiblen Gruppen** herunter, um festzustellen, welche Änderungen von wem im gleichen Zeitraum vorgenommen wurden.

**Wartung**

Halten Sie die Zahl der Benutzer, die zum Ändern von sensiblen Gruppen autorisiert sind, so gering wie möglich.

Richten Sie gegebenenfalls [Privileged Access Management for Active Directory (Privileged Access Management für Active Directory)](https://docs.microsoft.com/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services) ein.

## <a name="suspicious-service-creation"></a>Erstellen eines verdächtigen Diensts
<a name="suspicious-service-creation"></a>

*Vorheriger Name*: Erstellen eines verdächtigen Diensts

**Beschreibung**

Ein verdächtiger Dienst wurde von Ihrer Organisation auf einem Domänencontroller erstellt. Diese Warnung basiert auf Ereignis 7045, um die verdächtige Aktivität zu identifizieren. 

**Untersuchung**

1. Wenn es sich bei dem betroffenen Computer um eine Arbeitsstation oder einen Computer handelt, auf dem Mitglieder des IT-Teams und Dienstkonten administrative Aufgaben ausführen, kann das Resultat ein falsch positives Ergebnis sein, und Sie sollten die Warnung **unterdrücken** und sie wenn nötig der Ausschlussliste hinzufügen.

2. Erkennen Sie den Dienst auf dem Computer?

 - Darf das fragliche **Konto** diesen Dienst installieren?

 - Wenn die Antwort auf beide Fragen *ja* ist, **schließen** Sie die Warnung, oder fügen Sie sie der Ausschlussliste hinzu.

3. Wenn die Antwort auf beide Fragen *nein* ist, sollte dieses Ereignis als richtig positiv behandelt werden.

**Wartung**

- Implementieren Sie den Zugriff mit weniger privilegierten Rechten auf Domänencomputern, um nur bestimmten Benutzern die Erstellung neuer Dienste zu erlauben.


## <a name="suspicious-vpn-connection"></a>Verdächtige VPN-Verbindung
<a name="suspicious-vpn-detection"></a>

*Vorheriger Name*: Verdächtige VPN-Verbindung 

**Beschreibung**

Azure ATP speichert Informationen zum Entitätsverhalten für VPN-Verbindungen von Benutzern für einen gleitenden Zeitraum von einem Monat. 

Das Modell für das VPN-Verhalten basiert auf den folgenden Aktivitäten: die Computer, auf denen sich die Benutzer angemeldet haben und die Standorte, von denen diese eine Verbindung hergestellt haben. 

Es wird eine Warnung ausgelöst, wenn basierend auf den Machine-Learning-Algorithmen eine Abweichung des Verhaltens der Entität vorliegt.

**Untersuchung**

1.  Soll der fragliche Benutzer diese Vorgänge ausführen?
2.  Die folgenden Fälle gelten als falsch positive Ergebnisse: ein Benutzer, der seinen Standort gewechselt hat und ein Benutzer, der unterwegs ist und sich von einem neuen Gerät aus anmeldet.

**Wartung**

1.  Sie sollten das Kennwort dieses Benutzers zurückzusetzen. Dadurch wird vermieden, dass der Angreifer mit den alten Anmeldeinformationen neue VPN-Verbindungen herstellt.
2.  Sie sollten für diesen Benutzer die Option blockieren, über VPN eine Verbindung herzustellen.


## <a name="suspected-wannacry-ransomware-attack"></a>Suspected WannaCry ransomware attack (Verdacht auf einen WannaCry-Ransomangriff)
<a name="unusual-protocol-implementation"></a>

*Vorheriger Name*: Ungewöhnliche Protokollimplementierung (potenzieller WannaCry-Ransomwareangriff)

**Beschreibung**

Angreifer verwenden Tools, die verschiedene Protokolle auf nicht standardmäßige Arten implementieren. Während diese Art des Netzwerkdatenverkehrs von Windows ohne Warnungen akzeptiert wird, kann Azure ATP potenziell böswillige Absichten erkennen. Das Verhalten weist auf Techniken hin, die von erweiterter Ransomware, z.B. WannaCry, verwendet werden.

**Untersuchung**

Überprüfen Sie die ungewöhnliche Aktivität in der Sicherheitswarnung in der Aktivitätszeitachse. Klicken Sie auf die Sicherheitswarnung, um die zugehörige Seite mit Details zu öffnen, und überprüfen Sie die möglicherweise betroffenen Entitäten sowie die Liste der Beweise. 

Ist das Ereignis *richtig positiv*, *unbedenklich richtig positiv* oder *falsch positiv*? 

1. Überprüfen Sie, ob WannaCry auf dem Quellcomputer ausgeführt wird. 

2. Wenn dies der Fall ist, ist diese Warnung richtig positiv. Um den Umfang der Sicherheitsverletzung zu ermitteln, führen Sie folgende Aktionen aus:
      - Untersuchen Sie den Quellcomputer.
      - Untersuchen Sie den betroffenen Computer. 

2. Wenn auf dem Quellcomputer kein Angriffstool ausgeführt wird, implementieren Anwendungen zuweilen einen eigenen NTLM- oder SMB-Stapel. Überprüfen Sie, ob auf dem Quellcomputer eine Anwendung ausgeführt wird, die einen eigenen NTLM- oder SMB-Stapel implementiert.

      1. Wenn ein solcher Stapel auf dem Computer ausgeführt wird, dies aber nicht so sein sollte, korrigieren Sie die Anwendungskonfiguration. In diesem Fall handelt es sich um eine unbedenkliche Aktivität, und die Sicherheitswarnung kann geschlossen werden.

      2. Wenn auf dem Computer ein eigener Stapel ausgeführt wird und die Konfiguration richtig ist, kann die Sicherheitswarnung geschlossen und der Computer ausgeschlossen werden, da es sich wahrscheinlich um eine unbedenkliche Aktivität handelt.

3. Klicken Sie auf den Quellcomputer, um die entsprechende Profilseite aufzurufen. Überprüfen Sie, was ungefähr zum Zeitpunkt der Warnung passiert ist. Suchen Sie nach ungewöhnlichen Aktivitäten, beispielsweise danach, welche Benutzer angemeldet waren und auf welche Ressourcen zugegriffen wurde. 

4. Wenn Sie die Windows Defender ATP-Integration aktiviert haben, klicken Sie auf das Windows Defender ATP-Badge, ![WD ATP](./media/wd-badge.png) um den Computer weiter zu untersuchen. In Windows Defender ATP können Sie sehen, welche Prozesse und Warnungen ungefähr gleichzeitig mit der Warnung aufgetreten sind.


**Wartung**

1. Kontrollieren Sie den Quellcomputer. 
      - [Entfernen von WannaCry](https://support.microsoft.com/help/890830/remove-specific-prevalent-malware-with-windows-malicious-software-remo)
      - WanaKiwi kann für einige Ransomwares die Daten in deren Besitz entschlüsseln. Dies ist aber nur möglich, wenn der Benutzer den Computer nicht neu gestartet oder ausgeschaltet hat. Weitere Informationen finden Sie unter [Wanna Cry Ransomware (WannaCry-Ransomware)](https://answers.microsoft.com/en-us/windows/forum/windows_10-security/wanna-cry-ransomware/5afdb045-8f36-4f55-a992-53398d21ed07?auth=1)
      - Suchen Sie nach Benutzern, die zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie MFA. 
2. Patchen Sie alle Computer, und stellen Sie sicher, dass Sicherheitsupdates angewendet werden. 
      - [Deaktivieren von SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)

## <a name="suspected-use-of-metasploit-hacking-framework"></a>Suspected use of Metasploit hacking framework (Verdacht auf Verwendung eines Hackerframeworks)


*Vorheriger Name*: Ungewöhnliche Protokollimplementierung (potenzielle Verwendung schädlicher Hackertools wie Metasploit)

**Beschreibung**

Angreifer verwenden Tools, die verschiedene Protokolle (SMB, Kerberos, NTLM) auf nicht standardmäßige Arten implementieren. Während diese Art des Netzwerkdatenverkehrs von Windows ohne Warnungen akzeptiert wird, kann Azure ATP potenziell böswillige Absichten erkennen. Das Verhalten weist auf Techniken wie z.B. die Verwendung des Metasploit-Hackerframeworks hin. 

**Untersuchung**

Überprüfen Sie die ungewöhnliche Aktivität in der Sicherheitswarnung in der Aktivitätszeitachse. Klicken Sie auf die Sicherheitswarnung, um die zugehörige Seite mit Details zu öffnen, und überprüfen Sie die möglicherweise betroffenen Entitäten sowie die Liste der Beweise.

Ist das Ereignis *richtig positiv*, *unbedenklich richtig positiv* oder *falsch positiv*? 

1. Überprüfen Sie, ob auf dem Quellcomputer ein Angriffstool wie Metasploit oder Medusa ausgeführt wird. 

2. Wenn dies der Fall ist, handelt es sich um ein richtig positives Ereignis. Um den Umfang der Sicherheitsverletzung zu ermitteln, führen Sie folgende Aktionen aus:
      - Untersuchen Sie den Quellcomputer.
      - Untersuchen Sie den betroffenen Computer. 

3. Wenn auf dem Quellcomputer kein Angriffstool ausgeführt wird, implementieren Anwendungen zuweilen einen eigenen NTLM- oder SMB-Stapel. Überprüfen Sie, ob auf dem Quellcomputer eine Anwendung ausgeführt wird, die einen eigenen NTLM- oder SMB-Stapel implementiert.

4. Wenn auf dem Computer ein eigener NTLM- oder SMB-Stapel ausgeführt wird, dies aber nicht so sein sollte, korrigieren Sie die Anwendungskonfiguration.
      1. In diesem Fall handelt es sich um eine unbedenkliche Aktivität, und die Sicherheitswarnung kann geschlossen werden. 
      2. Wenn auf dem Computer ein eigener Stapel ausgeführt wird und die Konfiguration richtig ist, kann die Sicherheitswarnung geschlossen und der Computer ausgeschlossen werden, da es sich wahrscheinlich um eine unbedenkliche Aktivität handelt.

5. Klicken Sie auf den Quellcomputer, um die entsprechende Profilseite aufzurufen. Überprüfen Sie, was ungefähr zum Zeitpunkt der Warnung passiert ist. Suchen Sie nach ungewöhnlichen Aktivitäten, z. B.: Wer war angemeldet, auf welche Ressourcen wurde zugegriffen. Wenn Sie die Windows Defender ATP-Integration aktiviert haben, klicken Sie auf das Windows Defender ATP-Badge, ![WD ATP](./media/wd-badge.png) um den Computer weiter zu untersuchen. In Windows Defender ATP können Sie sehen, welche Prozesse und Warnungen ungefähr gleichzeitig mit der Warnung aufgetreten sind.


**Wartung**

1. Setzen Sie die Kennwörter der betroffenen Benutzer zurück, und aktivieren Sie die mehrstufige Authentifizierung.
2. Kontrollieren Sie den Quellcomputer.
   1. Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
   2. Suchen Sie nach Benutzern, die zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind.
   3. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie die mehrstufige Authentifizierung. 
4. Setzen Sie die Kennwörter des Benutzers des Quellcomputers zurück, und aktivieren Sie die mehrstufige Authentifizierung. 
5. [Deaktivieren von SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)


## <a name="suspected-overpass-the-hash-attack-kerberos"></a>Suspected overpass-the-hash attack (Kerberos) (Verdacht auf einen Overpass-the-Hash-Angriff (Kerberos))
<a name="unusual-protocol-implementation"></a>

*Vorheriger Name*: Ungewöhnliche Kerberos-Protokollimplementierung (potenzieller Overpass-the-Hash-Angriff) 

**Beschreibung**

Angreifer verwenden Tools, die verschiedene Protokolle wie Kerberos und SMB auf nicht standardmäßige Arten implementieren. Während diese Art des Netzwerkdatenverkehrs von Windows ohne Warnungen akzeptiert wird, kann Azure ATP potenziell böswillige Absichten erkennen. Das Verhalten ist maßgeblich für Techniken wie Overpass-the-Hash, Brute Force und Exploits, die von erweiterter Ransomware, z.B. WannaCry, verwendet werden.

**Untersuchung**

Überprüfen Sie die ungewöhnliche Aktivität in der Sicherheitswarnung in der Aktivitätszeitachse. Klicken Sie auf die Sicherheitswarnung, um die zugehörige Seite mit Details zu öffnen, und überprüfen Sie die möglicherweise betroffenen Entitäten sowie die Liste der Beweise.

Ist das Ereignis *richtig positiv*, *unbedenklich richtig positiv* oder *falsch positiv*? 

 1. Zuweilen implementieren Anwendungen einen eigenen Kerberos-Stapel, der nicht der Kerberos-RFC-Dokumentation entspricht.
   1. Überprüfen Sie, ob auf dem Quellcomputer ein eigener Kerberos-Stapel ausgeführt wird. 
   2. Wenn auf dem Computer ein eigener Kerberos-Stapel ausgeführt wird, dies aber nicht so sein sollte, korrigieren Sie die Anwendungskonfiguration. In diesem Fall handelt es sich um eine unbedenkliche Aktivität, und die Sicherheitswarnung kann geschlossen werden. 
   3. Wenn auf dem Computer ein eigener Kerberos-Stapel ausgeführt wird und die Konfiguration richtig ist, kann die Sicherheitswarnung geschlossen und der Computer ausgeschlossen werden, da es sich wahrscheinlich um eine unbedenkliche Aktivität handelt.

 **Wartung**

1. Setzen Sie die Kennwörter der betroffenen Benutzer zurück, und aktivieren Sie die mehrstufige Authentifizierung.
2. Kontrollieren Sie den Quellcomputer. 
   1. Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
   2. Suchen Sie nach Benutzern, die zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind. 
   3. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie die mehrstufige Authentifizierung. 
4. Setzen Sie die Kennwörter des Benutzers des Quellcomputers zurück, und aktivieren Sie die mehrstufige Authentifizierung. 

## <a name="suspected-brute-force-attack-smb"></a>Suspected Brute Force attack (SMB) (Verdacht auf einen Brute-Force-Angriff (SMB))
<a name="unusual-protocol-implementation-smb"></a>

*Vorheriger Name*: Ungewöhnliche Protokollimplementierung (potenzielle Verwendung schädlicher Tools wie Hydra)

**Beschreibung**

Angreifer verwenden Tools, die verschiedene Protokolle wie SMB, Kerberos und NTLM auf nicht standardmäßige Arten implementieren. Während diese Art des Netzwerkdatenverkehrs von Windows ohne Warnungen akzeptiert wird, kann Azure ATP potenziell böswillige Absichten erkennen. Das Verhalten weist auf Brute-Force-Techniken hin. 

**Untersuchung**

Überprüfen Sie die ungewöhnliche Aktivität in der Sicherheitswarnung in der Aktivitätszeitachse. Klicken Sie auf die Sicherheitswarnung, um die zugehörige Seite mit Details zu öffnen, und überprüfen Sie die möglicherweise betroffenen Entitäten sowie die Liste der Beweise.

Ist das Ereignis *richtig positiv*, *unbedenklich richtig positiv* oder *falsch positiv*? 

1. Überprüfen Sie, ob auf dem Quellcomputer ein Angriffstool wie Hydra ausgeführt wird. 
   1. Wenn dies der Fall ist, handelt es sich um ein richtig positives Ereignis. Um den Umfang der Sicherheitsverletzung zu ermitteln, führen Sie folgende Aktionen aus:
      - Untersuchen Sie den Quellcomputer.
      - Untersuchen Sie den betroffenen Computer. 

2. Wenn auf dem Quellcomputer kein Angriffstool ausgeführt wird, implementieren Anwendungen zuweilen einen eigenen NTLM- oder SMB-Stapel. Überprüfen Sie, ob auf dem Quellcomputer eine Anwendung ausgeführt wird, die einen eigenen NTLM- oder SMB-Stapel implementiert.

3. Klicken Sie auf den Quellcomputer, um die entsprechende Profilseite aufzurufen. Überprüfen Sie, was ungefähr zum Zeitpunkt der Warnung passiert ist. Suchen Sie nach ungewöhnlichen Aktivitäten, beispielsweise danach, welche Benutzer angemeldet waren und auf welche Ressourcen zugegriffen wurde. Wenn Sie die Windows Defender ATP-Integration aktiviert haben, klicken Sie auf das Windows Defender ATP-Badge, ![WD ATP](./media/wd-badge.png) um den Computer weiter zu untersuchen. In Windows Defender ATP können Sie sehen, welche Prozesse und Warnungen ungefähr gleichzeitig mit der Warnung aufgetreten sind.

**Wartung**

1. Setzen Sie die Kennwörter der angenommenen Benutzer zurück, und aktivieren Sie die mehrstufige Authentifizierung.
2. Fügen Sie die angenommenen Benutzer zu einer Watchlist hinzu.
3. Kontrollieren Sie den Quellcomputer.
   1. Suchen Sie das Tool, das den Angriff ausgeführt hat, und entfernen Sie es.
   2. Suchen Sie nach Benutzern, die zum Zeitpunkt der Aktivität angemeldet waren, da diese möglicherweise auch betroffen sind.
   3. Setzen Sie ihre Kennwörter zurück, und aktivieren Sie die mehrstufige Authentifizierung. 
4. Erzwingen Sie komplexe und lange Kennwörter in der Organisation. Komplexe und lange Kennwörter stellen die notwendige erste Sicherheitsstufe zum Schutz vor zukünftigen Brute-Force-Angriffen dar.
5. [Deaktivieren von SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)


## <a name="user-and-ip-address-reconnaissance-smb"></a>User and IP address reconnaissance (SMB) (Reconnaissance über Benutzer und IP-Adressen (SMB))
<a name="reconnaissance-using-smb-session-enumeration"></a> Reconnaissance mithilfe der SMB-Sitzungsenumeration


**Beschreibung**

Mit der SMB-Enumeration (Server Message Block) können Angreifer Informationen dazu erhalten, welche Benutzer sich zuletzt angemeldet haben. Sobald Angreifer diese Informationen besitzen, können sie sich seitlich im Netzwerk bewegen, um zu einem bestimmten sensiblen Konto zu gelangen.

In dieser Erkennung wird eine Warnung ausgelöst, wenn eine SMB-Sitzungsenumeration auf einem Domänencontroller ausgeführt wird, denn dies sollte nicht der Fall sein.

**Untersuchung**

1. Klicken Sie auf die Warnung, um auf die Seite „Details“ zu gelangen. Überprüfen Sie, welche Konten den Vorgang ausgeführt haben und gegebenenfalls, welche Konten verfügbar gemacht wurden.

 - Wird auf dem Quellcomputer eine Art Sicherheitsscanner ausgeführt? Falls ja, können Sie die verdächtige Aktivität **schließen und ausschließen**.

2. Überprüfen Sie, welche beteiligten Benutzer den Vorgang ausgeführt haben. Melden sich diese normalerweise auf dem Quellcomputer an, oder handelt es sich bei diesen um Administratoren, die solche Aktionen ausführen sollen?  

3. Falls dies zutrifft und die Warnung aktualisiert wird, **unterdrücken** Sie die verdächtige Aktivität.  

4. Falls dies zutrifft, aber nicht weiterhin so gehandhabt werden soll, **schließen** Sie die verdächtige Aktivität.

5. Wenn die Antwort auf alle obigen Fragen „nein“ ist, gehen Sie von einem böswilligen Ereignis aus.

**Wartung**

Verwenden Sie das [Net Cease-Tool](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b), um den Schutz Ihrer Umgebung gegen diese Attacken zu erhöhen.



> [!NOTE]
> Wenn Sie eine Sicherheitswarnung deaktivieren möchten, wenden Sie sich an den Support.


## <a name="see-also"></a>Weitere Informationen
- [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
