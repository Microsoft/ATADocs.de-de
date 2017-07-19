---
title: "Untersuchung der Rechteausweitung durch Angriffe mit gefälschten Autorisierungsdaten | Microsoft-Dokumentation"
description: "In diesem Artikel werden Angriffe mit gefälschten Autorisierungsdaten beschrieben. Außerdem erhalten Sie Anweisungen zu Untersuchungen, die Sie durchführen können, wenn eine derartige Bedrohung auf Ihrem Netzwerk erkannt wird."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/4/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: f3db435e-9553-40a2-a2ad-278fad4f0ef5
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 842e9866c5fdb447f49600501c4486da6db902f2
ms.sourcegitcommit: 4118dd4bd98994ec8a7ea170b09aa301a4be2c8a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/05/2017
---
*Gilt für: Advanced Threat Analytics Version 1.8*

# <a name="investigating-privilege-escalation-using-forged-authorization-data-attacks"></a>Berechtigungsausweitung über Angriffe mit gefälschten Autorisierungsdaten

Die Funktionen zum Erkennen von Sicherheitsrisiken werden von Microsoft laufend optimiert. Außerdem wird daran gearbeitet, Informationen, die Handlungen erfordern, zeitnah an Sicherheitsanalytiker weiterzugeben. Advanced Threat Analytics (ATA) von Microsoft hilft bei diesem Wandel. Wenn ATA auf Ihrem Netzwerk eine Aktivität erkennt, die möglicherweise ein Angriff mit gefälschten Autorisierungsdaten ist, und dies an Sie meldet, hilft Ihnen dieser Artikel dabei, diese Bedrohung zu verstehen und zu untersuchen.

## <a name="what-is-a-privileged-attribute-certificate-pac"></a>Was ist ein Privileged Attribute Certificate (PAC)?

Das PAC ist die Datenstruktur des Kerberos-Tickets, die Autorisierungsinformationen enthält. Dazu zählen z.B. Gruppenmitgliedschaften, Sicherheits-IDs und Benutzerprofilinformationen. In einer AD-Domäne (Active Directory) können dadurch Autorisierungsdaten vom Domänencontroller (DC) an andere Memberserver und Arbeitsstationen für die Authentifizierung und Autorisierung übergeben werden. Neben Informationen zu Mitgliedschaften enthält die PAC-Datei zusätzliche Anmeldeinformationen, Profil- und Richtlinieninformationen und unterstützende Sicherheitsmetadaten. 

Die PAC-Datenstruktur wird von Authentifizierungsprotokollen (Protokolle, die Identitäten überprüfen) verwendet, um Autorisierungsinformationen zu übermitteln, die den Zugriff auf Ressourcen steuern.

### <a name="pac-validation"></a>PAC-Überprüfung

