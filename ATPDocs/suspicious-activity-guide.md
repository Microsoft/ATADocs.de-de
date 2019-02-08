---
title: Azure ATP-Leitfaden zu Sicherheitswarnungen | Microsoft-Dokumentation
d|Description: This article provides a list of the security alerts issued by Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 02/03/2019
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ca5d1c7b-11a9-4df3-84a5-f53feaf6e561
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f84e49846a0c144da0674b8a4594eab2ee33efba
ms.sourcegitcommit: 9236d279f5e01424b498ce23e9d84c407ebfcdf3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/04/2019
ms.locfileid: "55689352"
---
# <a name="azure-atp-security-alerts"></a>Azure ATP-Sicherheitswarnungen

Azure ATP-Sicherheitswarnungen erklären die durch Azure ATP-Sensoren in Ihrem Netzwerk erkannten verdächtigen Aktivitäten sowie die an den betreffenden Bedrohungen beteiligten Akteure und Computer.   Damit Sie einfach und direkt weitere Untersuchungen durchführen können, enthalten Beweislisten für Sicherheitswarnungen direkte Links zu den betroffenen Benutzern und Computern.

Azure ATP-Sicherheitswarnungen werden in die folgenden Kategorien oder Phasen unterteilt, wie die Phasen in einer typischen „Kill Chain“ eines Cyberangriffs. Öffnen Sie die folgenden Links, um mehr über die einzelnen Phasen, die Warnungen zur Erkennung der verschiedenen Angriffe sowie über die Verwendung der Warnungen zum Schutz Ihres Netzwerks zu erfahren:
  1. [Warnung zu Reconnaissancephase](atp-reconnaissance-alerts.md)
  2. [Warnungen zu Phase der kompromittierten Anmeldeinformationen](atp-compromised-credentials-alerts.md)
  3. [Warnungen zu Lateral Movement-Pfaden](atp-lateral-movement-alerts.md)
  4. [Warnungen zu Domänendominanzphase](atp-domain-dominance-alerts.md)
  5. [Warnungen zu Exfiltrationsphase](atp-exfiltration-alerts.md)

Weitere Informationen zur Struktur und zu gängigen Komponenten der Azure ATP-Sicherheitswarnungen finden Sie unter [Grundlegendes zu Sicherheitswarnungen](understanding-security-alerts.md).

## <a name="security-alert-name-mapping-and-unique-external-ids"></a>Zuordnen von Sicherheitswarnungsnamen und eindeutigen externen IDs

In Version 2.56 wurden alle Sicherheitswarnungen für Azure ATP umbenannt. Die neuen Namen sind jetzt verständlicher. In der folgenden Tabelle sind die neuen und alten Namen sowie die eindeutigen externalIds nebeneinander aufgelistet. Für Skripts oder die Automatisierung empfiehlt Microsoft die Verwendung von externen IDs zur Warnung anstelle von Warnungsnamen, da nur externe IDs dauerhaft für Sicherheitswarnungen verwendet und nicht geändert werden.

> [!div class="mx-tableFixed"] 

