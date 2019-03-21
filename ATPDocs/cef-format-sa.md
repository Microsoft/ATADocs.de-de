---
title: Referenz zum Azure ATP-SIEM-Protokoll | Microsoft-Dokumentation
description: Stellt Beispiele über verdächtige Aktivitätsprotokolle bereit, die von Azure ATP an SIEM gesendet werden.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 03/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 3261155c-3c72-4327-ba29-c113c63a4e6d
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: eeb158ed3da07b57a3071b5fa9f60b8ec9d20db7
ms.sourcegitcommit: 9252c74620abb99d8fa2b8d2cc2169018078bec9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/19/2019
ms.locfileid: "58136891"
---
# <a name="azure-atp-siem-log-reference"></a>Referenz zum Azure ATP-SIEM-Protokoll

Azure ATP kann Ereignisse zu Sicherheitswarnungen und Warnungen zur Überwachung an SIEM weiterleiten. Warnungen und Ereignisse weisen das CEF-Format auf. Dieser Referenzartikel enthält Beispiele für die Protokolle, die an SIEM gesendet werden.

## <a name="sample-azure-atp-security-alerts-in-cef-format"></a>Beispielsicherheitswarnungen von Azure ATP im CEF-Format
Die folgenden Felder und deren Werte werden an Ihren SIEM-Agent weitergeleitet:

|Detail|Erläuterung|
|---------|---------------|
|start|Startzeit der Warnung|
|suser|Konto (normalerweise das Benutzerkonto), das an der Warnung beteiligt ist|
|machine account|Konto (normalerweise das Benutzerkonto), das an der Warnung beteiligt ist|
|outcome|Sofern relevant, ein Erfolg oder Fehler bei der verdächtigen Aktivität in der Warnung|
|msg|Eine Beschreibung der Warnung|
|cnt|Für Warnungen, die die Anzahl der Zeiten angeben, zu denen die Aktivität erfolgt ist (z.B. Brute Force mit einer Anzahl geschätzter Kennwörter)|
|app |In dieser Warnung verwendetes Protokoll|
|externalId|Ereignistyp-ID, die Azure ATP in das Ereignisprotokoll schreibt, das jedem Warnungstyp entspricht|
|cs#label|Die für CEF zulässigen Kundenzeichenfolgen, wobei „cs#label“ der Name des neuen Felds ist |
|cs#|Die für CEF zulässigen Kundenzeichenfolgen, wobei „cs#“ der Wert ist.|
|
- Zum Beispiel: cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa
<br> Das Feld „cs1“ ist die Warnungs-URL. 

- Zum Beispiel: cs2Label=trigger cs2=new
<br> Das Feld „cs2“ ermittelt, ob die Warnung neu ist oder aktualisiert wurde.


> [!NOTE]
> Wenn Sie eine Automatisierung oder Skripts für Azure ATP-SIEM-Protokoll erstellen möchten, sollten Sie zur Identifizierung des Warnungstyps das Feld **externalID** statt des Warnungsnamens verwenden. Warnungsnamen können nämlich gelegentlich geändert werden, während die **externalId** jeder Warnung dauerhaft ist.  

## <a name="azure-atp-security-alert-unique-externalids"></a>Azure ATP-Sicherheitswarnung: Eindeutige externalIds

> [!div class="mx-tableFixed"] 

