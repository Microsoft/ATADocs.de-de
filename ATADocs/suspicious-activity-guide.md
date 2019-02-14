---
title: ATA-Handbuch zu verdächtigen Aktivitäten | Microsoft-Dokumentation
d|Description: This article provides a list of the suspicious activities ATA can detect and steps for remediation.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 10/14/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 1fe5fd6f-1b79-4a25-8051-2f94ff6c71c1
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: ae708a434b7d7110289581523aaef2a8e78c1926
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2019
ms.locfileid: "56077982"
---
# <a name="advanced-threat-analytics-suspicious-activity-guide"></a>Advanced Threat Analytics-Handbuch zu verdächtigen Aktivitäten


*Gilt für: Advanced Threat Analytics Version 1.9*

Wenn eine ordnungsgemäße Untersuchung befolgt wird, kann jede verdächtige Aktivität folgendermaßen klassifiziert werden:

-   **Richtig positiv**: Eine von ATA erkannte schädliche Aktion.

-   **Unbedenklich richtig positiv**: Eine von ATA erkannte Aktion, die tatsächlich durchgeführt wurde, aber nicht schädlich ist, z. B. ein Penetrationstest.

-   **Falsch positiv**: Ein falscher Alarm, das heißt, die Aktivität wurde nicht ausgeführt.

Weitere Informationen zum Arbeiten mit ATA-Warnungen finden Sie unter [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md).

Bei Fragen oder Feedback wenden Sie sich unter [ATAEval@microsoft.com](mailto:ATAEval@microsoft.com) an das ATA-Team.

## <a name="abnormal-modification-of-sensitive-groups"></a>Ungewöhnliche Modifizierung von sensiblen Gruppen


**Beschreibung**

Angreifer fügen Benutzer zu sehr privilegierten Gruppen hinzu. Dadurch können sie Zugriff auf weitere Ressourcen und Beständigkeit erhalten. Erkennungen basieren auf dem Erfassen der Aktivitäten von Benutzergruppen, die Aktivitäten ändern, und den Warnungen, die bei nicht ordnungsgemäßen Ergänzungen zu einer sensiblen Gruppe angezeigt werden. Die Erfassung wird kontinuierlich von ATA ausgeführt. Der Mindestzeitraum, bevor eine Warnung ausgelöst werden kann, beträgt einen Monat pro Domänencontroller.