|Neuer Sicherheitswarnungsname|Alter Sicherheitswarnungsname|Eindeutige externe ID|
|---------|----------|---------|
|[Reconnaissance mithilfe von Kontoenumeration](atp-reconnaissance-alerts.md#account-enumeration-reconnaissance-external-id-2003)|Reconnaissance mithilfe von Kontoenumeration|2003|
|[Datenexfiltration über SMB](atp-exfiltration-alerts.md#data-exfiltration-over-smb---preview-external-id-2030)| N/V| 2030|
|[Honeytoken-Aktivität](atp-compromised-credentials-alerts.md#honeytoken-activity-external-id-2014)|Honeytoken-Aktivität|2014|
|[Böswillige Anforderung des Datenschutz-API-Hauptschlüssels](atp-domain-dominance-alerts.md#malicious-request-of-data-protection-api-master-key-external-id-2020)|Böswillige Anforderung privater Informationen im Rahmen der Datensicherheit|2020|
|[Reconnaissance über Netzwerkzuordnung (DNS)](atp-reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)|Reconnaissance über DNS|2007|
|[Versuchte Remotecodeausführung](atp-domain-dominance-alerts.md#remote-code-execution-attempt-external-id-2019)|Versuchte Remote-Codeausführung|2019|
|[Remote-Codeausführung über DNS – Vorschau](atp-lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036---preview)|N/V|2036|
|[Vermuteter Brute-Force-Angriff (LDAP)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-ldap-external-id-2004)|Brute-Force-Angriff mithilfe einer einfachen LDAP-Bindung|2004|
|[Vermuteter Brute-Force-Angriff (Kerberos NTLM)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-kerberos-ntlm-external-id-2023)|Verdächtige Authentifizierungsfehler|2023|
|[Vermuteter Brute-Force-Angriff (SMB)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033)|Ungewöhnliche Protokollimplementierung (potenzielle Verwendung schädlicher Tools wie Hydra)|2033|
|[Vermuteter DCShadow-Angriff (Heraufstufung von Domänencontrollern)](atp-domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-promotion-external-id-2028)|Verdächtige Heraufstufung zu Domänencontrollern (potenzieller DcShadow-Angriff)|2028|
|[Vermuteter DCShadow-Angriff (Replikationsanforderung an Domänencontroller)](atp-domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-replication-request-external-id-2029)|Verdächtige Replikationsanforderung von Domänencontroller (potenzieller DCShadow-Angriff)|2029|
|[Vermuteter DCSync-Angriff (Replikation von Verzeichnisdiensten)](atp-domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006)|Böswillige Replikation von Verzeichnisdiensten|2006|
|[Vermutete Golden Ticket-Verwendung (Herabstufung der Verschlüsselung)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-encryption-downgrade-external-id-2009)|Aktivität zur Herabstufung der Verschlüsselung (potenzieller Golden Ticket-Angriff)|2009|
|[Vermutete Golden Ticket-Verwendung (gefälschte Autorisierungsdaten)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-forged-authorization-data-external-id-2013) |Berechtigungsausweitung mithilfe von gefälschten Autorisierungsdaten|2013|
|[Vermutete Golden Ticket-Verwendung (nicht vorhandenes Konto)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-nonexistent-account-external-id-2027)|Kerberos Golden Ticket: nicht vorhandenes Konto|2027|
|[Vermutete Golden Ticket-Verwendung (Ticketanomalie)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-external-id-2032)|N/V|2032|
|[Vermutete Golden Ticket-Verwendung (Zeitanomalie)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-time-anomaly-external-id-2022)|Kerberos Golden Ticket – Zeitanomalie|2022|
|[Vermuteter Identitätsdiebstahl (Pass-the-Hash)](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-hash-external-id-2017)|Identitätsdiebstahl mithilfe eines Pass-the-Hash-Angriffs|2017|
|[Vermuteter Identitätsdiebstahl (Pass-the-Ticket)](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-ticket-external-id-2018)|Identitätsdiebstahl mithilfe eines Pass-the-Ticket-Angriffs|2018|
|[Vermuteter Over-Pass-the-Hash-Angriff (Herabstufung der Verschlüsselung)](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-encryption-downgrade-external-id-2008)|Aktivität zur Herabstufung der Verschlüsselung (potenzieller Overpass-the-Hash-Angriff)|2008|
|[Vermuteter Overpass-the-Hash-Angriff (Kerberos)](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-kerberos-external-id-2002)|Ungewöhnliche Kerberos-Protokollimplementierung (potenzieller Overpass-the-Hash-Angriff)|2002|
|[Vermutete Verwendung des Metasploit-Hackerframeworks](atp-compromised-credentials-alerts.md#suspected-use-of-metasploit-hacking-framework-external-id-2034)|Ungewöhnliche Protokollimplementierung (potenzielle Verwendung schädlicher Hackertools wie Metasploit)|2034|
|[Suspected Skeleton Key attack (encryption downgrade) (Verdacht auf Skeleton-Key-Angriff (Herabstufung der Verschlüsselung)](atp-domain-dominance-alerts.md#suspected-skeleton-key-attack-encryption-downgrade-external-id-2010)|Aktivität zur Herabstufung der Verschlüsselung (potenzieller Skeleton Key-Angriff)|2010|
|[Vermuteter WannaCry-Ransomware-Angriff](atp-compromised-credentials-alerts.md#suspected-wannacry-ransomware-attack-external-id-2035)|Ungewöhnliche Protokollimplementierung (potenzieller WannaCry-Ransomwareangriff)|2035|
|[Verdächtige Kommunikation über DNS](atp-exfiltration-alerts.md#suspicious-communication-over-dns-external-id-2031)|Verdächtige Kommunikation über DNS|2031|
|[Verdächtige Modifizierung von sensiblen Gruppen](atp-domain-dominance-alerts.md#suspicious-modification-of-sensitive-groups-external-id-2024)|Verdächtige Modifizierung von sensiblen Gruppen|2024|
|[Erstellen eines verdächtigen Diensts](atp-domain-dominance-alerts.md#suspicious-service-creation-external-id-2026)|Erstellen eines verdächtigen Diensts|2026|
|[Verdächtige VPN-Verbindung](atp-compromised-credentials-alerts.md#suspicious-vpn-connection-external-id-2025)|Verdächtige VPN-Verbindung|2025|
|[Reconnaissance über Benutzer und Gruppenmitgliedschaften (SAMR)](atp-reconnaissance-alerts.md#user-and-group-membership-reconnaissance-samr-external-id-2021)|Reconnaissance mithilfe von Verzeichnisdienstabfragen|2021|
|[Reconnaissance über Benutzer und IP-Adressen (SMB)](atp-reconnaissance-alerts.md#user-and-ip-address-reconnaissance-smb-external-id-2012)|Reconnaissance mithilfe der SMB-Sitzungsenumeration|2012|

> [!NOTE]
> Wenn Sie eine Sicherheitswarnung deaktivieren möchten, wenden Sie sich an den Support.


## <a name="see-also"></a>Weitere Informationen
- [Arbeiten mit Sicherheitswarnungen](working-with-suspicious-activities.md)
- [Verstehen von Sicherheitswarnungen](understanding-security-alerts.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
