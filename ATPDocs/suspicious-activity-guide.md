---
title: Leitfaden zu Azure ATP-Sicherheitswarnungen
d|Description: This article provides a list of the security alerts issued by Azure ATP.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 01/22/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: ca5d1c7b-11a9-4df3-84a5-f53feaf6e561
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 39fbd3f42cfccd60a007b8640421a8af1c178243
ms.sourcegitcommit: 8bb80eaef3c2a1085834b98839564c5d37334f56
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/22/2020
ms.locfileid: "76515679"
---
# <a name="azure-atp-security-alerts"></a>Azure ATP-Sicherheitswarnungen

> [!NOTE]
> Die auf dieser Seite erläuterten Azure ATP-Features sind auch über das neue [Portal](https://portal.cloudappsecurity.com) zugänglich.

Azure ATP-Sicherheitswarnungen erklären die durch Azure ATP-Sensoren in Ihrem Netzwerk erkannten verdächtigen Aktivitäten sowie die an den betreffenden Bedrohungen beteiligten Akteure und Computer. Damit Sie einfach und direkt weitere Untersuchungen durchführen können, enthalten Beweislisten für Sicherheitswarnungen direkte Links zu den betroffenen Benutzern und Computern.

Azure ATP-Sicherheitswarnungen werden in die folgenden Kategorien oder Phasen unterteilt, wie die Phasen in einer typischen „Kill Chain“ eines Cyberangriffs. Öffnen Sie die folgenden Links, um mehr über die einzelnen Phasen, die Warnungen zur Erkennung der verschiedenen Angriffe sowie über die Verwendung der Warnungen zum Schutz Ihres Netzwerks zu erfahren:

  1. [Warnung zu Reconnaissancephase](atp-reconnaissance-alerts.md)
  2. [Warnungen zu Phase der kompromittierten Anmeldeinformationen](atp-compromised-credentials-alerts.md)
  3. [Lateral movement phase alerts (Warnung zur Lateral Movement-Phase)](atp-lateral-movement-alerts.md)
  4. [Warnungen zu Domänendominanzphase](atp-domain-dominance-alerts.md)
  5. [Warnungen zu Exfiltrationsphase](atp-exfiltration-alerts.md)

Weitere Informationen zur Struktur und zu gängigen Komponenten der Azure ATP-Sicherheitswarnungen finden Sie unter [Understanding security alerts (Grundlegendes zu Sicherheitswarnungen)](understanding-security-alerts.md).

## <a name="security-alert-name-mapping-and-unique-external-ids"></a>Zuordnen von Sicherheitswarnungsnamen und eindeutigen externen IDs

In der folgenden Tabelle wird die Zuordnung zwischen den Warnungsnamen, den entsprechenden eindeutigen externen IDs und ihren Microsoft Cloud App Security-Warnungs-IDs aufgelistet. Für Skripts oder die Automatisierung empfiehlt Microsoft die Verwendung von externen IDs zur Warnung anstelle von Warnungsnamen, da nur externe IDs dauerhaft für Sicherheitswarnungen verwendet und nicht geändert werden.

# <a name="external-idstabexternal"></a>[Externe IDs](#tab/external)

> [!div class="mx-tdBreakAll"]
> |Neuer Sicherheitswarnungsname|Eindeutige externe ID|Schweregrad|MITRE ATT&CK Matrix™|
> |---|---|---|---|
> |[Reconnaissance mithilfe von Kontoenumeration](atp-reconnaissance-alerts.md#account-enumeration-reconnaissance-external-id-2003)|2003|Mittel|Ermittlung|
> |[Datenexfiltration über den SMB](atp-exfiltration-alerts.md#data-exfiltration-over-smb-external-id-2030)|2030|Hoch|Exfiltration,<br>Seitliche Verschiebung,<br>Befehl und Steuerelement|
> |[Honeytoken-Aktivität](atp-compromised-credentials-alerts.md#honeytoken-activity-external-id-2014)|2014|Mittel|Zugriff über Anmeldeinformationen,<br>Ermittlung|
> |[Malicious request of Data Protection API master key (Böswillige Anforderung eines Masterschlüssels zur Datenschutz-API)](atp-domain-dominance-alerts.md#malicious-request-of-data-protection-api-master-key-external-id-2020)|2020|Hoch|Zugriff über Anmeldeinformationen|
> |[Reconnaissance über Netzwerkzuordnung (DNS)](atp-reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)|2007|Mittel|Ermittlung|
> |[Versuchte Remotecodeausführung](atp-domain-dominance-alerts.md#remote-code-execution-attempt-external-id-2019)|2019|Mittel|Ausführung,<br>Persistenz,<br>Ausweitung von Berechtigungen,<br>Umgehung der Verteidigung,<br>Seitliche Verschiebung|
> |[Remotecodeausführung über DNS](atp-lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036)|2036|Mittel|Ausweitung von Berechtigungen,<br>Seitliche Verschiebung|
> |[Sicherheitsprinzipalreconnaissance (LDAP)](atp-reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038)|2038|Mittel|Zugriff über Anmeldeinformationen|
> |[Suspected Brute Force attack (Kerberos NTLM) (Verdacht auf einen Brute-Force-Angriff (Kerberos NTLM))](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-kerberos-ntlm-external-id-2023)|2023|Mittel|Zugriff über Anmeldeinformationen|
> |[Suspected Brute Force attack (LDAP) (Verdacht auf einen Brute-Force-Angriff (LDAP))](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-ldap-external-id-2004)|2004|Mittel|Zugriff über Anmeldeinformationen|
> |[Suspected Brute Force attack (SMB) (Verdacht auf einen Brute-Force-Angriff (SMB))](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033)|2033|Mittel|Seitliche Verschiebung|
> |[Suspected DCShadow attack (domain controller promotion) (Verdacht auf DCShadow-Angriff (Heraufstufung von Domänencontrollern))](atp-domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-promotion-external-id-2028)|2028|Hoch|Umgehung der Verteidigung|
> |[Verdacht auf DCShadow-Angriff (Replikationsanforderung an Domänencontroller)](atp-domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-replication-request-external-id-2029)|2029|Hoch|Umgehung der Verteidigung|
> |[Suspected DCSync attack (replication of directory services) (Verdacht auf einen DCSync-Angriff (Replikation von Verzeichnisdiensten))](atp-domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006)|2006|Hoch|Persistenz,<br>Zugriff über Anmeldeinformationen|
> |[Verdacht auf Verwendung eines Golden Ticket (Herabstufung der Verschlüsselung)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-encryption-downgrade-external-id-2009)|2009|Mittel|Ausweitung von Berechtigungen,<br>Seitliche Verschiebung,<br>Persistenz|
> |[Suspected Golden Ticket usage (forged authorization data) (Verdacht auf Verwendung eines Golden Ticket (gefälschte Autorisierungsdaten))](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-forged-authorization-data-external-id-2013)|2013|Hoch|Ausweitung von Berechtigungen,<br>Seitliche Verschiebung,<br>Persistenz|
> |[Suspected Golden Ticket usage (nonexistent account) (Verdacht auf Verwendung eines Golden Ticket (nicht vorhandenes Konto))](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-nonexistent-account-external-id-2027)|2027|Hoch|Ausweitung von Berechtigungen,<br>Seitliche Verschiebung,<br>Persistenz|
> |[Vermutete Golden Ticket-Verwendung (Ticketanomalie)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-external-id-2032)|2032|Hoch|Ausweitung von Berechtigungen,<br>Seitliche Verschiebung,<br>Persistenz|
> |[Suspected golden ticket usage (time anomaly) (Verdacht auf Verwendung eines Golden Ticket (Zeitanomalie))](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-time-anomaly-external-id-2022)|2022|Hoch|Ausweitung von Berechtigungen,<br>Seitliche Verschiebung,<br>Persistenz|
> |[Suspected identity theft (Pass-the-Hash) (Verdacht auf Identitätsdiebstahl (Pass-the-Hash))](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-hash-external-id-2017)|2017|Hoch|Seitliche Verschiebung|
> |[Suspected identity theft (Pass-the-Ticket) (Verdacht auf Identitätsdiebstahl (Pass-the-Ticket))](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-ticket-external-id-2018)|2018|Hoch oder Mittel|Seitliche Verschiebung|
> |[Suspected NTLM authentication tampering (Vermutete Manipulation der NTLM-Authentifizierung)](atp-lateral-movement-alerts.md#suspected-ntlm-authentication-tampering-external-id-2039)|2039|Mittel|Ausweitung von Berechtigungen, <br>Seitliche Verschiebung|
> |[Vermuteter NTLM-Relaisangriff](atp-lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037)|2037|Mittel oder Niedrig, wenn mithilfe von signiertem NTLMv2-Protokoll beobachtet|Ausweitung von Berechtigungen, <br>Seitliche Verschiebung|
> |[Suspected over-pass-the-hash attack (encryption downgrade) (Verdacht auf Over-Pass-the-Hash-Angriff (Herabstufung der Verschlüsselung))](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-encryption-downgrade-external-id-2008)|2008|Mittel|Seitliche Verschiebung|
> |[Suspected overpass-the-hash attack (Kerberos) (Verdacht auf einen Overpass-the-Hash-Angriff (Kerberos))](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-kerberos-external-id-2002)|2002|Mittel|Seitliche Verschiebung|
> |[Suspected Skeleton Key attack (encryption downgrade) (Verdacht auf Skeleton-Key-Angriff (Herabstufung der Verschlüsselung))](atp-domain-dominance-alerts.md#suspected-skeleton-key-attack-encryption-downgrade-external-id-2010)|2010|Mittel|Seitliche Verschiebung,<br>Persistenz|
> |[Suspected use of Metasploit hacking framework](atp-compromised-credentials-alerts.md#suspected-use-of-metasploit-hacking-framework-external-id-2034)|2034|Mittel|Seitliche Verschiebung|
> |[Suspected WannaCry ransomware attack (Verdacht auf einen WannaCry-Ransomangriff)](atp-compromised-credentials-alerts.md#suspected-wannacry-ransomware-attack-external-id-2035)|2035|Mittel|Seitliche Verschiebung|
> |[Verdächtige Ergänzungen zu sensiblen Gruppen](atp-domain-dominance-alerts.md#suspicious-additions-to-sensitive-groups-external-id-2024)|2024|Mittel|Zugriff über Anmeldeinformationen,<br>Persistenz|
> |[Verdächtige Kommunikation über DNS](atp-exfiltration-alerts.md#suspicious-communication-over-dns-external-id-2031)|2031|Mittel|Exfiltration|
> |[Erstellung von verdächtigen Diensten](atp-domain-dominance-alerts.md#suspicious-service-creation-external-id-2026)|2026|Mittel|Ausführung,<br>Persistenz,<br>Ausweitung von Berechtigungen,<br>Umgehung der Verteidigung,<br>Seitliche Verschiebung|
> |[Verdächtige VPN-Verbindung](atp-compromised-credentials-alerts.md#suspicious-vpn-connection-external-id-2025)|2025|Mittel|Persistenz,<br>Umgehung der Verteidigung|
> |[User and group membership reconnaissance (SAMR) (Reconnaissance über Benutzer und Gruppenmitgliedschaften (SAMR))](atp-reconnaissance-alerts.md#user-and-group-membership-reconnaissance-samr-external-id-2021)|2021|Mittel|Ermittlung|
> |[Reconnaissance über Benutzer und IP-Adressen (SMB)](atp-reconnaissance-alerts.md#user-and-ip-address-reconnaissance-smb-external-id-2012)|2012|Mittel|Ermittlung|

# <a name="cloud-app-security-idstabcloud-app-security"></a>[Cloud App Security-API](#tab/cloud-app-security)

> [!div class="mx-tdBreakAll"]
> |Neuer Sicherheitswarnungsname|Cloud App Security-Warnungs-ID|
> |---|---|
> |[Reconnaissance mithilfe von Kontoenumeration](atp-reconnaissance-alerts.md#account-enumeration-reconnaissance-external-id-2003)|ALERT_EXTERNAL_AATP_ACCOUNT_ENUMERATION_SECURITY_ALERT|
> |[Datenexfiltration über den SMB](atp-exfiltration-alerts.md#data-exfiltration-over-smb-external-id-2030)|ALERT_EXTERNAL_AATP_SMB_DATA_EXFILTRATION_SECURITY_ALERT|
> |[Honeytoken-Aktivität](atp-compromised-credentials-alerts.md#honeytoken-activity-external-id-2014)|ALERT_EXTERNAL_AATP_HONEYTOKEN_ACTIVITY_SECURITY_ALERT|
> |[Malicious request of Data Protection API master key (Böswillige Anforderung eines Masterschlüssels zur Datenschutz-API)](atp-domain-dominance-alerts.md#malicious-request-of-data-protection-api-master-key-external-id-2020)|ALERT_EXTERNAL_AATP_RETRIEVE_DATA_PROTECTION_BACKUP_KEY_SECURITY_ALERT|
> |[Reconnaissance über Netzwerkzuordnung (DNS)](atp-reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)|ALERT_EXTERNAL_AATP_DNS_RECONNAISSANCE_SECURITY_ALERT|
> |[Versuchte Remotecodeausführung](atp-domain-dominance-alerts.md#remote-code-execution-attempt-external-id-2019)|ALERT_EXTERNAL_AATP_REMOTE_EXECUTION_SECURITY_ALERT|
> |[Remotecodeausführung über DNS](atp-lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036)|ALERT_EXTERNAL_AATP_DNS_REMOTE_CODE_EXECUTION_SECURITY_ALERT|
> |[Sicherheitsprinzipalreconnaissance (LDAP)](atp-reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038)|ALERT_EXTERNAL_AATP_LDAP_SEARCH_RECONNAISSANCE_SECURITY_ALERT|
> |[Suspected Brute Force attack (Kerberos NTLM) (Verdacht auf einen Brute-Force-Angriff (Kerberos NTLM))](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-kerberos-ntlm-external-id-2023)|ALERT_EXTERNAL_AATP_REMOTE_EXECUTION_SECURITY_ALERT|
> |[Suspected Brute Force attack (LDAP) (Verdacht auf einen Brute-Force-Angriff (LDAP))](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-ldap-external-id-2004)|ALERT_EXTERNAL_AATP_LDAP_BRUTE_FORCE_SECURITY_ALERT|
> |[Suspected Brute Force attack (SMB) (Verdacht auf einen Brute-Force-Angriff (SMB))](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033)|ALERT_EXTERNAL_AATP_ABNORMAL_SMB_BRUTE_FORCE_SECURITY_ALERT|
> |[Suspected DCShadow attack (domain controller promotion) (Verdacht auf DCShadow-Angriff (Heraufstufung von Domänencontrollern))](atp-domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-promotion-external-id-2028)|ALERT_EXTERNAL_AATP_DIRECTORY_SERVICES_ROGUE_PROMOTION_SECURITY_ALERT|
> |[Verdacht auf DCShadow-Angriff (Replikationsanforderung an Domänencontroller)](atp-domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-replication-request-external-id-2029)|ALERT_EXTERNAL_AATP_DIRECTORY_SERVICES_ROGUE_PROMOTION_SECURITY_ALERT|
> |[Suspected DCSync attack (replication of directory services) (Verdacht auf einen DCSync-Angriff (Replikation von Verzeichnisdiensten))](atp-domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006)|ALERT_EXTERNAL_AATP_DIRECTORY_SERVICES_REPLICATION_SECURITY_ALERT|
> |[Verdacht auf Verwendung eines Golden Ticket (Herabstufung der Verschlüsselung)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-encryption-downgrade-external-id-2009)|ALERT_EXTERNAL_AATP_GOLDEN_TICKET_ENCRYPTION_DOWNGRADE_SECURITY_ALERT|
> |[Suspected Golden Ticket usage (forged authorization data) (Verdacht auf Verwendung eines Golden Ticket (gefälschte Autorisierungsdaten))](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-forged-authorization-data-external-id-2013)|ALERT_EXTERNAL_AATP_FORGED_PAC_SECURITY_ALERT|
> |[Suspected Golden Ticket usage (nonexistent account) (Verdacht auf Verwendung eines Golden Ticket (nicht vorhandenes Konto))](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-nonexistent-account-external-id-2027)|ALERT_EXTERNAL_AATP_FORGED_PRINCIPAL_SECURITY_ALERT|
> |[Vermutete Golden Ticket-Verwendung (Ticketanomalie)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-external-id-2032)|ALERT_EXTERNAL_AATP_GOLDEN_TICKET_SIZE_ANOMALY_SECURITY_ALERT|
> |[Suspected golden ticket usage (time anomaly) (Verdacht auf Verwendung eines Golden Ticket (Zeitanomalie))](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-time-anomaly-external-id-2022)|ALERT_EXTERNAL_AATP_GOLDEN_TICKET_SECURITY_ALERT|
> |[Suspected identity theft (Pass-the-Hash) (Verdacht auf Identitätsdiebstahl (Pass-the-Hash))](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-hash-external-id-2017)|ALERT_EXTERNAL_AATP_PASS_THE_HASH_SECURITY_ALERT|
> |[Suspected identity theft (Pass-the-Ticket) (Verdacht auf Identitätsdiebstahl (Pass-the-Ticket))](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-ticket-external-id-2018)|ALERT_EXTERNAL_AATP_PASS_THE_TICKET_SECURITY_ALERT|
> |[Suspected NTLM authentication tampering (Vermutete Manipulation der NTLM-Authentifizierung)](atp-lateral-movement-alerts.md#suspected-ntlm-authentication-tampering-external-id-2039)|ALERT_EXTERNAL_AATP_ABNORMAL_NTLM_SIGNING_SECURITY_ALERT|
> |[Vermuteter NTLM-Relaisangriff](atp-lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037)|ALERT_EXTERNAL_AATP_NTLM_RELAY_SECURITY_ALERT|
> |[Suspected over-pass-the-hash attack (encryption downgrade) (Verdacht auf Over-Pass-the-Hash-Angriff (Herabstufung der Verschlüsselung))](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-encryption-downgrade-external-id-2008)|ALERT_EXTERNAL_AATP_OVERPASS_THE_HASH_ENCRYPTION_DOWNGRADE_SECURITY_ALERT|
> |[Suspected overpass-the-hash attack (Kerberos) (Verdacht auf einen Overpass-the-Hash-Angriff (Kerberos))](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-kerberos-external-id-2002)|ALERT_EXTERNAL_AATP_ABNORMAL_KERBEROS_OVERPASS_THE_HASH_SECURITY_ALERT|
> |[Suspected Skeleton Key attack (encryption downgrade) (Verdacht auf Skeleton-Key-Angriff (Herabstufung der Verschlüsselung))](atp-domain-dominance-alerts.md#suspected-skeleton-key-attack-encryption-downgrade-external-id-2010)|ALERT_EXTERNAL_AATP_SKELETON_KEY_ENCRYPTION_DOWNGRADE_SECURITY_ALERT|
> |[Suspected use of Metasploit hacking framework](atp-compromised-credentials-alerts.md#suspected-use-of-metasploit-hacking-framework-external-id-2034)|ALERT_EXTERNAL_AATP_ABNORMAL_SMB_METASPLOIT_SECURITY_ALERT|
> |[Suspected WannaCry ransomware attack (Verdacht auf einen WannaCry-Ransomangriff)](atp-compromised-credentials-alerts.md#suspected-wannacry-ransomware-attack-external-id-2035)|ALERT_EXTERNAL_AATP_ABNORMAL_SMB_WANNA_CRY_SECURITY_ALERT|
> |[Verdächtige Ergänzungen zu sensiblen Gruppen](atp-domain-dominance-alerts.md#suspicious-additions-to-sensitive-groups-external-id-2024)|ALERT_EXTERNAL_AATP_ABNORMAL_SENSITIVE_GROUP_MEMBERSHIP_CHANGE_SECURITY_ALERT|
> |[Verdächtige Kommunikation über DNS](atp-exfiltration-alerts.md#suspicious-communication-over-dns-external-id-2031)|ALERT_EXTERNAL_AATP_DNS_SUSPICIOUS_COMMUNICATION_SECURITY_ALERT|
> |[Erstellung von verdächtigen Diensten](atp-domain-dominance-alerts.md#suspicious-service-creation-external-id-2026)|ALERT_EXTERNAL_AATP_MALICIOUS_SERVICE_CREATION_SECURITY_ALERT|
> |[Verdächtige VPN-Verbindung](atp-compromised-credentials-alerts.md#suspicious-vpn-connection-external-id-2025)|ALERT_EXTERNAL_AATP_ABNORMAL_VPN_SECURITY_ALERT|
> |[User and group membership reconnaissance (SAMR) (Reconnaissance über Benutzer und Gruppenmitgliedschaften (SAMR))](atp-reconnaissance-alerts.md#user-and-group-membership-reconnaissance-samr-external-id-2021)|ALERT_EXTERNAL_AATP_SAMR_RECONNAISSANCE_SECURITY_ALERT|
> |[Reconnaissance über Benutzer und IP-Adressen (SMB)](atp-reconnaissance-alerts.md#user-and-ip-address-reconnaissance-smb-external-id-2012)|ALERT_EXTERNAL_AATP_ENUMERATE_SESSIONS_SECURITY_ALERT|

> [!NOTE]
> Wenn Sie eine Sicherheitswarnung deaktivieren möchten, wenden Sie sich an den Support.

## <a name="see-also"></a>Weitere Informationen

- [Arbeiten mit Sicherheitswarnungen](working-with-suspicious-activities.md)
- [Verstehen von Sicherheitswarnungen](understanding-security-alerts.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
