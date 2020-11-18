---
title: Leitfaden für Microsoft Defender for Identity-Sicherheitswarnungen
description: Dieser Artikel enthält eine Liste der Sicherheitswarnungen, die von Microsoft Defender for Identity ausgegeben werden.
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
ms.openlocfilehash: b343d5a708791de4658389985423f104e3f57762
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2020
ms.locfileid: "94846696"
---
# <a name="product-long-security-alerts"></a>[!INCLUDE [Product long](includes/product-long.md)]-Sicherheitswarnungen

> [!NOTE]
> Die auf dieser Seite erläuterten [!INCLUDE [Product long](includes/product-long.md)]-Features sind auch über das neue [Portal](https://portal.cloudappsecurity.com) zugänglich.

[!INCLUDE [Product long](includes/product-long.md)]-Sicherheitswarnungen erklären die durch [!INCLUDE [Product short](includes/product-short.md)]-Sensoren in Ihrem Netzwerk erkannten verdächtigen Aktivitäten sowie die an den betreffenden Bedrohungen beteiligten Akteure und Computer. Damit Sie einfach und direkt weitere Untersuchungen durchführen können, enthalten Beweislisten für Sicherheitswarnungen direkte Links zu den betroffenen Benutzern und Computern.

[!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnungen werden in die folgenden Kategorien oder Phasen unterteilt, wie die Phasen in einer typischen „Kill Chain“ eines Cyberangriffs. Öffnen Sie die folgenden Links, um mehr über die einzelnen Phasen, die Warnungen zur Erkennung der verschiedenen Angriffe sowie über die Verwendung der Warnungen zum Schutz Ihres Netzwerks zu erfahren:

1. [Warnung zu Reconnaissancephase](reconnaissance-alerts.md)
1. [Warnungen zu Phase der kompromittierten Anmeldeinformationen](compromised-credentials-alerts.md)
1. [Lateral movement phase alerts (Warnung zur Lateral Movement-Phase)](lateral-movement-alerts.md)
1. [Warnungen zu Domänendominanzphase](domain-dominance-alerts.md)
1. [Warnungen zu Exfiltrationsphase](exfiltration-alerts.md)

Weitere Informationen zur Struktur und zu gängigen Komponenten der [!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnungen finden Sie unter [Understanding security alerts](understanding-security-alerts.md) (Grundlegendes zu Sicherheitswarnungen).

## <a name="security-alert-name-mapping-and-unique-external-ids"></a>Zuordnen von Sicherheitswarnungsnamen und eindeutigen externen IDs

In der folgenden Tabelle wird die Zuordnung zwischen den Warnungsnamen, den entsprechenden eindeutigen externen IDs und ihren Microsoft Cloud App Security-Warnungs-IDs aufgelistet. Für Skripts oder die Automatisierung empfiehlt Microsoft die Verwendung von externen IDs zur Warnung anstelle von Warnungsnamen, da nur externe IDs dauerhaft für Sicherheitswarnungen verwendet und nicht geändert werden.

# <a name="external-ids"></a>[Externe IDs](#tab/external)

> [!div class="mx-tdBreakAll"]
> |Sicherheitswarnungsname|Eindeutige externe ID|Schweregrad|MITRE ATT&CK Matrix&trade;|
> |---|---|---|---|
> |[Reconnaissance mithilfe von Kontoenumeration](reconnaissance-alerts.md#account-enumeration-reconnaissance-external-id-2003)|2003|Mittel|Ermittlung|
> |[Active Directory-Attributreconnaissance (LDAP)](reconnaissance-alerts.md#active-directory-attributes-reconnaissance-ldap-external-id-2210)|2210|Mittel|Ermittlung|
> |[Datenexfiltration über den SMB](exfiltration-alerts.md#data-exfiltration-over-smb-external-id-2030)|2030|Hoch|Exfiltration,<br>Seitliche Verschiebung,<br>Befehl und Steuerung|
> |[Honeytoken-Aktivität](compromised-credentials-alerts.md#honeytoken-activity-external-id-2014)|2014|Mittel|Zugriff über Anmeldeinformationen,<br>Ermittlung|
> |[Malicious request of Data Protection API master key (Böswillige Anforderung eines Masterschlüssels zur Datenschutz-API)](domain-dominance-alerts.md#malicious-request-of-data-protection-api-master-key-external-id-2020)|2020|Hoch|Zugriff über Anmeldeinformationen|
> |[Network mapping reconnaissance (DNS) (Reconnaissance über Netzwerkzuordnung (DNS))](reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)|2007|Mittel|Ermittlung|
> |[Versuchte Remotecodeausführung](domain-dominance-alerts.md#remote-code-execution-attempt-external-id-2019)|2019|Mittel|Ausführung,<br>Persistenz,<br>Ausweitung von Berechtigungen,<br>Umgehung der Verteidigung,<br>Seitwärtsbewegung|
> |[Remotecodeausführung über DNS](lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036)|2036|Mittel|Ausweitung von Berechtigungen,<br>Seitwärtsbewegung|
> |[Sicherheitsprinzipalreconnaissance (LDAP)](reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038)|2038|Mittel|Zugriff über Anmeldeinformationen|
> |[Vermuteter Brute-Force-Angriff (Kerberos, NTLM)](compromised-credentials-alerts.md#suspected-brute-force-attack-kerberos-ntlm-external-id-2023)|2023|Mittel|Zugriff über Anmeldeinformationen|
> |[Vermuteter Brute-Force-Angriff (LDAP)](compromised-credentials-alerts.md#suspected-brute-force-attack-ldap-external-id-2004)|2004|Mittel|Zugriff über Anmeldeinformationen|
> |[Vermuteter Brute-Force-Angriff (SMB)](compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033)|2033|Mittel|Seitwärtsbewegung|
> |[Suspected DCShadow attack (domain controller promotion) (Verdacht auf DCShadow-Angriff (Heraufstufung von Domänencontrollern))](domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-promotion-external-id-2028)|2028|Hoch|Umgehung der Verteidigung|
> |[Verdacht auf DCShadow-Angriff (Replikationsanforderung an Domänencontroller)](domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-replication-request-external-id-2029)|2029|Hoch|Umgehung der Verteidigung|
> |[Suspected DCSync attack (replication of directory services) (Verdacht auf einen DCSync-Angriff (Replikation von Verzeichnisdiensten))](domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006)|2006|Hoch|Persistenz,<br>Zugriff über Anmeldeinformationen|
> |[Verdacht auf Verwendung eines Golden Ticket (Herabstufung der Verschlüsselung)](domain-dominance-alerts.md#suspected-golden-ticket-usage-encryption-downgrade-external-id-2009)|2009|Mittel|Ausweitung von Berechtigungen,<br>Seitliche Verschiebung,<br>Persistenz|
> |[Suspected Golden Ticket usage (forged authorization data) (Verdacht auf Verwendung eines Golden Ticket (gefälschte Autorisierungsdaten))](domain-dominance-alerts.md#suspected-golden-ticket-usage-forged-authorization-data-external-id-2013)|2013|Hoch|Ausweitung von Berechtigungen,<br>Seitliche Verschiebung,<br>Persistenz|
> |[Suspected Golden Ticket usage (nonexistent account) (Verdacht auf Verwendung eines Golden Ticket (nicht vorhandenes Konto))](domain-dominance-alerts.md#suspected-golden-ticket-usage-nonexistent-account-external-id-2027)|2027|Hoch|Ausweitung von Berechtigungen,<br>Seitliche Verschiebung,<br>Persistenz|
> |[Vermutete Golden Ticket-Verwendung (Ticketanomalie)](domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-external-id-2032)|2032|Hoch|Ausweitung von Berechtigungen,<br>Seitliche Verschiebung,<br>Persistenz|
> |[Vermutete Golden Ticket-Verwendung (Ticketanomalie mithilfe von RBCD)](domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-using-rbcd-external-id-2040)|2040|Hoch|Persistenz|
> |[Suspected golden ticket usage (time anomaly) (Verdacht auf Verwendung eines Golden Ticket (Zeitanomalie))](domain-dominance-alerts.md#suspected-golden-ticket-usage-time-anomaly-external-id-2022)|2022|Hoch|Ausweitung von Berechtigungen,<br>Seitliche Verschiebung,<br>Persistenz|
> |[Suspected identity theft (Pass-the-Hash) (Verdacht auf Identitätsdiebstahl (Pass-the-Hash))](lateral-movement-alerts.md#suspected-identity-theft-pass-the-hash-external-id-2017)|2017|Hoch|Seitliche Verschiebung|
> |[Suspected identity theft (Pass-the-Ticket) (Verdacht auf Identitätsdiebstahl (Pass-the-Ticket))](lateral-movement-alerts.md#suspected-identity-theft-pass-the-ticket-external-id-2018)|2018|Hoch oder Mittel|Seitwärtsbewegung|
> |[Mutmaßliche Kerberos-SPN-Offenlegung (externe ID: 2410)](compromised-credentials-alerts.md#suspected-kerberos-spn-exposure-external-id-2410)|2410|Hoch|Zugriff über Anmeldeinformationen|
> |[Verdächtigter Netlogon-Rechteerweiterungsversuch (CVE-2020-1472-Ausnutzung)](compromised-credentials-alerts.md#suspected-netlogon-priv-elev-2411)|2411|Hoch|Berechtigungsausweitung|
> |[Suspected NTLM authentication tampering (Vermutete Manipulation der NTLM-Authentifizierung)](lateral-movement-alerts.md#suspected-ntlm-authentication-tampering-external-id-2039)|2039|Mittel|Ausweitung von Berechtigungen, <br>Seitwärtsbewegung|
> |[Vermuteter NTLM-Relaisangriff](lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037)|2037|Mittel oder Niedrig, wenn mithilfe von signiertem NTLMv2-Protokoll beobachtet|Ausweitung von Berechtigungen, <br>Seitwärtsbewegung|
> |[Suspected overpass-the-hash attack (Kerberos) (Verdacht auf einen Overpass-the-Hash-Angriff (Kerberos))](lateral-movement-alerts.md#suspected-overpass-the-hash-attack-kerberos-external-id-2002)|2002|Mittel|Seitliche Verschiebung|
> |[Mutmaßliche Verwendung von Rogue-Kerberos-Zertifikat](lateral-movement-alerts.md#suspected-rogue-kerberos-certificate-usage-external-id-2047)|2047|Hoch|Seitliche Verschiebung|
> |[Vermuteter Skeleton Key-Angriff (Herabstufung der Verschlüsselung)](domain-dominance-alerts.md#suspected-skeleton-key-attack-encryption-downgrade-external-id-2010)|2010|Mittel|Seitliche Verschiebung,<br>Persistenz|
> |[Mutmaßliche Manipulation von SMB-Paketen (Exploit von CVE-2020-0796) (Vorschau)](lateral-movement-alerts.md#suspected-smb-packet-manipulation-cve-2020-0796-exploitation-external-id-2406)|2406|Hoch|Seitliche Verschiebung|
> |[Suspected use of Metasploit hacking framework (Verdacht auf Verwendung eines Hackerframeworks)](compromised-credentials-alerts.md#suspected-use-of-metasploit-hacking-framework-external-id-2034)|2034|Mittel|Seitwärtsbewegung|
> |[Suspected WannaCry ransomware attack (Verdacht auf einen WannaCry-Ransomangriff)](compromised-credentials-alerts.md#suspected-wannacry-ransomware-attack-external-id-2035)|2035|Mittel|Seitwärtsbewegung|
> |[Verdächtige Ergänzungen zu sensiblen Gruppen](domain-dominance-alerts.md#suspicious-additions-to-sensitive-groups-external-id-2024)|2024|Mittel|Zugriff über Anmeldeinformationen,<br>Persistenz|
> |[Verdächtige Kommunikation über DNS](exfiltration-alerts.md#suspicious-communication-over-dns-external-id-2031)|2031|Mittel|Exfiltration|
> |[Erstellung von verdächtigen Diensten](domain-dominance-alerts.md#suspicious-service-creation-external-id-2026)|2026|Mittel|Ausführung,<br>Persistenz,<br>Ausweitung von Berechtigungen,<br>Umgehung der Verteidigung,<br>Seitwärtsbewegung|
> |[Verdächtige VPN-Verbindung](compromised-credentials-alerts.md#suspicious-vpn-connection-external-id-2025)|2025|Mittel|Persistenz,<br>Umgehung der Verteidigung|
> |[Reconnaissance über Benutzer und Gruppenmitgliedschaften (SAMR)](reconnaissance-alerts.md#user-and-group-membership-reconnaissance-samr-external-id-2021)|2021|Mittel|Ermittlung|
> |[Reconnaissance über Benutzer und IP-Adressen (SMB)](reconnaissance-alerts.md#user-and-ip-address-reconnaissance-smb-external-id-2012)|2012|Mittel|Ermittlung|


# <a name="cloud-app-security-ids"></a>[Cloud App Security-API](#tab/cloud-app-security)

> [!div class="mx-tdBreakAll"]
> |Sicherheitswarnungsname|Cloud App Security-Warnungs-ID|
> |---|---|
> |[Reconnaissance mithilfe von Kontoenumeration](reconnaissance-alerts.md#account-enumeration-reconnaissance-external-id-2003)|ALERT_EXTERNAL_AATP_ACCOUNT_ENUMERATION_SECURITY_ALERT|
> |[Active Directory-Attributreconnaissance (LDAP)](reconnaissance-alerts.md#active-directory-attributes-reconnaissance-ldap-external-id-2210)|ALERT_EXTERNAL_AATP_LDAP_SENSITIVE_ATTRIBUTE_RECONNAISSANCE_SECURITY_ALERT|
> |[Datenexfiltration über den SMB](exfiltration-alerts.md#data-exfiltration-over-smb-external-id-2030)|ALERT_EXTERNAL_AATP_SMB_DATA_EXFILTRATION_SECURITY_ALERT|
> |[Honeytoken-Aktivität](compromised-credentials-alerts.md#honeytoken-activity-external-id-2014)|ALERT_EXTERNAL_AATP_HONEYTOKEN_ACTIVITY_SECURITY_ALERT|
> |[Malicious request of Data Protection API master key (Böswillige Anforderung eines Masterschlüssels zur Datenschutz-API)](domain-dominance-alerts.md#malicious-request-of-data-protection-api-master-key-external-id-2020)|ALERT_EXTERNAL_AATP_RETRIEVE_DATA_PROTECTION_BACKUP_KEY_SECURITY_ALERT|
> |[Network mapping reconnaissance (DNS) (Reconnaissance über Netzwerkzuordnung (DNS))](reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)|ALERT_EXTERNAL_AATP_DNS_RECONNAISSANCE_SECURITY_ALERT|
> |[Versuchte Remotecodeausführung](domain-dominance-alerts.md#remote-code-execution-attempt-external-id-2019)|ALERT_EXTERNAL_AATP_REMOTE_EXECUTION_SECURITY_ALERT|
> |[Remotecodeausführung über DNS](lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036)|ALERT_EXTERNAL_AATP_DNS_REMOTE_CODE_EXECUTION_SECURITY_ALERT|
> |[Sicherheitsprinzipalreconnaissance (LDAP)](reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038)|ALERT_EXTERNAL_AATP_LDAP_SEARCH_RECONNAISSANCE_SECURITY_ALERT|
> |[Vermuteter Brute-Force-Angriff (Kerberos, NTLM)](compromised-credentials-alerts.md#suspected-brute-force-attack-kerberos-ntlm-external-id-2023)|ALERT_EXTERNAL_AATP_REMOTE_EXECUTION_SECURITY_ALERT|
> |[Vermuteter Brute-Force-Angriff (LDAP)](compromised-credentials-alerts.md#suspected-brute-force-attack-ldap-external-id-2004)|ALERT_EXTERNAL_AATP_LDAP_BRUTE_FORCE_SECURITY_ALERT|
> |[Vermuteter Brute-Force-Angriff (SMB)](compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033)|ALERT_EXTERNAL_AATP_ABNORMAL_SMB_BRUTE_FORCE_SECURITY_ALERT|
> |[Suspected DCShadow attack (domain controller promotion) (Verdacht auf DCShadow-Angriff (Heraufstufung von Domänencontrollern))](domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-promotion-external-id-2028)|ALERT_EXTERNAL_AATP_DIRECTORY_SERVICES_ROGUE_PROMOTION_SECURITY_ALERT|
> |[Verdacht auf DCShadow-Angriff (Replikationsanforderung an Domänencontroller)](domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-replication-request-external-id-2029)|ALERT_EXTERNAL_AATP_DIRECTORY_SERVICES_ROGUE_PROMOTION_SECURITY_ALERT|
> |[Suspected DCSync attack (replication of directory services) (Verdacht auf einen DCSync-Angriff (Replikation von Verzeichnisdiensten))](domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006)|ALERT_EXTERNAL_AATP_DIRECTORY_SERVICES_REPLICATION_SECURITY_ALERT|
> |[Verdacht auf Verwendung eines Golden Ticket (Herabstufung der Verschlüsselung)](domain-dominance-alerts.md#suspected-golden-ticket-usage-encryption-downgrade-external-id-2009)|ALERT_EXTERNAL_AATP_GOLDEN_TICKET_ENCRYPTION_DOWNGRADE_SECURITY_ALERT|
> |[Suspected Golden Ticket usage (forged authorization data) (Verdacht auf Verwendung eines Golden Ticket (gefälschte Autorisierungsdaten))](domain-dominance-alerts.md#suspected-golden-ticket-usage-forged-authorization-data-external-id-2013)|ALERT_EXTERNAL_AATP_FORGED_PAC_SECURITY_ALERT|
> |[Suspected Golden Ticket usage (nonexistent account) (Verdacht auf Verwendung eines Golden Ticket (nicht vorhandenes Konto))](domain-dominance-alerts.md#suspected-golden-ticket-usage-nonexistent-account-external-id-2027)|ALERT_EXTERNAL_AATP_FORGED_PRINCIPAL_SECURITY_ALERT|
> |[Vermutete Golden Ticket-Verwendung (Ticketanomalie)](domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-external-id-2032)|ALERT_EXTERNAL_AATP_GOLDEN_TICKET_SIZE_ANOMALY_SECURITY_ALERT|
> |[Vermutete Golden Ticket-Verwendung (Ticketanomalie mithilfe von RBCD)](domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-using-rbcd-external-id-2040)|ALERT_EXTERNAL_AATP_RESOURCE_BASED_CONSTRAINED_DELEGATION_GOLDEN_TICKET_SECURITY_ALERT|
> |[Suspected golden ticket usage (time anomaly) (Verdacht auf Verwendung eines Golden Ticket (Zeitanomalie))](domain-dominance-alerts.md#suspected-golden-ticket-usage-time-anomaly-external-id-2022)|ALERT_EXTERNAL_AATP_GOLDEN_TICKET_SECURITY_ALERT|
> |[Suspected identity theft (Pass-the-Hash) (Verdacht auf Identitätsdiebstahl (Pass-the-Hash))](lateral-movement-alerts.md#suspected-identity-theft-pass-the-hash-external-id-2017)|ALERT_EXTERNAL_AATP_PASS_THE_HASH_SECURITY_ALERT|
> |[Suspected identity theft (Pass-the-Ticket) (Verdacht auf Identitätsdiebstahl (Pass-the-Ticket))](lateral-movement-alerts.md#suspected-identity-theft-pass-the-ticket-external-id-2018)|ALERT_EXTERNAL_AATP_PASS_THE_TICKET_SECURITY_ALERT|
> |[Mutmaßliche Kerberos-SPN-Offenlegung (externe ID: 2410)](compromised-credentials-alerts.md#suspected-kerberos-spn-exposure-external-id-2410)|ALERT_EXTERNAL_AATP_KERBEROASTING_SECURITY_ALERT|
> |[Verdächtigter Netlogon-Rechteerweiterungsversuch (CVE-2020-1472-Ausnutzung)](compromised-credentials-alerts.md#suspected-netlogon-priv-elev-2411)|ALERT_EXTERNAL_AATP_NETLOGON_BYPASS_SECURITY_ALERT|
> |[Suspected NTLM authentication tampering (Vermutete Manipulation der NTLM-Authentifizierung)](lateral-movement-alerts.md#suspected-ntlm-authentication-tampering-external-id-2039)|ALERT_EXTERNAL_AATP_ABNORMAL_NTLM_SIGNING_SECURITY_ALERT|
> |[Vermuteter NTLM-Relaisangriff](lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037)|ALERT_EXTERNAL_AATP_NTLM_RELAY_SECURITY_ALERT|
> |[Suspected overpass-the-hash attack (Kerberos) (Verdacht auf einen Overpass-the-Hash-Angriff (Kerberos))](lateral-movement-alerts.md#suspected-overpass-the-hash-attack-kerberos-external-id-2002)|ALERT_EXTERNAL_AATP_ABNORMAL_KERBEROS_OVERPASS_THE_HASH_SECURITY_ALERT|
> |[Mutmaßliche Verwendung von Rogue-Kerberos-Zertifikat](lateral-movement-alerts.md#suspected-rogue-kerberos-certificate-usage-external-id-2047)|ALERT_EXTERNAL_AATP_ROGUE_CERTIFICATE_USAGE_SECURITY_ALERT|
> |[Vermuteter Skeleton Key-Angriff (Herabstufung der Verschlüsselung)](domain-dominance-alerts.md#suspected-skeleton-key-attack-encryption-downgrade-external-id-2010)|ALERT_EXTERNAL_AATP_SKELETON_KEY_ENCRYPTION_DOWNGRADE_SECURITY_ALERT|
> |[Mutmaßliche Manipulation von SMB-Paketen (Exploit von CVE-2020-0796) (Vorschau)](lateral-movement-alerts.md#suspected-smb-packet-manipulation-cve-2020-0796-exploitation-external-id-2406)|ALERT_EXTERNAL_AATP_SMB_GHOST_SECURITY_ALERT|
> |[Suspected use of Metasploit hacking framework (Verdacht auf Verwendung eines Hackerframeworks)](compromised-credentials-alerts.md#suspected-use-of-metasploit-hacking-framework-external-id-2034)|ALERT_EXTERNAL_AATP_ABNORMAL_SMB_METASPLOIT_SECURITY_ALERT|
> |[Suspected WannaCry ransomware attack (Verdacht auf einen WannaCry-Ransomangriff)](compromised-credentials-alerts.md#suspected-wannacry-ransomware-attack-external-id-2035)|ALERT_EXTERNAL_AATP_ABNORMAL_SMB_WANNA_CRY_SECURITY_ALERT|
> |[Verdächtige Ergänzungen zu sensiblen Gruppen](domain-dominance-alerts.md#suspicious-additions-to-sensitive-groups-external-id-2024)|ALERT_EXTERNAL_AATP_ABNORMAL_SENSITIVE_GROUP_MEMBERSHIP_CHANGE_SECURITY_ALERT|
> |[Verdächtige Kommunikation über DNS](exfiltration-alerts.md#suspicious-communication-over-dns-external-id-2031)|ALERT_EXTERNAL_AATP_DNS_SUSPICIOUS_COMMUNICATION_SECURITY_ALERT|
> |[Erstellung von verdächtigen Diensten](domain-dominance-alerts.md#suspicious-service-creation-external-id-2026)|ALERT_EXTERNAL_AATP_MALICIOUS_SERVICE_CREATION_SECURITY_ALERT|
> |[Verdächtige VPN-Verbindung](compromised-credentials-alerts.md#suspicious-vpn-connection-external-id-2025)|ALERT_EXTERNAL_AATP_ABNORMAL_VPN_SECURITY_ALERT|
> |[Reconnaissance über Benutzer und Gruppenmitgliedschaften (SAMR)](reconnaissance-alerts.md#user-and-group-membership-reconnaissance-samr-external-id-2021)|ALERT_EXTERNAL_AATP_SAMR_RECONNAISSANCE_SECURITY_ALERT|
> |[Reconnaissance über Benutzer und IP-Adressen (SMB)](reconnaissance-alerts.md#user-and-ip-address-reconnaissance-smb-external-id-2012)|ALERT_EXTERNAL_AATP_ENUMERATE_SESSIONS_SECURITY_ALERT|

<!-- FROM TOP TABLE |[Suspected over-pass-the-hash attack (encryption downgrade)](lateral-movement-alerts.md#suspected-overpass-the-hash-attack-encryption-downgrade-external-id-2008)|2008|Medium|Lateral movement|-->
<!-- FROM BOTTOM TABLE |[Suspected over-pass-the-hash attack (encryption downgrade)](lateral-movement-alerts.md#suspected-overpass-the-hash-attack-encryption-downgrade-external-id-2008)|ALERT_EXTERNAL_AATP_OVERPASS_THE_HASH_ENCRYPTION_DOWNGRADE_SECURITY_ALERT|-->

> [!NOTE]
> Wenn Sie eine Sicherheitswarnung deaktivieren möchten, wenden Sie sich an den Support.

## <a name="see-also"></a>Weitere Informationen

- [Arbeiten mit Sicherheitswarnungen](working-with-suspicious-activities.md)
- [Verstehen von Sicherheitswarnungen](understanding-security-alerts.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
