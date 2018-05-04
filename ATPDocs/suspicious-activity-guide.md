---
title: Azure ATP-Handbuch zu verdächtigen Aktivitäten | Microsoft-Dokumentation
d|Description: This article provides a list of the suspicious activities Azure ATP can detect and steps for remediation.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/15/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ca5d1c7b-11a9-4df3-84a5-f53feaf6e561
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6246849cf7e8566b27c969b73e9c96cb0e7b7978
ms.sourcegitcommit: e0209c6db649a1ced8303bb1692596b9a19db60d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
*Gilt für: Azure Advanced Threat Protection*


# <a name="azure-advanced-threat-protection-suspicious-activity-guide"></a>Azure Advanced Threat Protection-Handbuch zu verdächtigen Aktivitäten

Wenn eine ordnungsgemäße Untersuchung befolgt wird, kann jede verdächtige Aktivität folgendermaßen klassifiziert werden:

-   **Richtig positiv**: Eine böswillige, von Azure ATP erkannte Aktion.

-   **Unbedenklich richtig positiv**: Eine von Azure ATP erkannte Aktion, die tatsächlich durchgeführt wurde, aber nicht böswillig ist, wie z.B. ein Penetrationstest.

-   **Falsch positiv**: Ein falscher Alarm, das heißt, die Aktivität wurde nicht ausgeführt.

Weitere Informationen zum Arbeiten mit Azure ATP-Warnungen finden Sie unter [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md).


## <a name="abnormal-sensitive-group-modification"></a>Ungewöhnliche Modifizierung von sensiblen Gruppen


**Beschreibung**

Angreifer fügen Benutzer zu sehr privilegierten Gruppen hinzu. Dadurch können Sie Zugriff auf weitere Ressourcen und Beständigkeit erhalten. Die Erkennung basiert auf dem Erfassen der Aktivitäten von Benutzern, die Gruppen ändern und den Warnungen, die bei nicht ordnungsgemäßen Ergänzungen zu einer sensiblen Gruppe angezeigt werden. Die Erfassung wird kontinuierlich von ATP ausgeführt. Der Mindestzeitraum, bevor eine Warnung ausgelöst werden kann, beträgt einen Monat pro Domänencontroller.

Eine Definition von sensiblen Gruppen in Azure ATP finden Sie unter [Working with the sensitive accounts (Arbeiten mit sensiblen Konten)](sensitive-accounts.md).


Die Erkennung basiert auf [Ereignissen, die auf Domänencontrollern überwacht werden](configure-event-collection.md).
So stellen Sie sicher, dass Ihre Domänencontroller die benötigten Ereignisse überwachen.

**Untersuchung**

1. Ist das Ändern der Gruppe zulässig? </br>Zulässige Änderungen an Gruppen, die selten auftreten und nicht als „normal“ gelernt wurden, können eine Warnung auslösen. Dies würde als unbedenklich richtig positives Ereignis betrachtet werden.

2. Wenn es sich beim hinzugefügten Objekt um ein Benutzerkonto handelt, überprüfen Sie, welche Aktionen das Benutzerkonto durchgeführt hat, nachdem es zu der Administratorgruppe hinzugefügt wurde. Wechseln Sie für weiteren Kontext zu der Seite des Benutzers in Azure ATP. Gab es vor oder nach dem Hinzufügen andere verdächtige Aktivitäten im Zusammenhang mit dem Konto? Laden Sie den Bericht **Änderungen an sensiblen Gruppen** herunter, um festzustellen, welche Änderungen von wem im gleichen Zeitraum vorgenommen wurden.

**Wartung**

Halten Sie die Zahl der Benutzer, die zum Ändern von sensiblen Gruppen autorisiert sind, so gering wie möglich.

