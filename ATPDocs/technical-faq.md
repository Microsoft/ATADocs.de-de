---
title: Häufig gestellte Fragen zu Azure Advanced Threat Protection
description: Liste häufig gestellter Fragen zu Azure ATP und zugehörige Antworten
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 09/21/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 6a9b5273-eb26-414e-9cdd-f64406e24ed8
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 8ef149c7792d8fce3ffbe1bc3303d1937827aa4c
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2020
ms.locfileid: "90909768"
---
# <a name="azure-atp-frequently-asked-questions"></a>Häufig gestellte Fragen zu Azure ATP

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

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

Microsoft verwendet diese Daten zu folgenden Zwecken:

- Zum proaktiven Identifizieren von Angriffsindikatoren (Indicators of Attack, IOAs) in Ihrer Organisation
- Zum Generieren von Warnungen, wenn ein möglicher Angriff erkannt wurde
- Zum Bereitstellen von Sicherheitsvorgängen mit einen Einblick in Entitäten, die mit Bedrohungssignalen aus Ihrem Netzwerk verknüpft sind. So können Sie überprüfen und ermitteln, ob Sicherheitsbedrohungen vorhanden sind.

Microsoft extrahiert Ihre Daten nicht zu Werbezwecken oder anderen Zwecken als die Bereitstellung des Dienstes für Sie.

### <a name="how-many-directory-service-credentials-does-azure-atp-support"></a>Wie viele Anmeldeinformationen für Verzeichnisdienste werden von Azure ATP unterstützt?

Azure ATP unterstützt derzeit das Hinzufügen von bis zu 10 verschiedenen Anmeldeinformationen für Verzeichnisdienste, um Active Directory-Umgebungen mit nicht vertrauenswürdigen Gesamtstrukturen zu unterstützen. Wenn Sie weitere Konten benötigen, eröffnen Sie ein Supportticket.

### <a name="does-azure-atp-only-leverage-traffic-from-active-directory"></a>Nutzt Azure ATP nur Active Directory-Datenverkehr?

Zusätzlich zur Analyse des Active Directory-Datenverkehrs mit der DPI-Technologie (Deep Packet Inspection) kann Azure ATP auch relevante Windows-Ereignisse aus Ihrem Domänencontroller sammeln und Entitätenprofile auf Grundlage von Informationen aus Active Directory Domain Services erstellen. Azure ATP unterstützt auch die RADIUS-Kontoführung beim Empfangen von VPN-Protokollen von unterschiedlichen Lieferanten (Microsoft, Cisco, F5 und Checkpoint).

### <a name="does-azure-atp-monitor-only-domain-joined-devices"></a>Überwacht Azure ATP nur Geräte, die der Domäne angehören?

Nein. Azure ATP überwacht alle Geräte im Netzwerk und führt die Authentifizierung sowie Autorisierungsanfragen für Active Directory durch. Dies schließt Nicht-Windows-Geräte und mobile Geräte ein.

### <a name="does-azure-atp-monitor-computer-accounts-as-well-as-user-accounts"></a>Überwacht Azure ATP sowohl Computerkonten als auch Benutzerkonten?

Ja. Da Computerkonten (ebenso wie alle anderen Entitäten) zum Durchführen böswilliger Aktivitäten verwendet werden können, überwacht Azure ATP das Verhalten aller Computerkonten und aller weiteren Entitäten in der Umgebung.

### <a name="what-is-the-difference-between-advanced-threat-analytics-ata-and-azure-atp"></a>Worin besteht der Unterschied zwischen Advanced Threat Analytics (ATA) und Azure ATP?

ATA ist eine eigenständige lokale Lösung mit mehreren Komponenten, zum Beispiel ATA Center, die dediziert Hardware lokal erfordern.

Azure ATP ist eine cloudbasierte Sicherheitslösung, die Ihre lokalen Active Directory-Signale (Azure AD) nutzt. Die Lösung ist hochgradig skalierbar und wird laufend aktualisiert.

