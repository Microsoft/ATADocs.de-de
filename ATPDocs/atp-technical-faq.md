---
title: Häufig gestellte Fragen zu Azure Advanced Threat Protection | Microsoft-Dokumentation
description: Liste häufig gestellter Fragen zu Azure ATP und zugehörige Antworten
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 03/07/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 6a9b5273-eb26-414e-9cdd-f64406e24ed8
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 10db395065b7d5038aee662d52a5f6350f845a1a
ms.sourcegitcommit: 76b818e4a95842e2175e0efb4db142704b66daa2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/07/2019
ms.locfileid: "57562226"
---
# <a name="azure-atp-frequently-asked-questions"></a>Häufig gestellte Fragen zu Azure ATP
Dieser Artikel enthält eine Reihe häufig gestellter Fragen und Antworten zu Azure ATP, unterteilt in die folgenden Kategorien: 
- [Was ist Azure ATP?](#what-is-azure-atp)
- [Lizenzierung und Datenschutz](#licensing-and-privacy)
- [Bereitstellung](#deployment)
- [Vorgänge](#operation)
- [Problembehandlung](#troubleshooting)

## <a name="what-is-azure-atp"></a>Was ist Azure ATP?

### <a name="what-can-azure-atp-detect"></a>Was kann Azure ATP erkennen?

Azure ATP erkennt bekannte Angriffe und Techniken, Sicherheitsprobleme und Risiken in Ihrem Netzwerk.
Die vollständige Liste der Azure ATP-Erkennungen finden Sie unter [What detections does Azure ATP perform? (Welche Erkennungsvorgänge führt Azure ATP durch?)](suspicious-activity-guide.md).

### <a name="what-data-does-azure-atp-collect"></a>Welche Daten erfasst Azure ATP? 
Azure ATP sammelt und speichert Informationen von Ihren konfigurierten Servern (Domänencontroller, Mitgliedsserver usw.) in einer Datenbank, die für den Dienst für Nachverfolgungs- und Berichterstellungszwecke sowie für administrative Zwecke spezifisch sind. Gesammelte Informationen sind unter anderem Netzwerkdatenverkehr von und zu Domänencontrollern (z.B. Kerberos-Authentifizierung, NTLM-Authentifizierung, DNS-Abfragen), Sicherheitsprotokolle (z.B. Windows-Sicherheitsereignisse), Active Directory-Informationen (Struktur, Subnetze, Websites) sowie Entitätsinformationen (z.B. Namen, E-Mail-Adressen und Telefonnummern). 

Microsoft verwendet diese Daten zu den folgenden Zwecken: 

-   Zum proaktiven Identifizieren von Angriffsindikatoren (Indicators of Attack, IOAs) in Ihrer Organisation 
-   Zum Generieren von Warnungen, wenn ein möglicher Angriff erkannt wurde 
-   Zum Bereitstellen von Sicherheitsvorgängen mit einen Einblick in Entitäten, die mit Bedrohungssignalen aus Ihrem Netzwerk verknüpft sind. So können Sie überprüfen und ermitteln, ob Sicherheitsbedrohungen vorhanden sind. 

Microsoft extrahiert Ihre Daten nicht zu Werbezwecken oder anderen Zwecken als die Bereitstellung des Dienstes für Sie. 

### <a name="does-azure-atp-only-leverage-traffic-from-active-directory"></a>Nutzt Azure ATP nur Active Directory-Datenverkehr?
Zusätzlich zur Analyse des Active Directory-Datenverkehrs mit der DPI-Technologie (Deep Packet Inspection) kann Azure ATP auch relevante Windows-Ereignisse aus Ihrem Domänencontroller sammeln und Entitätenprofile auf Grundlage von Informationen aus Active Directory Domain Services erstellen. Azure ATP unterstützt auch die RADIUS-Kontoführung beim Empfangen von VPN-Protokollen von unterschiedlichen Lieferanten (Microsoft, Cisco, F5 und Checkpoint).

### <a name="does-azure-atp-monitor-only-domain-joined-devices"></a>Überwacht Azure ATP nur Geräte, die der Domäne angehören?
Nein. Azure ATP überwacht alle Geräte im Netzwerk und führt die Authentifizierung sowie Autorisierungsanfragen für Active Directory durch. Dies schließt Nicht-Windows-Geräte und mobile Geräte ein.

### <a name="does-azure-atp-monitor-computer-accounts-as-well-as-user-accounts"></a>Überwacht Azure ATP sowohl Computerkonten als auch Benutzerkonten?
Ja. Da Computerkonten (ebenso wie alle anderen Entitäten) zum Durchführen böswilliger Aktivitäten verwendet werden können, überwacht Azure ATP das Verhalten aller Computerkonten und aller weiteren Entitäten in der Umgebung.

## <a name="licensing-and-privacy"></a>Lizenzierung und Datenschutz 
### <a name="where-can-i-get-a-license-for-azure-advanced-threat-protection-atp"></a>Wo erhalte ich eine Lizenz für Azure Advanced Threat Protection (ATP)?

Azure ATP steht als Teil von Enterprise Mobility + Security 5-Suite (EMS E5) und als eine eigenständige Lizenz zur Verfügung. Sie können eine Lizenz entweder direkt über das [Microsoft 365-Portal](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-pricing) oder über das CSP-Lizenzierungsmodell (Cloud Solution Partner) erwerben.

### <a name="is-this-going-to-be-a-part-of-azure-active-directory-or-on-premises-active-directory"></a>Wird das Produkt ein Bestandteil von Azure Active Directory oder von lokalem Active Directory sein?
Diese Azure ATP-Lösung ist derzeit ein eigenständiges Angebot. Sie ist kein Bestandteil von Azure Active Directory oder von lokalem Active Directory.

### <a name="is-my-data-isolated-from-other-customer-data"></a>Sind die Daten von anderen Kundendaten isoliert? 

Ja, Ihre Daten werden durch Zugriffsauthentifizierung und logischer Trennung basierend auf der Kundennummer getrennt. Jeder Kunde kann nur auf Daten zugreifen, die von der eigenen Organisation gesammelt wurden, sowie auf generische Daten, die von Microsoft bereitgestellt werden.

### <a name="do-i-have-the-flexibility-to-select-where-to-store-my-data"></a>Kann ich frei wählen, wo ich meine Daten speichern möchte? 

Nein. Wenn Ihre Azure-ATP-Instanz erstellt wird, wird sie automatisch im Länderrechenzentrum gespeichert, das dem geografischen Standort Ihres AAD-Mandanten am nächsten liegt. Azure ATP-Daten können nicht verschoben werden, sobald Ihre Azure ATP-Instanz in einem anderen Rechenzentrum erstellt wurde.                

### <a name="how-does-microsoft-prevent-malicious-insider-activities-and-abuse-of-high-privilege-roles"></a>Wie verhindert Microsoft schädliche Insideraktivitäten und den Missbrauch von privilegierten Rollen? 

Microsoft-Entwickler und -Administratoren verfügen systembedingt über genügend Privilegien zum Ausführen der Ihnen zugewiesenen Aufgaben, um den Dienst zu betreiben und weiterzuentwickeln. Microsoft stellt zum Schützen vor Aktivitäten von unautorisierten Entwicklern und/oder Administratoren eine Kombination aus vorbeugenden und reaktiven Steuerelementen sowie Erkennungssteuerelemente einschließlich der folgenden Mechanismen bereit: 

-   Enge Zugriffssteuerung für vertrauliche Daten 
-   Kombination aus Steuerelementen, die die unabhängige Erkennung von schädlicher Aktivität deutlich verbessern 
-   Mehrere Überwachungs-, Protokollierungs- und Berichterstattungsebenen 

Darüber hinaus führt Microsoft Hintergrundüberprüfungen von bestimmten Betriebsmitarbeitern durch und beschränkt den Zugriff auf Anwendungen, Systeme sowie die Netzwerkinfrastruktur im Verhältnis zur Ebene der Hintergrundüberprüfung. Betriebsmitarbeiter folgen einem formellen Prozess, wenn sie auf das Konto eines Kunden oder auf verwandte Informationen während der Ausübung ihrer Aufgaben zugreifen müssen. 

## <a name="deployment"></a>Bereitstellung
### <a name="how-many-azure-atp-sensors-do-i-need"></a>Wie viele Azure ATP-Sensoren benötige ich?

Alle Domänencontroller in der Umgebung sollten von einem ATP-Sensor oder einem eigenständigen Sensor abgedeckt sein. Weitere Informationen finden Sie unter [Azure ATP sensor Sizing (Größeneinstellung zum Azure ATP-Sensor)](atp-capacity-planning.md#sizing). 

### <a name="does-azure-atp-work-with-encrypted-traffic"></a>Funktioniert Azure ATP mit verschlüsseltem Datenverkehr?
Netzwerkprotokolle mit verschlüsseltem Datenverkehr (z.B. LDAPS und IPsec) werden nicht verschlüsselt, sondern von den Sensoren analysiert.

### <a name="does-azure-atp-work-with-kerberos-armoring"></a>Funktioniert Azure ATP mit Kerberos Armoring?
Die Aktivierung von Kerberos Armoring (auch als Flexible Authentication Secure Tunneling, FAST, bezeichnet) wird von Azure ATP unterstützt. Einzige Ausnahme ist die Overpass-The-Hash-Erkennung, die nicht von Kerberos Armoring unterstützt wird.

### <a name="how-do-i-monitor-a-virtual-domain-controller-using-azure-atp"></a>Wie kann ich einen virtuellen Domänencontroller mit Azure ATP überwachen?
Die meisten virtuellen Domänencontroller können vom Azure ATP-Sensor abgedeckt werden. Um festzustellen, ob der Azure ATP-Sensor sich für Ihre Umgebung eignet, lesen Sie die Informationen unter [Azure ATP-Kapazitätsplanung](atp-capacity-planning.md).

Wenn ein virtueller Domänencontroller nicht durch den Azure ATP-Sensor abgedeckt werden kann, können Sie einen virtuellen oder physischen eigenständigen Azure ATP-Sensor verwenden, wie unter [Konfigurieren der Portspiegelung](configure-port-mirroring.md) beschrieben.  <br />Die einfachste Möglichkeit ist jeweils einen virtuellen eigenständigen Azure ATP-Sensor auf jedem Host, auf dem ein virtueller Domänencontroller vorhanden ist.<br />Wenn die virtuellen Domänencontroller zwischen Hosts verschoben werden, müssen Sie einen der folgenden Schritte ausführen:

-   Wenn der virtuelle Domänencontroller auf einen anderen Host verschoben wird, konfigurieren Sie den eigenständigen Azure ATP-Sensor auf diesem Host so vor, dass der Datenverkehr von dem zuvor verschobenen virtuellen Domänencontroller empfangen wird.
-   Stellen Sie sicher, dass Sie den virtuellen eigenständigen Azure ATP-Sensor dem virtuellen Domänencontroller zuordnen, sodass der eigenständige Azure ATP-Sensor ggf. mit dem Controller verschoben wird.
-   Es gibt einige virtuelle Switches, über die der Datenverkehr zwischen Hosts gesendet werden kann.

### <a name="how-do-i-configure-the-azure-atp-sensors-to-communicate-with-azure-atp-cloud-service-when-i-have-a-proxy"></a>Wie konfiguriere ich Azure ATP-Sensoren so, dass sie mit dem Azure ATP-Clouddienst kommunizieren, wenn ich über einen Proxyserver verfüge?

Für die Kommunikation Ihrer Domänencontroller mit dem Clouddienst müssen Sie in Ihrer Firewall und auf Ihrem Proxyserver Port 443 für „*.atp.azure.com“ freigeben. Informationen hierzu finden Sie unter [Configure your proxy or firewall to enable communication with Azure ATP sensors (Konfigurieren Ihres Proxyservers oder Ihrer Firewall zum Aktivieren der Kommunikation mit Azure ATP-Sensoren)](configure-proxy.md).

### <a name="can-azure-atp-monitored-domain-controllers-be-virtualized-on-your-iaas-solution"></a>Kann Azure ATP in Ihrer IaaS-Lösung virtualisierte Domänencontroller überwachen?
Ja, Sie können mit dem Azure ATP-Sensor Domänencontroller in einer beliebigen IaaS-Lösung überwachen.

### <a name="can-azure-atp-support-multi-domain-and-multi-forest"></a>Kann Azure ATP mehrere Domänen und mehrere Gesamtstrukturen unterstützen?
Azure Advanced Threat Protection unterstützt Umgebungen und mehrere Gesamtstrukturen. Weitere Informationen und Anforderungen in Bezug auf Vertrauensstellungen finden Sie unter [Unterstützung für mehrere Gesamtstrukturen](atp-multi-forest.md).

### <a name="can-you-see-the-overall-health-of-the-deployment"></a>Kann die Gesamtintegrität der Bereitstellung angezeigt werden?
Ja, Sie können die Gesamtintegrität der Bereitstellung sowie spezifische Probleme im Zusammenhang mit der Konfiguration, Konnektivität usw. anzeigen und werden bei Eintreten eines Problems mit Zustandswarnungen zu Azure ATP benachrichtigt.

## <a name="operation"></a>Vorgang

### <a name="what-kind-of-integration-does-azure-atp-have-with-siems"></a>Welche Art der Integration weist Azure ATP in SIEMs auf?
Azure ATP kann so konfiguriert werden, dass bei Integritätswarnungen und Feststellung einer Sicherheitswarnung eine Syslog-Warnung an einen SIEM-Server gesendet wird, der das CEF-Format verwendet. Weitere Informationen finden Sie unter [Referenz zum SIEM-Protokoll](cef-format-sa.md).

### <a name="why-are-certain-accounts-considered-sensitive"></a>Warum gelten bestimmte Konten als sensible Konten?
Dies ist der Fall, wenn ein Konto Mitglied bestimmter Gruppen ist, die als sensibel festgelegt sind (z. B. „Domänen-Admins“).

Um nachzuvollziehen, warum ein Konto ein sensibles Konto ist, können Sie seine Gruppenmitgliedschaft überprüfen, um festzustellen, welchen sensiblen Gruppen es angehört (die Gruppe, der das Konto angehört, kann auch wegen einer anderen Gruppe eine sensible Gruppe sein. Daher sollten Sie immer die höchste sensible Gruppe überprüfen). Sie können auch manuell [Konten als vertraulich kennzeichnen](sensitive-accounts.md).

### <a name="do-you-have-to-write-your-own-rules-and-create-a-thresholdbaseline"></a>Müssen eigene Regeln geschrieben und ein Schwellenwert/eine Basislinie erstellt werden?
Bei Azure Advanced Threat Protection besteht keine Notwendigkeit zum Erstellen von Regeln, Schwellenwerten oder Basislinien und der anschließenden Optimierung. Azure ATP analysiert das Verhalten von Benutzern, Geräten und Ressourcen – sowie deren Beziehungen untereinander – und kann verdächtige Aktivitäten sowie bekannte Angriffe schnell erkennen. Drei Wochen nach der Bereitstellung beginnt Azure ATP, verdächtige Verhaltensaktivitäten zu erkennen. Bekannte Angriffe und Sicherheitsprobleme werden hingegen sofort nach der Bereitstellung von Azure ATP erkannt.

## <a name="troubleshooting"></a>Problembehandlung
### <a name="what-should-i-do-if-the-azure-atp-sensor-or-standalone-sensor-doesnt-start"></a>Wie soll ich vorgehen, wenn der Azure ATP-Sensor oder der eigenständige Sensor nicht gestartet wird?
Sehen Sie sich den letzten Fehlereintrag im aktuellen [Fehlerprotokoll](troubleshooting-atp-using-logs.md) an (Installationsverzeichnis von Azure ATP unter dem Ordner „Logs“ (Protokolle)).


## <a name="see-also"></a>Weitere Informationen
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Azure ATP capacity planning (Azure ATP-Kapazitätsplanung)](atp-capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-forwarding.md)
- [Problembehandlung](troubleshooting-atp-known-issues.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
