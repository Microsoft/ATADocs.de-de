---
title: Häufig gestellte Fragen zu Microsoft Defender für Identitäten
description: Enthält eine Liste mit häufig gestellten Fragen zu Microsoft Defender für Identity und den zugehörigen Antworten.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/27/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b677512817fc910c5845fa7e1544003bfec60593
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2020
ms.locfileid: "94848940"
---
# <a name="product-long-frequently-asked-questions"></a>[!INCLUDE [Product long](includes/product-long.md)] häufig gestellte Fragen

Dieser Artikel enthält eine Liste mit häufig gestellten Fragen und Antworten, [!INCLUDE [Product long](includes/product-long.md)] die in die folgenden Kategorien unterteilt sind:

- [Was ist [!INCLUDE [Product short](includes/product-short.md)]](#what-is-azure-atp)
- [Lizenzierung und Datenschutz](#licensing-and-privacy)
- [Bereitstellung](#deployment)
- [Vorgänge](#operation)
- [Problembehandlung](#troubleshooting)

<a name="what-is-azure-atp"></a>

## <a name="what-is-product-short"></a>Was ist [!INCLUDE [Product short](includes/product-short.md)]?

### <a name="what-can-product-short-detect"></a>Was kann [!INCLUDE [Product short](includes/product-short.md)] erkennen?

[!INCLUDE [Product short](includes/product-short.md)] erkennt bekannte böswillige Angriffe und Techniken, Sicherheitsprobleme und Risiken in Ihrem Netzwerk.
Die vollständige Liste der [!INCLUDE [Product short](includes/product-short.md)] Erkennungen finden Sie unter Was wird von [Erkennungen [!INCLUDE [Product short](includes/product-short.md)] durchgeführt?](suspicious-activity-guide.md).

### <a name="what-data-does-product-short-collect"></a>Welche Daten werden [!INCLUDE [Product short](includes/product-short.md)] gesammelt?

[!INCLUDE [Product short](includes/product-short.md)] sammelt und speichert Informationen von ihren konfigurierten Servern (Domänen Controller, Mitglieds Server usw.) in einer Datenbank, die für den Dienst für die Verwaltung, Überwachung und Berichterstellung spezifisch ist. Gesammelte Informationen sind unter anderem Netzwerkdatenverkehr von und zu Domänencontrollern (z.B. Kerberos-Authentifizierung, NTLM-Authentifizierung, DNS-Abfragen), Sicherheitsprotokolle (z.B. Windows-Sicherheitsereignisse), Active Directory-Informationen (Struktur, Subnetze, Websites) sowie Entitätsinformationen (z.B. Namen, E-Mail-Adressen und Telefonnummern).

Microsoft verwendet diese Daten zu folgenden Zwecken:

- Zum proaktiven Identifizieren von Angriffsindikatoren (Indicators of Attack, IOAs) in Ihrer Organisation
- Zum Generieren von Warnungen, wenn ein möglicher Angriff erkannt wurde
- Zum Bereitstellen von Sicherheitsvorgängen mit einen Einblick in Entitäten, die mit Bedrohungssignalen aus Ihrem Netzwerk verknüpft sind. So können Sie überprüfen und ermitteln, ob Sicherheitsbedrohungen vorhanden sind.

Microsoft extrahiert Ihre Daten nicht zu Werbezwecken oder anderen Zwecken als die Bereitstellung des Dienstes für Sie.

### <a name="how-many-directory-service-credentials-does-product-short-support"></a>Wie viele Verzeichnisdienst-Anmelde Informationen werden [!INCLUDE [Product short](includes/product-short.md)] unterstützt?

[!INCLUDE [Product short](includes/product-short.md)] unterstützt derzeit das Hinzufügen von bis zu 10 verschiedenen Verzeichnisdienst-Anmelde Informationen zur Unterstützung Active Directory Umgebungen mit nicht vertrauenswürdigen Gesamtstrukturen Wenn Sie weitere Konten benötigen, eröffnen Sie ein Supportticket.

### <a name="does-product-short-only-leverage-traffic-from-active-directory"></a>Nutzt [!INCLUDE [Product short](includes/product-short.md)] nur Datenverkehr von Active Directory?

Zusätzlich zur Analyse Active Directory Datenverkehrs mithilfe der Technologie für die umfassende Paket Untersuchung werden [!INCLUDE [Product short](includes/product-short.md)] von auch relevante Windows-Ereignisse von Ihrem Domänen Controller gesammelt und Entitäts profile basierend auf Informationen aus Active Directory Domain Services erstellt. [!INCLUDE [Product short](includes/product-short.md)] unterstützt auch das Empfangen der RADIUS-Kontoführung von VPN-Protokollen von verschiedenen Anbietern (Microsoft, Cisco, F5 und Checkpoint).

### <a name="does-product-short-monitor-only-domain-joined-devices"></a>Werden von nur in die [!INCLUDE [Product short](includes/product-short.md)] Domäne eingebundenen Geräten überwacht?

Nein. [!INCLUDE [Product short](includes/product-short.md)] überwacht alle Geräte im Netzwerk, die Authentifizierungs-und Autorisierungs Anforderungen für Active Directory ausführen, einschließlich nicht-Windows-und mobiler Geräte.

### <a name="does-product-short-monitor-computer-accounts-as-well-as-user-accounts"></a>[!INCLUDE [Product short](includes/product-short.md)]Überwacht sowohl Computer Konten als auch Benutzerkonten?

Ja. Da Computer Konten (ebenso wie alle anderen Entitäten) zum Durchführen böswilliger Aktivitäten verwendet werden können, [!INCLUDE [Product short](includes/product-short.md)] überwacht das Verhalten aller Computer Konten und aller anderen Entitäten in der Umgebung.

### <a name="what-is-the-difference-between-advanced-threat-analytics-ata-and-product-short"></a>Worin besteht der Unterschied zwischen Advanced Threat Analytics (ATA) und [!INCLUDE [Product short](includes/product-short.md)] ?

ATA ist eine eigenständige lokale Lösung mit mehreren Komponenten, zum Beispiel ATA Center, die dediziert Hardware lokal erfordern.

[!INCLUDE [Product short](includes/product-short.md)] ist eine cloudbasierte Sicherheitslösung, die ihre lokalen Active Directory Signale (Azure AD) nutzt. Die Lösung ist hochgradig skalierbar und wird laufend aktualisiert.

Die endgültige Version von ATA ist [allgemein verfügbar](https://support.microsoft.com/help/4568997/update-3-for-microsoft-advanced-threat-analytics-1-9). ATA wird die grundlegende Unterstützung am 12. Januar 2021 beenden. Der erweiterte Support wird bis zum 2026. Januar fortgesetzt. Weitere Informationen finden Sie in [unserem Blog](https://techcommunity.microsoft.com/t5/microsoft-security-and/end-of-mainstream-support-for-advanced-threat-analytics-january/ba-p/1539181).

Im Gegensatz zum ATA-Sensor verwendet der [!INCLUDE [Product short](includes/product-short.md)] Sensor auch Datenquellen wie z. b. die Ereignis Ablauf Verfolgung für Windows (ETW), [!INCLUDE [Product short](includes/product-short.md)] um zusätzliche Erkennungen bereitzustellen.

[!INCLUDE [Product short](includes/product-short.md)]zu den häufigen Updates zählen die folgenden Features und Funktionen:

- **Unterstützung für [Umgebungen mit mehreren Gesamtstrukturen](multi-forest.md)** : Stellt Sichtbarkeit in Azure AD-Gesamtstrukturen für Organisationen bereit

- **[Bewertungen des Identitätssicherheitsstatus](isp-overview.md)** : Identifizieren häufige Fehlkonfigurationen sowie ausnutzbare Komponenten und stellen Wiederherstellungspfade zum Reduzieren der Angriffsfläche bereit

- **[UEBA-Funktionen](/cloud-app-security/tutorial-ueba)** : Einblicke in Risiken individueller Benutzer über die Bewertung der Benutzeruntersuchungspriorität. Die Bewertung kann SecOps bei der Untersuchung unterstützen und Analysten dabei helfen, ungewöhnliche Aktivitäten für den Benutzer und die Organisation zu verstehen.

- **Native Integrationen**: In Microsoft Cloud App Security und Azure AD Identity Protection integriert, bieten sie eine hybride Ansicht über Vorgänge in den lokalen und hybriden Umgebungen.

- **Beiträgt an Microsoft 365 Defender**: unterstützt Warnungen und Bedrohungs Daten in Microsoft 365 Defender. Microsoft 365 Defender nutzt das Microsoft 365 Sicherheits Portfolio (Identitäten, Endpunkte, Daten und Anwendungen), um Domänen übergreifende Bedrohungs Daten automatisch zu analysieren und so ein umfassendes Bild der einzelnen Angriffe in einem einzelnen Dashboard zu erhalten. Dank dieser breiten-und Übersichtlichkeit können sich die Defender auf kritische Bedrohungen konzentrieren und nach anspruchsvollen Sicherheitsverletzungen suchen, die darauf vertrauen, dass die leistungsstarke Automatisierung von Microsoft 365 Defender Angriffe an einer beliebigen Stelle in der Kill-Kette stoppt und die Organisation in einen sicheren Zustand versetzt.

## <a name="licensing-and-privacy"></a>Lizenzierung und Datenschutz

### <a name="where-can-i-get-a-license-for-product-long"></a>Wo erhalte ich eine Lizenz [!INCLUDE [Product long](includes/product-long.md)] ?

[!INCLUDE [Product short](includes/product-short.md)] ist als Teil von Enterprise Mobility + Security 5 Suite (EMS E5) und als eigenständige Lizenz verfügbar. Sie können eine Lizenz entweder direkt über das [Microsoft 365-Portal](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-pricing) oder über das CSP-Lizenzierungsmodell (Cloud Solution Partner) erwerben.

### <a name="does-product-short-need-only-a-single-license-or-does-it-require-a-license-for-every-user-i-want-to-protect"></a>Ist [!INCLUDE [Product short](includes/product-short.md)] nur eine einzelne Lizenz erforderlich, oder ist eine Lizenz für jeden Benutzer erforderlich, den Sie schützen möchten?

Informationen zu [!INCLUDE [Product short](includes/product-short.md)] Lizenzanforderungen finden Sie im [ [!INCLUDE [Product short](includes/product-short.md)] Leitfaden zur Lizenzierung](/office365/servicedescriptions/microsoft-365-service-descriptions/microsoft-365-tenantlevel-services-licensing-guidance/microsoft-365-security-compliance-licensing-guidance#azure-advanced-threat-protection).

### <a name="is-my-data-isolated-from-other-customer-data"></a>Sind die Daten von anderen Kundendaten isoliert?

Ja, Ihre Daten werden durch Zugriffsauthentifizierung und logischer Trennung basierend auf der Kundennummer getrennt. Jeder Kunde kann nur auf Daten zugreifen, die von der eigenen Organisation gesammelt wurden, sowie auf generische Daten, die von Microsoft bereitgestellt werden.

### <a name="do-i-have-the-flexibility-to-select-where-to-store-my-data"></a>Kann ich frei wählen, wo ich meine Daten speichern möchte?

Nein. Wenn Ihre [!INCLUDE [Product short](includes/product-short.md)] Instanz erstellt wird, wird Sie automatisch in dem Land-Rechenzentrum gespeichert, das dem geografischen Standort Ihres Aad-Mandanten am nächsten liegt. [!INCLUDE [Product short](includes/product-short.md)] Daten können nicht verschoben werden, nachdem die [!INCLUDE [Product short](includes/product-short.md)] Instanz in einem anderen Rechenzentrum erstellt wurde.

### <a name="how-does-microsoft-prevent-malicious-insider-activities-and-abuse-of-high-privilege-roles"></a>Wie verhindert Microsoft schädliche Insideraktivitäten und den Missbrauch von privilegierten Rollen?

Microsoft-Entwickler und -Administratoren verfügen systembedingt über genügend Privilegien zum Ausführen der Ihnen zugewiesenen Aufgaben, um den Dienst zu betreiben und weiterzuentwickeln. Microsoft stellt zum Schützen vor Aktivitäten von unautorisierten Entwicklern und/oder Administratoren eine Kombination aus vorbeugenden und reaktiven Steuerelementen sowie Erkennungssteuerelemente einschließlich der folgenden Mechanismen bereit:

- Enge Zugriffssteuerung für vertrauliche Daten
- Kombination aus Steuerelementen, die die unabhängige Erkennung von schädlicher Aktivität deutlich verbessern
- Mehrere Überwachungs-, Protokollierungs- und Berichterstattungsebenen

Darüber hinaus führt Microsoft Hintergrundüberprüfungen von bestimmten Betriebsmitarbeitern durch und beschränkt den Zugriff auf Anwendungen, Systeme sowie die Netzwerkinfrastruktur im Verhältnis zur Ebene der Hintergrundüberprüfung. Betriebsmitarbeiter folgen einem formellen Prozess, wenn sie bei der Ausübung ihrer Aufgaben auf das Konto eines Kunden oder auf zugehörige Informationen zugreifen müssen.

## <a name="deployment"></a>Bereitstellung

### <a name="how-many-product-short-sensors-do-i-need"></a>Wie viele [!INCLUDE [Product short](includes/product-short.md)] Sensoren benötige ich?

Jeder Domänen Controller in der Umgebung sollte durch einen [!INCLUDE [Product short](includes/product-short.md)] Sensor oder eigenständigen Sensor abgedeckt werden. Weitere Informationen finden Sie unter [ [!INCLUDE [Product short](includes/product-short.md)] Sensor Größen](capacity-planning.md#sizing)Anpassung.

### <a name="does-product-short-work-with-encrypted-traffic"></a>[!INCLUDE [Product short](includes/product-short.md)]Funktioniert mit verschlüsseltem Datenverkehr?

Netzwerkprotokolle mit verschlüsseltem Datenverkehr (z.B. AtSvc und WMI) werden nicht verschlüsselt, sondern von den Sensoren analysiert.

### <a name="does-product-short-work-with-kerberos-armoring"></a>Funktioniert die Verwendung [!INCLUDE [Product short](includes/product-short.md)] von Kerberos armoring?

Die Aktivierung von Kerberos armoring (auch als flexible Authentifizierung Secure Tunneling (fast) bezeichnet) wird von unterstützt [!INCLUDE [Product short](includes/product-short.md)] , mit Ausnahme der over-Pass-the-Hash-Erkennung, die nicht mit Kerberos armoring funktioniert.

### <a name="how-do-i-monitor-a-virtual-domain-controller-using-product-short"></a>Gewusst wie Überwachen eines virtuellen Domänen Controllers mithilfe von [!INCLUDE [Product short](includes/product-short.md)] ?

Die meisten virtuellen Domänen Controller können vom Sensor abgedeckt werden [!INCLUDE [Product short](includes/product-short.md)] , um zu bestimmen, ob der [!INCLUDE [Product short](includes/product-short.md)] Sensor für Ihre Umgebung geeignet ist. Weitere Informationen finden Sie unter [ [!INCLUDE [Product short](includes/product-short.md)] Kapazitätsplanung](capacity-planning.md).

Wenn ein virtueller Domänen Controller nicht durch den Sensor abgedeckt werden kann [!INCLUDE [Product short](includes/product-short.md)] , können Sie einen virtuellen oder physischen [!INCLUDE [Product short](includes/product-short.md)] eigenständigen Sensor wie unter [Konfigurieren der Port Spiegelung](configure-port-mirroring.md)beschrieben haben.  
Die einfachste Möglichkeit besteht darin, [!INCLUDE [Product short](includes/product-short.md)] auf jedem Host, auf dem ein virtueller Domänen Controller vorhanden ist, einen virtuellen eigenständigen Sensor zu haben.  
Wenn die virtuellen Domänencontroller zwischen Hosts verschoben werden, müssen Sie einen der folgenden Schritte ausführen:

- Wenn der virtuelle Domänen Controller auf einen anderen Host verschoben wird, konfigurieren [!INCLUDE [Product short](includes/product-short.md)] Sie den eigenständigen Sensor auf diesem Host so, dass der Datenverkehr vom kürzlich verschobene virtuellen Domänen Controller empfangen wird.
- Stellen Sie sicher, dass Sie den virtuellen [!INCLUDE [Product short](includes/product-short.md)] eigenständigen Sensor dem virtuellen Domänen Controller angleichen, damit der [!INCLUDE [Product short](includes/product-short.md)] eigenständige Sensor bei der Verschiebung mit dem virtuellen Domänen Controller verschoben wird.
- Es gibt einige virtuelle Switches, über die der Datenverkehr zwischen Hosts gesendet werden kann.

### <a name="how-do-i-configure-the-product-short-sensors-to-communicate-with-product-short-cloud-service-when-i-have-a-proxy"></a>Gewusst wie die Sensoren so konfigurieren [!INCLUDE [Product short](includes/product-short.md)] , dass Sie mit dem [!INCLUDE [Product short](includes/product-short.md)] clouddienst kommunizieren, wenn ich über einen Proxy verfüge?

Für die Kommunikation Ihrer Domänencontroller mit dem Clouddienst müssen Sie in Ihrer Firewall und auf Ihrem Proxyserver Port 443 für „*.atp.azure.com“ freigeben. Anweisungen dazu finden Sie unter [Konfigurieren des Proxys oder der Firewall zum Aktivieren der Kommunikation mit [!INCLUDE [Product short](includes/product-short.md)] Sensoren](configure-proxy.md).

### <a name="can-product-short-monitored-domain-controllers-be-virtualized-on-your-iaas-solution"></a>Können [!INCLUDE [Product short](includes/product-short.md)] überwachte Domänen Controller in ihrer IaaS-Lösung virtualisiert werden?

Ja, Sie können den [!INCLUDE [Product short](includes/product-short.md)] Sensor zum Überwachen von Domänen Controllern verwenden, die sich in einer beliebigen IaaS-Lösung befinden.

### <a name="can-product-short-support-multi-domain-and-multi-forest"></a>Können [!INCLUDE [Product short](includes/product-short.md)] mehrere Domänen und mehrere Gesamtstrukturen unterstützt werden?

[!INCLUDE [Product short](includes/product-short.md)] unterstützt Umgebungen mit mehreren Domänen und mehrere Gesamtstrukturen. Weitere Informationen und Anforderungen in Bezug auf Vertrauensstellungen finden Sie unter [Unterstützung für mehrere Gesamtstrukturen](multi-forest.md).

### <a name="can-you-see-the-overall-health-of-the-deployment"></a>Kann die Gesamtintegrität der Bereitstellung angezeigt werden?

Ja, Sie können die allgemeine Integrität der Bereitstellung sowie spezifische Probleme im Zusammenhang mit der Konfiguration, Konnektivität usw. anzeigen, und Sie werden benachrichtigt, sobald Sie mit Integritäts [!INCLUDE [Product short](includes/product-short.md)] Warnungen auftreten.

## <a name="operation"></a>Vorgang

### <a name="what-kind-of-integration-does-product-short-have-with-siems"></a>Welche Art von Integration bietet [!INCLUDE [Product short](includes/product-short.md)] Siems?

[!INCLUDE [Product short](includes/product-short.md)] kann so konfiguriert werden, dass eine syslog-Warnung an alle Siem-Server gesendet wird, die das CEF-Format verwenden, um Integritäts Warnungen und eine Sicherheitswarnung zu erhalten. Weitere Informationen finden Sie unter [Referenz zum SIEM-Protokoll](cef-format-sa.md).

### <a name="why-are-certain-accounts-considered-sensitive"></a>Warum gelten bestimmte Konten als sensible Konten?

Dies ist der Fall, wenn ein Konto Mitglied bestimmter Gruppen ist, die als sensibel festgelegt sind (z. B. „Domänen-Admins“).

Um nachzuvollziehen, warum ein Konto ein sensibles Konto ist, können Sie seine Gruppenmitgliedschaft überprüfen, um festzustellen, welchen sensiblen Gruppen es angehört (die Gruppe, der das Konto angehört, kann auch wegen einer anderen Gruppe eine sensible Gruppe sein. Daher sollten Sie immer die höchste sensible Gruppe überprüfen). Sie können auch manuell [Konten als vertraulich kennzeichnen](sensitive-accounts.md).

### <a name="do-you-have-to-write-your-own-rules-and-create-a-thresholdbaseline"></a>Müssen eigene Regeln geschrieben und ein Schwellenwert/eine Basislinie erstellt werden?

Mit [!INCLUDE [Product short](includes/product-short.md)] ist es nicht erforderlich, Regeln, Schwellenwerte oder Basis Linien zu erstellen und dann eine Feinabstimmung durchführen. [!INCLUDE [Product short](includes/product-short.md)] analysiert das Verhalten von Benutzern, Geräten und Ressourcen sowie deren Beziehungen untereinander und kann eine verdächtige Aktivität und bekannte Angriffe schnell erkennen. Drei Wochen nach der Bereitstellung [!INCLUDE [Product short](includes/product-short.md)] beginnt, verdächtige Verhaltens Aktivitäten zu erkennen. Auf der anderen Seite [!INCLUDE [Product short](includes/product-short.md)] werden bekannte böswillige Angriffe und Sicherheitsprobleme sofort nach der Bereitstellung erkennen.

### <a name="which-traffic-does-product-short-generate-in-the-network-from-domain-controllers-and-why"></a>Welcher Datenverkehr wird [!INCLUDE [Product short](includes/product-short.md)] von Domänen Controllern im Netzwerk generiert und warum?

[!INCLUDE [Product short](includes/product-short.md)] generiert Datenverkehr von Domänen Controllern zu Computern in der Organisation in einem von drei Szenarien:

1. **Netzwerknamensauflösung**  
[!INCLUDE [Product short](includes/product-short.md)] erfasst Datenverkehr und Ereignisse, das Erlernen und die Profilerstellung für Benutzer und Computeraktivitäten im Netzwerk. Zum Erlernen und Erstellen von Profilen für Aktivitäten gemäß den Computern in der Organisation [!INCLUDE [Product short](includes/product-short.md)] muss IPS in Computer Konten aufgelöst werden. Zum Auflösen von IP-Adressen für Computernamen können Sie [!INCLUDE [Product short](includes/product-short.md)] die IP-Adresse des Computer namens *hinter* der IP-Adresse anfordern.

    Anforderungen erfolgen mithilfe einer von vier Methoden:
    - NTLM über RPC (TCP-Port 135)
    - NetBIOS (UDP-Port 137)
    - RDP (TCP-Port 3389)
    - Abfragen des DNS-Servers mittels Reverse-DNS-Lookup der IP-Adresse (UDP 53)

    Nachdem Sie den Computernamen erhalten haben,  [!INCLUDE [Product short](includes/product-short.md)] überprüfen die Sensoren die Details in Active Directory, um festzustellen, ob ein korreliertes Computer Objekt mit demselben Computernamen vorhanden ist. Wenn eine Übereinstimmung gefunden wird, erfolgt eine Zuordnung zwischen der IP-Adresse und dem übereinstimmenden Computerobjekt.
2. **Lateral-Movement-Pfad (LMP)**  
Um potenzielle LMPS für sensible Benutzer zu erstellen, sind [!INCLUDE [Product short](includes/product-short.md)] Informationen zu den lokalen Administratoren auf Computern erforderlich. In diesem Szenario verwendet der [!INCLUDE [Product short](includes/product-short.md)] Sensor Sam-R (TCP 445) zum Abfragen der im Netzwerk Datenverkehr identifizierten IP-Adresse, um die lokalen Administratoren des Computers zu bestimmen. Weitere Informationen zu [!INCLUDE [Product short](includes/product-short.md)] und Sam-r finden Sie unter [Konfigurieren von Sam-r erforderliche Berechtigungen](install-step8-samr.md).

3. **Abfragen von Active Directory über LDAP** für Entitätsdaten  
[!INCLUDE [Product short](includes/product-short.md)] Sensoren Fragen den Domänen Controller aus der Domäne ab, zu der die Entität gehört. Es kann derselbe Sensor oder ein anderer Domänencontroller aus dieser Domäne sein.

|Protokoll|Dienst|Port|Quelle| Richtung|
|---------|---------|---------|---------|--------|
|LDAP|TCP und UDP|389|Domänencontroller|Ausgehend|
|Sicheres LDAP (LDAPS)|TCP|636|Domänencontroller|Ausgehend|
|LDAP an globalen Katalog|TCP|3268|Domänencontroller|Ausgehend|
|LDAPs an globalen Katalog|TCP|3269|Domänencontroller|Ausgehend|

### <a name="why-dont-activities-always-show-both-the-source-user-and-computer"></a>Warum werden in Aktivitäten nicht immer sowohl der Quellbenutzer als auch der Quellcomputer angezeigt?

[!INCLUDE [Product short](includes/product-short.md)] erfasst Aktivitäten über viele verschiedene Protokolle. In manchen Fällen [!INCLUDE [Product short](includes/product-short.md)] empfängt nicht die Daten des Quell Benutzers im Datenverkehr. [!INCLUDE [Product short](includes/product-short.md)] versucht, die Sitzung des Benutzers mit der-Aktivität zu korrelieren, und wenn der Versuch erfolgreich ist, wird der Quell Benutzer der Aktivität angezeigt. Schlagen Korrelationsversuche des Benutzers aber fehl, wird nur der Quellcomputer angezeigt.

## <a name="troubleshooting"></a>Problembehandlung

### <a name="what-should-i-do-if-the-product-short-sensor-or-standalone-sensor-doesnt-start"></a>Was soll ich tun, wenn der [!INCLUDE [Product short](includes/product-short.md)] Sensor oder der eigenständige Sensor nicht gestartet wird?

Sehen Sie sich den letzten Fehler im aktuellen Fehler [Protokoll](troubleshooting-using-logs.md) an (in dem [!INCLUDE [Product short](includes/product-short.md)] unter dem Ordner "Logs" installiert ist).

## <a name="see-also"></a>Weitere Informationen

- [Voraussetzungen für [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md)
- [Kapazitätsplanung für [!INCLUDE [Product short](includes/product-short.md)]](capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-forwarding.md)
- [Problembehandlung](troubleshooting-known-issues.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