Die endgültige Version von ATA ist [allgemein verfügbar](https://support.microsoft.com/help/4568997/update-3-for-microsoft-advanced-threat-analytics-1-9). ATA wird die grundlegende Unterstützung am 12. Januar 2021 beenden. Der erweiterte Support wird bis zum 2026. Januar fortgesetzt. Weitere Informationen finden Sie in [unserem Blog](https://techcommunity.microsoft.com/t5/microsoft-security-and/end-of-mainstream-support-for-advanced-threat-analytics-january/ba-p/1539181).

Im Gegensatz zum ATA-Sensor verwendet der Azure ATP-Sensor auch Datenquellen wie die Ereignisablaufverfolgung für Windows (Event Tracing for Windows, ETW), um Azure ATP zu ermöglichen, zusätzliche Erkennungen zu übermitteln.

Die häufigen Updates für Azure ATP enthalten die folgenden Features und Funktionen:

- **Unterstützung für [Umgebungen mit mehreren Gesamtstrukturen](multi-forest.md)** : Stellt Sichtbarkeit in Azure AD-Gesamtstrukturen für Organisationen bereit

- **[Bewertungen des Identitätssicherheitsstatus](isp-overview.md)** : Identifizieren häufige Fehlkonfigurationen sowie ausnutzbare Komponenten und stellen Wiederherstellungspfade zum Reduzieren der Angriffsfläche bereit

- **[UEBA-Funktionen](/cloud-app-security/tutorial-ueba)** : Einblicke in Risiken individueller Benutzer über die Bewertung der Benutzeruntersuchungspriorität. Die Bewertung kann SecOps bei der Untersuchung unterstützen und Analysten dabei helfen, ungewöhnliche Aktivitäten für den Benutzer und die Organisation zu verstehen.

- **Native Integrationen**: In Microsoft Cloud App Security und Azure AD Identity Protection integriert, bieten sie eine hybride Ansicht über Vorgänge in den lokalen und hybriden Umgebungen.

- **Beitrag zu Microsoft Threat Protection (MTP)** : Trägt Warnungs- und Bedrohungsdaten zu MTP bei. MTP nutzt das Microsoft 365-Sicherheitsportfolio (Identitäten, Endpunkte, Daten und Anwendungen), um domänenübergreifende Bedrohungsdaten automatisch zu analysieren und so ein vollständiges Bild der Angriffe in einem einzelnen Dashboard zu erhalten. Dank dieser breiten und ausführlichen Übersichtlichkeit können sich Verteidiger auf kritische Bedrohung konzentrieren und nach anspruchsvollen Sicherheitsverletzungen suchen. Dabei wird die leistungsstarke Automatisierung von MTP genutzt und darauf vertraut, dass diese Angriffe an jedem Punkt der Kette der Angriffsabwehr stoppt und die Organisation wieder in einen sicheren Zustand versetzt.

## <a name="licensing-and-privacy"></a>Lizenzierung und Datenschutz

### <a name="where-can-i-get-a-license-for-azure-advanced-threat-protection-atp"></a>Wo erhalte ich eine Lizenz für Azure Advanced Threat Protection (ATP)?

Azure ATP steht als Teil von Enterprise Mobility + Security 5-Suite (EMS E5) und als eine eigenständige Lizenz zur Verfügung. Sie können eine Lizenz entweder direkt über das [Microsoft 365-Portal](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-pricing) oder über das CSP-Lizenzierungsmodell (Cloud Solution Partner) erwerben.

### <a name="does-azure-atp-need-only-a-single-license-or-does-it-require-a-license-for-every-user-i-want-to-protect"></a>Benötigt Azure ATP nur eine einzige Lizenz, oder ist eine Lizenz für jeden Benutzer erforderlich, der geschützt werden soll?

Azure ATP setzt voraus, dass alle Benutzer in Azure AD eine Lizenz besitzen.

### <a name="is-my-data-isolated-from-other-customer-data"></a>Sind die Daten von anderen Kundendaten isoliert?

Ja, Ihre Daten werden durch Zugriffsauthentifizierung und logischer Trennung basierend auf der Kundennummer getrennt. Jeder Kunde kann nur auf Daten zugreifen, die von der eigenen Organisation gesammelt wurden, sowie auf generische Daten, die von Microsoft bereitgestellt werden.

### <a name="do-i-have-the-flexibility-to-select-where-to-store-my-data"></a>Kann ich frei wählen, wo ich meine Daten speichern möchte?

Nein. Wenn Ihre Azure-ATP-Instanz erstellt wird, wird sie automatisch im Länderrechenzentrum gespeichert, das dem geografischen Standort Ihres AAD-Mandanten am nächsten liegt. Azure ATP-Daten können nicht verschoben werden, sobald Ihre Azure ATP-Instanz in einem anderen Rechenzentrum erstellt wurde.

### <a name="how-does-microsoft-prevent-malicious-insider-activities-and-abuse-of-high-privilege-roles"></a>Wie verhindert Microsoft schädliche Insideraktivitäten und den Missbrauch von privilegierten Rollen?

Microsoft-Entwickler und -Administratoren verfügen systembedingt über genügend Privilegien zum Ausführen der Ihnen zugewiesenen Aufgaben, um den Dienst zu betreiben und weiterzuentwickeln. Microsoft stellt zum Schützen vor Aktivitäten von unautorisierten Entwicklern und/oder Administratoren eine Kombination aus vorbeugenden und reaktiven Steuerelementen sowie Erkennungssteuerelemente einschließlich der folgenden Mechanismen bereit:

- Enge Zugriffssteuerung für vertrauliche Daten
- Kombination aus Steuerelementen, die die unabhängige Erkennung von schädlicher Aktivität deutlich verbessern
- Mehrere Überwachungs-, Protokollierungs- und Berichterstattungsebenen

Darüber hinaus führt Microsoft Hintergrundüberprüfungen von bestimmten Betriebsmitarbeitern durch und beschränkt den Zugriff auf Anwendungen, Systeme sowie die Netzwerkinfrastruktur im Verhältnis zur Ebene der Hintergrundüberprüfung. Betriebsmitarbeiter folgen einem formellen Prozess, wenn sie bei der Ausübung ihrer Aufgaben auf das Konto eines Kunden oder auf zugehörige Informationen zugreifen müssen.

## <a name="deployment"></a>Bereitstellung

### <a name="how-many-azure-atp-sensors-do-i-need"></a>Wie viele Azure ATP-Sensoren benötige ich?

Alle Domänencontroller in der Umgebung sollten von einem ATP-Sensor oder einem eigenständigen Sensor abgedeckt sein. Weitere Informationen finden Sie unter [Azure ATP sensor Sizing (Größeneinstellung zum Azure ATP-Sensor)](capacity-planning.md#sizing).

### <a name="does-azure-atp-work-with-encrypted-traffic"></a>Funktioniert Azure ATP mit verschlüsseltem Datenverkehr?

Netzwerkprotokolle mit verschlüsseltem Datenverkehr (z.B. AtSvc und WMI) werden nicht verschlüsselt, sondern von den Sensoren analysiert.

### <a name="does-azure-atp-work-with-kerberos-armoring"></a>Funktioniert Azure ATP mit Kerberos Armoring?

Die Aktivierung von Kerberos Armoring (auch als Flexible Authentication Secure Tunneling, FAST, bezeichnet) wird von Azure ATP unterstützt. Einzige Ausnahme ist die Overpass-The-Hash-Erkennung, die nicht von Kerberos Armoring unterstützt wird.

### <a name="how-do-i-monitor-a-virtual-domain-controller-using-azure-atp"></a>Wie kann ich einen virtuellen Domänencontroller mit Azure ATP überwachen?

Die meisten virtuellen Domänencontroller können vom Azure ATP-Sensor abgedeckt werden. Um festzustellen, ob der Azure ATP-Sensor sich für Ihre Umgebung eignet, lesen Sie die Informationen unter [Azure ATP-Kapazitätsplanung](capacity-planning.md).

Wenn ein virtueller Domänencontroller nicht durch den Azure ATP-Sensor abgedeckt werden kann, können Sie einen virtuellen oder physischen eigenständigen Azure ATP-Sensor verwenden, wie unter [Konfigurieren der Portspiegelung](configure-port-mirroring.md) beschrieben.  
Die einfachste Möglichkeit ist jeweils einen virtuellen eigenständigen Azure ATP-Sensor auf jedem Host, auf dem ein virtueller Domänencontroller vorhanden ist.  
Wenn die virtuellen Domänencontroller zwischen Hosts verschoben werden, müssen Sie einen der folgenden Schritte ausführen:

- Wenn der virtuelle Domänencontroller auf einen anderen Host verschoben wird, konfigurieren Sie den eigenständigen Azure ATP-Sensor auf diesem Host so vor, dass der Datenverkehr von dem zuvor verschobenen virtuellen Domänencontroller empfangen wird.
- Stellen Sie sicher, dass Sie den virtuellen eigenständigen Azure ATP-Sensor dem virtuellen Domänencontroller zuordnen, sodass der eigenständige Azure ATP-Sensor ggf. mit dem Controller verschoben wird.
- Es gibt einige virtuelle Switches, über die der Datenverkehr zwischen Hosts gesendet werden kann.

### <a name="how-do-i-configure-the-azure-atp-sensors-to-communicate-with-azure-atp-cloud-service-when-i-have-a-proxy"></a>Wie konfiguriere ich Azure ATP-Sensoren so, dass sie mit dem Azure ATP-Clouddienst kommunizieren, wenn ich über einen Proxyserver verfüge?

Für die Kommunikation Ihrer Domänencontroller mit dem Clouddienst müssen Sie in Ihrer Firewall und auf Ihrem Proxyserver Port 443 für „*.atp.azure.com“ freigeben. Informationen hierzu finden Sie unter [Configure your proxy or firewall to enable communication with Azure ATP sensors (Konfigurieren Ihres Proxyservers oder Ihrer Firewall zum Aktivieren der Kommunikation mit Azure ATP-Sensoren)](configure-proxy.md).

### <a name="can-azure-atp-monitored-domain-controllers-be-virtualized-on-your-iaas-solution"></a>Kann Azure ATP in Ihrer IaaS-Lösung virtualisierte Domänencontroller überwachen?

Ja, Sie können mit dem Azure ATP-Sensor Domänencontroller in einer beliebigen IaaS-Lösung überwachen.

### <a name="can-azure-atp-support-multi-domain-and-multi-forest"></a>Kann Azure ATP mehrere Domänen und mehrere Gesamtstrukturen unterstützen?

Azure Advanced Threat Protection unterstützt Umgebungen und mehrere Gesamtstrukturen. Weitere Informationen und Anforderungen in Bezug auf Vertrauensstellungen finden Sie unter [Unterstützung für mehrere Gesamtstrukturen](multi-forest.md).

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

### <a name="which-traffic-does-azure-atp-generate-in-the-network-from-domain-controllers-and-why"></a>Welchen Datenverkehr generiert Azure ATP im Netzwerk von Domänencontrollern und warum?

Azure ATP generiert Datenverkehr von Domänencontrollern zu Computern in der Organisation in einem von drei Szenarien:

1. **Netzwerknamensauflösung**  
Azure ATP erfasst Datenverkehr und Ereignisse, wobei es Benutzer und Computeraktivitäten im Netzwerk erlernt und Profile dazu erstellt. Um Aktivitäten zu Computern in der Organisation zu erlernen und die Profile zu erstellen, muss Azure ATP IPs zu Computerkonten auflösen. Um IPs zu Computernamen aufzulösen, fordern ATP-Sensoren die IP-Adresse für den Computernamen *hinter* der Adresse an.

    Anforderungen erfolgen mithilfe einer von vier Methoden:
    - NTLM über RPC (TCP-Port 135)
    - NetBIOS (UDP-Port 137)
    - RDP (TCP-Port 3389)
    - Abfragen des DNS-Servers mittels Reverse-DNS-Lookup der IP-Adresse (UDP 53)

    Nach Abruf des Computernamens führen Azure ATP-Sensoren eine Gegenprüfung der Details in Active Directory durch, um zu ermitteln, ob es ein zugehöriges Computerobjekt mit demselben Computernamen gibt. Wenn eine Übereinstimmung gefunden wird, erfolgt eine Zuordnung zwischen der IP-Adresse und dem übereinstimmenden Computerobjekt.
2. **Lateral-Movement-Pfad (LMP)**  
Um potenzielle LMPs zu sensiblen Benutzern erstellen zu können, benötigt Azure ATP Informationen zu den lokalen Administratoren auf Computern. In diesem Szenario verwendet der Azure ATP-Sensor SAM-R (TCP 445) zum Abfragen der im Netzwerkverkehr identifizierten IP-Adresse, um die lokalen Administratoren des Computers zu ermitteln. Weitere Informationen zu Azure ATP und SAM-R finden Sie unter [Konfigurieren von für SAM-R erforderliche Berechtigungen](install-step8-samr.md).

3. **Abfragen von Active Directory über LDAP** für Entitätsdaten  
Azure ATP-Sensoren fragen den Domänencontroller aus der Domäne ab, zu der die Entität gehört. Es kann derselbe Sensor oder ein anderer Domänencontroller aus dieser Domäne sein.

|Protokoll|Dienst|Port|Quelle| Richtung|
|---------|---------|---------|---------|--------|
|LDAP|TCP und UDP|389|Domänencontroller|Ausgehend|
|Sicheres LDAP (LDAPS)|TCP|636|Domänencontroller|Ausgehend|
|LDAP an globalen Katalog|TCP|3268|Domänencontroller|Ausgehend|
|LDAPs an globalen Katalog|TCP|3269|Domänencontroller|Ausgehend|

### <a name="why-dont-activities-always-show-both-the-source-user-and-computer"></a>Warum werden in Aktivitäten nicht immer sowohl der Quellbenutzer als auch der Quellcomputer angezeigt?

Azure ATP erfasst Aktivitäten über viele verschiedene Protokolle. In einigen Fällen empfängt Azure ATP die Daten des Quellbenutzers nicht im Datenverkehr. Dann versucht Azure ATP, die Sitzung des Benutzers mit der Aktivität zu korrelieren. Wenn der Versuch erfolgreich ist, wird der Quellbenutzer der Aktivität angezeigt. Schlagen Korrelationsversuche des Benutzers aber fehl, wird nur der Quellcomputer angezeigt.

## <a name="troubleshooting"></a>Problembehandlung

### <a name="what-should-i-do-if-the-azure-atp-sensor-or-standalone-sensor-doesnt-start"></a>Wie soll ich vorgehen, wenn der Azure ATP-Sensor oder der eigenständige Sensor nicht gestartet wird?

Sehen Sie sich den letzten Fehlereintrag im aktuellen [Fehlerprotokoll](troubleshooting-using-logs.md) an (Installationsverzeichnis von Azure ATP unter dem Ordner „Logs“ (Protokolle)).

## <a name="see-also"></a>Weitere Informationen

- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](prerequisites.md)
- [Azure ATP capacity planning (Azure ATP-Kapazitätsplanung)](capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-forwarding.md)
- [Problembehandlung](troubleshooting-known-issues.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)