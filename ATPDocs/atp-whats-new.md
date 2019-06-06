---
title: Neuerungen in Azure Advanced Threat Protection (Azure ATP) | Microsoft-Dokumentation
description: Beschreibt die neuesten Releases von Azure ATP und enthält Informationen zu den Neuerungen in den einzelnen Version.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 05/27/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 7d0f33db-2513-4146-a395-290e001f4199
ms.reviewer: ort
ms.suite: ems
ms.openlocfilehash: 63a1dfa60d96e7f34cb406b0ccbc5a3584fbbb5b
ms.sourcegitcommit: 07abbd941d91299475df2af469ee5a9a99e07e0f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/28/2019
ms.locfileid: "66264931"
---
# <a name="whats-new-in-azure-atp"></a>Neuerungen in Azure ATP

## <a name="azure-atp-release-279"></a>Azure ATP Release 2.79
Veröffentlicht: 26. Mai 2019

- **Allgemeine Verfügbarkeit: Sicherheitsprinzipalreconnaissance (LDAP) (externe ID 2038)**

    Diese Warnung ist jetzt allgemein verfügbar. Weitere Informationen zu Warnung, Warnfeatures und empfohlenen Abhilfemaßnahmen und Schritten zur Vorbeugung finden Sie unter in der [Sicherheitsprinzipalreconnaissance (LDAP) – Warnungsbeschreibung](atp-reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038)

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-278"></a>Azure ATP Release 2.78

Veröffentlicht: 19. Mai 2019

- **Featureerweiterung: Sensible Entitäten**<br> Manuelles Kennzeichnen von Exchange-Servern als „sensibel“

    Sie können Entitäten jetzt manuell als Exchange-Server während der Konfiguration kennzeichnen.

    So kennzeichnen Sie eine Entität als Exchange-Server:
    1. Greifen Sie im Azure ATP-Portal auf das Menü **Konfiguration** zu.
    2. Wählen Sie unter **Erkennung** zunächst die Option **Entitätstags** und anschließend **sensibel** aus.
    3. Wählen Sie **Exchange-Server** aus, und fügen Sie dann die Entität hinzu, die Sie kennzeichnen möchten.

    Nach dem Kennzeichnen eines Computers als Exchange-Server wird dieser als „sensibel“ gekennzeichnet und zeigt an, dass er als Exchange-Server gekennzeichnet wurde.  Die Kennzeichnung „sensibel“ wird im Entitätsprofil des Computers angezeigt, und der Computer wird in allen Erkennungen berücksichtigt, die auf vertraulichen Konten und Lateral Movement-Pfaden basieren.

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-277"></a>Azure ATP Release 2.77

Veröffentlicht: 12. Mai 2019

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-276"></a>Azure ATP Release 2.76

Veröffentlicht: 6. Mai 2019

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-275"></a>Azure ATP Release 2.75

Veröffentlicht: 28. April 2019

- **Featureerweiterung: Sensible Entitäten**<br> Ab dieser Version (2.75) werden die von Azure ATP als Exchange-Server identifizierte Computer nun automatisch als **Sensibel** gekennzeichnet.  

    Entitäten, die automatisch als **Sensibel** gekennzeichnet werden, da sie als Exchange-Server fungieren, führen diese Klassifizierung als Grund für die Kennzeichnung auf. 

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-274"></a>Azure ATP Release 2.74

Wird am 14. April 2019 veröffentlicht

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-273"></a>Azure ATP Release 2.73

Wird am 10. April 2019 veröffentlicht

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-272"></a>Azure ATP Release 2.72

Veröffentlicht: 31. März 2019

- **Featureerweiterung: Durch Lateral-Movement-Pfad (LMP) eingeschränkte Tiefe**<br>
Lateral-Movement-Pfade (LMP) sind eine wichtige Methode für die Ermittlung von Bedrohungen und Risiken in Azure ATP. Um sich auf die kritischen Risiken für Ihre sensibelsten Benutzer zu konzentrieren, macht es dieses Update einfacher und schneller, Risiken für die sensiblen Benutzer in jedem LMP zu analysieren und zu beseitigen, indem Umfang und Tiefe der einzelnen angezeigten Graphen begrenzt werden.   

    Unter [Lateral-Movement-Pfade](use-case-lateral-movement-path.md) erfahren Sie mehr darüber, wie Azure ATP LMPs verwendet, um Zugriffsrisiken für jede Entität in Ihrer Umgebung zu vermeiden.   

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-271"></a>Azure ATP Release 2.71

Veröffentlicht: 24. März 2019

- **Featureerweiterung: Überwachungsbenachrichtigungen der Netzwerknamensauflösung (Network Name Resolution, NNR)**<br>
Überwachungswarnungen wurden für Konfidenzniveaus hinzugefügt, die Azure ATP-Sicherheitswarnungen zugeordnet sind, die sich auf NNR beziehen. Jede Überwachungswarnung enthält umsetzbare und ausführliche Empfehlungen, wie Abhilfe bei niedriger NNR-Erfolgsquote geschaffen werden kann. 

    Informationen dazu, wie Azure ATP NNR verwendet und warum dies für die Genauigkeit von Warnungen wichtig ist, finden Sie unter [Was ist Netzwerknamensauflösung](atp-nnr-policy.md). 

- **Serverunterstützung: Es wurde Unterstützung für Server 2019 mithilfe von KB4487044 hinzugefügt**<br>
Es wurde Unterstützung für die Verwendung von Windows Server-2019 mit dem Patchlevel KB4487044 hinzugefügt. Die Verwendung von Server 2019 ohne den Patch wird nicht unterstützt und kann aus diesem Update nicht gestartet werden. 

- **Featureerweiterung: Benutzerbasierter Ausschluss von Warnungen**<br>
Erweiterte Ausschlussoptionen ermöglichen jetzt den Ausschluss bestimmter Benutzer von bestimmten Warnungen. Ein solcher Ausschluss kann Situationen vermeiden helfen, in denen die Verwendung oder Konfiguration bestimmter Typen von interner Software wiederholt gutartige Sicherheitswarnungen auslöst.

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-270"></a>Azure ATP Release 2.70
Veröffentlicht: 17. März 2019

- **Featureerweiterung: Der Vertrauensgrad der Auflösung des Netzwerknamens (Network Name Resolution, NNR) wurde mehreren Warnungen hinzugefügt**<br> Die Auflösung des Netzwerknamens wird verwendet, um die Identität der Quellentität vermuteter Angriffe eindeutig zu bestimmen. Durch Hinzufügen des NNR-Vertrauensgrads zur Beweisliste für Sicherheitswarnungen von Azure ATP können Sie nun sofort auf den NNR-Vertrauensgrad, der in Zusammenhang mit den möglichen identifizierten Quellen steht, zugreifen, diesen nachvollziehen und entsprechende Korrekturen durchführen. 

    Der Beweis für den NNR-Vertrauensgrad wurde den folgenden Warnungen hinzugefügt:
  - [Network mapping reconnaissance (DNS) (Reconnaissance über Netzwerkzuordnung (DNS))](atp-reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)
  - [Suspected identity theft (Pass-the-Ticket) (Verdacht auf Identitätsdiebstahl (Pass-the-Ticket))](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-ticket-external-id-2018) 
  - [Suspected NTLM relay attack (Exchange account) - preview (Vermuteter NTLM-Relaisangriff (Exchange-Konto) – Vorschauversion)](atp-lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037---preview)
  - [Suspected DCSync attack (replication of directory services) (Verdacht auf einen DCSync-Angriff (Replikation von Verzeichnisdiensten))](atp-domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006)

- **Zusätzliches Szenario zu Integritätswarnungen: Fehler beim Starten des Azure ATP-Sensordiensts**<br>Für Instanzen, bei denen der Azure ATP-Sensordienst aufgrund eines Problems mit dem Treiber für die Netzwerkerfassung nicht gestartet werden konnte, wird nun eine Warnung für die Sensorintegrität ausgelöst. Weitere Informationen zu Azure ATP-Protokollen und deren Verwendung finden Sie unter [Troubleshooting Azure ATP sensor with Azure ATP logs (Problembehandlung eines Azure ATP-Sensors mit Azure ATP-Protokollen)](troubleshooting-atp-using-logs.md). 
  
- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-269"></a>Azure ATP Release 2.69
Veröffentlicht: 10. März 2019

- **Featureerweiterung: Vermuteter Identitätsdiebstahl (Pass-the-Ticket)**<br> Diese Warnung enthält nun neue Details zu Verbindungen, die mithilfe des Remotedesktopprotokolls (RDP) hergestellt wurden. Durch diese zusätzlichen Details lässt sich das bekannte Problem der B-TP-Warnungen (Benign true positive, unbedenklich richtig positiv) korrigieren, die durch die Verwendung von Remote Credential Guard bei RDP-Verbindungen verursacht werden. 

- **Featureerweiterung: Remotecodeausführung über DNS-Warnung**<br> Diese Warnung enthält nun weitere Sicherheitsupdatestatus Ihres Domänencontrollers, und Sie werden darüber informiert, wenn Updates erforderlich sind.   

- **Neues Dokumentationsfeature: Azure ATP-Sicherheitswarnungen mit MITRE ATT&CK Matrix™**<br>

    Zur Erläuterung und einfacheren Zuordnung der Beziehung zwischen Azure ATP-Sicherheitswarnungen und der bekannten MITRE ATT&CK Matrix haben wir die relevanten MITRE-Methoden zur Liste der Azure ATP-Sicherheitswarnungen hinzugefügt. Durch diesen zusätzlichen Verweis lässt sich die vermutete Angriffsmethode leichter verstehen, die beim Auslösen einer Azure ATP-Sicherheitswarnung möglicherweise verwendet wird. Erfahren Sie mehr über den [Leitfaden zu Azure ATP-Sicherheitswarnungen](suspicious-activity-guide.md).  

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-268"></a>Azure ATP Release 2.68
Veröffentlicht: 3. März 2019

- **Featureerweiterung: Suspected Brute Force attack (LDAP) alert** (Warnung bei Verdacht auf einen Brute-Force-Angriff (LDAP))<br>
Die Benutzerfreundlichkeit dieser Sicherheitswarnung wurde erheblich verbessert. Zu den Verbesserungen zählen u.a. eine überarbeitete Beschreibung, die Bereitstellung zusätzlicher Quellinformationen, neue Infografiken und Details zu Rateversuchen, um eine schnellere Behebung zu erreichen. Erfahren Sie mehr zu Sicherheitswarnungen für [Suspected Brute Force attack (LDAP)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-ldap-external-id-2004) (Verdacht auf einen Brute-Force-Angriff (LDAP)) 

- **Neues Dokumentationsfeature: Sicherheitswarnungsumgebung**<br>

    Um die Leistungsfähigkeit von Azure ATP bei der Erkennung der tatsächlichen Bedrohungen für Ihre Arbeitsumgebung zu erklären, haben wir dieser Dokumentation eine neue **Sicherheitswarnungsumgebung** hinzugefügt. Die **Sicherheitswarnungsumgebung** hilft Ihnen, schnell ein Labor oder eine Testumgebung einzurichten, und erklärt die beste Verteidigung gegen gängige, realitätsnahe Bedrohungen und Angriffe.  

    Das [Schritt-für-Schritt-Umgebung](atp-playbook-lab-overview.md) wurde entwickelt, um sicherzustellen, dass Sie nur wenig Zeit für den Aufbau aufwenden und mehr Zeit investieren können, sich über Ihre Bedrohungslage und die verfügbaren Azure ATP-Warnmeldungen und den Schutz zu informieren. Wir freuen uns auf Ihr Feedback.

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-267"></a>Azure ATP Release 2.67
Veröffentlichung: 24. Februar 2019

- **Neue Sicherheitswarnung: Sicherheitsprinzipalreconnaissance (LDAP) – Vorschauversion**<br>

    [Sicherheitsprinzipalreconnaissance (LDAP) – Vorschauversion](atp-reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038)-Sicherheitswarnung für Azure ATP ist jetzt als öffentliche Vorschauversion verfügbar. <br> In dieser Erkennung wird eine Azure ATP-Sicherheitswarnung ausgelöst, wenn Sicherheitsprinzipalreconnaissance von Angreifern verwendet wird, um wichtige Informationen über die Domänenumgebung zu erlangen. Diese Informationen helfen Angreifern, die Domänenstruktur zu erfassen, und identifizieren auch privilegierte Konten für die Verwendung in späteren Schritten in ihrer Angriffsabwehrkette. 

    Lightweight Directory Access Protocol (LDAP) ist eine der sowohl für zulässige als auch böswillige Zwecke am häufigsten verwendeten Methoden zum Abfragen von Active Directory. LDAP-fokussierte Sicherheitsprinzipalreconnaissance wird häufig als erste Phase eines Kerberoasting-Angriffs verwendet. Mit Kerberoasting-Angriffen wird eine Zielliste von Sicherheitsprinzipalnamen (Security Principal Names, SPNs) abgerufen, für die Angreifer dann versuchen, Ticket Granting Server-Tickets (TGS) zu erhalten.

- **Featureerweiterung: Reconnaissance über Kontoauflistung (NTLM)** <br> 
    Verbesserte **Reconnaissance über Kontoauflistung (NTLM)** -Warnung, die zusätzliche Analysen und verbesserte Erkennungslogik zum Reduzieren von **B-TP**- und **FP**-Warnungsergebnissen verwendet. 
 
- **Featureerweiterung: „Reconnaissance über Netzwerkzuordnung“-Warnung (DNS)** <br>
    Neue Typen von Erkennungen wurden „Reconnaissance über Netzwerkzuordnung“-Warnungen (DNS) hinzugefügt. Außer verdächtigen AXFR-Anfragen erkennt Azure ATP jetzt verdächtige Typen von Anforderungen von Nicht-DNS-Servern, die eine übermäßige Anzahl von Anforderungen verwenden.

 - Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-266"></a>Azure ATP Release 2.66
Veröffentlichung: 17. Februar 2019

- **Featureerweiterung: Vermuteter DCSync-Angriff (Replikation der Verzeichnisdienste)**<br>
Die Benutzerfreundlichkeit dieser Sicherheitswarnung wurde verbessert. Zu den Verbesserungen zählen u.a. eine überarbeitete Beschreibung, die Bereitstellung zusätzlicher Quellinformationen, neue Infografiken und mehr Nachweisinformationen. Erfahren Sie mehr über die Sicherheitswarnung [Vermuteter DCSync-Angriff (Replikation der Verzeichnisdienste)](atp-domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006). 

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-265"></a>Azure ATP, Release 2.65
Veröffentlichung: 10. Februar 2019

- **Neue Sicherheitswarnung: Suspected NTLM relay attack (Exchange account) - preview** (Vermuteter NTLM-Relaisangriff (Exchange-Konto) – Vorschauversion)<br>
Die Azure ATP-Sicherheitswarnung [Suspected NTLM relay attack (Exchange account) - preview](atp-lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037---preview) (Vermuteter NTLM-Relaisangriff (Exchange-Konto) – Vorschauversion) ist jetzt als öffentliche Vorschauversion verfügbar. <br> Hierbei wird eine Azure ATP-Sicherheitswarnung ausgelöst, wenn ermittelt wird, dass die Anmeldeinformationen eines Exchange-Kontos von einer verdächtigen Quelle verwendet werden. Bei solchen Angriffen werden NTLM-Relaistechniken verwendet, um die Exchange-Berechtigungen eines Domänencontrollers zu erlangen. Sie werden deshalb als **PrivExchange** bezeichnet. Weitere Informationen zur **PrivExchange**-Technik erhalten Sie in der [Sicherheitsempfehlung ADV190007](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/ADV190007) (Erstveröffentlichung: 31. Januar 2019) und im Blogbeitrag zur [Reaktion auf Warnungen in Azure ATP](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/How-to-win-the-latest-security-race-over-NTLM-relay/ba-p/334511).  