Richten Sie gegebenenfalls [Privileged Access Management for Active Directory (Privileged Access Management für Active Directory)](https://docs.microsoft.com/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services) ein.


## <a name="brute-force-attack-using-ldap-simple-bind"></a>Brute-Force-Angriff mithilfe einer einfachen LDAP-Bindung

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

## <a name="encryption-downgrade-activity"></a>Aktivität zur Herabstufung der Verschlüsselung

**Beschreibung**

Die Herabstufung der Verschlüsselung ist eine Methode, die dazu dient, Kerberos zu schwächen, indem für die Verschlüsselungsstufe von unterschiedlichen Feldern des Protokolls, die normalerweise mit der höchsten Verschlüsselungsstufe verschlüsselt werden, ein Downgrade durchgeführt wird. Ein abgeschwächtes verschlüsseltes Feld ist ein leichteres Ziel für versuchte Brute-Force-Angriffe offline. Verschiedene Angriffsmethoden nutzen schwache Kerberos-Verschlüsselungsverfahren. In dieser Erkennung lernt Azure ATP die Kerberos-Verschlüsselungsverfahren, die von Computern und Benutzern verwendet werden und benachrichtigt Sie, wenn ein schwächeres Verschlüsselungsverfahren verwendet wird, das: (1) unüblich für den Quellcomputer und/oder den Benutzer ist und (2) mit bekannten Angriffstechniken übereinstimmt.

Es gibt drei Arten von Erkennung:

1.  Skeleton Key ist eine Schadsoftware, die auf einem Domänencontroller ausgeführt wird und mit der eine Authentifizierung bei der Domäne mit jedem Konto möglich ist, ohne das jeweilige Kennwort zu wissen. Diese Schadsoftware verwendet häufig schwächere Verschlüsselungsalgorithmen, um einen Hashwert für das Kennwort des Benutzers auf dem Domänencontroller zu erstellen. In dieser Erkennung wurde die Verschlüsselungsmethode der KRB_ERR-Nachricht vom Domänencontroller an das Konto, von dem aus ein Ticket erstellt wird, im Vergleich zum zuvor gelernten Verhalten heruntergestuft.

2.  Golden Ticket: Bei einer [Golden Ticket](#golden-ticket)-Warnung wurde die Verschlüsselungsmethode des TGT-Felds der TGS_REQ-Nachricht (Dienstanforderung) vom Quellcomputer im Vergleich zum zuvor gelernten Verhalten heruntergestuft. Dies basiert nicht auf einer Zeitanomalie (wie bei der anderen Golden Ticket-Erkennung). Zusätzlich gab es keine Kerberos-Authentifizierungsanforderung, die der vorherigen von ATP erkannten Dienstanforderung zugeordnet ist.

3.  Overpass-the-Hash: Ein Angreifer kann einen schwachen gestohlenen Hash zur Erstellung eines starken Tickets verwenden, zusammen mit einer Anfrage für die Kerberos-Authentifizierung. In dieser Erkennung wurde der AS_REQ-Nachrichtenverschlüsselungstyp des Quellcomputers im Vergleich zum zuvor gelernten Verhalten heruntergestuft (der Computer hat also AES verwendet).

**Untersuchung**

Überprüfen Sie zunächst die Beschreibung der Warnung, um festzustellen, welche der drei oben aufgeführten Arten von Erkennung vorliegt. Laden Sie für weitere Informationen das Excel-Arbeitsblatt herunter.

1.  Skeleton Key: Sie können überprüfen, ob Ihre Domänencontroller von Skeleton Key betroffen sind, indem Sie [den vom Azure ATP-Team entwickelten Scanner](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73) verwenden. Wenn der Scanner Schadsoftware auf einem oder mehreren Ihrer Domänencontroller findet, ist dies ein richtig positives Ereignis.

2.  Golden Ticket: Wechseln Sie im Excel-Arbeitsblatt zur Registerkarte mit der Netzwerkaktivität. Sie werden feststellen, dass das entsprechende heruntergestufte Feld **Request Ticket Encryption Type** ist und dass **Source Computer Supported Encryption Types** stärkere Verschlüsselungsmethoden enthält.

  1. Überprüfen Sie den Quellcomputer und das Konto. Überprüfen Sie im Fall von mehreren Quellcomputern und Konten, ob sie etwas gemeinsam haben (alle Marketingmitarbeiter verwenden z.B. eine bestimmte App, die die Warnung möglicherweise auslöst). Es gibt Fälle, in denen eine benutzerdefinierte Anwendung, die selten genutzt wird, mit einem niedrigeren Verschlüsselungsverfahren authentifiziert wird. Überprüfen Sie, ob solche Apps auf dem Quellcomputer vorhanden sind. Falls ja, ist dies wahrscheinlich ein unbedenklich richtig positives Ereignis und kann unterdrückt werden.
  
  2. Überprüfen Sie die Ressource, auf die von diesen Tickets zugegriffen wird. Wenn auf eine Ressource von allen zugegriffen wird, stellen Sie sicher, dass es sich um eine gültige Ressource handelt, auf die zugegriffen werden soll. Überprüfen Sie zudem, ob die Zielressource starke Verschlüsselungsmethoden unterstützt. Sie können dies in Active Directory überprüfen, indem Sie das Attribut „msDS-SupportedEncryptionTypes“ des Ressourcendienstkontos überprüfen.

3.  Overpass-the-Hash: Wechseln Sie im Excel-Arbeitsblatt zur Registerkarte mit der Netzwerkaktivität. Sie werden feststellen, dass das entsprechende heruntergestufte Feld **Encrypted Timestamp Encryption Type** ist und dass **Source Computer Supported Encryption Types** stärkere Verschlüsselungsmethoden enthält.

  1. Es gibt Fälle, in denen diese Warnung ausgelöst werden kann, wenn sich Benutzer mit Smartcards anmelden und die Smartcardkonfiguration kürzlich geändert wurde. Überprüfen Sie, ob solche Änderungen für die beteiligten Konten vorgenommen wurden. Falls ja, ist dies wahrscheinlich ein unbedenklich richtig positives Ereignis und kann unterdrückt werden.
  2. Überprüfen Sie die Ressource, auf die von diesen Tickets zugegriffen wird. Wenn auf eine Ressource von allen zugegriffen wird, stellen Sie sicher, dass es sich um eine gültige Ressource handelt, auf die zugegriffen werden soll. Überprüfen Sie zudem, ob die Zielressource starke Verschlüsselungsmethoden unterstützt. Sie können dies in Active Directory überprüfen, indem Sie das Attribut „msDS-SupportedEncryptionTypes“ des Ressourcendienstkontos überprüfen.

**Wartung**

1.  Skeleton Key – Entfernen der Schadsoftware Weitere Informationen finden Sie in der [Skeleton Key Malware Analysis (Analyse der Skeleton Key-Schadsoftware)](https://www.secureworks.com/research/skeleton-key-malware-analysis) von SecureWorks.

2.  Golden Ticket: Befolgen Sie die Anweisungen zu verdächtigen Aktivitäten unter [Golden Ticket](#golden-ticket).   
    Implementieren Sie ebenfalls die [Pass the hash recommendations (Empfehlungen zu Pass-the-Hash)](http://aka.ms/PtH), da für das Erstellen eines Golden Tickets Domänenadministratorrechte erforderlich sind.

3.  Overpass-the-Hash: Wenn das beteiligte Konto nicht vertraulich ist, setzen Sie das Kennwort für dieses Konto zurück. Dies hindert den Angreifer daran, neue Kerberos-Tickets aus dem Kennworthash zu erstellen. Bestehende Tickets können jedoch weiterhin verwendet werden, bis sie ablaufen. Wenn es sich um ein vertrauliches Konto handelt, sollten Sie das KRBTGT-Konto wie bei verdächtigen Aktivitäten mit Golden Tickets zweimal zurücksetzen. Durch das zweimalige Zurücksetzen von KRBTGT werden alle Kerberos-Tickets in dieser Domäne ungültig. Daher sollten Sie diesen Schritt im Voraus planen. Weitere Informationen finden Sie im Leitfaden [KRBTGT Account Password Reset Scripts now available for customers (Skripts zum Zurücksetzen von Kennwörtern des KRBTGT-Kontos stehen Kunden jetzt zur Verfügung)](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/). Beachten Sie auch die Verwendung des [Reset the KRBTGT account password/keys tool (Tools zum Zurücksetzen des Kennworts/Schlüssels eines KRBTGT-Kontos)](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Da es sich dabei um eine Technik mit seitlicher Bewegung handelt, führen Sie die bewährten Methoden der [Pass the hash recommendations (Empfehlungen zu Pass-the-Hash)](http://aka.ms/PtH) aus.

## Golden Ticket<a name="golden-ticket"></a>

**Beschreibung**

Angreifer mit Domänenadministratorrechten können das [KRBTGT account (KRBTGT-Konto)](https://technet.microsoft.com/library/dn745899(v=ws.11).aspx#Sec_KRBTGT) beeinträchtigen. Indem diese das KRBTGT-Konto verwenden, können sie ein Kerberos Ticket Granting Ticket (TGT) erstellen, das die Autorisierung für jede Ressource erteilen und den Ablaufzeitpunkt des Tickets auf einen beliebigen Zeitpunkt festlegen kann. Dieses gefälschte TGT wird als „Golden Ticket“ bezeichnet und ermöglicht es Angreifern, Beständigkeit im Netzwerk zu erreichen.

In dieser Erkennung wird eine Warnung ausgelöst, wenn ein Kerberos Ticket Granting Ticket länger als die erlaubte Dauer verwendet wird. Diese ist in der Sicherheitsrichtlinie [Max. Gültigkeitsdauer des Benutzertickets](https://technet.microsoft.com/library/jj852169(v=ws.11).aspx) angegeben.

**Untersuchung**

1. Wurden kürzlich (innerhalb der letzten Stunden) Änderungen an der Einstellung **Maximale Lebensdauer für Benutzertickets** in der Gruppenrichtlinie vorgenommen? Falls ja, **schließen** Sie die Warnung (diese war falsch positiv).

2. Ist der eigenständige Azure ATP-Sensor in diese Warnung an einen virtuellen Computer involviert? Falls ja, wurde dieser kürzlich aus einem gespeicherten Zustand fortgesetzt? Falls ja, **schließen** Sie diese Warnung.

3. Wenn die Antwort auf die obigen Fragen „nein“ ist, gehen Sie von einem böswilligen Ereignis aus.

**Wartung**

Ändern Sie das Kennwort für das Kerberos Ticket Granting Ticket (KRBTGT) zweimal gemäß den Anweisungen unter [KRBTGT Account Password Reset Scripts now available for customers (Skripts zum Zurücksetzen von Kennwörtern des KRBTGT-Kontos stehen Kunden jetzt zur Verfügung)](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) mithilfe des [Reset the KRBTGT account password/keys tool (Tools zum Zurücksetzen des Kennworts/Schlüssels eines KRBTGT-Kontos)](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Durch das zweimalige Zurücksetzen von KRBTGT werden alle Kerberos-Tickets in dieser Domäne ungültig. Daher sollten Sie diesen Schritt im Voraus planen. Implementieren Sie ebenfalls die [Pass the hash recommendations (Empfehlungen zu Pass-the-Hash)](http://aka.ms/PtH), da für das Erstellen eines Golden Tickets Domänenadministratorrechte erforderlich sind.

## <a name="honeytoken-activity"></a>Honeytoken-Aktivität


**Beschreibung**

Honeytoken-Konten sind Köderkonten, die eingerichtet werden, um schädliche Aktivitäten, die versuchen, diese Konten zu verwenden, zu erkennen und zu verfolgen. Honeytoken-Konten sollten nicht verwendet werden, aber einen attraktiven Namen besitzen, um Angreifer anzulocken (z.B. SQL-Admin). Jede von diesen ausgehende Aktivität kann auf böswilliges Verhalten hinweisen.

Weitere Informationen zu Honeytoken-Konten finden Sie unter [Installieren von Azure ATP – Schritt 7](install-atp-step7.md).

**Untersuchung**

1.  Überprüfen Sie, ob der Besitzer des Quellcomputers das Honeytoken-Konto für die Authentifizierung verwendet hat. Verwenden Sie dazu die auf der Seite „Verdächtige Aktivitäten“ beschriebene Methode (z.B. Kerberos, LDAP, NTLM).

2.  Navigieren Sie zu den Profilseiten des Quellcomputers, und überprüfen Sie, welche anderen Konten darüber authentifiziert wurden. Wenden Sie sich an die Besitzer dieser Konten, um festzustellen, ob Sie das Honeytoken-Konto verwendet haben.

3.  Dabei könnte es sich um eine nicht interaktive Anmeldung handeln. Überprüfen Sie deshalb Anwendungen oder Skripts, die auf dem Quellcomputer ausgeführt werden.

Wenn nach dem Ausführen von Schritt 1 bis 3 keine Beweise dafür vorliegen, dass es sich um eine harmlose Verwendung handelt, gehen Sie von einem böswilligen Ereignis aus.

**Wartung**

Stellen Sie sicher, dass Honeytoken-Konten nur für den beabsichtigten Zweck verwendet werden, andernfalls könnten sie viele Warnungen generieren.

## <a name="identity-theft-using-pass-the-hash-attack"></a>Identitätsdiebstahl mithilfe eines Pass-the-Hash-Angriffs

**Beschreibung**

Pass-the-Hash ist eine Technik mit seitlicher Bewegung, bei der Angreifer den NTLM-Hash eines Benutzers von einem Computer stehlen und diesen verwenden, um Zugriff auf einen anderen Computer zu erlangen. 

**Untersuchung**

Stammt der verwendete Hash von einem Computer, der dem Zielbenutzer gehört oder regelmäßig von diesem verwendet wird? Falls ja, handelt es sich dabei um ein falsch positives Ereignis. Wenn nicht, handelt es sich dabei wahrscheinlich um ein richtig positives Ereignis.

**Wartung**

1. Wenn das beteiligte Konto nicht vertraulich ist, setzen Sie das Kennwort für dieses Konto zurück. Dies hindert den Angreifer daran, neue Kerberos-Tickets aus dem Kennworthash zu erstellen. Bestehende Tickets können jedoch weiterhin verwendet werden, bis sie ablaufen. 

2. Wenn es sich um ein vertrauliches Konto handelt, sollten Sie das KRBTGT-Konto wie bei verdächtigen Aktivitäten mit Golden Tickets zweimal zurücksetzen. Durch das zweimalige Zurücksetzen von KRBTGT werden alle Kerberos-Tickets in dieser Domäne ungültig. Daher sollten Sie diesen Schritt im Voraus planen. Siehe [KRBTGT Account Password Reset Scripts now available for customers (Skripts zum Zurücksetzen von Kennwörtern des KRBTGT-Kontos stehen Kunden jetzt zur Verfügung)](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/). Beachten Sie auch die Verwendung des [Reset the KRBTGT account password/keys tool (Tools zum Zurücksetzen des Kennworts/Schlüssels eines KRBTGT-Kontos)](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Da es sich dabei um eine Technik mit seitlicher Bewegung handelt, führen Sie die bewährten Methoden der [Pass the hash recommendations (Empfehlungen zu Pass-the-Hash)](http://aka.ms/PtH) aus.

## <a name="identity-theft-using-pass-the-ticket-attack"></a>Identitätsdiebstahl mithilfe eines Pass-the-Ticket-Angriffs

**Beschreibung**

Pass-the-Ticket ist eine Technik mit seitlicher Bewegung, bei der die Angreifer ein Kerberos-Ticket von einem Computer stehlen und dieses verwenden, um Zugriff auf einen anderen Computer zu erlangen, indem sie das gestohlene Ticket wiederverwenden. In dieser Erkennung wird ein Kerberos-Ticket auf zwei (oder mehr) verschiedenen Computern verwendet.

**Untersuchung**

1. Klicken Sie auf die Schaltfläche **Details herunterladen**, um eine vollständige Liste der beteiligten IP-Adressen anzuzeigen. Gehört die IP-Adresse von einem oder beiden Computern zu einem Subnetz, das aus einem zu kleinen DHCP-Pool (z.B. VPN oder WiFi) zugewiesen wird? Ist die IP-Adresse freigegeben? Beispielsweise durch ein NAT-Gerät? Gibt es eine oder mehrere der Quell-IP-Adressen, die nicht vom Sensor aufgelöst werden? (Dies könnte darauf hinweisen, dass die richtigen Ports zwischen dem Sensor und den Geräten nicht ordnungsgemäß geöffnet sind.) Wenn die Antwort auf eine dieser Fragen „ja“ lautet, handelt es sich um ein falsch positives Ereignis.

2. Gibt es eine benutzerdefinierte Anwendung, die Tickets im Auftrag des Benutzers weiterleitet? Falls ja, handelt es sich um ein unbedenklich richtig positives Ereignis.

**Wartung**

1. Wenn das beteiligte Konto nicht vertraulich ist, setzen Sie das Kennwort für dieses Konto zurück. Dies hindert den Angreifer daran, neue Kerberos-Tickets aus dem Kennworthash zu erstellen. Bestehende Tickets können jedoch weiterhin verwendet werden, bis sie ablaufen.  

2. Wenn es sich um ein vertrauliches Konto handelt, sollten Sie das KRBTGT-Konto wie bei verdächtigen Aktivitäten mit Golden Tickets zweimal zurücksetzen. Durch das zweimalige Zurücksetzen von KRBTGT werden alle Kerberos-Tickets in dieser Domäne ungültig. Daher sollten Sie diesen Schritt im Voraus planen. Siehe [KRBTGT Account Password Reset Scripts now available for customers (Skripts zum Zurücksetzen von Kennwörtern des KRBTGT-Kontos stehen Kunden jetzt zur Verfügung)](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/). Beachten Sie auch die Verwendung des [Reset the KRBTGT account password/keys tool (Tools zum Zurücksetzen des Kennworts/Schlüssels eines KRBTGT-Kontos)](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).  Da es sich dabei um eine Technik mit seitlicher Bewegung handelt, führen Sie die bewährten Methoden der [Pass the hash recommendations (Empfehlungen zu Pass-the-Hash)](http://aka.ms/PtH) aus.

## <a name="malicious-data-protection-private-information-request"></a>Böswillige Anforderung privater Informationen im Rahmen der Datensicherheit

**Beschreibung**

Die Datenschutz-API (DPAPI) wird von Windows verwendet, um von Browsern gespeicherte Kennwörter, verschlüsselte Dateien und andere sensible Daten sicher zu schützen. Domänencontroller enthalten einen Hauptschlüssel zur Sicherung, der verwendet werden kann, um alle mit der DPAPI verschlüsselten Geheimnisse auf mit einer Domäne verbundenen Windows-Computern zu entschlüsseln. Angreifer können diesen Hauptschlüssel verwenden, um sämtliche von DPAPI geschützten Geheimnisse auf allen mit einer Domäne verbundenen Computern zu entschlüsseln.
In dieser Erkennung wird eine Warnung ausgelöst, wenn die DPAPI zum Abrufen des Sicherungshauptschlüssels verwendet wird.

**Untersuchung**

1. Wird auf dem Quellcomputer ein von der Organisation genehmigter Sicherheitsscanner für Active Directory ausgeführt?

2. Falls dies zutrifft und von Ihnen so gewünscht ist, können Sie die verdächtige Aktivität **schließen und ausschließen**.

3. Falls dies zutrifft und von Ihnen nicht so gewünscht ist, **schließen** Sie die verdächtige Aktivität.

**Wartung**

Ein Angreifer benötigt Domänenadministratorrechte zum Verwenden der DPAPI. Implementieren Sie [Pass the hash recommendations (Empfehlungen zu Pass-the-Hash)](http://aka.ms/PtH).

## <a name="malicious-replication-requests"></a>Böswillige Replikationsanforderungen


**Beschreibung**

Bei der Replikation mit Active Directory werden Änderungen eines Domänencontrollers mit allen anderen Domänencontrollern synchronisiert. Mit den erforderlichen Berechtigungen können Angreifer eine Replikationsanforderung initiieren, die ihnen das Abrufen der in Active Directory gespeicherten Daten ermöglicht, einschließlich der Kennworthashes.

In dieser Erkennung wird eine Warnung ausgelöst, wenn eine Replikationsanforderung von einem Computer initiiert wird, der kein Domänencontroller ist.

**Untersuchung**

1.  Ist der fragliche Computer ein Domänencontroller? Beispielsweise ein neu hochgestufter Domänencontroller mit Replikationsproblemen. Falls ja, **schließen** Sie die verdächtige Aktivität. 
2.  Soll der fragliche Computer Daten von Active Directory replizieren? Beispielsweise Azure AD Connect. Falls ja, können Sie die verdächtige Aktivität **schließen und ausschließen**.
3.  Klicken Sie auf den Quellcomputer oder das Konto, um die entsprechende Profilseite aufzurufen. Überprüfen Sie, was ungefähr zum Zeitpunkt der Replikation passiert ist. Suchen Sie nach ungewöhnlichen Aktivitäten wie z.B.: Wer war angemeldet, auf welche Ressourcen wurde zugegriffen. Wenn Sie die Windows Defender ATP-Integration aktiviert haben, klicken Sie auf das Windows Defender ATP-Badge, ![Windows Defender ATP-Badge](./media/wd-badge.png) um den Computer weiter zu untersuchen. In Windows Defender ATP können Sie sehen, welche Prozesse und Warnungen ungefähr gleichzeitig mit der Warnung aufgetreten sind. 


**Wartung**

Überprüfen Sie die folgenden Berechtigungen: 

- Replizieren von Verzeichnisänderungen   

- Replizieren von allen Verzeichnisänderungen  

Weitere Informationen finden Sie unter [Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013 (Erteilen von AD DS-Berechtigungen für die Profilsynchronisierung in SharePoint Server 2013)](https://technet.microsoft.com/library/hh296982.aspx).
Nutzen Sie [AD ACL Scanner](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/), oder erstellen Sie ein Windows PowerShell-Skript, um festzustellen, wer in der Domäne über diese Berechtigungen verfügt.


## <a name="password-exposed-in-cleartext-report"></a>Kennwort ist in Klartextbericht offengelegt

**Beschreibung**

Einige Dienste senden Anmeldeinformationen im Nur-Text-Format. Dies kann sogar bei Benutzerkonten geschehen. Angreifer, die Ihren Netzwerkdatenverkehr überwachen, können diese Anmeldeinformationen abfangen und diese zu böswilligen Zwecken verwenden. 

**Untersuchung**

Klicken Sie auf die Berichtseite, und laden Sie den Bericht mit dem im Klartext offengelegten Kennwort herunter. Entnehmen Sie der Excel-Tabelle, welche Konten offengelegt sind.
Üblicherweise gibt es ein Skript oder eine ältere Anwendung auf den Quellcomputern, die die einfache LDAP-Bindung verwenden.

**Wartung**

Überprüfen Sie die Konfiguration des Quellcomputers, um sicherzustellen, dass Sie keine einfache LDAP-Bindung verwenden. Statt einfachen LDAP-Bindungen können Sie LDAP SALS oder LDAPS verwenden.

## <a name="privilege-escalation-using-forged-authorization-data"></a>Berechtigungsausweitung mithilfe von gefälschten Autorisierungsdaten

**Beschreibung**

Durch bekannte Sicherheitslücken in älteren Versionen von Windows Server können Angreifer das Privileged Attribute Certificate (PAC) manipulieren. Dabei handelt es sich um ein Feld im Kerberos-Ticket, das die Autorisierungsdaten eines Benutzer enthält (in Active Directory ist dies die Gruppenmitgliedschaft) und Angreifern zusätzliche Berechtigungen erteilt.

**Untersuchung**

1. Klicken Sie auf die Warnung, um auf die Seite „Details“ zu gelangen.

2. Ist der Zielcomputer (in der Spalte **ACCESSED**) mit MS14-068 (Domänencontroller) oder MS11-013 (Server) gepatcht? Falls ja, **schließen** Sie die verdächtige Aktivität (diese ist falsch positiv).

3. Wenn nicht, wird auf dem Quellcomputer ausgeführt (in der Spalte **FROM**) ein Betriebssystem bzw. eine Anwendung ausgeführt, die dafür bekannt sind, das PAC zu ändern? Falls ja, **unterdrücken** Sie die verdächtige Aktivität (diese ist unbedenklich richtig positiv).

4. Wenn die Antwort auf die obigen zwei Fragen „nein“ ist, gehen Sie von einem böswilligen Ereignis aus.

**Wartung**

Stellen Sie sicher, dass alle Domänencontroller mit Betriebssystemen bis Windows Server 2012 R2 mit [KB3011780](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privilege) installiert sind, und dass alle Memberserver und Domänencontroller bis 2012 R2 das aktuellste KB2496930 haben. Weitere Informationen finden Sie unter [Silver PAC](https://technet.microsoft.com/library/security/ms11-013.aspx) und [Gefälschte PAC-Datei](https://technet.microsoft.com/library/security/ms14-068.aspx).

## <a name="reconnaissance-using-account-enumeration"></a>Reconnaissance mithilfe von Kontoenumeration

**Beschreibung**

Bei einer Reconnaissance zur Kontoenumeration verwendet ein Angreifer ein Wörterbuch mit tausenden von Benutzernamen oder Tools wie KrbGuess, um Benutzernamen in Ihrer Domäne zu erraten. Der Angreifer führt Kerberos-Anforderungen mit diesen Namen durch, um so auf einen gültigen Benutzernamen zu stoßen. Wenn dadurch ein Benutzername bestimmt wird, erhält der Angreifer die Kerberos-Fehlermeldung **Preauthentication required** (Vorauthentifizierung erforderlich) statt der Meldung **Security principal unknown** (Unbekannter Sicherheitsprinzipal). 

Bei dieser Erkennung kann Azure ATP erkennen, von wo der Angriff durchgeführt wurde, wie viele Versuche vorgenommen wurden und bei wie vielen dieser Versuche Übereinstimmungen gefunden wurden. Wenn es zu viele unbekannte Benutzer gibt, erkennt Azure ATP dies als verdächtige Aktivität. 

**Untersuchung**

1. Klicken Sie auf die Warnung, um auf die Seite „Details“ zu gelangen. 

2. Ist es zulässig, dass dieser Hostcomputer den Domänencontroller nach der Existenz von Konten abfragt (z.B. Exchange-Server)? <br></br>
Wird auf dem Host ein Skript oder eine Anwendung ausgeführt, die dieses Verhalten verursachen könnten? <br></br>
Wenn Sie eine dieser Fragen mit „ja“ beantworten können, **schließen Sie die verdächtige Aktivität** (dabei handelt es sich um ein harmloses richtig positives Ergebnis), und schließen Sie den Host aus der verdächtigen Aktivität aus.

3. Laden Sie die Warnungsdetails in einer Excel-Tabelle herunter, um sich eine nach vorhandenen und nicht vorhandenen Konten aufgeteilte Liste anzusehen. Wenn Sie sich das Arbeitsblatt mit den nicht vorhandenen Konten ansehen, und Ihnen diese Konten bekannt vorkommen, handelt es sich dabei möglicherweise um deaktivierte Konten oder Angestellte, die nicht mehr in Ihrem Unternehmen arbeiten. In diesem Fall ist es unwahrscheinlich, dass es sich um einen Angriff mit einem Wörterbuch mit Benutzernamen handelt. Wahrscheinlich ging das Verhalten von einer Anwendung oder einem Skript aus, die überprüfen, welche Konten in Active Directory noch vorhanden sind. Dies bedeutet, dass es sich um ein harmloses richtig positives Ergebnis handelt.

3. Wenn Ihnen die Namen zum größten Teil unbekannt sind, fragen Sie sich Folgendes: Stimmt einer der geratenen Benutzernamen mit einem tatsächlichen Kontonamen in Active Directory überein? Wenn es keine Übereinstimmungen gibt, war der Versuch nicht erfolgreich. Dennoch sollten Sie diese Warnung im Blick behalten, falls Sie im Laufe der Zeit aktualisiert wird.

4. Wenn einer der Rateversuche mit einem vorhandenen Kontonamen übereinstimmt, kennt der Angreifer vorhandene Konten in Ihrer Umgebung und kann mit Brute-Force-Angriffen und gefundenen Benutzernamen versuchen, Zugriff auf Ihre Domäne zu erhalten. Überprüfen Sie die erratenen Kontonamen auf weitere verdächtige Aktivitäten. Überprüfen Sie, ob es sich bei den Konten um sensible Konten handelt.


**Wartung**

[Komplexe bzw. lange Kennwörter](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) stellen die erste Sicherheitsstufe zum Schutz gegen Brute-Force-Angriffe dar.


## <a name="reconnaissance-using-directory-services-queries"></a>Reconnaissance mithilfe von Verzeichnisdienstabfragen

**Beschreibung**

Die Reconnaissance von Verzeichnisdiensten wird von Angreifern verwendet, um die Verzeichnisstruktur und die Zielkonten mit hohen Berechtigungen für die weiteren Schritte eines Angriffs auszukundschaften. Das Protokoll Security Account Manager Remote (SAM-R) ist eine Methode, die zum Abfragen des Verzeichnisses verwendet wird, um eine solche Zuordnung vorzunehmen.

In dieser Erkennung werden im ersten Monat nach der Bereitstellung von Azure ATP keine Warnungen ausgelöst. Während der Lernphase erfasst Azure ATP, welche SAM-R-Abfragen (Enumerationsabfragen und einzelne Abfragen von sensiblen Konten) von welchen Computern gestellt werden.

**Untersuchung**

1. Klicken Sie auf die Warnung, um auf die Seite „Details“ zu gelangen. Überprüfen Sie, welche Abfragen gestellt wurden (z.B. Unternehmensadministratoren oder Administratoren) und ob diese erfolgreich waren oder nicht.

2. Sollen solche Abfragen vom fraglichen Zielcomputer aus gestellt werden?

3. Falls dies zutrifft und die Warnung aktualisiert wird, **unterdrücken** Sie die verdächtige Aktivität.

4. Falls dies zutrifft, aber nicht weiterhin so gehandhabt werden soll, **schließen** Sie die verdächtige Aktivität.

5. Wenn Informationen über das beteiligte Konto vorhanden sind: Sollen solche Abfragen von diesem Konto gestellt werden, oder wird dieses Konto normalerweise auf dem Quellcomputer angemeldet?

 - Falls dies zutrifft und die Warnung aktualisiert wird, **unterdrücken** Sie die verdächtige Aktivität.

 - Falls dies zutrifft, aber nicht weiterhin so gehandhabt werden soll, **schließen** Sie die verdächtige Aktivität.

 - Wenn die Antwort auf alle obigen Fragen „nein“ ist, gehen Sie von einem böswilligen Ereignis aus.

6. Wenn es keine Informationen über das involvierte Konto gibt, können Sie zum Endpunkt navigieren und überprüfen, welches Konto zur Zeit der Warnung angemeldet war.

**Wartung**

Nutzen Sie folgendes Verfahren, um den Schutz Ihrer Umgebung gegen diese Technik zu erhöhen:
1. Wird ein Tool zur Überprüfung des Sicherheitsrisikos auf Ihrem Computer ausgeführt?  
2. Überprüfen Sie, ob die im Angriff abgefragten Benutzer und Gruppen über hohe Berechtigungen verfügen oder anderweitig wichtig sind (d.h. CEO, CFO, IT-Abteilung usw.).  Falls dies der Fall ist, überprüfen Sie auch andere Aktivitäten auf diesem Endpunkt, und überwachen Sie Computer, auf denen die abgefragten Konten angemeldet sind, da diese für Lateral Movement-Methoden verwendet werden können.

## <a name="reconnaissance-using-dns"></a>Reconnaissance über DNS

**Beschreibung**

Ihr DNS-Server enthält eine Struktur aller Computer, IP-Adressen und Dienste in Ihrem Netzwerk. Diese Informationen werden von Angreifern verwendet, um Ihre Netzwerkstruktur auszukundschaften und um interessante Zielcomputer zu bestimmten, die sie in den nächsten Schritten des Angriffs benötigen.

Es gibt mehrere Abfragetypen im DNS-Protokoll. Azure ATP erkennt die AXFR-Anforderung (Transfer), die von Nicht-DNS-Servern stammt.

**Untersuchung**

1. Ist der Quellcomputer (**Stammt von...**) ein DNS-Server? Falls ja, ist dieses Ereignis wahrscheinlich falsch positiv. Klicken Sie zur Überprüfung auf die Warnung, um auf die Seite „Details“ zu gelangen. Überprüfen Sie in der Tabelle unter **Abfrage**, welche Domänen abgefragt wurden. Sind diese Domänen vorhanden? Falls ja, **schließen** Sie die verdächtige Aktivität (diese ist falsch positiv). Stellen Sie zusätzlich sicher, dass der UDP-Port 53 zwischen dem eigenständigen Azure ATP-Server und dem Quellcomputer geöffnet ist, um falsch positive Ereignisse zukünftig zu verhindern.

2. Wird auf dem Quellcomputer ein Sicherheitsscanner ausgeführt? Falls ja, **schließen Sie die Entitäten** in ATP aus, entweder direkt mit **Schließen und Ausschließen** oder über die Seite **Ausschluss** (unter **Konfiguration**, verfügbar für Azure ATP-Administratoren).

3. Falls die Antwort auf alle obigen Fragen „nein“ ist, setzen Sie die Untersuchung fort, und konzentrieren Sie sich dabei auf den Quellcomputer. Klicken Sie auf den Quellcomputer, um die entsprechende Profilseite aufzurufen. Überprüfen Sie, was ungefähr zum Zeitpunkt der Anforderung passiert ist. Suchen Sie nach ungewöhnlichen Aktivitäten wie z.B.: Wer war angemeldet, auf welche Ressourcen wurde zugegriffen. Wenn Sie die Windows Defender ATP-Integration aktiviert haben, klicken Sie auf das Windows Defender ATP-Badge, ![Windows Defender ATP-Badge](./media/wd-badge.png) um den Computer weiter zu untersuchen. In Windows Defender ATP können Sie sehen, welche Prozesse und Warnungen ungefähr gleichzeitig mit der Warnung aufgetreten sind. 

**Wartung**

Die Sicherung eines internen DNS-Servers, um zu verhindern, dass Reconnaissance mithilfe von DNS auftritt, kann von der Deaktivierung oder Einschränkung von Zonenübertragungen nur auf bestimmte IP-Adressen erreicht werden. Weitere Informationen zum Einschränken von Zonenübertragungen finden Sie unter [Restrict Zone Transfers (Einschränken von Zonenübertragungen)](https://technet.microsoft.com/library/ee649273(v=ws.10).aspx).
Das Bearbeiten von Zonenübertragungen ist eine Aufgabe innerhalb einer Prüfliste, die für das [Sichern des DNS-Servers gegen interne und externe Angriffe](https://technet.microsoft.com/library/cc770432(v=ws.11).aspx) gelten sollte.

## <a name="reconnaissance-using-smb-session-enumeration"></a>Reconnaissance mithilfe der SMB-Sitzungsenumeration


**Beschreibung**

Mit der SMB-Enumeration (Server Message Block) können Angreifer Informationen dazu erhalten, welche Benutzer sich zuletzt angemeldet haben. Sobald Angreifer diese Informationen besitzen, können sie sich seitlich im Netzwerk bewegen, um zu einem bestimmten sensiblen Konto zu gelangen.

In dieser Erkennung wird eine Warnung ausgelöst, wenn eine SMB-Sitzungsenumeration auf einem Domänencontroller ausgeführt wird, denn dies sollte nicht der Fall sein.

**Untersuchung**

1. Klicken Sie auf die Warnung, um auf die Seite „Details“ zu gelangen. Überprüfen Sie, welche Konten den Vorgang ausgeführt haben und gegebenenfalls, welche Konten verfügbar gemacht wurden.

 - Wird auf dem Quellcomputer eine Art Sicherheitsscanner ausgeführt? Falls ja, können Sie die verdächtige Aktivität **schließen und ausschließen**.

2. Überprüfen Sie, welche beteiligten Benutzer die Vorgänge ausgeführt haben. Melden sich diese normalerweise auf dem Quellcomputer an, oder handelt es sich bei diesen um Administratoren, die solche Aktionen ausführen sollen?  

3. Falls dies zutrifft und die Warnung aktualisiert wird, **unterdrücken** Sie die verdächtige Aktivität.  

4. Falls dies zutrifft, aber nicht weiterhin so gehandhabt werden soll, **schließen** Sie die verdächtige Aktivität.

5. Wenn die Antwort auf alle obigen Fragen „nein“ ist, gehen Sie von einem böswilligen Ereignis aus.

**Wartung**

Verwenden Sie das [Net Cease-Tool](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b), um den Schutz Ihrer Umgebung gegen diese Attacken zu erhöhen.

## <a name="remote-execution-attempt"></a>Remoteausführungsversuch

**Beschreibung**

Angreifer, die Administratoranmeldeinformationen kompromittiert haben oder einen Zero-Day-Exploit verwenden, können Remotebefehle auf Ihrem Domänencontroller ausführen. Damit können sie Beständigkeit erhalten, Informationen sammeln, oder DOS-Attacken (Denial of Service) ausführen usw. Azure ATP erkennt PSexec-Verbindungen und WMI-Remoteverbindungen.

**Untersuchung**

1. Dies tritt häufig bei administrativen Arbeitsstationen, IT-Teammitgliedern und Dienstkonten auf, die administrative Aufgaben auf den Domänencontrollern ausführen. Wenn dies der Fall ist und die Warnung aktualisiert wird, da die Aufgabe vom selben Administrator und/oder Computer ausgeführt wird, **unterdrücken** Sie die Warnung.

2. Ist der fragliche **Computer** berechtigt, diese Remoteausführung auf Ihrem Domänencontroller auszuführen?

 - Ist das fragliche **Konto** berechtigt, diese Remoteausführung auf Ihrem Domänencontroller auszuführen?

 - Wenn die Antwort auf beide Fragen *ja* ist, **schließen** Sie die Warnung.

3. Wenn die Antwort auf beide Fragen „nein“ ist, sollte dieses Ereignis als richtig positiv behandelt werden. Versuchen Sie die Quelle des Versuchs zu ermitteln, indem Sie Computer- und Kontoprofile überprüfen. Klicken Sie auf den Quellcomputer oder das Konto, um die entsprechende Profilseite aufzurufen. Überprüfen Sie, was ungefähr zum Zeitpunkt dieser Versuche passiert ist. Suchen Sie nach ungewöhnlichen Aktivitäten wie z.B.: Wer war angemeldet, auf welche Ressourcen wurde zugegriffen. Wenn Sie die Windows Defender ATP-Integration aktiviert haben, klicken Sie auf das Windows Defender ATP-Badge, ![Windows Defender ATP-Badge](./media/wd-badge.png) um den Computer weiter zu untersuchen. In Windows Defender ATP können Sie sehen, welche Prozesse und Warnungen ungefähr gleichzeitig mit der Warnung aufgetreten sind. 

**Wartung**

1. Schränken Sie den Remotezugriff auf Domänencontroller von Computern ein, die nicht den Tier 0 aufweisen.

2. Implementieren Sie [privilegierten Zugriff](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/securing-privileged-access), damit nur abgesicherte Computer eine Verbindung für Administratoren mit dem Domänencontroller herstellen können.

## <a name="suspicious-authentication-failures"></a>Verdächtige Authentifizierungsfehler

**Beschreibung**

Bei einem Brute-Force-Angriff versucht ein Angreifer, sich mit vielen verschiedenen Kennwörtern für verschiedene Konten anzumelden, bis ein korrektes Kennwort für mindestens ein Konto gefunden wird. Sobald eines gefunden wurde, kann sich der Angreifer mit diesem Konto anmelden.

In dieser Erkennung wird eine Warnung ausgelöst, wenn viele Authentifizierungsfehler mit Kerberos oder der integrierten Windows-Authentifizierung auftreten. Dies kann entweder horizontal mit einem kleinen Satz von Kennwörtern für viele Benutzer oder vertikal mit einem großen Satz von Kennwörtern für wenige Benutzer geschehen. Auch eine beliebige Kombination dieser beiden Optionen ist möglich. Der Mindestzeitraum, bevor eine Warnung ausgelöst werden kann, beträgt eine Woche.

**Untersuchung**

1.  Klicken Sie auf **Details herunterladen**, um die vollständigen Informationen in einem Excel-Arbeitsblatt anzuzeigen. Sie können die folgenden Informationen abrufen: 
   -    Liste der angegriffenen Konten
   -    Liste der erratenen Konten, bei denen Anmeldeversuche mit einer erfolgreichen Authentifizierung endeten
   -    Wenn die Authentifizierungsversuche über NTLM ausgeführt wurden, sehen Sie die relevanten Ereignisaktivitäten 
   -    Wenn die Authentifizierungsversuche über Kerberos ausgeführt wurden, sehen Sie die relevanten Netzwerkaktivitäten

2.  Klicken Sie auf den Quellcomputer, um die entsprechende Profilseite aufzurufen. Überprüfen Sie, was ungefähr zum Zeitpunkt dieser Versuche passiert ist. Suchen Sie nach ungewöhnlichen Aktivitäten wie z.B.: Wer war angemeldet, auf welche Ressourcen wurde zugegriffen. Wenn Sie die Windows Defender ATP-Integration aktiviert haben, klicken Sie auf das Windows Defender ATP-Badge, ![Windows Defender ATP-Badge](./media/wd-badge.png) um den Computer weiter zu untersuchen. In Windows Defender ATP können Sie sehen, welche Prozesse und Warnungen ungefähr gleichzeitig mit der Warnung aufgetreten sind. 

3.  Wenn die Authentifizierung mithilfe von NTLM durchgeführt wurde und Sie sehen, dass die Warnung mehrfach aufgetreten ist, aber keine ausreichenden Informationen zum Server verfügbar sind, auf den der Quellcomputer zugreifen wollte, sollten Sie **NTLM-Überwachung** auf den betroffenen Domänencontrollern aktivieren. Aktivieren Sie dazu Ereignis 8004. Dies ist das NTLM-Authentifizierungsereignis, das Informationen zum Quellcomputer, Benutzerkonto und **Server** enthält, auf die der Quellcomputer zugreifen wollte. Wenn Sie wissen, welcher Server die Authentifizierungsüberprüfung gesendet hat, sollten Sie den Server untersuchen, indem Sie seine Ereignisse, wie z.B. 4624, überprüfen, um den Authentifizierungsprozess besser zu verstehen. 

**Wartung**

[Komplexe bzw. lange Kennwörter](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) stellen die erste Sicherheitsstufe zum Schutz gegen Brute-Force-Angriffe dar.

## <a name="suspicious-service-creation"></a>Erstellen eines verdächtigen Diensts

**Beschreibung**

Ein verdächtiger Dienst wurde von Ihrer Organisation auf einem Domänencontroller erstellt. Diese Warnung basiert auf Ereignis 7045, um die verdächtige Aktivität auf Ihren Endpunkten zu identifizieren. 

**Untersuchung**

1. Wenn es sich bei dem betroffenen Computer um eine Arbeitsstation oder einen Computer handelt, auf dem Mitglieder des IT-Teams und Dienstkonten administrative Aufgaben ausführen, kann das Resultat ein falsch positives Ergebnis sein, und Sie sollten die Warnung **unterdrücken** und sie wenn nötig der Ausschlussliste hinzufügen.

2. Erkennen Sie den Dienst auf dem Computer?

 - Darf das fragliche **Konto** diesen Dienst installieren?

 - Wenn die Antwort auf beide Fragen *ja* ist, **schließen** Sie die Warnung, oder fügen Sie sie der Ausschlussliste hinzu.

3. Wenn die Antwort auf beide Fragen *nein* ist, sollte dieses Ereignis als richtig positiv behandelt werden.

**Wartung**

- Implementieren Sie den Zugriff mit weniger privilegierten Rechten auf Domänencomputern, um nur bestimmten Benutzern die Erstellung neuer Dienste zu erlauben.

## <a name="unusual-protocol-implementation"></a>Ungewöhnliche Protokollimplementierung


**Beschreibung**

Angreifer verwenden Tools, die verschiedene Protokolle (SMB, Kerberos, NTLM) auf nicht standardmäßige Arten implementieren. Während diese Art des Netzwerkdatenverkehrs von Windows ohne Warnungen akzeptiert wird, kann Azure ATP potenziell böswillige Absichten erkennen. Das Verhalten ist maßgeblich für Techniken wie Overpass-the-Hash, Brute Force und Exploits, die von erweiterter Ransomware, z.B. WannaCry, verwendet werden.

**Untersuchung**

Identifizieren Sie das ungewöhnliche Protokoll, und klicken Sie auf der Zeitachse der verdächtigen Aktivitäten auf die verdächtige Aktivität, um zu der Seite „Details“ zu gelangen. Das Protokoll wird über dem Pfeil angezeigt: Kerberos oder NTLM.

- **Kerberos**: Dies wird häufig ausgelöst, wenn ein Hacking-Tool wie Mimikatz verwendet wurde, das möglicherweise einen Overpass-the-Hash-Angriff ausführt. Überprüfen Sie, ob auf dem Quellcomputer eine Anwendung ausgeführt wird, die im Widerspruch zur Kerberos-RFC ihren eigenen Kerberos-Stapel implementiert. Wenn dies der Fall ist, ist das Ereignis unbedenklich richtig positiv, und Sie können die Warnung **schließen**. Wenn die Warnung weiterhin ausgelöst wird und dies immer noch der Fall ist, können Sie die Warnung **unterdrücken**.

- **NTLM**: Es könnte sich um WannaCry oder Tools wie Metasploit, Medusa und Hydra handeln.  

Um festzustellen, ob es sich dabei um einen WannaCry-Angriff handelt, führen Sie folgende Schritte aus:

1. Überprüfen Sie, ob auf dem Quellcomputer ein Angriffstool wie Metasploit, Medusa oder Hydra ausgeführt wird.

2. Wenn keine Angriffstools gefunden werden, überprüfen Sie, ob auf dem Quellcomputer eine Anwendung ausgeführt wird, die ihren eigenen NTLM- oder SMB-Stapel implementiert.

3. Wenn nicht, überprüfen Sie, ob dies von WannaCry verursacht wird, indem Sie ein WannaCry-Scannerskript (z.B. [diesen Scanner](https://github.com/apkjet/TrustlookWannaCryToolkit/tree/master/scanner)) auf dem Quellcomputer ausführen, der an der verdächtigen Aktivität beteiligt ist. Wenn der Scanner feststellt, dass der Computer infiziert oder anfällig ist, patchen Sie den Computer, entfernen Sie die Schadsoftware, und blockieren Sie diese vom Netzwerk.

4. Wenn das Skript feststellt, dass der Computer nicht infiziert oder anfällig ist, könnte er trotzdem infiziert sein, denn SMBv1 könnte deaktiviert, oder der Computer könnte gepatcht worden sein. Beides beeinflusst das Überprüfungstool.

**Wartung**

Patchen Sie all Ihre Computer, und führen Sie insbesondere Sicherheitsupdates durch.

1. [Deaktivieren von SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)

2. [Entfernen von WannaCry](https://support.microsoft.com/help/890830/remove-specific-prevalent-malware-with-windows-malicious-software-remo)

3. WanaKiwi kann für einige Ransomwares die Daten in deren Besitz entschlüsseln. Dies ist aber nur möglich, wenn der Benutzer den Computer nicht ausgeschaltet oder neu gestartet hat. Weitere Informationen finden Sie unter [Wanna Cry Ransomware (WannaCry-Ransomware)](https://answers.microsoft.com/en-us/windows/forum/windows_10-security/wanna-cry-ransomware/5afdb045-8f36-4f55-a992-53398d21ed07?auth=1)


> [!NOTE]
> Wenden Sie sich an den Support, um eine verdächtige Aktivität zu deaktivieren.


## <a name="see-also"></a>Weitere Informationen
- [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)