Die PAC-Überprüfung ist eine Sicherheitsfunktion, die verhindert, dass ein Angreifer unautorisierten Zugriff auf ein System oder dessen Ressourcen durch einen Man-In-The-Middle-Angriff erhält. Dies gilt besonders für Anwendungen mit Benutzeridentitätswechseln. Bei Benutzerwechseln sind vertrauenswürdige Identitäten involviert, wie z.B. ein Dienstkonto, dem erweiterte Berechtigungen für den Zugriff auf Ressourcen und das Ausführen von Aufgaben erteilt wurden. Die PAC-Überprüfung trägt zur Aufrechterhaltung einer sicheren Autorisierungsumgebung bei Authentifizierungseinstellungen von Kerberos bei, und zwar dort, wo Benutzerwechsel vorkommen. Die [PAC-Überprüfung](https://blogs.msdn.microsoft.com/openspecification/2009/04/24/understanding-microsoft-kerberos-pac-validation/) stellt sicher, dass ein Benutzer genau die Autorisierungdaten angibt, die ihm im Kerberos-Ticket erteilt wurden, und dass die Berechtigungen des Tickets nicht modifiziert wurden.

Bei einer PAC-Überprüfung verschlüsselt der Server eine Anforderungsnachricht, die den Typ und die Länger der PAC-Signatur enthält, und sendet diese an den DC. Der DC entschlüsselt die Anforderung und extrahiert die Prüfsumme des Servers und die Werte der KDC-Prüfsumme. Wenn die Überprüfung der Prüfsumme erfolgreich ist, gibt der DC einen Erfolgscode an den Server zurück. Ein nicht erfolgreicher Rückgabecode weist darauf hin, dass die PAC-Datei verändert wurde. 

Der PAC-Inhalt von Kerberos wird zweimal signiert: 
- Einmal mit dem Hauptschlüssel des KDC, um böswillige Dienste auf der Serverseite daran zu hindern, die Autorisierungsdaten zu ändern
- Und einmal mit dem Hauptschlüssel des Serverkontos der Zielressource, um Benutzer daran zu hindern, den PAC-Inhalt zu ändern und ihre eigenen Autorisierungsdaten hinzuzufügen

### <a name="pac-vulnerability"></a>PAC-Sicherheitsrisiko
Die Sicherheitsbulletins [MS14-068](https://technet.microsoft.com/library/security/MS14-068.aspx) und [MS11-013](https://technet.microsoft.com/library/security/ms11-013.aspx) behandeln Sicherheitslücken im Kerberos-KDC, durch die es einem Angreifer möglicherweise möglich ist, das PAC-Feld in einem gültigen Kerberos-Ticket zu manipulieren, sodass er zusätzliche Berechtigungen erhält.

## <a name="privilege-escalation-using-forged-authorization-data-attack"></a>Berechtigungsausweitung über Angriffe mit gefälschten Autorisierungsdaten

Mit einem Angriff mit gefälschten Autorisierungsdaten versucht ein Angreifer, diese PAC-Sicherheitslücken auszunutzen, um seine Berechtigungen in Ihrer AD-Struktur oder -Domäne zu erweitern. Für einen Angriff braucht der Angreifer Folgendes:
-   Anmeldeinformationen eines Domänenbenutzers
-   eine Netzwerkverbindung mit einem DC, der zur Authentifizierung mit kompromittierten Domänenanmeldeinformationen verwendet wird
-   die passenden Tools Das PyKEK (Python Kerberos Exploitation Kit) ist ein Tool, das zum Fälschen von PAC-Dateien verwendet werden kann.

Wenn der Angreifer über die nötigen Anmeldeinformationen und die erforderliche Verbindung verfügt, kann er die PAC-Datei des Anmeldetokens eines vorhandenen Kerberos-Benutzers (Ticket Granting Ticket, TGT) fälschen oder modifizieren. Der Angreifer ändert den Anspruch der Gruppenmitgliedschaft in eine Gruppe mit erweiterten Berechtigungen (z.B. „Domänenadministratoren“ oder „Administratoren des Unternehmens“). Dann fügt der Angreifer die modifizierte PAC-Datei in das Kerberos-Ticket ein. Dieses Kerberos-Ticket verwendet er dann, um von einem nicht gepatchten DC ein Dienstticket anzufordern. Damit erhält der Angreifer erweiterte Berechtigungen in der Domäne und ist autorisiert, Aktionen auszuführen, die er eigentlich nicht ausführen darf. Ein Angreifer kann mit dem modifizierten Anmeldetoken (TGT) Zugriff auf jede Ressource in der Domäne erhalten, indem er Ressourcenzugriffstoken anfragt (Ticket Granting Server). Das heißt, dass ein Angreifer alle für Ressourcen konfigurierte ACLs umgehen kann, die den Zugriff auf das Netzwerk einschränken, indem er Autorisierungsdaten (PAC) für jeden Benutzer in AD spooft.

## <a name="discovering-the-attack"></a>Erkennen des Angriffs
Wenn der Angreifer versucht, seine Berechtigungen zu erweitern, wird dies von ATA erkannt und als Warnung mit hohem Schweregrad markiert.

![Verdächtige Aktivität mit gefälschten Papieren](./media/forged-pac.png)

ATA gibt in der Warnung zur verdächtigen Aktivität an, ob die Rechteausweitung mit gefälschten Autorisierungsdaten Erfolg hatte. Sowohl erfolgreiche als auch fehlgeschlagene Warnungen sollten untersucht werden, da auch erfolglose Versuche auf einen Angreifer in Ihrer Umgebung hinweisen können.

## <a name="investigating"></a>Untersuchung
Nachdem Sie eine Warnung bezüglich einer Rechteausweitung mit gefälschten Autorisierungsdaten erhalten haben, müssen Sie entscheiden, was gemacht werden muss, um die Auswirkungen des Angriffs abzuschwächen. Dazu müssen Sie die Warnung zuerst in eine der folgenden Kategorien einordnen: 
-   Richtig positiv: eine böswillige, von ATA erkannte Aktion
-   Falsch positiv: Eine falsche Warnung. Es gab keine Rechteausweitung mit gefälschten Autorisierungsdaten (dies ist ein Ereignis, das ATA fälschlicherweise für einen Datenangriff zur Rechteausweitung mit gefälschten Autorisierungsdaten gehalten hat)
-   Unbedenklich richtig positiv: eine von ATA erkannte Aktion, die tatsächlich durchgeführt wurde, aber nicht böswillig ist, wie z.B. ein Penetrationstest

Folgendes Diagramm hilft Ihnen dabei, zu bestimmen, welche Schritte sie durchführen müssen:

![Diagramm zu gefälschten PAC-Dateien](./media/forged-pac-diagram.png)

1. Überprüfen Sie zunächst die Warnung in der Angriffszeitachse in ATA, um festzustellen, ob der Angriffsversuch mit gefälschter Autorisierung erfolgreich war, fehlgeschlagen ist oder es bei einem Versuch geblieben ist (versuchte Angriffe gelten ebenfalls als fehlgeschlagen). Sowohl erfolgreiche als auch fehlgeschlagene Versuche können zu einem richtig positiven Ergebnis führen. Diese sind jedoch von unterschiedlichem Schweregrad in der Umgebung.
 
 ![Verdächtige Aktivität mit gefälschten Papieren](./media/forged-pac-sa.png)


2.  Wenn der erkannte Angriff zur Rechteausweitung mit gefälschten Autorisierungsdaten Erfolg hatte:
    -   Wenn der DC, auf dem die Warnung ausgelöst wurde, ordnungsgemäß gepatcht ist, ist die Warnung falsch positiv. In diesem Fall können Sie die Warnung schließen und eine E-Mail mit der entsprechenden Information an das ATA-Team unter ATAEval@microsoft.com schicken, damit die Erkennung laufend verbessert werden kann. 
    -   Wenn der DC, den die Warnung betrifft, nicht ordnungsgemäß gepatcht ist:
        -   Wenn der in der Warnung aufgelistete Dienst nicht über einen eigenen Autorisierungsmechanismus verfügt, handelt es sich um eine richtig positive Meldung. Dann sollten Sie den Prozess der Reaktion auf Sicherheitsfälle einleiten. 
        -   Wenn der in der Warnung aufgelistete Dienst über einen internen Autorisierungsmechanismus verfügt, der Autorisierungsdaten verlangt, kann es sein, dass er fälschlicherweise als Angriff zur Rechteausweitung mit gefälschten Autorisierungsdaten identifiziert wird. 

3.  Wenn der erkannte Angriff fehlgeschlagen ist:
    -   Wenn bekannt ist, dass das Betriebssystem oder die Anwendung die PAC-Datei modifiziert, ist es sehr wahrscheinlich, dass es sich hierbei um ein unbedenklich richtig positives Ergebnis handelt. Sie sollte sich mit dem Besitzer des Betriebssystems oder der Anwendung in Verbindung setzen, um dieses Verhalten zu beheben.

    -   Wenn bekannt ist, dass das Betriebssystem oder die Anwendung die PAC-Datei modifiziert: 

        -   Wenn der aufgelistete Dienst nicht über einen eigenen Autorisierungsdienst verfügt, handelt es sich um eine richtig positive Meldung. Dann sollten Sie den Prozess der Reaktion auf Sicherheitsfälle einleiten. Auch wenn der Angreifer keinen Erfolg dabei hatte, seine Berechtigungen in der Domäne zu erweitern, können Sie davon ausgehen, dass sich ein Angreifer in Ihrem Netzwerk befindet. Diesen sollten Sie so schnell wie möglich ausfindig machen, bevor er andere bekannte erweiterte persistente Angriffe startet, um seine Berechtigungen zu erweitern. 
        -   Wenn der in der Warnung aufgelistete Dienst über seinen eigenen Autorisierungsmechanismus verfügt, der Autorisierungsdaten verlangt, kann es sein, dass er fälschlicherweise als eine gefälschte PAC-Datei identifiziert wird.

## <a name="post-investigation"></a>Nachuntersuchung
Es wird von Microsoft empfohlen, ein professionelles Team zur Reaktion auf Sicherheitsfälle und zur Wiederherstellung einzusetzen, das Sie über das Microsoft-Kontoteam erreichen können. Dieses kann Ihnen dabei helfen, zu erkennen, ob ein Angreifer eine Persistenzmethode in Ihrem Netzwerk bereitgestellt hat.


## <a name="mitigation"></a>Maßnahme

Wenden Sie die Sicherheitsbulletins [MS14-068](https://technet.microsoft.com/library/security/MS14-068.aspx) und [MS11-013](https://technet.microsoft.com/library/security/ms11-013.aspx) an, die Sicherheitslücken in Kerberos-KDC behandeln. 


## <a name="see-also"></a>Siehe auch
- [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