Eine Definition von sensiblen Gruppen in ATA finden Sie unter [Arbeiten mit der ATA-Konsole](working-with-ata-console.md#sensitive-groups).


Die Erkennung basiert auf [Ereignissen, die auf Domänencontrollern überwacht werden](https://docs.microsoft.com/advanced-threat-analytics/configure-event-collection).
Um sicherzustellen, dass Ihre Domänencontroller die erforderlichen Ereignisse überwachen, verwenden Sie das Tool, auf das unter [ATA Auditing (AuditPol, Advanced Audit Settings Enforcement, Lightweight Gateway Service discovery)](https://aka.ms/ataauditingblog) (ATA-Überwachung (AuditPol, Erzwingen erweiterter Überwachungseinstellungen, Ermittlung des Lightweight-Gatewaydiensts)) verwiesen wird.

**Untersuchung**

1. Ist das Ändern der Gruppe zulässig? </br>Zulässige Änderungen an Gruppen, die selten auftreten und nicht als „normal“ gelernt wurden, können eine Warnung auslösen. Dies würde als unbedenklich richtig positives Ereignis betrachtet werden.

2. Wenn es sich beim hinzugefügten Objekt um ein Benutzerkonto handelt, überprüfen Sie, welche Aktionen das Benutzerkonto durchgeführt hat, nachdem es zu der Administratorgruppe hinzugefügt wurde. Wechseln Sie für weiteren Kontext zu der Seite des Benutzers in ATA. Gab es vor oder nach dem Hinzufügen andere verdächtige Aktivitäten im Zusammenhang mit dem Konto? Laden Sie den Bericht **Änderungen an sensiblen Gruppen** herunter, um festzustellen, welche Änderungen von wem im gleichen Zeitraum vorgenommen wurden.

**Wartung**

Halten Sie die Zahl der Benutzer, die zum Ändern von sensiblen Gruppen autorisiert sind, so gering wie möglich.

Richten Sie gegebenenfalls [Privileged Access Management for Active Directory (Privileged Access Management für Active Directory)](https://docs.microsoft.com/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services) ein.

## <a name="broken-trust-between-computers-and-domain"></a>Fehlerhafte Vertrauensstellung zwischen Computern und Domäne

> [!NOTE]
> Die Warnung „Fehlerhafte Vertrauensstellung zwischen Computern und Domäne“ ist veraltet und wird nur in ATA-Versionen vor 1.9 angezeigt.

**Beschreibung**

Eine fehlerhafte Vertrauensstellung bedeutet, dass Sicherheitsanforderungen von Active Directory für diese Computer möglicherweise nicht wirksam sind. Dies ist ein grundlegender Sicherheits- und Kompatibilitätsfehler und stellt ein leichtes Ziel für Angreifer dar. In dieser Erkennung wird eine Warnung ausgelöst, wenn mehr als fünf Kerberos-Authentifizierungsfehler von einem Computerkonto innerhalb von 24 Stunden angezeigt werden.

**Untersuchung**

Gestattet der untersuchte Computer Domänenbenutzern das Anmelden? 
- Falls ja, können Sie diesen Computer in den Wiederherstellungsschritten ignorieren.

**Wartung**

Verknüpfen Sie den Computer falls notwendig erneut mit der Domäne, oder setzen Sie das Computerkennwort zurück.


## <a name="brute-force-attack-using-ldap-simple-bind"></a>Brute-Force-Angriff mithilfe einer einfachen LDAP-Bindung

**Beschreibung**

>[!NOTE]
> Der Hauptunterschied zwischen **verdächtigen Authentifizierungsfehlern** und dieser Erkennung ist der, dass in dieser Erkennung durch ATA bestimmt werden kann, ob verschiedene Kennwörter verwendet wurden.

Bei einem Brute-Force-Angriff versucht ein Angreifer, sich mit vielen verschiedenen Kennwörtern für verschiedene Konten anzumelden, bis ein korrektes Kennwort für mindestens ein Konto gefunden wird. Sobald eines gefunden wurde, kann sich der Angreifer mit diesem Konto anmelden.

In dieser Erkennung wird eine Warnung ausgelöst, wenn ATA eine signifikante Anzahl von Authentifizierungen mit einfacher Bindung erkennt. Dies kann entweder *horizontal* mit einem kleinen Satz von Kennwörtern für viele Benutzer oder *vertikal* mit einem großen Satz von Kennwörtern für wenige Benutzer geschehen. Auch eine beliebige Kombination dieser beiden Optionen ist möglich.

**Untersuchung**

1. Wenn viele Konten beteiligt sind, klicken Sie auf **Details herunterladen**, um die Liste in einem Excel-Arbeitsblatt anzuzeigen.

2. Klicken Sie auf die Warnung, um zu der dedizierten Seite zu gelangen. Überprüfen Sie, ob Anmeldeversuche mit einer erfolgreichen Authentifizierung beendet wurden. Die Versuche erscheinen als **Erratene Konten** auf der rechten Seite der Infografik. Falls ja, werden von den **erratenen Konten** einige normalerweise vom Quellcomputer verwendet? Falls ja, **unterdrücken** Sie die verdächtige Aktivität.

3. Wenn es keine **erratenen Konten** gibt, werden einige von den **angegriffenen Konten** normalerweise vom Quellcomputer verwendet? Falls ja, **unterdrücken** Sie die verdächtige Aktivität.

**Wartung**

[Komplexe bzw. lange Kennwörter](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) stellen die erste Sicherheitsstufe zum Schutz gegen Brute-Force-Angriffe dar.

## <a name="encryption-downgrade-activity"></a>Aktivität zur Herabstufung der Verschlüsselung

**Beschreibung**

Die Herabstufung der Verschlüsselung ist eine Methode, die dazu dient, Kerberos zu schwächen, indem für die Verschlüsselungsstufe von unterschiedlichen Feldern des Protokolls, die normalerweise mit der höchsten Verschlüsselungsstufe verschlüsselt werden, ein Downgrade durchgeführt wird. Ein abgeschwächtes verschlüsseltes Feld ist ein leichteres Ziel für versuchte Brute-Force-Angriffe offline. Verschiedene Angriffsmethoden nutzen schwache Kerberos-Verschlüsselungsverfahren. In dieser Erkennung lernt ATA die Kerberos-Verschlüsselungstypen, die von Computern und Benutzern verwendet werden, und benachrichtigt Sie, wenn ein schwächeres Verschlüsselungsverfahren verwendet wird, das (1) unüblich für den Quellcomputer und/oder den Benutzer ist und (2) mit bekannten Angriffstechniken übereinstimmt.

Es gibt drei Arten von Erkennung:

1.  Skeleton Key ist eine Schadsoftware, die auf einem Domänencontroller ausgeführt wird und mit der eine Authentifizierung bei der Domäne mit jedem Konto möglich ist, ohne das jeweilige Kennwort zu wissen. Diese Schadsoftware verwendet häufig schwächere Verschlüsselungsalgorithmen, um einen Hashwert für das Kennwort des Benutzers auf dem Domänencontroller zu erstellen. In dieser Erkennung wurde die Verschlüsselungsmethode der KRB_ERR-Nachricht vom Domänencontroller an das Konto, von dem aus ein Ticket erstellt wird, im Vergleich zum zuvor gelernten Verhalten heruntergestuft.

2.  Golden Ticket: Bei einer [Golden Ticket](#golden-ticket)-Warnung wurde die Verschlüsselungsmethode des TGT-Felds der TGS_REQ-Nachricht (Dienstanforderung) vom Quellcomputer im Vergleich zum zuvor gelernten Verhalten heruntergestuft. Dies basiert nicht auf einer Zeitanomalie (wie bei der anderen Golden Ticket-Erkennung). Zusätzlich gab es keine Kerberos-Authentifizierungsanforderung, die der vorherigen von ATA erkannten Dienstanforderung zugeordnet ist.

3.  Overpass-the-Hash: Ein Angreifer kann einen schwachen gestohlenen Hash zur Erstellung eines starken Tickets verwenden, zusammen mit einer Kerberos-AS-Anforderung. In dieser Erkennung wurde der AS_REQ-Nachrichtenverschlüsselungstyp des Quellcomputers im Vergleich zum zuvor gelernten Verhalten heruntergestuft (der Computer hat also AES verwendet).

**Untersuchung**

Überprüfen Sie zunächst die Beschreibung der Warnung, um festzustellen, mit welcher der drei obenstehenden Arten der Erkennung Sie es zu tun haben. Laden Sie für weitere Informationen das Excel-Arbeitsblatt herunter.
1.  Skeleton Key: Sie können überprüfen, ob Ihre Domänencontroller von Skeleton Key betroffen sind, indem Sie [den vom ATA-Team entwickelten Scanner verwenden](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73). Wenn der Scanner Schadsoftware auf einem oder mehreren Ihrer Domänencontroller findet, ist dies ein richtig positives Ereignis.
2.  Golden Ticket: Wechseln Sie im Excel-Arbeitsblatt zur Registerkarte **Netzwerkaktivität**. Sie werden feststellen, dass das entsprechende heruntergestufte Feld **Request Ticket Encryption Type** ist und dass **Source Computer Supported Encryption Types** stärkere Verschlüsselungsmethoden auflistet.
  ein.    Überprüfen Sie den Quellcomputer und das Konto. Überprüfen Sie im Fall von mehreren Quellcomputern und Konten, ob diese etwas gemeinsam haben (alle Marketingmitarbeiter verwenden z.B. eine bestimmte App, die die Warnung möglicherweise ausgelöst hat). Es gibt Fälle, in denen eine benutzerdefinierte Anwendung, die selten genutzt wird, mit einem niedrigeren Verschlüsselungschiffre authentifiziert wird. Überprüfen Sie, ob solche Apps auf dem Quellcomputer vorhanden sind. Falls ja, ist dies wahrscheinlich ein unbedenklich richtig positives Ereignis und kann **unterdrückt** werden.
  b.    Überprüfen Sie die Ressource, auf die von diesen Tickets aus zugegriffen wird. Wenn auf eine Ressource von allen zugegriffen wird, stellen Sie sicher, dass es sich um eine gültige Ressource handelt, auf die zugegriffen werden soll. Überprüfen Sie zudem, ob die Zielressource starke Verschlüsselungsmethoden unterstützt. Sie können dies in Active Directory überprüfen, indem Sie das Attribut `msDS-SupportedEncryptionTypes` des Ressourcendienstkontos überprüfen.
3.  Overpass-the-Hash: Wechseln Sie im Excel-Arbeitsblatt zur Registerkarte **Netzwerkaktivität**. Sie werden feststellen, dass das entsprechende heruntergestufte Feld **Encrypted Timestamp Encryption Type** ist und dass **Source Computer Supported Encryption Types** stärkere Verschlüsselungsmethoden enthält.
  ein.    Es gibt Fälle, in denen diese Warnung ausgelöst werden kann, wenn sich Benutzer mit Smartcards anmelden und die Smartcardkonfiguration kürzlich geändert wurde. Überprüfen Sie, ob solche Änderungen für die beteiligten Konten vorgenommen wurden. Falls ja, ist dies wahrscheinlich ein unbedenklich richtig positives Ereignis und kann **unterdrückt** werden.
  b.    Überprüfen Sie die Ressource, auf die von diesen Tickets aus zugegriffen wird. Wenn auf eine Ressource von allen zugegriffen wird, stellen Sie sicher, dass es sich um eine gültige Ressource handelt, auf die zugegriffen werden soll. Überprüfen Sie zudem, ob die Zielressource starke Verschlüsselungsmethoden unterstützt. Sie können dies in Active Directory überprüfen, indem Sie das Attribut `msDS-SupportedEncryptionTypes` des Ressourcendienstkontos überprüfen.

**Wartung**

1.  Skeleton Key – Entfernen der Schadsoftware Weitere Informationen finden Sie in der [Skeleton Key Malware Analysis](https://www.virusbulletin.com/virusbulletin/2016/01/paper-digital-bian-lian-face-changing-skeleton-key-malware) (Analyse der Skeleton Key-Schadsoftware).

2.  Golden Ticket: Befolgen Sie die Anweisungen zu verdächtigen Aktivitäten unter [Golden Ticket](#golden-ticket).   
    Implementieren Sie ebenfalls die  [Pass the hash recommendations (Empfehlungen zu Pass-the-Hash)](https://www.microsoft.com/download/details.aspx?id=36036), da für das Erstellen eines Golden Tickets Domänenadministratorrechte erforderlich sind.

3.  Overpass-the-Hash: Wenn das beteiligte Konto nicht vertraulich ist, setzen Sie das Kennwort für dieses Konto zurück. Dies hindert den Angreifer daran, neue Kerberos-Tickets aus dem Kennworthash zu erstellen. Bestehende Tickets können jedoch weiterhin verwendet werden, bis sie ablaufen. Wenn es sich um ein vertrauliches Konto handelt, sollten Sie das KRBTGT-Konto wie bei verdächtigen Aktivitäten mit Golden Tickets zweimal zurücksetzen. Durch das zweimalige Zurücksetzen von KRBTGT werden alle Kerberos-Tickets in dieser Domäne ungültig. Daher sollten Sie diesen Schritt im Voraus planen. Weitere Informationen finden Sie im Leitfaden [KRBTGT Account Password Reset Scripts now available for customers (Skripts zum Zurücksetzen von Kennwörtern des KRBTGT-Kontos stehen Kunden jetzt zur Verfügung)](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/). Beachten Sie auch die Verwendung des  [Reset the KRBTGT account password/keys tool (Tool zum Zurücksetzen des Kennworts/Schlüssels eines KRBTGT-Kontos)](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Da es sich dabei um eine Technik mit seitlicher Bewegung handelt, führen Sie die bewährten Methoden der [Pass the hash recommendations (Empfehlungen zu Pass-the-Hash)](https://www.microsoft.com/download/details.aspx?id=36036) aus.


## <a name="honeytoken-activity"></a>Honeytoken-Aktivität


**Beschreibung**

Honeytoken-Konten sind Köderkonten, die eingerichtet werden, um schädliche Aktivitäten, die versuchen, diese Konten zu verwenden, zu erkennen und zu verfolgen. Honeytoken-Konten sollten nicht verwendet werden, aber einen attraktiven Namen besitzen, um Angreifer anzulocken (z.B. SQL-Admin). Jede von diesen ausgehende Aktivität kann auf böswilliges Verhalten hinweisen.

Weitere Informationen zu Honeytoken-Konten finden Sie unter [Installieren von ATA – Schritt 7](install-ata-step7.md).

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

Überprüfen Sie, ob der verwendete Hash von einem Computer stammt, der dem Zielbenutzer gehört oder von diesem regelmäßig verwendet wird. Falls dies zutrifft, ist die Warnung falsch positiv, andernfalls ist sie wahrscheinlich richtig positiv.

**Wartung**

1. Wenn das beteiligte Konto nicht vertraulich ist, setzen Sie das Kennwort für dieses Konto zurück. Durch Zurücksetzen des Kennworts wird verhindert, dass der Angreifer neue Kerberos-Tickets aus dem Kennworthash erstellt. Vorhandene Tickets sind immer noch verwendbar, bis sie ablaufen. 

2. Wenn das betroffene Konto vertraulich ist, sollten Sie das KRBTGT-Konto wie bei verdächtigen Aktivitäten mit Golden Tickets zweimal zurücksetzen. Weil durch das zweimalige Zurücksetzen von KRBTGT alle Domänen-Kerberos-Tickets ungültig werden, sollten Sie diesen Schritt im Hinblick auf die Auswirkungen im Voraus planen. Siehe [KRBTGT Account Password Reset Scripts now available for customers (Skripts zum Zurücksetzen von Kennwörtern des KRBTGT-Kontos stehen Kunden jetzt zur Verfügung)](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/). Beachten Sie auch die Verwendung des  [Reset the KRBTGT account password/keys tool (Tools zum Zurücksetzen des Kennworts/Schlüssels eines KRBTGT-Kontos)](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Da es sich dabei normalerweise um eine Technik mit seitlicher Bewegung handelt, führen Sie die bewährten Methoden der [Pass the hash recommendations (Empfehlungen zu Pass-the-Hash)](https://www.microsoft.com/download/details.aspx?id=36036) aus.

## <a name="identity-theft-using-pass-the-ticket-attack"></a>Identitätsdiebstahl mithilfe eines Pass-the-Ticket-Angriffs

**Beschreibung**

Pass-the-Ticket ist eine Technik mit seitlicher Bewegung, bei der die Angreifer ein Kerberos-Ticket von einem Computer stehlen und dieses verwenden, um Zugriff auf einen anderen Computer zu erlangen, indem sie das gestohlene Ticket wiederverwenden. In dieser Erkennung wird ein Kerberos-Ticket auf zwei (oder mehr) verschiedenen Computern verwendet.

**Untersuchung**

1. Klicken Sie auf die Schaltfläche **Details herunterladen**, um eine vollständige Liste der beteiligten IP-Adressen anzuzeigen. Ist die IP-Adresse von einem oder beiden Computern Teil eines Subnetzes, das aus einem zu kleinen DHCP-Pool (z.B. VPN oder WiFi) zugewiesen wurde? Ist die IP-Adresse freigegeben? Beispielsweise durch ein NAT-Gerät? Wenn die Antwort auf eine dieser Fragen „ja“ lautet, handelt es sich um eine falsch positive Warnung.

2. Gibt es eine benutzerdefinierte Anwendung, die Tickets im Auftrag des Benutzers weiterleitet? Falls ja, handelt es sich um ein unbedenklich richtig positives Ereignis.

**Wartung**

1. Wenn das beteiligte Konto nicht vertraulich ist, setzen Sie das Kennwort für dieses Konto zurück. Durch erneutes Senden des Kennworts wird verhindert, dass der Angreifer neue Kerberos-Tickets aus dem Kennworthash erstellt. Alle vorhandenen Tickets bleiben verwendbar, bis sie abgelaufen sind.  

2. Wenn es sich um ein vertrauliches Konto handelt, sollten Sie das KRBTGT-Konto wie bei verdächtigen Aktivitäten mit Golden Tickets zweimal zurücksetzen. Durch das zweimalige Zurücksetzen von KRBTGT werden alle Kerberos-Tickets in dieser Domäne ungültig. Daher sollten Sie diesen Schritt im Voraus planen. Siehe [KRBTGT Account Password Reset Scripts now available for customers (Skripts zum Zurücksetzen von Kennwörtern des KRBTGT-Kontos stehen Kunden jetzt zur Verfügung)](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/). Beachten Sie auch die Verwendung des  [Reset the KRBTGT account password/keys tool (Tool zum Zurücksetzen des Kennworts/Schlüssels eines KRBTGT-Kontos)](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).  Da es sich dabei um eine Technik mit seitlicher Bewegung handelt, führen Sie die bewährten Methoden der [Pass the hash recommendations (Empfehlungen zu Pass-the-Hash)](https://www.microsoft.com/download/details.aspx?id=36036) aus.

## Golden Ticket-Aktivität von Kerberos<a name="golden-ticket"></a>

**Beschreibung**

Angreifer mit Domänenadministratorrechten können Ihr [KRBTGT-Konto](https://technet.microsoft.com/library/dn745899(v=ws.11).aspx#Sec_KRBTGT) beeinträchtigen. Angreifer können das KRBTGT-Konto verwenden, um ein Kerberos Ticket Granting Ticket (TGT) zu erstellen, das Autorisierung für jede Ressource bietet. Der Ablaufzeitpunkt des Tickets kann auf einen beliebigen Zeitpunkt festgelegt werden. Dieses gefälschte TGT wird als „Golden Ticket“ bezeichnet und ermöglicht es Angreifern, Beständigkeit in Ihrem Netzwerk zu erreichen und beizubehalten.

In dieser Erkennung wird eine Warnung ausgelöst, wenn ein Kerberos Ticket Granting Ticket (TGT) länger als die erlaubte Dauer verwendet wird. Diese ist in der Sicherheitsrichtlinie [Max. Gültigkeitsdauer des Benutzertickets](https://technet.microsoft.com/library/jj852169(v=ws.11).aspx) angegeben.

**Untersuchung**

1. Wurden kürzlich (innerhalb der letzten Stunden) Änderungen an der Einstellung **Maximale Lebensdauer für Benutzertickets** in der Gruppenrichtlinie vorgenommen? Falls ja, **schließen** Sie die Warnung (diese war falsch positiv).

2. Ist das an dieser Warnung beteiligte ATA-Gateway ein virtueller Computer? Falls ja, wurde dieser kürzlich aus einem gespeicherten Zustand fortgesetzt? Falls ja, **schließen** Sie diese Warnung.

3. Wenn die Antwort auf die obigen Fragen „nein“ ist, gehen Sie von einem böswilligen Ereignis aus.

**Wartung**

Ändern Sie das Kennwort für das Kerberos Ticket Granting Ticket (KRBTGT) zweimal gemäß den Anweisungen unter [KRBTGT Account Password Reset Scripts now available for customers (Skripts zum Zurücksetzen von Kennwörtern des KRBTGT-Kontos stehen Kunden jetzt zur Verfügung)](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) mithilfe des  [Reset the KRBTGT account password/keys tool (Tools zum Zurücksetzen des Kennworts/Schlüssels eines KRBTGT-Kontos)](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Durch das zweimalige Zurücksetzen von KRBTGT werden alle Kerberos-Tickets in dieser Domäne ungültig. Daher sollten Sie diesen Schritt im Voraus planen.  
Implementieren Sie ebenfalls die  [Pass the hash recommendations (Empfehlungen zu Pass-the-Hash)](https://www.microsoft.com/download/details.aspx?id=36036), da für das Erstellen eines Golden Tickets Domänenadministratorrechte erforderlich sind.


## <a name="malicious-data-protection-private-information-request"></a>Böswillige Anforderung privater Informationen im Rahmen der Datensicherheit

**Beschreibung**

Die Datenschutz-API (DPAPI) wird von Windows verwendet, um von Browsern gespeicherte Kennwörter, verschlüsselte Dateien und andere sensible Daten sicher zu schützen. Domänencontroller enthalten einen Hauptschlüssel zur Sicherung, der verwendet werden kann, um alle mit der DPAPI verschlüsselten Geheimnisse auf mit einer Domäne verbundenen Windows-Computern zu entschlüsseln. Angreifer können diesen Hauptschlüssel verwenden, um sämtliche von DPAPI geschützten Geheimnisse auf allen mit einer Domäne verbundenen Computern zu entschlüsseln.
In dieser Erkennung wird eine Warnung ausgelöst, wenn die DPAPI zum Abrufen des Sicherungshauptschlüssels verwendet wird.

**Untersuchung**

1. Wird auf dem Quellcomputer ein von der Organisation genehmigter Sicherheitsscanner für Active Directory ausgeführt?

2. Falls dies zutrifft und von Ihnen so gewünscht ist, können Sie die verdächtige Aktivität **schließen und ausschließen**.

3. Falls dies zutrifft und von Ihnen nicht so gewünscht ist, **schließen Sie die verdächtige Aktivität.

**Wartung**

Ein Angreifer benötigt Domänenadministratorrechte zum Verwenden der DPAPI. Implementieren Sie  [Pass the hash recommendations (Empfehlungen zu Pass-the-Hash)](https://www.microsoft.com/download/details.aspx?id=36036).

## <a name="malicious-replication-of-directory-services"></a>Böswillige Replikation von Verzeichnisdiensten


**Beschreibung**

Bei der Replikation mit Active Directory werden Änderungen eines Domänencontrollers mit allen anderen Domänencontrollern synchronisiert. Mit den erforderlichen Berechtigungen können Angreifer eine Replikationsanforderung initiieren, die ihnen das Abrufen der in Active Directory gespeicherten Daten ermöglicht, einschließlich der Kennworthashes.

In dieser Erkennung wird eine Warnung ausgelöst, wenn eine Replikationsanforderung von einem Computer initiiert wird, der kein Domänencontroller ist.

**Untersuchung**

1.  Ist der fragliche Computer ein Domänencontroller? Beispielsweise ein neu hochgestufter Domänencontroller mit Replikationsproblemen. Falls ja, **schließen** Sie die verdächtige Aktivität. 
2.  Soll der fragliche Computer Daten von Active Directory replizieren? Beispielsweise Azure AD Connect. Falls ja, können Sie die verdächtige Aktivität **schließen und ausschließen**.
3.  Klicken Sie auf den Quellcomputer oder das Konto, um die entsprechende Profilseite aufzurufen. Überprüfen Sie, was ungefähr zum Zeitpunkt der Replikation passiert ist. Suchen Sie nach ungewöhnlichen Aktivitäten wie z.B.: Wer war angemeldet, auf welche Ressourcen wurde zugegriffen. 


**Wartung**

Überprüfen Sie die folgenden Berechtigungen: 

- Replizieren von Verzeichnisänderungen   

- Replizieren von allen Verzeichnisänderungen  

Weitere Informationen finden Sie unter  [Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013 (Erteilen von AD DS-Berechtigungen für die Profilsynchronisierung in SharePoint Server 2013)](https://technet.microsoft.com/library/hh296982.aspx).
Nutzen Sie  [AD ACL Scanner](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) , oder erstellen Sie ein Windows PowerShell-Skript, um festzustellen, wer in der Domäne über diese Berechtigungen verfügt.

## <a name="massive-object-deletion"></a>Umfangreiche Objektlöschungen

**Beschreibung**

In manchen Szenarien führen Angreifer Denial-of-Service-Angriffe (DoS) durch, statt nur Informationen zu stehlen. Das Löschen einer großen Anzahl von Konten ist eine Methode des Versuchs eines DoS-Angriffs. 

In dieser Erkennung wird eine Warnung immer dann ausgelöst, wenn mehr als 5 % aller Konten gelöscht werden. Die Erkennung erfordert Lesezugriff auf die gelöschten Objektcontainer.  
Informationen zum Konfigurieren des schreibgeschützten Zugriffs auf den Container mit gelöschten Objekten finden Sie unter **Ändern von Berechtigungen für einen Container mit gelöschten Objekten** in [View or Set Permissions on a Directory Object (Anzeigen und Festlegen von Berechtigungen für ein Verzeichnisobjekt)](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx).

**Untersuchung**

Überprüfen Sie die Liste der gelöschten Konten, und ermitteln Sie, ob es ein Muster oder einen geschäftlichen Grund gibt, der einen umfangreichen Löschvorgang rechtfertigt.

**Wartung**

Entziehen Sie Benutzern die Berechtigung, Konten in AD löschen zu können. Weitere Informationen finden Sie unter [View or Set Permissions on a Directory Object (Anzeigen oder Festlegen von Berechtigungen in einem Verzeichnisobjekt)](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx).

## <a name="privilege-escalation-using-forged-authorization-data"></a>Berechtigungsausweitung mithilfe von gefälschten Autorisierungsdaten

**Beschreibung**

Über bekannte Sicherheitslücken in älteren Versionen von Windows Server können Angreifer das Privileged Attribute Certificate (PAC) manipulieren. PAC ist ein Feld im Kerberos-Ticket, das über Benutzerdaten für die Autorisierung verfügt (in Active Directory ist dies eine Gruppenmitgliedschaft) und das Angreifern zusätzliche Berechtigungen gewährt.

**Untersuchung**

1. Klicken Sie auf die Warnung, um auf die Seite „Details“ zuzugreifen.

2. Ist der Zielcomputer (in der Spalte **ACCESSED**) mit MS14-068 (Domänencontroller) oder MS11-013 (Server) gepatcht? Falls ja, **schließen** Sie die verdächtige Aktivität (diese ist falsch positiv).

3. Wenn der Zielcomputer nicht gepatcht ist, wird auf dem Quellcomputer (in der Spalte **FROM**) ein Betriebssystem bzw. eine Anwendung ausgeführt, die dafür bekannt ist, das PAC zu ändern? Falls ja, **unterdrücken** Sie die verdächtige Aktivität (diese ist unbedenklich richtig positiv).

4. Wenn die Antwort auf die beiden vorstehenden Fragen „Nein“ lautet, gehen Sie von einer böswilligen Aktivität aus.

**Wartung**

Stellen Sie sicher, dass alle Domänencontroller mit Betriebssystemen bis Windows Server 2012 R2 mit  [KB3011780](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privilege)  installiert sind und dass alle Memberserver und Domänencontroller bis 2012 R2 das aktuellste KB2496930 haben. Weitere Informationen finden Sie unter  [Silver PAC](https://technet.microsoft.com/library/security/ms11-013.aspx)  und  [Gefälschte PAC-Datei](https://technet.microsoft.com/library/security/ms14-068.aspx).

## <a name="reconnaissance-using-account-enumeration"></a>Reconnaissance mithilfe von Kontoenumeration

**Beschreibung**

Bei einer Reconnaissance zur Kontoenumeration verwendet ein Angreifer ein Wörterbuch mit tausenden von Benutzernamen oder Tools wie KrbGuess, um Benutzernamen in Ihrer Domäne zu erraten. Der Angreifer führt Kerberos-Anforderungen mit diesen Namen durch, um so auf einen gültigen Benutzernamen zu stoßen. Wenn dadurch ein Benutzername bestimmt wird, erhält der Angreifer die Kerberos-Fehlermeldung **Preauthentication required** (Vorauthentifizierung erforderlich) statt der Meldung **Security principal unknown** (Unbekannter Sicherheitsprinzipal). 

Bei dieser Erkennung kann ATA erkennen, von wo der Angriff durchgeführt wurde, wie viele Versuche vorgenommen wurden und bei vielen dieser Versuche Übereinstimmungen gefunden wurden. Wenn es zu viele unbekannte Benutzer gibt, erkennt ATA dies als verdächtige Aktivität. 

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


## <a name="reconnaissance-using-directory-services-queries"></a>Reconnaissance mithilfe von Verzeichnisdienstabfragen

**Beschreibung**

Die Reconnaissance von Verzeichnisdiensten wird von Angreifern verwendet, um die Verzeichnisstruktur und die Zielkonten mit hohen Berechtigungen für die weiteren Schritte eines Angriffs auszukundschaften. Das Protokoll Security Account Manager Remote (SAM-R) ist eine Methode, die zum Abfragen des Verzeichnisses verwendet wird, um eine solche Zuordnung vorzunehmen.

In dieser Erkennung werden im ersten Monat nach der Bereitstellung von ATA keine Warnungen ausgelöst. Während der Lernphase erfasst ATA, welche SAM-R-Abfragen (Enumerationsabfragen und einzelne Abfragen von sensiblen Konten) von welchen Computern gestellt werden.

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

Verwenden Sie das [SAMRi10-Tool](https://gallery.technet.microsoft.com/SAMRi10-Hardening-Remote-48d94b5b), um den Schutz Ihrer Umgebung gegen diese Technik zu erhöhen.
Wenn das Tool auf Ihren Domänencontroller nicht angewendet werden kann:
1. Wird ein Tool zur Überprüfung des Sicherheitsrisikos auf Ihrem Computer ausgeführt?  
2. Überprüfen Sie, ob die im Angriff abgefragten Benutzer und Gruppen über hohe Berechtigungen verfügen oder anderweitig wichtig sind (d.h. CEO, CFO, IT-Abteilung usw.).  Falls dies der Fall ist, überprüfen Sie auch andere Aktivitäten auf diesem Endpunkt, und überwachen Sie Computer, auf denen die abgefragten Konten angemeldet sind, da diese für Lateral Movement-Methoden verwendet werden können.

## <a name="reconnaissance-using-dns"></a>Reconnaissance über DNS

**Beschreibung**

Ihr DNS-Server enthält eine Struktur aller Computer, IP-Adressen und Dienste in Ihrem Netzwerk. Diese Informationen werden von Angreifern verwendet, um Ihre Netzwerkstruktur auszukundschaften und um interessante Zielcomputer zu bestimmten, die sie in den nächsten Schritten des Angriffs benötigen.

Es gibt mehrere Abfragetypen im DNS-Protokoll. ATA erkennt die AXFR-Anforderung (Transfer), die von Nicht-DNS-Servern stammt.

**Untersuchung**

1. Ist der Quellcomputer (**Stammt von...**) ein DNS-Server? Falls ja, ist dieses Ereignis wahrscheinlich falsch positiv. Klicken Sie zur Überprüfung auf die Warnung, um auf die Seite „Details“ zu gelangen. Überprüfen Sie in der Tabelle unter **Abfrage**, welche Domänen abgefragt wurden. Sind diese Domänen vorhanden? Falls ja, **schließen** Sie die verdächtige Aktivität (diese ist falsch positiv). Stellen Sie zusätzlich sicher, dass der UDP-Port 53 zwischen dem ATA-Gateway und dem Quellcomputer geöffnet ist, um falsch positive Ereignisse zukünftig zu verhindern.
2.  Wird auf dem Quellcomputer ein Sicherheitsscanner ausgeführt? Falls ja, **schließen Sie die Entitäten** in ATA aus, entweder direkt mit **Schließen und Ausschließen** oder über die Seite **Ausschluss** (unter **Konfiguration**, verfügbar für ATA-Administratoren).
3.  Falls Sie alle obigen Fragen verneinen können, setzen Sie die Untersuchung mit Fokus auf dem Quellcomputer fort. Klicken Sie auf den Quellcomputer, um die entsprechende Profilseite aufzurufen. Überprüfen Sie, was ungefähr zum Zeitpunkt der Anforderung passiert ist. Suchen Sie nach ungewöhnlichen Aktivitäten wie z.B.: Wer war angemeldet, auf welche Ressourcen wurde zugegriffen.


**Wartung**

Die Sicherung eines internen DNS-Servers, um zu verhindern, dass Reconnaissance mithilfe von DNS auftritt, kann von der Deaktivierung oder Einschränkung von Zonenübertragungen nur auf bestimmte IP-Adressen erreicht werden. Weitere Informationen zum Einschränken von Zonenübertragungen finden Sie unter [Restrict Zone Transfers (Einschränken von Zonenübertragungen)](https://technet.microsoft.com/library/ee649273(v=ws.10).aspx).
Das Bearbeiten von Zonenübertragungen ist eine Aufgabe innerhalb einer Prüfliste, die für das  [Sichern des DNS-Servers gegen interne und externe Angriffe](https://technet.microsoft.com/library/cc770432(v=ws.11).aspx) gelten sollte.

## <a name="reconnaissance-using-smb-session-enumeration"></a>Reconnaissance mithilfe der SMB-Sitzungsenumeration


**Beschreibung**

Mit der SMB-Enumeration (Server Message Block) können Angreifer Informationen dazu erhalten, welche Benutzer sich zuletzt angemeldet haben. Sobald Angreifer diese Informationen besitzen, können sie sich seitlich im Netzwerk bewegen, um zu einem bestimmten sensiblen Konto zu gelangen.

In dieser Erkennung wird eine Warnung ausgelöst, wenn eine SMB-Sitzungsenumeration auf einem Domänencontroller ausgeführt wird.

**Untersuchung**

1. Klicken Sie auf die Warnung, um auf die Seite „Details“ zu gelangen. Überprüfen Sie das Konto/die Konten, das/die den Vorgang ausgeführt haben und gegebenenfalls, welche Konten verfügbar gemacht wurden.

   - Wird auf dem Quellcomputer eine Art Sicherheitsscanner ausgeführt? Falls ja, können Sie die verdächtige Aktivität **schließen und ausschließen**.

2. Überprüfen Sie, welche beteiligten Benutzer die Vorgänge ausgeführt haben. Melden sich diese normalerweise auf dem Quellcomputer an, oder handelt es sich bei diesen um Administratoren, die solche Aktionen ausführen sollen?  

3. Falls dies zutrifft und die Warnung aktualisiert wird, **unterdrücken** Sie die verdächtige Aktivität.  

4. Falls dies zutrifft und die Warnung nicht aktualisiert werden sollte, **schließen** Sie die verdächtige Aktivität.

5. Wenn die Antwort auf alle vorstehenden Fragen „nein“ lautet, gehen Sie von einer böswilligen Aktivität aus.

**Wartung**

Verwenden Sie das [Net Cease-Tool](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b), um den Schutz Ihrer Umgebung gegen diese Art von Angriff zu erhöhen.

## <a name="remote-execution-attempt-detected"></a>Erkannter Remoteausführungsversuch

**Beschreibung**

Angreifer, die Administratoranmeldeinformationen kompromittiert haben oder einen Zero-Day-Exploit verwenden, können Remotebefehle auf Ihrem Domänencontroller ausführen. Damit können sie Persistenz erhalten, Informationen sammeln, DOS-Attacken (Denial of Service) ausführen usw. ATA erkennt PSexec-Verbindungen und WMI-Remoteverbindungen.

**Untersuchung**

1. Dies tritt häufig bei administrativen Arbeitsstationen, IT-Teammitgliedern und Dienstkonten auf, die administrative Aufgaben auf den Domänencontrollern ausführen. Wenn dies der Fall ist und die Warnung aktualisiert wird, weil die Aufgabe vom selben Administrator oder Computer ausgeführt wird, **unterdrücken** Sie die Warnung.
2. Ist der fragliche Computer berechtigt, diese Remoteausführung auf Ihrem Domänencontroller auszuführen?
   - Ist das fragliche Konto berechtigt, diese Remoteausführung auf Ihrem Domänencontroller auszuführen?
   - Wenn Sie beide Fragen bejahen können, **schließen** Sie die Warnung.
3. Wenn Sie beide Fragen verneinen können, sollte diese Aktivität als richtig positiv behandelt werden. Versuchen Sie, die Quelle des Versuchs zu ermitteln, indem Sie Computer- und Kontoprofile überprüfen. Klicken Sie auf den Quellcomputer oder das Konto, um die entsprechende Profilseite aufzurufen. Überprüfen Sie, was ungefähr zum Zeitpunkt dieser Versuche passiert ist. Suchen Sie nach ungewöhnlichen Aktivitäten wie z.B.: Wer war angemeldet, auf welche Ressourcen wurde zugegriffen.


**Wartung**

1. Schränken Sie den Remotezugriff auf Domänencontroller von Computern ein, die nicht den Tier 0 aufweisen.

2. Implementieren Sie  [privilegierten Zugriff](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/securing-privileged-access) , damit nur abgesicherte Computer eine Verbindung für Administratoren mit dem Domänencontroller herstellen können.

## <a name="sensitive-account-credentials-exposed--services-exposing-account-credentials"></a>Offengelegte sensible Anmeldeinformationen und Dienste, die Anmeldeinformationen offenlegen

> [!NOTE]
> Diese verdächtige Aktivität ist veraltet und wird nur in ATA-Versionen vor 1.9 angezeigt. Informationen zu ATA 1.9 und höher finden Sie unter [Berichte](reports.md).

**Beschreibung**

Einige Dienste senden Anmeldeinformationen im Nur-Text-Format. Dies kann sogar bei sensiblen Konten geschehen. Angreifer, die Ihren Netzwerkdatenverkehr überwachen, können diese Anmeldeinformationen abfangen und diese zu böswilligen Zwecken verwenden. Jedes Klartextkennwort für ein sensibles Konto löst eine Warnung aus. Bei nicht sensiblen Konten wird die Warnung hingegen ausgelöst, wenn mindestens fünf verschiedene Konten Klartextkennwörter vom selben Quellcomputer aus senden. 

**Untersuchung**

Klicken Sie auf die Warnung, um auf die Seite „Details“ zu gelangen. Sie können sehen, welche Konten verfügbar gemacht wurden. Wenn es viele solche Konten gibt, klicken Sie auf **Details herunterladen**, um die Liste in einem Excel-Arbeitsblatt anzuzeigen.

Üblicherweise gibt es ein Skript oder eine ältere Anwendung auf den Quellcomputern, die die einfache LDAP-Bindung verwenden.

**Wartung**

Überprüfen Sie die Konfiguration des Quellcomputers, um sicherzustellen, dass Sie keine einfache LDAP-Bindung verwenden. Statt einfachen LDAP-Bindungen können Sie LDAP SALS oder LDAPS verwenden.

## <a name="suspicious-authentication-failures"></a>Verdächtige Authentifizierungsfehler

**Beschreibung**

Bei einem Brute-Force-Angriff versucht ein Angreifer, sich mit vielen verschiedenen Kennwörtern für verschiedene Konten anzumelden, bis ein korrektes Kennwort für mindestens ein Konto gefunden wird. Sobald eines gefunden wurde, kann sich der Angreifer mit diesem Konto anmelden.

In dieser Erkennung wird eine Warnung ausgelöst, wenn viele Authentifizierungsfehler mit Kerberos oder der integrierten Windows-Authentifizierung auftreten. Dies kann entweder horizontal mit einem kleinen Satz von Kennwörtern für viele Benutzer oder vertikal mit einem großen Satz von Kennwörtern für wenige Benutzer geschehen. Auch eine beliebige Kombination dieser beiden Optionen ist möglich. Der Mindestzeitraum, bevor eine Warnung ausgelöst werden kann, beträgt eine Woche.

**Untersuchung**

1. Klicken Sie auf **Details herunterladen**, um die vollständigen Informationen in einem Excel-Arbeitsblatt anzuzeigen. Sie können die folgenden Informationen abrufen: 
   - Liste der angegriffenen Konten
   - Liste der erratenen Konten, bei denen Anmeldeversuche mit einer erfolgreichen Authentifizierung endeten
   - Wenn die Authentifizierungsversuche über NTLM ausgeführt wurden, werden die relevanten Ereignisaktivitäten angezeigt. 
   - Wenn die Authentifizierungsversuche über Kerberos ausgeführt wurden, werden die relevanten Netzwerkaktivitäten angezeigt.
2. Klicken Sie auf den Quellcomputer, um die entsprechende Profilseite aufzurufen. Überprüfen Sie, was zum Zeitpunkt der Versuche passiert ist. Suchen Sie nach ungewöhnlichen Aktivitäten, indem Sie beispielsweise überprüfen, wer angemeldet war und auf welche Ressourcen zugegriffen wurde. 
3. Wenn die Authentifizierung mithilfe von NTLM durchgeführt wurde und Sie sehen, dass die Warnung mehrfach aufgetreten ist, aber keine ausreichenden Informationen zum Server verfügbar sind, auf den der Quellcomputer zugreifen wollte, sollten Sie die **NTLM-Überwachung** auf dem betroffenen Domänencontroller aktivieren. Aktivieren Sie dazu Ereignis 8004. Dies ist das NTLM-Authentifizierungsereignis, das Informationen zum Quellcomputer, Benutzerkonto und **Server** enthält, auf die der Quellcomputer zugreifen wollte. Wenn Sie wissen, welcher Server die Authentifizierungsüberprüfung gesendet hat, sollten Sie den Server untersuchen, indem Sie seine Ereignisse, z.B. 4624, überprüfen, um den Authentifizierungsprozess besser nachvollziehen zu können. 


**Wartung**

[Komplexe bzw. lange Kennwörter](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) stellen die erste Sicherheitsstufe zum Schutz gegen Brute-Force-Angriffe dar.

## Erstellen eines verdächtigen Diensts <a name="suspicious-service-creation"></a>

**Beschreibung**

Angreifer versuchen, verdächtige Dienste auf Ihrem Netzwerk auszuführen. ATA löst eine Warnung aus, wenn ein neuer Dienst, der verdächtig erscheint, auf einem Domänencontroller erstellt wird. Diese Warnung basiert auf Ereignis 7045 und wird von jedem Domänencontroller erkannt, der von einem ATA- oder einem Lightweight-Gateway abgedeckt wird.

**Untersuchung**

1. Wenn es sich bei dem betroffenen Computer um eine Arbeitsstation oder einen Computer handelt, auf dem Mitglieder des IT-Teams und Dienstkonten administrative Aufgaben ausführen, kann das Resultat ein falsch positives Ergebnis sein, und Sie sollten die Warnung **unterdrücken** und sie wenn nötig der Ausschlussliste hinzufügen.

2. Erkennen Sie den Dienst auf dem Computer?

   - Darf das fragliche **Konto** diesen Dienst installieren?

   - Wenn die Antwort auf beide Fragen *ja* ist, **schließen** Sie die Warnung, oder fügen Sie sie der Ausschlussliste hinzu.

3. Wenn die Antwort auf beide Fragen *nein* ist, sollte dieses Ereignis als richtig positiv behandelt werden.

**Wartung**

- Implementieren Sie den Zugriff mit weniger privilegierten Rechten auf Domänencomputern, um nur bestimmten Benutzern die Erstellung neuer Dienste zu erlauben.


## <a name="suspicion-of-identity-theft-based-on-abnormal-behavior"></a>Verdacht des Identitätsdiebstahls auf Grundlage von ungewöhnlichem Verhalten

**Beschreibung**

ATA erlernt das Entitätsverhalten für Benutzer, Computer und Ressourcen über einen gleitenden Zeitraum von drei Wochen. Das Verhaltensmodell basiert auf folgenden Aktivitäten: Die Computer, auf denen die Entitäten angemeldet sind, die Ressourcen, für die die Entität Zugriff anfordert, und die Uhrzeit, zu der diese Vorgänge stattgefunden haben. ATA sendet eine Warnung, wenn eine Abweichung des Verhaltens der Entität vorliegt, basierend auf den Machine-Learning-Algorithmen. 

**Untersuchung**

1. Soll der fragliche Benutzer diese Vorgänge ausführen?

2. Betrachten Sie folgende Fälle als potenziell falsch positive Ereignisse: Ein Benutzer, der aus dem Urlaub zurückkam, IT-Personal, das den übermäßigen Zugriff als Teil seiner Pflicht ausführt (z.B. eine Spitze in der Helpdesk-Unterstützung an einem bestimmten Tag oder in einer bestimmten Woche), Remotedesktopanwendungen. Wenn Sie die Warnung **schließen und ausschließen**, ist der Benutzer nicht mehr Teil der Erkennung.


**Wartung**

 Je nachdem, wodurch dieses ungewöhnliche Verhalten ausgelöst wurde, sollten verschiedene Aktionen ausgeführt werden. Wenn das Netzwerk beispielsweise gescannt wurde, sollte der Quellcomputer aus dem Netzwerk blockiert werden (außer wenn er genehmigt wurde).

## <a name="unusual-protocol-implementation"></a>Ungewöhnliche Protokollimplementierung


**Beschreibung**

Angreifer verwenden Tools, die verschiedene Protokolle (SMB, Kerberos, NTLM) auf nicht standardmäßige Arten implementieren. Während diese Art des Netzwerkdatenverkehrs von Windows ohne Warnungen akzeptiert wird, kann ATA potenziell böswillige Absichten erkennen. Das Verhalten ist maßgeblich für Techniken wie Overpass-the-Hash und Exploits, die von erweiterter Ransomware, z.B. WannaCry, verwendet werden.

**Untersuchung**

Identifizieren Sie das ungewöhnliche Protokoll, und klicken Sie auf der Zeitachse der verdächtigen Aktivitäten auf die verdächtige Aktivität, um auf die Seite „Details“ zuzugreifen. Das Protokoll wird über dem Pfeil angezeigt: Kerberos oder NTLM.

- **Kerberos**: Wird häufig ausgelöst, wenn ein Hacking-Tool wie Mimikatz möglicherweise für einen Overpass-the-Hash-Angriff verwendet wurde. Überprüfen Sie, ob auf dem Quellcomputer eine Anwendung ausgeführt wird, die im Widerspruch zur Kerberos-RFC ihren eigenen Kerberos-Stapel implementiert. In diesem Fall ist das Ereignis unbedenklich richtig positiv, und die Warnung kann **Geschlossen** werden. Wenn die Warnung weiterhin ausgelöst wird und dies immer noch der Fall ist, können Sie die Warnung **unterdrücken**.

- **NTLM**: Es könnte sich um WannaCry oder Tools wie Metasploit, Medusa und Hydra handeln.  

Um festzustellen, ob es sich bei der Aktivität um einen WannaCry-Angriff handelt, führen Sie folgende Schritte aus:

1. Überprüfen Sie, ob auf dem Quellcomputer ein Angriffstool wie Metasploit, Medusa oder Hydra ausgeführt wird.

2. Wenn keine Angriffstools gefunden werden, überprüfen Sie, ob auf dem Quellcomputer eine Anwendung ausgeführt wird, die ihren eigenen NTLM- oder SMB-Stapel implementiert.

3. Wenn nicht, überprüfen Sie, ob es von WannaCry verursacht wird, indem Sie ein WannaCry-Scannerskript (z.B. [diesen Scanner](https://github.com/apkjet/TrustlookWannaCryToolkit/tree/master/scanner)) auf dem Quellcomputer ausführen, der an der verdächtigen Aktivität beteiligt ist. Wenn der Scanner feststellt, dass der Computer infiziert oder anfällig ist, patchen Sie den Computer, entfernen Sie die Schadsoftware, und blockieren Sie diese vom Netzwerk.

4. Wenn das Skript feststellt, dass der Computer nicht infiziert oder anfällig ist, könnte er trotzdem infiziert sein, denn SMBv1 könnte deaktiviert, oder der Computer könnte gepatcht worden sein. Beides beeinflusst das Überprüfungstool.

**Wartung**

Wenden Sie die aktuellsten Patches auf alle Ihre Computer an, und überprüfen Sie, ob alle Sicherheitsupdates angewendet wurden.

1. [Deaktivieren von SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)

2. [Entfernen von WannaCry](https://support.microsoft.com/help/890830/remove-specific-prevalent-malware-with-windows-malicious-software-remo)

3.  Daten unter der Kontrolle von bestimmter Ransomware können manchmal verschlüsselt werden. Entschlüsselung ist nur möglich, wenn der Benutzer den Computer nicht neu gestartet oder ausgeschaltet hat. Weitere Informationen finden Sie unter [Wanna Cry Ransomware (WannaCry-Ransomware)](https://answers.microsoft.com/en-us/windows/forum/windows_10-security/wanna-cry-ransomware/5afdb045-8f36-4f55-a992-53398d21ed07?auth=1)


>[!NOTE]
> Wenn Sie eine Warnung zu verdächtiger Aktivität deaktivieren möchten, wenden Sie sich an den Support.

## <a name="related-videos"></a>Verwandte Videos
- [Joining the security community](https://channel9.msdn.com/Shows/Microsoft-Security/Join-the-Security-Community) (Der Sicherheitscommunity beitreten)


## <a name="see-also"></a>Weitere Informationen
- [Verdächtige ATA-Aktivitäten – Playbook](http://aka.ms/ataplaybook)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md)