- **Allgemeine Verfügbarkeit: Remotecodeausführung über DNS**<br>
Diese Warnung ist jetzt allgemein verfügbar. Weitere Informationen und Warnungsfeatures finden Sie auf der Beschreibungsseite zur Warnung [Remotecodeausführung über DNS](atp-lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036). 

- **Allgemeine Verfügbarkeit: Datenexfiltration über den SMB**<br>
Diese Warnung ist jetzt allgemein verfügbar. Weitere Informationen und Warnungsfeatures finden Sie auf der Beschreibungsseite zur Warnung [Datenexfiltration über SMB](atp-exfiltration-alerts.md#data-exfiltration-over-smb-external-id-2030).


- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-264"></a>Azure ATP Release 2.64
Veröffentlicht: 4. Februar 2019

- **Allgemeine Verfügbarkeit: Vermutete Golden Ticket-Verwendung (Ticketanomalie)**<br>
Diese Warnung ist jetzt allgemein verfügbar. Weitere Informationen und Warnungsfeatures finden Sie auf der Beschreibungsseite zur Warnung [Vermutete Golden Ticket-Verwendung (Ticketanomalie)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-external-id-2032). 

- **Featureerweiterung: Reconnaissance über Netzwerkzuordnung (DNS)**<br>
Verbesserte Erkennungslogik für diese Warnung, um falsch-positive Ergebnisse zu minimieren und eine zu hohe Anzahl von Warnungen zu vermeiden. Für diese Warnung gilt ab sofort eine Lernphase von acht Tagen, bevor die Warnung möglicherweise zum ersten Mal ausgelöst wird. Weitere Informationen zu dieser Warnung finden Sie auf der Beschreibungsseite zur Warnung [Reconnaissance über Netzwerkzuordnung (DNS)](atp-reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007). 

    **Aufgrund der Verbesserung dieser Warnung sollte die nslookup-Methode nicht mehr verwendet werden, um die Azure ATP-Konnektivität während der Erstkonfiguration zu testen.** 

- **Featureerweiterung:**<br>
Diese Version umfasst neu gestaltete Warnungsseiten und neue Nachweise, die eine bessere Untersuchung der Warnungen ermöglichen. 
    - [Suspected Brute Force attack (SMB) (Verdacht auf einen Brute-Force-Angriff (SMB))](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033)
    - [Vermutete Golden Ticket-Verwendung (Ticketanomalie): Beschreibungsseite zur Warnung](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-time-anomaly-external-id-2022)
    - [Suspected overpass-the-hash attack (Kerberos) (Verdacht auf einen Overpass-the-Hash-Angriff (Kerberos))](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-kerberos-external-id-2002)
    - [Suspected use of Metasploit hacking framework (Verdacht auf Verwendung eines Hackerframeworks)](atp-compromised-credentials-alerts.md#suspected-use-of-metasploit-hacking-framework-external-id-2034)
    - [Suspected WannaCry ransomware attack (Verdacht auf einen WannaCry-Ransomangriff)](atp-compromised-credentials-alerts.md#suspected-wannacry-ransomware-attack-external-id-2035)

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.


## <a name="azure-atp-release-263"></a>Azure ATP Release 2.63
Veröffentlicht am 27. Januar 2019

- **Neues Feature: Unterstützung nicht vertrauenswürdiger Gesamtstrukturen (Preview)**<br>
Die Azure ATP-Unterstützung von Sensoren in nicht vertrauenswürdigen Gesamtstrukturen befindet sich nun in der Public Preview. Über die **Verzeichnisdienste**-Seite im Azure ATP-Portal können Sie zusätzliche Anmeldeinformationen konfigurieren, um Azure ATP-Sensoren zu ermöglichen, Verbindungen mit verschiedenen Active Directory-Gesamtstrukturen herzustellen und Informationen an den Azure ATP-Dienst zurückzugeben. Weitere Informationen finden Sie unter [Azure ATP für mehrere Gesamtstrukturen](atp-multi-forest.md). 

- **Neues Feature: Abdeckung des Domänencontrollers**<br>
Azure ATP stellt nun Abdeckungsinformationen für überwachte Azure ATP-Domänencontroller bereit.  
Sie können die Anzahl der überwachten und nicht überwachten Domänencontroller, die Azure ATP in Ihrer Umgebung ermittelt hat, auf der Seite **Sensoren** im Azure ATP-Portal anzeigen. Laden Sie die Liste der überwachten Domänencontroller für weitere Analysen herunter, und erstellen Sie einen Aktionsplan. Weitere Informationen finden Sie in der Vorgehensweise zum [Überwachen von Domänencontrollern](atp-sensor-monitoring.md). 

- **Featureerweiterung: Reconnaissance mithilfe von Kontoenumeration**<br>
Die Ermittlung der Reconnaissance mithilfe der Azure ATP-Kontoenumeration ermittelt und löst Warnungen bei Enumerationsangriffen mit Kerberos und NTLM aus. Zuvor wurden nur Versuche mit Kerberos ermittelt. Weitere Informationen finden Sie unter [Azure ATP-Warnungen zur Reconnaissance](atp-reconnaissance-alerts.md#account-enumeration-reconnaissance-external-id-2003). 

- **Featureerweiterung: Warnung für versuchte Remotecodeausführung**<br>
    - Jegliche Aktivitäten bezüglich der Remoteausführung, z. B. Diensterstellung, WMI-Ausführung und die neue **PowerShell**-Ausführung, wurden zur Profilzeitachse von Zielcomputern hinzugefügt. Der Zielcomputer ist der Domänencontroller, auf dem der Befehl ausgeführt wurde. 
    - Die **PowerShell**-Ausführung wurde zur Aktivitätsliste der Remotecodeausführungen hinzugefügt, die im Entitätsprofil auf der Zeitachse für Warnungen aufgeführt werden.
    - Weitere Informationen finden Sie unter [Versuch der Remotecodeausführung](atp-domain-dominance-alerts.md#remote-code-execution-attempt-external-id-2019).  

- **Windows Server 2019-LSASS-Problem und Azure ATP**<br>
Gemäß des Kundenfeedbacks zur Nutzung von Azure ATP mit Domänencontrollern, auf denen Windows Server 2019 ausgeführt wird, enthält dieses Update weitere Logik zur Vermeidung des gemeldeten Verhaltens auf Windows Server 2019-Computern. Die vollständige Unterstützung von Azure ATP-Sensoren unter Windows Server 2019 ist für ein zukünftiges Azure ATP-Update geplant. Das Installieren und Ausführen von Azure ATP unter Windows Server 2019 wird derzeit **nicht** unterstützt. Weitere Informationen finden Sie unter [Voraussetzungen für den Azure ATP-Sensor](atp-prerequisites.md#azure-atp-sensor-requirements). 

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.


## <a name="azure-atp-release-262"></a>Azure ATP Release 2.62
Veröffentlicht am 20. Januar 2019

- **Neue Sicherheitswarnung: Remotecodeausführung über DNS (Preview)**<br>
Die Azure ATP-Sicherheitswarnung [Remotecodeausführung über DNS](atp-lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036) ist nun in der öffentlichen Vorschauversion verfügbar. <br> Bei dieser Erkennung wird eine Azure ATP-Sicherheitswarnung ausgelöst, wenn DNS-Abfragen an einen Domänencontroller im Netzwerk gerichtet werden, die im Verdacht stehen, die Sicherheitslücke [CVE-2018-8626](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2018-8626) auszunutzen.

- **Featureerweiterung: Um 72 Stunden verzögertes Sensorupdate** <br> Geänderte Option, damit nach jedem Releaseupdate von Azure ATP die Updates für ausgewählte Sensoren um 72 Stunden (anstelle der vorherigen 24-Stunden-Verzögerung) verzögert werden. Anweisungen zur Konfiguration finden Sie unter [Update für Azure ATP-Sensoren](sensor-update.md). 


- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-261"></a>Azure ATP Release 2.61
Veröffentlicht: 13. Januar 2019

- **Neue Sicherheitswarnung: Data exfiltration over SMB (Datenexfiltration über SMB) (Vorschauversion)**<br>
Die Azure ATP-Sicherheitswarnung [Data exfiltration over SMB](atp-exfiltration-alerts.md) (Datenexfiltration über SMB) ist nun in der öffentlichen Vorschauversion enthalten. <br> Angreifer mit Domänenadministratorrechten können das KRBTGT-Konto beeinträchtigen. Angreifer können das KRBTGT-Konto verwenden, um ein Kerberos Ticket Granting Ticket (TGT) zu erstellen, das die Autorisierung für jede beliebige Ressource erlaubt. 


- **Featureerweiterung: Remote code execution attempt (Versuchte Remotecodeausführung)** Sicherheitswarnung <br> Eine neue Warnungsbeschreibung und ein zusätzlicher Beweis sind hinzugefügt worden, damit die Warnung einfacher zu verstehen ist, und um bessere Untersuchungsworkflows zu bieten. 


- **Featureerweiterung: DNS query logical activities (Logische Aktivitäten zur DNS-Abfrage)** <br>Weitere Abfragetypen sind den [von Azure ATP überwachten Aktivitäten](monitored-activities.md) hinzugefügt worden. Darunter die folgenden: **TXT**, **MX**, **NS**, **SRV**, **ANY**, **DNSKEY**. 

- **Featureerweiterung: Suspected Golden Ticket usage (ticket anomaly) (Verdacht auf Verwendung eines Golden Ticket (anomalie)) und Suspected Golden Ticket usage (nonexistent account) (Verdacht auf Verwendung eines Golden Ticket (nicht vorhandenes Ticket))** <br>
Eine verbesserte Erkennungslogik wurde für beide Warnungen angewendet, um die Anzahl von FP-Warnungen zu reduzieren und genauere Ergebnisse zu liefern.

- **Featureerweiterung: Dokumentation zu Azure ATP-Sicherheitswarnungen** <br>
Die Dokumentation zu Azure ATP-Sicherheitswarnungen ist optimiert und erweitert worden, um bessere Warnungsbeschreibungen, genauere Klassifizierungen sowie Erklärungen zu Beweisen und Abhilfe- und Präventionsmaßnahmen einzuschließen. Lernen Sie über die folgenden Links das neuen Design der Dokumentation zu Sicherheitswarnungen kennen: 
    - [Azure ATP-Sicherheitswarnungen](suspicious-activity-guide.md)
    - [Verstehen von Sicherheitswarnungen](understanding-security-alerts.md)
        - [Warnung zu Reconnaissancephase](atp-reconnaissance-alerts.md)
        - [Warnungen zu Phase der kompromittierten Anmeldeinformationen](atp-compromised-credentials-alerts.md)
        - [Lateral movement phase alerts (Warnung zur Lateral Movement-Phase)](atp-lateral-movement-alerts.md)
        - [Warnungen zu Domänendominanzphase](atp-domain-dominance-alerts.md)
        - [Warnungen zu Exfiltrationsphase](atp-exfiltration-alerts.md)
    - [Untersuchen eines Computers](investigate-a-computer.md)
    - [Untersuchen eines Benutzers](investigate-a-user.md)

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.


## <a name="azure-atp-release-260"></a>Azure ATP, Release 2.60
Veröffentlichung am 6. Januar 2019

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-259"></a>Azure ATP, Release 2.59
Am 16. Dezember 2018 veröffentlicht

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.


## <a name="azure-atp-release-258"></a>Azure ATP, Release 2.58

Veröffentlicht am 9. Dezember 2018

- **Erweiterung von Sicherheitswarnungen: Aufteilung der Warnung zu ungewöhnlichen Protokollimplementierungen**<br>
Die Azure ATP-Serie von Sicherheitswarnungen zu ungewöhnlichen Protokollimplementierungen, die zuvor eine externalId (2002) gemeinsam genutzt haben, ist jetzt in vier verschiedene Warnungen aufgeteilt, die jeweils eine eindeutige externe ID aufweisen. 

### <a name="new-alert-externalids"></a>Neue externalIds für Warnungen

> [!div class="mx-tableFixed"] 

|Neuer Sicherheitswarnungsname|Alter Sicherheitswarnungsname|Eindeutige externe ID|
|---------|----------|---------|
|Suspected Brute Force attack (SMB) (Verdacht auf einen Brute-Force-Angriff (SMB))|Ungewöhnliche Protokollimplementierung (potenzielle Verwendung schädlicher Tools wie Hydra)|2033
|Suspected overpass-the-hash attack (Kerberos) (Verdacht auf einen Overpass-the-Hash-Angriff (Kerberos))|Ungewöhnliche Kerberos-Protokollimplementierung (potenzieller Overpass-the-Hash-Angriff)|2002|
|Suspected use of Metasploit hacking framework (Verdacht auf Verwendung eines Hackerframeworks)|Ungewöhnliche Protokollimplementierung (potenzielle Verwendung schädlicher Hackertools wie Metasploit)|2034
|Suspected WannaCry ransomware attack (Verdacht auf einen WannaCry-Ransomangriff)|Ungewöhnliche Protokollimplementierung (potenzieller WannaCry-Ransomwareangriff)|2035
|

- **Neue überwachte Aktivität: Dateikopie über SMB**<br>
Das Kopieren von Dateien über SMB ist jetzt eine überwachte und filterbare Aktivität. Erfahren Sie mehr über [von Azure ATP überwachte Aktivitäten](monitored-activities.md) und über das [Filtern von und Suchen nach überwachten Aktivitäten](atp-activities-search.md) im Portal. 

- **Imageerweiterung für lange Lateral Movement-Pfade**<br>
Beim Anzeigen von langen Lateral Movement-Pfaden hebt Azure ATP jetzt nur die Knoten hervor, die mit einer ausgewählten Entität verbunden sind, anstatt die anderen Knoten unscharf darzustellen. Diese Änderung führt zu einer erheblichen Beschleunigung beim Rendern von langen Lateral Movement-Pfaden. 

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-257"></a>Azure ATP Release 2.57
Veröffentlicht am 2. Dezember 2018

- **Neue Sicherheitswarnung: Verdacht auf Verwendung eines Golden Ticket – Ticketanomalie (Vorschau)**<br>
Die Azure ATP-Sicherheitswarnung [Verdacht auf Verwendung eines Golden Ticket – Ticketanomalie](suspicious-activity-guide.md) ist jetzt in der öffentlichen Vorschau verfügbar. <br> Angreifer mit Domänenadministratorrechten können das KRBTGT-Konto beeinträchtigen. Angreifer können das KRBTGT-Konto verwenden, um ein Kerberos Ticket Granting Ticket (TGT) zu erstellen, das Autorisierung für jede beliebige Ressource bietet. 
<br>Ein gefälschtes TGT wird als „Golden Ticket“ bezeichnet, da Angreifer damit dauerhafte Netzwerkpersistenz erlangen. Gefälschte Golden Tickets dieses Typs weisen eindeutige Merkmale auf, für deren Identifikation diese neue Erkennung konzipiert ist. 


- **Featureerweiterung: Automatisierte Erstellung von Azure ATP-Instanzen (Arbeitsbereichen)** <br>
Ab heute heißen Azure ATP-*Arbeitsbereiche* Azure ATP-*Instanzen*. Azure ATP unterstützt jetzt eine Azure ATP-Instanz pro Azure ATP-Konto. Instanzen für neue Kunden werden mithilfe des Assistenten für die Instanzenerstellung im [Azure ATP-Portal](https://portal.atp.azure.com) erstellt. Vorhandene Azure ATP-Arbeitsbereiche werden mit diesem Update automatisch in Azure ATP-Instanzen konvertiert.  

  - Vereinfachte Instanzerstellung für schnellere Bereitstellung und Schutz mit [Erstellung Ihrer Azure ATP-Instanz](install-atp-step1.md) 
  - Alle [Anforderungen an Datenschutz und Compliance](atp-privacy-compliance.md) bleiben unverändert. 

  Weitere Informationen zu Azure ATP-Instanzen finden Sie unter [Create your Azure ATP instance (Erstellen Ihrer Azure ATP-Instanz)](install-atp-step1.md). 

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-256"></a>Azure ATP Release 2.56
Veröffentlicht: 25. November 2018


- **Featureerweiterung: Lateral Movement-Pfade (LMPs)** <br>
Zwei zusätzliche Funktionen wurden hinzugefügt, um die Fähigkeiten von Azure ATP Lateral Movement-Pfaden (LMP) zu verbessern:

  - Der LMP-Verlauf wird jetzt pro Entität gespeichert und erkannt, und bei der Verwendung von LMP-Berichten. 
  - Verfolgen Sie eine Entität in einem LMP über die Aktivitätszeitachse und nehmen Sie die Untersuchung anhand zusätzlicher Beweise vor, die für die Ermittlung potenzieller Angriffspfade zur Verfügung stehen. 

  Weitere Informationen zur Verwendung und Untersuchung mit verbesserten LMPs finden Sie unter [Azure ATP Lateral Movement-Pfade](use-case-lateral-movement-path.md). 

- **Erweiterungen der Dokumentation: Lateral Movement-Pfade, Namen von Sicherheitswarnungen**<br> Es wurden Ergänzungen und Aktualisierungen zu Azure ATP-Artikeln vorgenommen, die Beschreibungen und Funktionen des Lateral Movement-Pfads beschreiben, und es wurde eine Namenszuordnung von alten Namen von Sicherheitswarnungen zu den neuen Namen und externe IDs hinzugefügt. 
  - Weitere Informationen finden Sie unter [Azure ATP Lateral Movement-Pfade](use-case-lateral-movement-path.md), [Untersuchen von Lateral Movement-Pfaden](investigate-lateral-movement-path.md) und [Leitfaden für Sicherheitswarnungen](suspicious-activity-guide.md).   

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-255"></a>Azure ATP Release 2.55
Veröffentlicht: 18. November 2018

- **Sicherheitswarnung: Verdächtige Kommunikation über DNS – allgemeine Verfügbarkeit**<br>
Der Azure ATP-Sicherheitshinweis [Verdächtige Kommunikation über DNS](suspicious-activity-guide.md) ist jetzt allgemein verfügbar. <br> In den meisten Organisationen wird das DNS-Protokoll nicht überwacht und nur selten vor böswilligen Angriffen geschützt. Das gibt einem Angreifer auf einem kompromittierten Computer die Möglichkeit, das DNS-Protokoll zu missbrauchen. Schädliche Kommunikation über DNS kann für Datenexfiltration, Command-and-Control-Zugriff und/oder zur Umgehung von Einschränkungen des Unternehmensnetzwerks verwendet werden.

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-254"></a>Azure ATP Release 2.54
Veröffentlicht am 11. November 2018

- **Featureerweiterung: Standarddomänenausschlüsse zur Warnung aufgrund verdächtiger Kommunikation über DNS hinzugefügt**<br>   Es wurden drei beliebte Domänen zur Ausschlussliste der Standarddomäne hinzugefügt. Die Ausschlussliste bleibt vollständig anpassbar. Weitere Informationen finden Sie unter [Ausschließen von Entitäten von der Erkennung](excluding-entities-from-detections.md) 

- **Erweiterungen der Dokumentation: SIEM-Protokollaktualisierung, Leitfaden zu bekannten Problemen**<br>    Die externalId-Zuordnung sowie zusätzliche Erläuterungen wurden den Beschreibungen des SIEM-Protokolls hinzugefügt. Weitere Informationen finden Sie in der [Referenz zum SIEM-Protokoll](cef-format-sa.md). <br>Es wurde ein neuer Artikel zum Leitfaden für derzeit bekannte Probleme hinzugefügt. Weitere Informationen finden Sie unter: [Azure ATP Known Issues (Azure ATP: Bekannte Probleme)](known-issues.md).  

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-253"></a>Azure ATP Release 2.53
Veröffentlicht: 4. November 2018

- **Erweiterung von Sicherheitswarnungen: Verdächtiger Authentifizierungsfehler**<br>
[Sicherheitswarnungen zu verdächtigen Authentifizierungsfehlern](suspicious-activity-guide.md) in Azure ATP umfassen nun die Überwachung für die Erkennung von Kennwort-Spray- oder Brute-Force-Angriffen.
Bei einem typischen **Kennwort-Spray-Angriff** testen Angreifer nach erfolgreichem Durchzählen einer Liste von gültigen Benutzern aus dem Domänencontroller EIN sorgfältig erstelltes Kennwort für ALLE bekannten Benutzerkonten (ein Kennwort für n Konten). Wenn beim ersten Kennwort-Spray-Angriff ein Fehler auftritt, wiederholen sie den Vorgang mit einem anderen sorgfältig erstellten Kennwort – normalerweise nach einer Wartezeit von 30 Minuten zwischen den Versuchen. Durch die Wartezeit verhindern Angreifer, dass meist zeitbasierte Schwellenwerte für die Kontosperre ausgelöst werden. Kennwort-Spray-Angriffe haben sich rasch zu einer beliebten Methode unter Angreifern und Pen-Testern entwickelt. Kennwort-Spray-Angriffe haben sich als effektiv erwiesen, um innerhalb einer Organisation einen Ankerpunkt zu finden und infolgedessen weitere Schwachstellen auszunutzen, um Berechtigungen auszuweiten. 

- **Featureerweiterung: Senden einer Syslog-Testnachricht**<br>   Ab sofort gibt es eine neue Möglichkeit, um eine Syslog-Testnachricht während des SIEM-Setupvorgangs zu senden. Weitere Informationen finden Sie unter [Integration in Syslog](setting-syslog.md). 

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-252"></a>Azure ATP Release 2.52
Veröffentlicht: 28. Oktober 2018


- **Erweiterung von Sicherheitswarnungen: Versuchte Remotecodeausführung**<br>
Die [Sicherheitswarnung zur versuchten Remotecodeausführung](suspicious-activity-guide.md) in Azure ATP umfasst jetzt die Überwachung auf verdächtige Versuche, PowerShell-Remotecode auf Ihren Domänencontrollern auszuführen. Remote-PowerShell ist eine gängige Methode zur Ausführung gültiger administrativer Befehle, wird aber häufig in böswilliger Absicht dazu verwendet, Skripts auf Remoteendpunkten auszuführen. 

- **Featureerweiterung: Festlegen der Berichtszeitplanung**
<br>Jetzt können Sie eine bestimmte Uhrzeit festlegen, um Ihre Azure ATP-Berichte über die Funktion [reports](reports.md#) zu planen. 

- **Ergänzung der Konfiguration: Rollenbasierte Zugriffssteuerung für Mandanten (RBAC)**
<br>Konfigurieren Sie die Sicherheitsrollen Ihres Mandanten im Azure Active Directory (AAD) Admin Center direkt über den neuen Administratorlink im Azure ATP-Portal. 

- **Überarbeitete Struktur und Inhalte der Dokumentation**
<br>Zu den neuesten inhaltlichen Änderungen an der Azure ATP-Dokumentation gehören neue Artikel, die eine vollständige Liste mit allen in Azure ATP überwachten Aktivitäten sowie Anweisungen zur Aktivitätsfilterung umfassen, sowie eine Neugestaltung der Struktur der Dokumentationswebsite zur Verbesserung der Benutzerfreundlichkeit:
  - [Von Azure ATP überwachte Aktivitäten](monitored-activities.md) 
  - [Azure ATP-Aktivitätsfilterung](atp-activities-search.md) 
  - [Azure ATP-Dokumentation](https://docs.microsoft.com/azure-advanced-threat-protection/)  

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-251"></a>Azure ATP Release 2.51
Veröffentlicht: 21. Oktober 2018

- Sie können die Integration von **WD-ATP** über den Bildschirm [Konfiguration](integrate-wd-atp.md#how-to-integrate-azure-atp-with-windows-defender-atp) im Azure ATP-Portal aktivieren oder deaktivieren. (Hierfür muss der Azure ATP-Benutzer ein globaler Administrator oder ein Sicherheitsadministrator im AAD-Mandanten sein.)

- Diese Version enthält ebenfalls Verbesserungen und Fehlerbehebungen für die interne Sensorinfrastruktur.

## <a name="azure-atp-release-250"></a>Azure ATP Release 2.50
Veröffentlicht: 14. Oktober 2018
- Diese Version enthält Fehlerbehebungen und Verbesserungen für mehrere Probleme.


## <a name="azure-atp-release-249"></a>Azure ATP Release 2.49
Veröffentlicht: 7. Oktober 2018
-   **Neue Erkennungen: Verdächtige DNS-Kommunikation** (Vorschau)<br>Es wurde eine neue Erkennung hinzugefügt, um vor verdächtigen DNS-Kommunikationsangriffen zu schützen:

    -   Diese Erkennung hilft dabei, Angriffe gegen das DNS-Protokoll zu erkennen: In den meisten Organisationen wird das DNS-Protokoll nicht überwacht und nur selten vor böswilligen Angriffen geschützt. Das gibt einem Angreifer auf einem kompromittierten Computer die Möglichkeit, das DNS-Protokoll zu missbrauchen. Böswillige Kommunikation über DNS kann zur Datenexfiltration, Zugriff über Command-and-Control-Server und/oder zur Umgehung von Netzwerkeinschränkungen führen.

- **Neue Funktionen** <br>Die Azure ATP-**Benutzerrolle** wurde mit den folgenden Funktionen verbessert:
  - Der Status der Sicherheitswarnungen kann geändert werden (erneut öffnen, schließen, ausschließen, unterdrücken)
  - Geplante Berichte wurden festgelegt
  - Entitätstags (vertraulich und Honeytoken) können festgelegt werden.
  - Ausschluss von Erkennung
  - Ändern der Sprache
  - Benachrichtigung über E-Mail oder Syslog wurden festgelegt


- Sicherheitswarnungen des Typs **Reconnaissance mithilfe von Verzeichnisdienstabfragen**, die am 16. September 2018 kurzzeitig vermehrt aufgetreten sind, wurden identifiziert und behoben. 

- Diese Version enthält darüber hinaus Fehlerbehebungen und Verbesserungen für mehrere Probleme.


## <a name="azure-atp-release-248"></a>Azure ATP Release 2.48
Veröffentlicht: 16. September 2018
- **Sicherheitswarnung:** Reconnaissance mithilfe von Verzeichnisdienstabfragen

  Diese Sicherheitswarnung enthält nun verbesserte Infografiken und Beweise. 

- **Ausschließen von Entitäten von der Erkennung** 

  Sie können Entitäten nun aus den folgenden Erkennungen ausschließen, um die Anzahl falsch positiver Ergebnisse zu reduzieren: 
  - Verdächtige VPN-Verbindung (Benutzerausschluss)
  - Verdächtige Heraufstufung zu Domänencontrollern (potenzieller DcShadow-Angriff)
  - Verdächtige Replikationsanforderung (potenzieller DcShadow-Angriff)

- Diese Version enthält darüber hinaus Fehlerbehebungen und Verbesserungen für mehrere Probleme.


## <a name="azure-atp-release-247"></a>Azure ATP Release 2.47
Veröffentlicht: 2. September 2018

- **Überprüfung der erweiterten Überwachungsrichtlinie von Azure ATP**
 
Azure Advanced Threat Protection überprüft jetzt die in Ihrem Domänencontroller vorhandenen erweiterten Überwachungsrichtlinien und empfiehlt Richtlinienänderungen, um die maximale Serviceabdeckung durch Azure ATP für Ihre Organisation zu garantieren. 

**Mit dieser Überprüfung können Sie nun folgende Aktionen ausführen:**
  -  fehlende Ereignisse in Ihren Windows-Ereignisprotokollen identifizieren, die derzeit von der Abdeckung durch Azure ATP ausgeschlossen sind
  -  ideale Einstellungen überprüfen und Änderungen basierend auf den bereitgestellten Empfehlungen für die Integritätswarnung durchführen
  -  zudem wird eine einzelne aggregierte Integritätswarnung für alle Ihre Domänencontroller ausgegeben, einschließlich Vorschlägen für die Wartung (falls benötigt).

Überprüfen Sie, wie [erweiterte Überwachungsrichtlinien konfiguriert werden](atp-advanced-audit-policy.md), um sicherzustellen, dass Ihr System ordnungsgemäß konfiguriert ist. 
- Diese Version enthält darüber hinaus Fehlerbehebungen und Verbesserungen für mehrere Probleme.

## <a name="azure-atp-release-246"></a>Azure ATP Release 2.46

Veröffentlicht: 26. August 2018

- Diese Version enthält Fehlerbehebungen und Verbesserungen für mehrere Probleme.

## <a name="azure-atp-release-245"></a>Azure ATP Release 2.45

Veröffentlicht: 19. August 2018

- **Azure ATP verfügt nun über die Event Trace for Windows (ETW) als zusätzliche Datenquelle**  <br> Die Ereignisablaufverfolgung für Windows (Event Tracing for Windows, ETW) wurde neben dem vorhandenen Netzwerkverkehr und den Windows-Ereignissen als zusätzliche Datenquelle hinzugefügt. Die ETW bietet zusätzlich die Erkennung von verdächtigen Aktivitäten wie den Folgenden: Verdächtige Heraufstufung zu Domänencontroller und verdächtige Domänencontroller-Replikationsanforderungen (beide stellen potenzielle DcShadow-Angriffe dar). <br>
Nur die auf Domänencontrollern installierten ATP-Sensoren unterstützen die Erkennung basierend auf der ETW. Die Erkennung der auf ETW basierenden Ereignissenke wird nicht von eigenständigen ATP-Sensoren unterstützt. <br>  

- **Vier neue Erkennungen ab sofort allgemein verfügbar** <br>
  - Verdächtige VPN-Verbindung
  - Kerberos Golden Ticket – nicht vorhandenes Konto 
  - Erkennung verdächtiger Heraufstufungen zu Domänencontrollern (potenzieller DcShadow-Angriff) – Erkennung basierend auf der ETW, nur bei ATP-Sensoren verfügbar 
  - Verdächtige Domänencontroller-Replikationsanforderung (potenzieller DcShadow-Angriff) – Erkennung basierend auf der ETW, nur bei ATP-Sensoren verfügbar

- Diese Version enthält darüber hinaus Fehlerbehebungen und Verbesserungen für mehrere Probleme.


## <a name="azure-atp-release-244"></a>Azure ATP Release 2.44

Veröffentlicht: 12. August 2018

- Diese Version enthält Fehlerbehebungen und Verbesserungen für mehrere Probleme.
- Die auf dem Sensorcomputer erstellten Protokolldateien enthalten nicht mehr das Protokoll „Ausnahmestatistik“.


## <a name="azure-atp-release-243"></a>Azure ATP Release 2.43

Veröffentlicht: 5. August 2018

- Diese Version enthält Fehlerbehebungen und Verbesserungen für mehrere Probleme.



## <a name="azure-atp-release-242"></a>Azure ATP Release 2.42

Veröffentlicht: 29. Juli 2018

- Diese Version enthält Fehlerbehebungen und Verbesserungen für mehrere Probleme. 


## <a name="azure-atp-release-241"></a>Azure ATP Release 2.41

Veröffentlicht: 22. Juli 2018

- **Unterstützung für mehrere Azure ATP-Gesamtstrukturen wird schrittweise eingeführt (Vorschau)** <br> Azure ATP kann jetzt Organisationen mit mehreren Gesamtstrukturen unterstützen, wodurch Sie die Möglichkeit erhalten, Aktivitäten und Profilbenutzer in allen Gesamtstrukturen zu überwachen. Diese neue Funktionalität ermöglicht Ihnen Folgendes:

  - Sie können Aktivitäten, die von Benutzern in mehreren Gesamtstrukturen ausgeführt werden, in einer zentralen Konsole im Blick behalten und untersuchen.
  - Durch erweiterte Active Directory-Integration und -Kontoauflösung lassen sich falsch positive Ergebnisse besser erkennen und reduzieren.
  - Sie profitieren von besseren Überwachungswarnungen und -berichten für eine organisationsübergreifende Übersicht.


-   **Neue Erkennungen: DCShadow**<br>Zwei neue Erkennungsfunktionen helfen Ihnen beim Schutz vor DCShadow-Angriffen (Domain Controller Shadow):

    -   Verdächtige Hochstufung zu Domänencontrollern (potenzieller DCShadow-Angriff): Diese Funktion hilft bei der Erkennung von Angriffen, bei denen ein Computer die Identität eines Domänencontrollers annimmt und dann versucht, die Replikation zu verwenden, um Änderungen an andere Domänencontroller in Ihrer Domäne zu verteilen.

    -   Verdächtige Replikationsanforderung (potenzieller DCShadow-Angriff): Diese Funktion hilft beim Schutz vor Angriffen, bei denen versucht wird, Computer, die keine Domänencontroller sind, zu Domänencontrollern hochzustufen, um Verzeichnisobjekte zu ändern.

-   **Verbesserte Informationen zu Verschlüsselungsdowngrades**<br>Die Erkennung von Verschlüsselungsdowngrades bietet jetzt mehr Informationen zum Typ des erkannten Angriffs: Overpass-the-Hash, Golden Ticket und Skeleton Key. Darüber hinaus wurden diese Warnungen aggregiert, um die Untersuchung zu vereinfachen.
- Diese Version enthält Fehlerbehebungen und Verbesserungen für mehrere Probleme. 


## <a name="azure-atp-release-240"></a>Azure ATP Release 2.40

Veröffentlicht: 15. Juli 2018

- Die Pass-the-Ticket-Erkennung enthält jetzt auf der Seite „Warnungsdetails“ einen Beweisabschnitt. Dort werden zusätzliche Informationen zu einer Warnung angezeigt.

- Benutzerzugriffssteuerungs-Flags, die im Profil eines Benutzers unter den Verzeichnisdaten zu finden sind, enthalten jetzt eine Legende, um zu verdeutlichen, welche Attribute aktiviert und welche deaktiviert sind.  

## <a name="azure-atp-release-239"></a>Azure ATP Release 2.39

Veröffentlicht: 5. Juli 2018
-   **Neue Erkennung hinzugefügt: Kerberos Golden Ticket – nicht vorhandenes Konto** (Vorschau)<br>Mit dieser neuen Erkennung können Sie Ihre Organisation vor Angriffen schützen, in denen ein Golden Ticket für ein Konto erstellt wird, das in Ihrer Domäne nicht existiert. Weitere Informationen finden Sie im [Azure Advanced Threat Protection-Handbuch zu verdächtigen Aktivitäten](suspicious-activity-guide.md).

- Diese Version enthält Fehlerbehebungen und Verbesserungen für mehrere Probleme. 


## <a name="azure-atp-release-238"></a>Azure ATP Release 2.38

Veröffentlicht: 1. Juli 2018

- Diese Version enthält Fehlerbehebungen und Verbesserungen für verschiedene Probleme sowie Erweiterungen des Azure ATP-Portals.

## <a name="azure-atp-release-237"></a>Azure ATP Release 2.37

Veröffentlicht: 24. Juni 2018

- Diese Version enthält Fehlerbehebungen und Verbesserungen für mehrere Probleme. 

## <a name="azure-atp-release-236"></a>Azure ATP Release 2.36

Veröffentlicht: 17. Juni 2018

- Diese Version enthält Fehlerbehebungen und Verbesserungen für mehrere Probleme. 


## <a name="azure-atp-release-235"></a>Azure ATP Release 2.35

Veröffentlicht am 10. Juni 2018
 
- **Vorschauversionen neuer Erkennungen**<br></br>Ab jetzt nutzt Azure ATP seine Funktion als Clouddienst – für den neue Features in kürzeren Zyklen bereitgestellt werden können –und bietet Ihnen so schnell wie möglich neue Erkennungen. Diese neuen Erkennungen werden als „Vorschauversion“ markiert, wenn sie das erste Mal veröffentlicht werden. In der Regel wechselt eine neue Erkennung innerhalb weniger Wochen von der Vorschauversion zu einer allgemein verfügbaren Version. Es werden standardmäßig Vorschauversionen neuer Erkennungen angezeigt. Weitere Informationen zum Deaktivieren dieser Standardeinstellung finden Sie unter [Preview Detections (Vorschauversionen neuer Erkennungen)](working-with-suspicious-activities.md#preview-detections).
 
- **Erkennung verdächtiger VPNs**<br></br>Mit dieser Vorschauversion wird eine Vorschauversion für eine Erkennung verdächtiger VPNs eingeführt. Azure ATP speichert Informationen zum VPN-Verhalten des Benutzers, einschließlich der Computer, auf denen die Benutzer angemeldet sind, und der Orte, von denen die Benutzer eine Verbindung herstellen. Sie erhalten eine Warnung, wenn nicht das erwartete Verhalten eintritt. Weitere Informationen finden Sie unter [Suspicious VPN detection (Erkennung verdächtiger VPNs)](suspicious-activity-guide.md).

- **Delayed update** (Verzögertes Update)<br></br>Sie haben jetzt die Möglichkeit auszuwählen, dass Azure ATP-Sensoren bei jedem Update von Azure ATP erst später aktualisiert werden. Sie können für jeden einzelnen Sensor die Option **Delayed update** (Verzögertes Update) auswählen, sodass das Update erst 24 Stunden nach dem Update des Azure ATP-Clouddiensts ausgeführt wird. Durch dieses Feature können Sie das Update für bestimmte Testsensoren ausprobieren und Ihre Produktionssensoren erst später aktualisieren. Wenn bei dem ersten Updatezyklus ein Problem auftritt, erstellen Sie ein Supportticket. Weitere Informationen finden Sie unter [Aktualisieren von Azure ATP-Sensoren](sensor-update.md).

- **Aktualisierte Erkennung für ungewöhnliche Protokollimplementierungen**<br></br>Mithilfe der Erkennung für ungewöhnliche Protokollimplementierungen können jetzt mehr Informationen bereitgestellt werden. Sie können jetzt sehen, welches potenzielle Angriffstool Azure ATP verdächtigt, auf Ihrem Netzwerk zu arbeiten. Weitere Informationen finden Sie im [Leitfaden zu verdächtigen Aktivitäten](suspicious-activity-guide.md).
 
- **Warnung bei veralteten Sensoren**<br></br>Azure ATP umfasst eine neue Überwachungswarnung, über die Sie informiert werden, wenn es bereits drei neue Versionen eines Sensors gibt und noch kein Update ausgeführt wurde. Wenn Ihnen diese Warnung angezeigt wird, sollten Sie den Sensor aktualisieren oder prüfen, warum der Sensor nicht automatisch aktualisiert wird. Wenn die Warnung wiederholt auftritt, deinstallieren Sie den Sensor und installieren Sie ihn erneut.

- Diese Version enthält Fehlerbehebungen und Verbesserungen für mehrere Probleme. 

## <a name="azure-atp-release-234"></a>Azure ATP Release 2.34

Veröffentlicht: 3. Juni 2018
 
- Diese Version enthält Fehlerbehebungen und Verbesserungen für mehrere Probleme. 

 
## <a name="azure-atp-release-233"></a>Azure ATP Release 2.33

Veröffentlicht: 27. Mai 2018

- Vorschaufeature: Azure ATP unterstützt jetzt neue Sprachen und 13 neue Gebietsschemas:
    - Tschechisch
    - Ungarisch
    - Italienisch
    - Koreanisch
    - Niederländisch
    - Polnisch
    - Portugiesisch (Brasilien)
    - Portugiesisch (Portugal)
    - Russische Föderation
    - Schwedisch
    - Türkisch
    - Chinesisch (China)
    - Chinesisch (Taiwan)


## <a name="azure-atp-release-232"></a>Azure ATP Release 2.32

Veröffentlicht: 13. Mai 2018
 
- Diese Version enthält Fehlerbehebungen und Verbesserungen für mehrere Probleme. 

## <a name="azure-atp-release-231"></a>Azure ATP Release 2.31

Veröffentlicht: 6.Mai 2018
 
- Verbesserungen wurden für die Namensauflösung hinzugefügt. Als Teil dieses Aufwands kann der Sensor zusätzlich zur aktiven RPC- und NetBIOS-Auflösung ein TSL Client Hello-Paket an den Port des RDP-Endpunkts (3389) übergeben. 
- Diese Version enthält Fehlerbehebungen und Verbesserungen für mehrere Probleme. 

## <a name="azure-atp-release-230"></a>Azure ATP Release 2.30

Veröffentlicht: 29. April 2018
 
- Verdächtige Aktivitäten zur Herabstufung der Verschlüsselung enthalten jetzt einen Beweisabschnitt, der die von Azure ATP erkannten Symptome beschreibt, auf denen der Verdacht basiert, dass eine Aktivität zur Herabstufung der Verschlüsselung stattgefunden hat. 
-   Azure ATP verwendet jetzt den Azure Email Orchestrator für alle von Azure ATP gesendeten E-Mail-Nachrichten einschließlich verdächtiger Aktivitäten, Überwachungswarnungen und Berichte. Sie werden feststellen, dass diese E-Mail-Benachrichtigungen jetzt im Interesse der Benutzerfreundlichkeit ein konsistentes Format aufweisen, und Excel-Dateien werden mit der E-Mail verknüpft, die von der Konsole heruntergeladen werden können.
 
 
## <a name="azure-atp-release-229"></a>Azure ATP-Version 2.29

Veröffentlicht: 22. April 2018
 
- Diese Version enthält Fehlerbehebungen und Verbesserungen für mehrere Probleme. 
 
 
## <a name="azure-atp-release-228"></a>Azure ATP-Version 2.28

Veröffentlicht: 15. April 2018
 
-   Benutzer, die Mitglieder der Rollengruppen für Azure ATP-Benutzer und anzeigende Azure ATP-Benutzer sind, sind jetzt berechtigt, Überwachungswarnungen anzuzeigen.
- Diese Version enthält Fehlerbehebungen und Verbesserungen für mehrere Probleme. 


## <a name="azure-atp-release-227"></a>Azure ATP-Version 2.27

Veröffentlicht: 8. April 2018

- Sie haben jetzt die Möglichkeit, Benutzerfeedback über die obere Navigationsleiste bereitzustellen. Durch Klicken auf das Smileysymbol in der Menüleiste können Sie eine E-Mail mit Ihrem Feedback an das Azure Advanced Threat Protection-Team senden.

- Diese Version enthält Fehlerbehebungen und Verbesserungen für mehrere Probleme. 
 

## <a name="azure-atp-release-226"></a>Azure ATP-Version 2.26

Veröffentlicht: 25. März 2018

- Wenn Azure ATP Sie über eine verdächtige Aktivität informiert, die Sie als unbedenklich positiv identifizieren (eine legitime Aktion, die keine verdächtige Aktivität ist), haben Sie die Möglichkeit, Computer und IP-Adressen von weiteren Erkennungen auszuschließen. Hierzu zählen: Herabstufen der Verschlüsselung, LDAP-Brute-Force, gefälschte PAC, Brute-Force und Pass-the-Hash.
-   Die Leistung des Azure ATP-Sensors wurde verbessert.
-   Eine neue Region für die Bereitstellung eines Arbeitsbereichs wurde hinzugefügt. Sie können ab sofort auch einen Arbeitsbereich in Asien bereitstellen. 


## <a name="azure-atp-release-225"></a>Azure ATP Version 2.25

Veröffentlicht: 18. März 2018

- Die mehrstufige Authentifizierung (Multi-factor authentication, MFA) wird jetzt von Azure ATP unterstützt. Mandanten, die MFA verwenden, können jetzt auf das Azure ATP-Portal zugreifen.
- Azure ATP verfügt jetzt über die Seite [**Systemstatus**](https://health.atp.azure.com/), auf der Sie Informationen dazu erhalten, ob das Portal zum Verwalten des Arbeitsbereichs aktiv ist und funktioniert, ob Probleme bei Ermittlungsvorgängen auftreten und ob der Sensor Datenverkehr an die Cloud senden kann. Sie können über die Menüleiste in Azure ATP auf den **Systemstatus** zugreifen.


## <a name="azure-atp-release-224"></a>Azure ATP Version 2.24

Veröffentlicht: 11. März 2018

**Neue und aktualisierte Erkennungen**
  - Erstellung verdächtiger Dienste – Angreifer versuchen, verdächtige Dienste in Ihrem Netzwerk auszuführen. Azure ATP gibt jetzt eine Warnung aus, wenn erkannt wird, dass jemand an einem bestimmten Computer einen neuen Dienst ausführt, der verdächtig erscheint. Diese Erkennung basiert auf Ereignissen (nicht auf Datenverkehr) und wird auf jedem Domänencontroller in Ihrem Netzwerk ausgelöst, der das Ereignis 7045 an Azure ATP weiterleitet. Weitere Informationen finden Sie im [Leitfaden zu verdächtigen Aktivitäten](suspicious-activity-guide.md).

**Verbesserte Untersuchung**
  - Azure ATP enthält ein erweitertes [Entitätsprofil](entity-profiles.md). Über das Entitätsprofil erhalten Sie eine Plattform, die auf eine detaillierte Untersuchung von Benutzeraktivitäten ausgerichtet ist. Zu diesen gehören u.a die verwendeten Ressourcen und Computer. Über das Entitätsprofil erhalten Sie Verzeichnisdaten, und Sie haben die Möglichkeit, potenzielle Lateral Movement-Pfade zu oder von der Entität zu identifizieren, wodurch Sie mehr über die potenziellen Sicherheitsverletzungen in Ihrer Organisation erfahren können.

  - ATP ermöglicht es Ihnen, Entitäten manuell als *vertraulich* zu kennzeichnen, um die Erkennung und Überwachung zu verbessern. Diese Kennzeichnung hat Auswirkungen auf viele Azure ATP-Vorgänge zum Erkennen von verdächtigen Diensten, wie z.B. die Vorgänge zum Erkennen von Änderungen sensibler Gruppen und [Lateral Movement-Pfaden](use-case-lateral-movement-path.md), die sensible Entitäten verwenden.

**Neue Berichte, um Sie bei Untersuchungen zu unterstützen**
  - Mithilfe des [Berichts zu Kennwörtern im Klartextformat](reports.md) können Sie erkennen, wenn Dienste Kontoanmeldeinformationen im Nur-Text-Format gesendet werden. Durch diese Funktion können Sie Dienste untersuchen und die Sicherheitsstufe Ihres Netzwerks verbessern. Der Bericht ersetzt die Klartextwarnungen über verdächtige Aktivität.
  - In [Lateral Movement-Pfaden zu sensiblen Konten](reports.md) werden die sensiblen Konten aufgeführt, die über Lateral Movement-Pfade zur Verfügung gestellt werden. Um die Angriffsfläche zu minimieren, kann so die Anzahl dieser Pfade verringert und die Sicherheit Ihres Netzwerks erhöht werden. Indem Lateral Movement-Vorgänge verhindert werden, können sich Angreifer nicht zwischen Benutzern und Computern in Ihrem Netzwerk bewegen, bis sie auf den Jackpot in Sachen virtuelle Sicherheit stoßen: die sensiblen Anmeldeinformationen Ihres Administratorkontos.

- Sie können jetzt einfach über den in einer Warnung über verdächtige Aktivität enthaltenen Link auf die Dokumentation zugreifen, um [Schritte, die Sie durchführen können](suspicious-activity-guide.md) anzuzeigen. 

**Leistungsverbesserungen**
 -  Die Azure ATP-Sensorinfrastruktur wurde bezüglich der Leistung verbessert: Die aggregierte Datenverkehrsansicht ermöglicht Optimierungen der CPU- und Paketpipeline und verwendet Sockets zu Domänencontrollern erneut, um SSL-Sitzungen zum DC zu minimieren.

## <a name="see-also"></a>Weitere Informationen
- [Was ist Azure Advanced Threat Protection?](what-is-atp.md)
- [Häufig gestellte Fragen](atp-technical-faq.md)
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Azure ATP capacity planning (Azure ATP-Kapazitätsplanung)](atp-capacity-planning.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