|Neuer Sicherheitswarnungsname|Alter Sicherheitswarnungsname|Eindeutige externe ID|MITRE ATT&CK Matrix™ |
|---------|----------|---------|---------|
|[Reconnaissance mithilfe von Kontoenumeration](atp-reconnaissance-alerts.md#account-enumeration-reconnaissance-external-id-2003)|Reconnaissance mithilfe von Kontoenumeration|2003|Ermittlung|
|[Data exfiltration over SMB (Datenexfiltration über den SMB)](atp-exfiltration-alerts.md#data-exfiltration-over-smb-external-id-2030)| N/V| 2030|Exfiltration,<br>Seitliche Verschiebung,<br>Befehl und Steuerelement|
|[Honeytoken-Aktivität](atp-compromised-credentials-alerts.md#honeytoken-activity-external-id-2014)|Honeytoken-Aktivität|2014||
|[Malicious request of Data Protection API master key (Böswillige Anforderung eines Masterschlüssels zur Datenschutz-API)](atp-domain-dominance-alerts.md#malicious-request-of-data-protection-api-master-key-external-id-2020)|Böswillige Anforderung privater Informationen im Rahmen der Datensicherheit|2020|Zugriff über Anmeldeinformationen|
|[Network mapping reconnaissance (DNS) (Reconnaissance über Netzwerkzuordnung (DNS))](atp-reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)|Reconnaissance über DNS|2007|Ermittlung|
|[Versuchte Remotecodeausführung](atp-domain-dominance-alerts.md#remote-code-execution-attempt-external-id-2019)|Versuchte Remote-Codeausführung|2019|Ausführung,<br> Persistenz,<br> Ausweitung von Berechtigungen,<br> Umgehung der Verteidigung,<br> Seitliche Verschiebung|
|[Remotecodeausführung über DNS](atp-lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036)|N/V|2036|Ausweitung von Berechtigungen,<br> Seitliche Verschiebung|
|[Sicherheitsprinzipalreconnaissance (LDAP) – Vorschauversion](atp-reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038---preview)|N/V|2038|Zugriff über Anmeldeinformationen|
|[Suspected Brute Force attack (Kerberos NTLM) (Verdacht auf einen Brute-Force-Angriff (Kerberos NTLM))](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-kerberos-ntlm-external-id-2023)|Verdächtige Authentifizierungsfehler|2023|Zugriff über Anmeldeinformationen|
|[Suspected Brute Force attack (LDAP) (Verdacht auf einen Brute-Force-Angriff (LDAP))](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-ldap-external-id-2004)|Brute-Force-Angriff mithilfe einer einfachen LDAP-Bindung|2004|Zugriff über Anmeldeinformationen|
|[Suspected Brute Force attack (SMB) (Verdacht auf einen Brute-Force-Angriff (SMB))](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033)|Ungewöhnliche Protokollimplementierung (potenzielle Verwendung schädlicher Tools wie Hydra)|2033|Seitliche Verschiebung|
|[Suspected DCShadow attack (domain controller promotion) (Verdacht auf DCShadow-Angriff (Heraufstufung von Domänencontrollern))](atp-domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-promotion-external-id-2028)|Verdächtige Heraufstufung zu Domänencontrollern (potenzieller DcShadow-Angriff)|2028|Umgehung der Verteidigung|
|[Verdacht auf DCShadow-Angriff (Replikationsanforderung an Domänencontroller)](atp-domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-replication-request-external-id-2029)|Verdächtige Replikationsanforderung von Domänencontroller (potenzieller DCShadow-Angriff)|2029|Umgehung der Verteidigung|
|[Suspected DCSync attack (replication of directory services) (Verdacht auf einen DCSync-Angriff (Replikation von Verzeichnisdiensten))](atp-domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006)|Böswillige Replikation von Verzeichnisdiensten|2006||
|[Verdacht auf Verwendung eines Golden Ticket (Herabstufung der Verschlüsselung)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-encryption-downgrade-external-id-2009)|Aktivität zur Herabstufung der Verschlüsselung (potenzieller Golden Ticket-Angriff)|2009|
|[Suspected Golden Ticket usage (forged authorization data) (Verdacht auf Verwendung eines Golden Ticket (gefälschte Autorisierungsdaten))](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-forged-authorization-data-external-id-2013) |Berechtigungsausweitung mithilfe von gefälschten Autorisierungsdaten|2013|Ausweitung von Berechtigungen,<br>Seitliche Verschiebung||
|[Suspected golden ticket usage (nonexistent account) (Verdacht auf Verwendung eines Golden Ticket (nicht vorhandenes Konto))](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-nonexistent-account-external-id-2027)|Kerberos Golden Ticket: nicht vorhandenes Konto|2027||
|[Vermutete Golden Ticket-Verwendung (Ticketanomalie)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-external-id-2032)|N/V|2032||
|[Suspected golden ticket usage (time anomaly) (Verdacht auf Verwendung eines Golden Ticket (Zeitanomalie))](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-time-anomaly-external-id-2022)|Kerberos Golden Ticket – Zeitanomalie|2022||
|[Suspected identity theft (Pass-the-Hash) (Verdacht auf Identitätsdiebstahl (Pass-the-Hash))](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-hash-external-id-2017)|Identitätsdiebstahl mithilfe eines Pass-the-Hash-Angriffs|2017|Seitliche Verschiebung|
|[Suspected identity theft (Pass-the-Ticket) (Verdacht auf Identitätsdiebstahl (Pass-the-Ticket))](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-ticket-external-id-2018)|Identitätsdiebstahl mithilfe eines Pass-the-Ticket-Angriffs|2018|Seitliche Verschiebung|
|[Suspected over-pass-the-hash attack (encryption downgrade) (Verdacht auf Over-Pass-the-Hash-Angriff (Herabstufung der Verschlüsselung))](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-encryption-downgrade-external-id-2008)|Aktivität zur Herabstufung der Verschlüsselung (potenzieller Overpass-the-Hash-Angriff)|2008||
|[Suspected overpass-the-hash attack (Kerberos) (Verdacht auf einen Overpass-the-Hash-Angriff (Kerberos))](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-kerberos-external-id-2002)|Ungewöhnliche Kerberos-Protokollimplementierung (potenzieller Overpass-the-Hash-Angriff)|2002|Seitliche Verschiebung|
|[Suspected Skeleton Key attack (encryption downgrade) (Verdacht auf Skeleton-Key-Angriff (Herabstufung der Verschlüsselung))](atp-domain-dominance-alerts.md#suspected-skeleton-key-attack-encryption-downgrade-external-id-2010)|Aktivität zur Herabstufung der Verschlüsselung (potenzieller Skeleton Key-Angriff)|2010||
|[Suspected use of Metasploit hacking framework (Verdacht auf Verwendung eines Hackerframeworks)](atp-compromised-credentials-alerts.md#suspected-use-of-metasploit-hacking-framework-external-id-2034)|Ungewöhnliche Protokollimplementierung (potenzielle Verwendung schädlicher Hackertools wie Metasploit)|2034|Seitliche Verschiebung|
|[Suspected WannaCry ransomware attack (Verdacht auf einen WannaCry-Ransomangriff)](atp-compromised-credentials-alerts.md#suspected-wannacry-ransomware-attack-external-id-2035)|Ungewöhnliche Protokollimplementierung (potenzieller WannaCry-Ransomwareangriff)|2035||
|[Suspected NTLM relay attack (Exchange account) - preview (Vermuteter NTLM-Relaisangriff (Exchange-Konto) – Vorschauversion)](atp-lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037---preview)|N/V|2037||
|[Verdächtige Kommunikation über DNS](atp-exfiltration-alerts.md#suspicious-communication-over-dns-external-id-2031)|Verdächtige Kommunikation über DNS|2031|Exfiltration|
|[Verdächtige Modifizierung von sensiblen Gruppen](atp-domain-dominance-alerts.md#suspicious-modification-of-sensitive-groups-external-id-2024)|Verdächtige Modifizierung von sensiblen Gruppen|2024|Zugriff über Anmeldeinformationen,<br>Persistenz|
|[Erstellen eines verdächtigen Diensts](atp-domain-dominance-alerts.md#suspicious-service-creation-external-id-2026)|Erstellen eines verdächtigen Diensts|2026|Ausführung,<br> Persistenz,<br> Ausweitung von Berechtigungen,<br> Umgehung der Verteidigung,<br>Seitliche Verschiebung|
|[Verdächtige VPN-Verbindung](atp-compromised-credentials-alerts.md#suspicious-vpn-connection-external-id-2025)|Verdächtige VPN-Verbindung|2025|Persistenz,<br>Umgehung der Verteidigung|
|[User and group membership reconnaissance (SAMR) (Reconnaissance über Benutzer und Gruppenmitgliedschaften (SAMR))](atp-reconnaissance-alerts.md#user-and-group-membership-reconnaissance-samr-external-id-2021)|Reconnaissance mithilfe von Verzeichnisdienstabfragen|2021|Ermittlung|
|[User and IP address reconnaissance (SMB) (Reconnaissance über Benutzer und IP-Adressen (SMB))](atp-reconnaissance-alerts.md#user-and-ip-address-reconnaissance-smb-external-id-2012)|Reconnaissance mithilfe der SMB-Sitzungsenumeration|2012|Ermittlung|

## <a name="sample-logs"></a>Beispielprotokolle

Die Beispielprotokolle gelten zwar für RFC 5242, doch Azure ATP unterstützt auch RFC 3164.

Prioritäten:

- 3=Niedrig
- 5=Mittel
- 10=Hoch

### <a name="account-enumeration-reconnaissance"></a>Reconnaissance mithilfe von Kontoenumeration 
02-21-2018  16:19:35    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:27.540731+00:00 CENTER CEF 6076 AccountEnumerationSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AccountEnumerationSecurityAlert|Reconnaissance using account enumeration|5|start=2018-02-21T14:19:02.6045416Z app=Kerberos shost=CLIENT1 suser=LMaldonado msg=Suspicious account enumeration activity using the Kerberos protocol, originating from CLIENT1, was observed and successfully guessed Lamon Maldonado (Software Engineer). externalId=2003 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/eb6a35da-ff7f-4ab5-a1b5-a07529a89e6d cs2Label=trigger cs2=new

### <a name="data-exfiltration-over-smb"></a>Datenexfiltration über den SMB
12-19-2018  14:17:46    Auth.Error     127.0.0.1      1 2018-12-19T12:17:34.645993+00:00 DC1 CEF 3288 SmbDataExfiltrationSecurityAlert ï»¿0|Microsoft|Azure ATP|2.60.0.0|SmbDataExfiltrationSecurityAlert|[PREVIEW] Data exfiltration over SMB|10|start=2018-12-19T12:14:12.4932821Z app=Smb shost=CLIENT1 msg=Eugene Jenkins (Software Engineer) on DC2 copied suspicious files to CLIENT1. externalId=2030 cs1Label=url cs1=https\://contoso-corp.atp.azure.com:13000/securityAlert/3ca2ec9d-2c67-44cc-a2d6-391716611bb6 cs2Label=trigger cs2=new

### <a name="honeytoken-activity"></a>Honeytoken-Aktivität
02-21-2018  16:20:36    Auth.Warning  192.168.0.220 1 2018-02-21T14:20:34.106162+00:00 CENTER CEF 6076 HoneytokenActivitySecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|HoneytokenActivitySecurityAlert|Honeytoken activity|5|start=2018-02-21T14:20:26.6705617Z app=Kerberos suser=honey msg=Die folgenden Aktivitäten wurden vom Honeytoken ausgeführt:\r\nAnmeldung bei CLIENT2 über DC1 durchgeführt. externalId=2014 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/9249fe9a-c883-46dd-a4da-2a1fca5f211c cs2Label=trigger cs2=new

### <a name="malicious-request-of-data-protection-api-master-key"></a>Malicious request of Data Protection API master key (Böswillige Anforderung eines Masterschlüssels zur Datenschutz-API) 
10-29-2018  11:22:04    Auth.Error  192.168.0.202   1 2018-10-29T09:22:00.350864+00:00 DC3 CEF 3908 RetrieveDataProtectionBackupKeyS ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|RetrieveDataProtectionBackupKeySecurityAlert|Malicious Data Protection Private Information Request|10|start=2018-10-29T09:19:45.6307993Z app=LsaRpc shost=CLIENT1 msg=user1 performed 1 successful attempts from CLIENT1 to retrieve DPAPI domain backup key from DC1. externalId=2020 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/2f5717cb-2434-4d54-8af4-b2c6d14bc15c cs2Label=trigger cs2=new

### <a name="network-mapping-reconnaissance-dns"></a>Network-mapping reconnaissance (DNS) (Reconnaissance über Netzwerkzuordnung (DNS))
10-29-2018  11:20:02    Auth.Warning    192.168.0.202   1 2018-10-29T09:19:59.056894+00:00 DC3 CEF 3908 DnsReconnaissanceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|DnsReconnaissanceSecurityAlert|Reconnaissance using DNS|5|start=2018-10-29T09:19:43.5033765Z app=Dns shost=CLIENT1 msg=Suspicious DNS activity was observed, originating from CLIENT1 (which is not a DNS server) against DC1. externalId=2007 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/23937d33-ff71-484d-be0a-3c417fe573ce cs2Label=trigger cs2=new

### <a name="reconnaissance-using-directory-services-queries"></a>Reconnaissance mithilfe von Verzeichnisdienstabfragen 
02-21-2018  16:22:08    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:54.267658+00:00 CENTER CEF 6076 SamrReconnaissanceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|SamrReconnaissanceSecurityAlert| Reconnaissance using directory services enumeration |5|start=2018-02-21T14:19:41.9912772Z app= Samr shost=CLIENT1 suser=user1 outcome=Success msg= The following directory services enumerations using SAMR protocol were attempted against DC1 from CLIENT1:\r\nSuccessful enumeration of all groups in domain1.test.local by user1. externalId=2019 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/f295029a-ffae-408b-9dd0-55424c81eac0 cs2Label=trigger cs2=new

### <a name="remote-code-execution-attempt"></a>Versuchte Remote-Codeausführung
10-29-2018  11:22:04    Auth.Warning    192.168.0.202   1 2018-10-29T09:22:00.100856+00:00 DC3 CEF 3908 RemoteExecutionSecurityAlert ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|RemoteExecutionSecurityAlert|Remote code execution attempt|5|start=2018-10-29T09:19:45.0552367Z shost=CLIENT1 msg=The following remote code execution attempts were performed on DC1 from CLIENT1:\r\nSuccessful remote scheduling of one or more tasks by user1.\r\nFailed remote scheduling of one or more tasks by user1.\r\nSuccessful remote execution of one or more WMI methods by user1. externalId=2019 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/f063c778-830c-4e9f-98d1-bc6c11c94e11 cs2Label=trigger cs2=new

### <a name="remote-code-execution-over-dns"></a>Remotecodeausführung über DNS
1-17-2019   08:24:54    Auth.Warning    192.168.0.202   1 2019-01-17T08:24:54.100856+00:00 DC3 CEF 3908 DnsRemoteCodeExecutionSecurityAlert ï»¿0|Microsoft|Azure ATP|2.63.0.0|DnsRemoteCodeExecutionSecurityAlert|[PREVIEW] Remote code execution over DNS|5|start=2019-01-17T08:24:54.5293800Z app=Dns shost=CLIENT1 msg=An actor attempted to run commands remotely on CLIENT1 from DC1, over DNS protocol. externalId=2036 cs1Label=url cs1=https\:////contoso-corp.atp.azure.com:13000/securityAlert/591f9769-d904-40b1-89fa-c307c2ca814f cs2Label=trigger cs2=new

### <a name="security-principal-reconnaissance-ldap---preview"></a>Sicherheitsprinzipalreconnaissance (LDAP) – Vorschauversion 
02-18-2019  16:48:08 Auth.Warning  127.0.0.1  1 2019-02-18T14:48:02.912264+00:00 DC1 CEF 4656 LdapSearchReconnaissanceSecurity ï»¿0|Microsoft|Azure ATP|2.66.0.0|LdapSearchReconnaissanceSecurityAlert|[PREVIEW] Reconnaissance using LDAP Queries|5|start=2019-02-18T14:46:29.4644276Z app=LdapSearch shost=CLIENT1 msg=An actor on CLIENT1 sent suspicious LDAP queries to DC1, searching for 4 types of enumeration and Server Operators (Members can administer domain servers) in 2 domains externalId=2038 cs1Label=url cs1=https\://contoso-corp.atp.azure..com:13000/securityAlert/81ea99c4-ce1f-4581-ac8f-7440fbed7cd0 cs2Label=trigger cs2=new

### <a name="suspected-brute-force-attack-ldap"></a>Suspected Brute Force attack (LDAP) (Verdacht auf einen Brute-Force-Angriff (LDAP))
02-21-2018  16:20:21    Auth.Warning    192.168.0.220   1 2018-02-21T14:20:06.156238+00:00 CENTER CEF 6076 LdapBruteForceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|LdapBruteForceSecurityAlert|Brute force attack using LDAP simple bind|5|start=2018-02-21T14:19:41.7422810Z app=Ldap suser=Wofford Thurston shost=CLIENT1 msg=A brute force attack using the Ldap protocol was attempted on Wofford Thurston (Software Engineer) from CLIENT1 (100 guess attempts). cnt=100 externalId=2004 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/57b8ac96-7907-4971-9b27-ec77ad8c029a cs2Label=trigger cs2=update

### <a name="suspected-brute-force-attack-kerberos-ntlm"></a>Suspected Brute Force attack (Kerberos NTLM) (Verdacht auf einen Brute-Force-Angriff (Kerberos NTLM))
10-29-2018  11:20:47    Auth.Warning    192.168.0.202   1 2018-10-29T09:20:44.478827+00:00 DC3 CEF 3908 BruteForceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|BruteForceSecurityAlert|Suspicious authentication failures|5|start=2018-10-29T09:19:44.9512286Z app=Kerberos shost=CLIENT1 msg=Verdächtige Authentifizierungsfehler, die auf einen möglichen Brute-Force-Angriff hindeuten, wurden von CLIENT1 beobachtet. externalId=2023 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/85042c8e-27fa-49b3-8667-dabc1aa31580 cs2Label=trigger cs2=new

### <a name="suspected-golden-ticket-usage-encryption-downgrade"></a>Verdacht auf Verwendung eines Golden Ticket (Herabstufung der Verschlüsselung)
10-29-2018  11:25:07    Auth.Warning    192.168.0.202   1 2018-10-29T09:25:01.007701+00:00 DC3 CEF 3908 GoldenTicketEncryptionDowngradeS ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|GoldenTicketEncryptionDowngradeSecurityAlert|Encryption downgrade activity (potential golden ticket attack)|5|start=2018-10-29T09:37:49.0849130Z app=Kerberos msg=W10-000007-Lap used a weaker encryption method (RC4),Â in the Kerberos service request (TGS_REQ),Â from W10-000007-Lap, to access host/domain1.test.local. externalId=2009 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/f01f8403-88b2-437e-b4ad-d72485fe05ac cs2Label=trigger cs2=new

### <a name="suspected-golden-ticket-usage-non-existent-account"></a>Suspected Golden Ticket usage (nonexistent account) (Verdacht auf Verwendung eines Golden Ticket (nicht vorhandenes Konto))
07-01-2018  14:28:49    Auth.Error  192.168.0.100   1 2018-07-01T11:28:35.546638+00:00 CENTER CEF 38768 ForgedPrincipalSecurityAlert ï»¿0|Microsoft|Azure ATP|2.39.0.0|ForgedPrincipalSecurityAlert|Kerberos Golden Ticket – nicht vorhandenes Konto|10|start=2018-07-01T09:48:31.2567987Z app=Kerberos suser=domain1.test.local\fake msg=domain1.test.local\fake, das nicht in Active Directory vorhanden ist, hat ein Kerberos-Ticket verwendet. Das Ticket wurde von zwei Computern für den Zugriff auf drei Ressourcen erkannt. Dies kann auf einen potenziellen Golden Ticket-Angriff hinweisen. externalId=2027 cs1Label=url cs1=https\://contoso-corp.atp.azure.com:13000/securityAlert/98f050d4-9134-429c-8e54-d8eeb19849c4 cs2Label=trigger cs2=update

### <a name="suspected-golden-ticket-usage-ticket-anomaly"></a>Verdacht auf Verwendung eines Golden Ticket (Ticketanomalie) 
1 2018-11-18T10:46:23.346946+00:00 MAXIMG-7050 CEF 24284 GoldenTicketSizeAnomalySecurityA 0|Microsoft|Azure ATP|2.56.0.0|GoldenTicketSizeAnomalySecurityAlert|[PREVIEW] Suspected Golden Ticket usage (ticket anomaly)|10|start=2018-11-18T10:44:12.9317797Z app=Kerberos shost=CLIENT2 suser=RFosdyke msg=Renzo Fosdyke (Software Engineer) used a suspicious Kerberos ticket from CLIENT2 to access ldap/domain1.test.local. externalId=2032 cs1Label=url cs1=https\://contoso-corp.atp.azure.com:13000/securityAlert/63600e03-f423-49bf-a92d-4010e1d52b9f cs2Label=trigger cs2=update

### <a name="suspected-golden-ticket-usage-time-anomaly"></a>Suspected golden ticket usage (time anomaly) (Verdacht auf Verwendung eines Golden Ticket (Zeitanomalie)) 
02-21-2018  16:22:39    Auth.Error  192.168.0.220   1 2018-02-21T14:22:34.274054+00:00 CENTER CEF 6076 GoldenTicketSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|GoldenTicketSecurityAlert|Kerberos Golden Ticket activity|10|start=2018-02-21T14:19:03.2416152Z app=Kerberos suser=Lanell Campos msg=Suspicious usage of Lanell Campos (Software Engineer)'s Kerberos ticket, indicating a potential Golden Ticket attack, was detected. externalId=2022 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/702c836e-6f49-4479-9892-80e8bccbfac0 cs2Label=trigger cs2=update

### <a name="suspected-golden-ticket-usage-forged-authorization-data"></a>Suspected Golden Ticket usage (forged authorization data) (Verdacht auf Verwendung eines Golden Ticket (gefälschte Autorisierungsdaten)) 
10-29-2018  11:22:04    Auth.Error  192.168.0.202   1 2018-10-29T09:21:59.288337+00:00 DC3 CEF 3908 ForgedPacSecurityAlert ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|ForgedPacSecurityAlert|Privilege escalation using forged authorization data|10|start=2018-10-29T09:19:43.6403358Z app=Kerberos suser=user1 msg=user1 failed to escalate privileges against DC1 to host/domain1.test.local from CLIENT1 by using forged authorization data. externalId=2013 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/b698d438-5013-4bca-be0b-f219f8b69108 cs2Label=trigger cs2=new

### <a name="suspected-identity-theft-pass-the-hash"></a>Suspected identity theft (Pass-the-Hash) (Verdacht auf Identitätsdiebstahl (Pass-the-Hash))
02-21-2018  17:04:47    Auth.Error  192.168.0.220   1 2018-02-21T15:04:33.537583+00:00 CENTER CEF 6076 PassTheHashSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|PassTheHashSecurityAlert|Identity theft using Pass-the-Hash attack|10|start=2018-02-21T15:02:22.2577465Z app=Kerberos suser=Eugene Jenkins msg=Eugene Jenkins (Software Engineer)'s hash was stolen from one of the computers previously logged into by Eugene Jenkins (Software Engineer) and used from CLIENT1. externalId=2017 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd cs2Label=trigger cs2=update

### <a name="suspected-identity-theft-pass-the-ticket"></a>Suspected identity theft (Pass-the-Ticket) (Verdacht auf Identitätsdiebstahl (Pass-the-Ticket)) 
02-21-2018  17:04:47    Auth.Error  192.168.0.220   1 2018-02-21T15:04:33.537583+00:00 CENTER CEF 6076 PassTheTicketSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|PassTheTicketSecurityAlert|Identitätsdiebstahl mit Pass-the-Ticket-Angriff|10|start=2018-02-21T15:02:22.2577465Z app=Kerberos suser=Eugene Jenkins msg=Kerberos-Tickets von Eugene Jenkins (Softwareentwickler) wurden vom Administrator-PC zum Einsatz auf dem PC des Opfers gestohlen und für den Zugriff auf krbtgt/DOMAIN1.TEST.LOCAL verwendet. externalId=2018 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd cs2Label=trigger cs2=new

### <a name="suspected-over-pass-the-hash-attack-encryption-downgrade"></a>Suspected over-pass-the-hash attack (encryption downgrade) (Verdacht auf Over-Pass-the-Hash-Angriff (Herabstufung der Verschlüsselung)) 
02-21-2018  16:21:07    Auth.Warning    192.168.0.220   1 2018-02-21T14:20:54.145833+00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|EncryptionDowngradeSecurityAlert|Encryption downgrade activity|5|start=2018-02-21T14:19:41.8737870Z app=Kerberos msg= The encryption method of the Encrypted_Timestamp field of AS_REQ message from CLIENT1 has been downgraded based on previously learned behavior. Grund dafür ist möglicherweise ein Diebstahl von Anmeldeinformationen bei einem Overpass-The-Hash-Angriff auf CLIENT1. externalId=2008 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2 cs2Label=trigger cs2=update

### <a name="suspected-skeleton-key-attack-encryption-downgrade"></a>Suspected Skeleton Key attack (encryption downgrade) (Verdacht auf Skeleton-Key-Angriff (Herabstufung der Verschlüsselung)) 
02-21-2018  16:21:07    Auth.Warning    192.168.0.220   1 2018-02-21T14:20:54.145833+00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|EncryptionDowngradeSecurityAlert|Encryption downgrade activity|5|start=2018-02-21T14:19:41.8737870Z app=Kerberos msg=The encryption method of the ETYPE_INFO2 field of KRB_ERR message from CLIENT1 has been downgraded based on previously learned behavior. Grund dafür ist möglicherweise ein Skeleton Key auf DC1. externalId=2010 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2 cs2Label=trigger cs2=new

### <a name="suspected-dcsync-attack-replication-of-directory-services"></a>Suspected DCSync attack (replication of directory services) (Verdacht auf einen DCSync-Angriff (Replikation von Verzeichnisdiensten))
02-21-2018  16:20:06    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:54.254930+00:00 CENTER CEF 6076 MaliciousServiceCreationSecurity ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|MaliciousServiceCreationSecurityAlert|Suspicious service creation|5|start=2018-02-21T14:19:41.7897808Z app=ServiceInstalledEvent shost=CLIENT1 msg=user1 created MaliciousService in order to execute potentially malicious commands on CLIENT1. externalId=2026 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/179229b6-b791-4895-b5aa-fdf3747a325c cs2Label=trigger cs2=update

### <a name="suspicious-authentication-failures"></a>Verdächtige Authentifizierungsfehler
02-21-2018  16:19:20    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:15.397995+00:00 CENTER CEF 6076 BruteForceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|BruteForceSecurityAlert|Suspicious authentication failures|5|start=2018-02-21T14:19:03.3831122Z app=Kerberos shost=CLIENT1 msg=Suspicious authentication failures indicating a potential brute-force attack were detected from CLIENT1. externalId=2023 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/fea88fc7-4110-454d-816d-349032474fd6 cs2Label=trigger cs2=new

### <a name="suspicious-communication-over-dns"></a>Verdächtige Kommunikation über DNS
10-04-2018  14:49:38    Auth.Warning    192.168.0.202   1 2018-10-04T11:49:25.954059+00:00 DC3 CEF 3604 DnsSuspiciousCommunicationSecuri ï»¿0|Microsoft|Azure ATP|2.49.5589.58606|DnsSuspiciousCommunicationSecurityAlert|Suspicious Communication over DNS|5|start=2018-10-04T11:49:11.0822077Z app=DnsEvent dhost= suspiciousdomainname msg=CLIENT1 sent suspicious DNS queries resolving suspiciousdomainname externalId=2031 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/0fc77777-49ca-40b3-a7ba-7644f355539e cs2Label=trigger cs2=new

### <a name="suspicious-domain-controller-promotion-potential-dcshadow-attack"></a>Verdächtige Heraufstufung zu Domänencontrollern (potenzieller DcShadow-Angriff)
07-12-2018  11:18:07    Auth.Error  192.168.0.200    1 2018-07-12T08:18:06.883880+00:00 DC1 CEF 3868 DirectoryServicesRoguePromotionS ï»¿0|Microsoft|Azure ATP|2.40.0.0|DirectoryServicesRoguePromotionSecurityAlert| **Suspicious domain controller promotion (potential DcShadow attack)**|10|start=2018-07-12T08:17:55.4067092Z app=Ldap shost=CLIENT1 msg=CLIENT1, which is a computer in domain1.test.local, registered as a domain controller on DC1. externalId=2028 cs1Label=url cs1=https\://contoso-corp.atp.azure.com:13000/securityAlert/97c59b43-dc18-44ee-9826-8fd5d03bd53 cs2Label=trigger cs2=update

### <a name="suspicious-modification-of-sensitive-groups"></a>Verdächtige Modifizierung von sensiblen Gruppen
10-29-2018  11:21:03    Auth.Warning    192.168.0.202   1 2018-10-29T09:20:49.667014+00:00 DC3 CEF 3908 AbnormalSensitiveGroupMembership ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|AbnormalSensitiveGroupMembershipChangeSecurityAlert|Suspicious modification of sensitive groups|5|start=2018-10-29T09:19:43.3013729Z app=GroupMembershipChangeEvent suser=user1 msg=user1 has uncharacteristically modified sensitive group memberships. externalId=2024 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/6f7e677e-f068-41e5-bada-708cd5a322b9 cs2Label=trigger cs2=new

### <a name="suspicious-replication-of-directory-services"></a>Verdächtige Replikation von Verzeichnisdiensten
02-21-2018  16:21:22    Auth.Error  192.168.0.220   1 2018-02-21T14:21:13.978554+00:00 CENTER CEF 6076 DirectoryServicesReplicationSecu ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|DirectoryServicesReplicationSecurityAlert|Malicious replication of directory services|10|start=2018-02-21T14:19:03.9975656Z app=Drsr shost=CLIENT1 msg=Malicious replication requests were successfully performed by user1, from CLIENT1 against DC1. outcome=Success externalId=2006 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/cb95648e-1b6f-4d3b-81b9-7605532787d7 cs2Label=trigger cs2=new

### <a name="suspicious-replication-request-potential-dcshadow-attack"></a>Verdächtige Replikationsanforderung (potenzieller DcShadow-Angriff)
07-12-2018  11:18:37    Auth.Error  192.168.0.200    1 2018-07-12T08:18:32.265989+00:00 DC1 CEF 3868 DirectoryServicesRogueReplicatio ï»¿0|Microsoft|Azure ATP|2.40.0.0|DirectoryServicesRogueReplicationSecurityAlert| **Suspicious replication request (potential DcShadow attack)**|10|start=2018-07-12T08:17:55.3816102Z **app=Replication Activity** shost=CLIENT1 msg=CLIENT1, which is not a valid domain controller in domain1.test.local, sent changes to directory objects on DC1. externalId=2029 cs1Label=url cs1=https\://contoso-corp.atp.azure.com:13000/securityAlert/1d5d1444-12cf-4db9-be48-39ebc2f51515 cs2Label=trigger cs2=new

### <a name="suspicious-service-creation"></a>Erstellen eines verdächtigen Diensts 
10-29-2018  11:20:02    Auth.Warning    192.168.0.202   1 2018-10-29T09:19:59.164874+00:00 DC3 CEF 3908 MaliciousServiceCreationSecurity ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|MaliciousServiceCreationSecurityAlert|Suspicious service creation|5|start=2018-10-29T09:19:44.9471965Z app=ServiceInstalledEvent shost=CLIENT1 msg=user1 created MaliciousService in order to execute potentially malicious commands on CLIENT1. externalId=2026 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/118bbe3d-fe72-40de-80d0-2678b68aa027 cs2Label=trigger cs2=new

### <a name="suspicious-vpn-connection"></a>Verdächtige VPN-Verbindung
07-03-2018  13:13:12    Auth.Warning  192.168.0.200   1 2018-07-03T10:13:06.187834+00:00 DC1 CEF 2520 AbnormalVpnSecurityAlert ï»¿0|Microsoft|Azure ATP|2.39.0.0|AbnormalVpnSecurityAlert|Suspicious VPN Connection|5|start=2018-06-30T15:34:05.3887333Z app=VpnConnection suser=user1 msg=user1 connected to a VPN using 3 computers from 3 Locations.     externalId=2025 cs1Label=url cs1=https\://contoso-corp.eng.atp.azure.com:13000/securityAlert/88c46b0e-372f-4c06-9935-67bd512c4f68 cs2Label=trigger cs2=new

### <a name="suspected-wannacry-ransomware-attack"></a>Suspected WannaCry ransomware attack (Verdacht auf einen WannaCry-Ransomangriff)
02-21-2018  16:21:22    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:13.916050+00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AbnormalProtocolSecurityAlert|SuspectedWannaCryRansomwareAttack|5|start=2018-02-21T14:19:03.1981155Z app=Ntlm shost=CLIENT2 outcome=Success msg=There were attempts to authenticate from CLIENT2 against DC1 using an unusual protocol implementation. Kann auf den Einsatz von schädlichen Tools zum Ausführen von Angriffen wie z.B. WannaCry hinweisen. externalId=2035 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label=trigger cs2=new

### <a name="suspected-brute-force-attack-smb"></a>Suspected Brute Force attack (SMB) (Verdacht auf einen Brute-Force-Angriff (SMB))
002-21-2018 16:21:22    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:13.916050+00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AbnormalProtocolSecurityAlert|SuspectedBrutForceAttack|5|start=2018-02-21T14:19:03.1981155Z app=Ntlm shost=CLIENT2 outcome=Success msg=There were attempts to authenticate from CLIENT2 against DC1 using an unusual protocol implementation. Kann auf den Einsatz von schädlichen Tools zum Ausführen von Angriffen wie z.B. Hydra hinweisen. externalId=2033 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label=trigger cs2=new

### <a name="suspected-use-of-metasploit-hacking-framework"></a>Suspected use of Metasploit hacking framework (Verdacht auf Verwendung eines Hackerframeworks)
002-21-2018 16:21:22    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:13.916050+00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AbnormalProtocolSecurityAlert|SuspectedAttackUsingMetasploit|5|start=2018-02-21T14:19:03.1981155Z app=Ntlm shost=CLIENT2 outcome=Success msg=There were attempts to authenticate from CLIENT2 against DC1 using an unusual protocol implementation. Kann auf den Einsatz von schädlichen Tools zum Ausführen von Angriffen wie z.B. Metasploit hinweisen. externalId=2034 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label=trigger cs2=new

### <a name="suspected-overpass-the-hash-attack-kerberos"></a>Suspected overpass-the-hash attack (Kerberos) (Verdacht auf einen Overpass-the-Hash-Angriff (Kerberos))
002-21-2018 16:21:22    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:13.916050+00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AbnormalProtocolSecurityAlert|SuspectedOverPassTheHashAttack|5|start=2018-02-21T14:19:03.1981155Z app=Ntlm shost=CLIENT2 outcome=Success msg=There were attempts to authenticate from CLIENT2 against DC1 using an unusual protocol implementation. Kann auf schädliche Aktivitäten unter Verwendung des Kerberos-Protokolls hinweisen. externalId=2002 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label=trigger cs2=new

### <a name="user-and-ip-address-reconnaissance-smb"></a>User and IP address reconnaissance (SMB) (Reconnaissance über Benutzer und IP-Adressen (SMB)) 
002-21-2018 16:21:22    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:13.916050+00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AbnormalProtocolSecurityAlert|ReconnaissanceusingSMBSessionEnumeration|5|start=2018-02-21T14:19:03.1981155Z app=Ntlm shost=CLIENT2 outcome=Success msg=There were attempts to authenticate from CLIENT2 against DC1 using an unusual protocol implementation. Kann auf den Einsatz von schädlichen Tools zum Ausführen von Angriffen wie z.B. Metasploit hinweisen. externalId=2034 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label=trigger cs2=new

## <a name="see-also"></a>Weitere Informationen
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Azure ATP capacity planning (Azure ATP-Kapazitätsplanung)](atp-capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-forwarding.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
