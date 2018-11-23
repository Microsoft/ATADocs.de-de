---
title: Referenz zum Azure ATP-SIEM-Protokoll | Microsoft-Dokumentation
description: Stellt Beispiele über verdächtige Aktivitätsprotokolle bereit, die von Azure ATP an SIEM gesendet werden.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 11/12/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 3261155c-3c72-4327-ba29-c113c63a4e6d
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 4d1a4d24e2102a019b9df627f2d00c1df981c3ae
ms.sourcegitcommit: 4d8e7c690453d9b78e6e597c3f8562250d335ba5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2018
ms.locfileid: "52177384"
---
*Gilt für: Azure Advanced Threat Protection*


# <a name="azure-atp-siem-log-reference"></a>Referenz zum Azure ATP-SIEM-Protokoll

Azure ATP kann Ereignisse zu Sicherheitswarnungen und Warnungen zur Überwachung an SIEM weiterleiten. Warnungen und Ereignisse weisen das CEF-Format auf. Dieser Referenzartikel enthält Beispiele für die Protokolle, die an SIEM gesendet werden.

## <a name="sample-azure-atp-security-alerts-in-cef-format"></a>Beispielsicherheitswarnungen von Azure ATP im CEF-Format
Die folgenden Felder und deren Werte werden an Ihren SIEM-Agent weitergeleitet:

|Detail|Erläuterung|
|---------|---------------|
|start|Startzeit der Warnung|
|suser|Konto (normalerweise das Benutzerkonto), das an der Warnung beteiligt ist|
|shost|Konto (normalerweise das Benutzerkonto), das an der Warnung beteiligt ist|
|outcome|Sofern relevant, ein Erfolg oder Fehler bei der verdächtigen Aktivität in der Warnung|
|msg|Eine Beschreibung der Warnung|
|cnt|Für Warnungen, die die Anzahl der Zeiten angeben, zu denen die Aktivität erfolgt ist (z.B. Brute Force mit einer Anzahl geschätzter Kennwörter)|
|app |In dieser Warnung verwendetes Protokoll|
|externalId|Ereignistyp-ID, die Azure ATP in das Ereignisprotokoll schreibt, das jedem Warnungstyp entspricht|
|cs#label|Die für CEF zulässigen Kundenzeichenfolgen, wobei „cs#label“ der Name des neuen Felds ist |
|cs#|Die für CEF zulässigen Kundenzeichenfolgen, wobei „cs#“ der Wert ist.|
|
- Beispiel: cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa
<br> Das Feld „cs1“ ist die Warnungs-URL. 

- Zum Beispiel: cs2Label=trigger cs2=new
<br> Das Feld „cs2“ ermittelt, ob die Warnung neu ist oder aktualisiert wurde.


> [!NOTE]
> Wenn Sie eine Automatisierung oder Skripts für Azure ATP-SIEM-Protokoll erstellen möchten, sollten Sie zur Identifizierung des Warnungstyps das Feld **externalID** statt des Warnungsnamens verwenden. Warnungsnamen können nämlich gelegentlich geändert werden, während die **externalId** jeder Warnung dauerhaft ist.  

## <a name="azure-atp-security-alert-unique-externalids"></a>Azure ATP-Sicherheitswarnung: Eindeutige externalIds

|Sicherheitswarnungsname|Eindeutige externalId|
|---------|---------|
|Brute-Force-Angriff mithilfe einer einfachen LDAP-Bindung|2004|
|Aktivität zur Herabstufung der Verschlüsselung: Skeleton Key|2011|
|Aktivität zur Herabstufung der Verschlüsselung (potenzieller Overpass-the-Hash-Angriff)|2008|
|Aktivität zur Herabstufung der Verschlüsselung (potenzieller Golden Ticket-Angriff)|2009|
|Aktivität zur Herabstufung der Verschlüsselung (potenzieller Skeleton Key-Angriff)|2010|
|Honeytoken-Aktivität|2014|
|Identitätsdiebstahl mithilfe eines Pass-the-Hash-Angriffs|2017|
|Identitätsdiebstahl mithilfe eines Pass-the-Ticket-Angriffs|2018|
|Golden Ticket von Kerberos: Zeitanomalie|2022|
|Kerberos Golden Ticket: nicht vorhandenes Konto|2027|
|Böswillige Anforderung privater Informationen im Rahmen der Datensicherheit|2020|
|Böswillige Replikation von Verzeichnisdiensten|2006|
|Berechtigungsausweitung mithilfe von gefälschten Autorisierungsdaten|2013|
|Reconnaissance mithilfe von Kontoenumeration|2003|
|Reconnaissance über DNS|2007|
|Reconnaissance mithilfe der SMB-Sitzungsenumeration|2012|
|Reconnaissance mithilfe von Verzeichnisdienstabfragen|2021|
|Versuchte Remote-Codeausführung|2019|
|Verdächtige Authentifizierungsfehler|2023|
|Verdächtige Replikationsanforderung von Domänencontroller (potenzieller DCShadow-Angriff)|2029|
|Verdächtige Heraufstufung zu Domänencontrollern (potenzieller DcShadow-Angriff)|2028|
|Verdächtige Kommunikation über DNS|2031|
|Verdächtige Modifizierung von sensiblen Gruppen|2024|
|Erstellen eines verdächtigen Diensts|2026|
|Verdächtige VPN-Verbindung|2025|
|Ungewöhnliche Protokollimplementierung (potenzieller WannaCry-Ransomwareangriff)*|2002|
|Ungewöhnliche Protokollimplementierung (potenzielle Verwendung schädlicher Tools wie Hydra)*|2002|
|Ungewöhnliche Protokollimplementierung (potenzielle Verwendung schädlicher Hackertools wie Metasploit)*|2002|
|Ungewöhnliche Kerberos-Protokollimplementierung (potenzieller Overpass-the-Hash-Angriff)*|2002|
|Warnungen von *ungewöhnlichen Protokollimplementierungen* haben derzeit die gleiche externalId. In einem zukünftigen Release soll jeder Warnungstyp eine eindeutige externalId erhalten.|****|

## <a name="sample-logs"></a>Beispielprotokolle

Die Beispielprotokolle gelten zwar für RFC 5242, doch Azure ATP unterstützt auch RFC 3164.

Prioritäten:

- 3=Niedrig
- 5=Mittel
- 10=Hoch

### <a name="brute-force-attack-using-ldap-simple-bind"></a>Brute-Force-Angriff mithilfe einer einfachen LDAP-Bindung
02-21-2018  16:20:21    Auth.Warning    192.168.0.220   1 2018-02-21T14:20:06.156238+00:00 CENTER CEF 6076 LdapBruteForceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|LdapBruteForceSecurityAlert|Brute force attack using LDAP simple bind|5|start=2018-02-21T14:19:41.7422810Z app=Ldap suser=Wofford Thurston shost=CLIENT1 msg=A brute force attack using the Ldap protocol was attempted on Wofford Thurston (Software Engineer) from CLIENT1 (100 guess attempts). cnt=100 externalId=2004 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/57b8ac96-7907-4971-9b27-ec77ad8c029a cs2Label=trigger cs2=update

### <a name="encryption-downgrade-activity---golden-ticket"></a>Aktivität zur Herabstufung der Verschlüsselung: Golden Ticket
10-29-2018  11:25:07    Auth.Warning    192.168.0.202   1 2018-10-29T09:25:01.007701+00:00 DC3 CEF 3908 GoldenTicketEncryptionDowngradeS ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|GoldenTicketEncryptionDowngradeSecurityAlert|Encryption downgrade activity (potential golden ticket attack)|5|start=2018-10-29T09:37:49.0849130Z app=Kerberos msg=W10-000007-Lap used a weaker encryption method (RC4),Â in the Kerberos service request (TGS_REQ),Â from W10-000007-Lap, to access host/domain1.test.local. externalId=2009 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/f01f8403-88b2-437e-b4ad-d72485fe05ac cs2Label=trigger cs2=new

### <a name="encryption-downgrade-activity----skeleton-key"></a>Aktivität zur Herabstufung der Verschlüsselung – Skeleton Key
02-21-2018  16:21:07    Auth.Warning    192.168.0.220   1 2018-02-21T14:20:54.145833+00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|EncryptionDowngradeSecurityAlert|Encryption downgrade activity|5|start=2018-02-21T14:19:41.8737870Z app=Kerberos msg=The encryption method of the ETYPE_INFO2 field of KRB_ERR message from CLIENT1 has been downgraded based on previously learned behavior. Grund dafür ist möglicherweise ein Skeleton Key auf DC1. externalId=2011 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2 cs2Label=trigger cs2=new

### <a name="encryption-downgrade-activity---overpass-the-hash"></a>Aktivität zur Herabstufung der Verschlüsselung – Overpass-the-Hash
02-21-2018  16:21:07    Auth.Warning    192.168.0.220   1 2018-02-21T14:20:54.145833+00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|EncryptionDowngradeSecurityAlert|Encryption downgrade activity|5|start=2018-02-21T14:19:41.8737870Z app=Kerberos msg= The encryption method of the Encrypted_Timestamp field of AS_REQ message from CLIENT1 has been downgraded based on previously learned behavior. Grund dafür ist möglicherweise ein Diebstahl von Anmeldeinformationen bei einem Overpass-The-Hash-Angriff auf CLIENT1. externalId=2011 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2 cs2Label=trigger cs2=update

### <a name="honeytoken-activity"></a>Honeytoken-Aktivität
02-21-2018  16:20:36    Auth.Warning  192.168.0.220 1 2018-02-21T14:20:34.106162+00:00 CENTER CEF 6076 HoneytokenActivitySecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|HoneytokenActivitySecurityAlert|Honeytoken activity|5|start=2018-02-21T14:20:26.6705617Z app=Kerberos suser=honey msg=Die folgenden Aktivitäten wurden vom Honeytoken ausgeführt:\r\nAnmeldung bei CLIENT2 über DC1 durchgeführt. externalId=2014 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/9249fe9a-c883-46dd-a4da-2a1fca5f211c cs2Label=trigger cs2=new

### <a name="identity-theft-using-pass-the-hash"></a>Identitätsdiebstahl mithilfe von Pass-the-Hash
02-21-2018  17:04:47    Auth.Error  192.168.0.220   1 2018-02-21T15:04:33.537583+00:00 CENTER CEF 6076 PassTheHashSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|PassTheHashSecurityAlert|Identity theft using Pass-the-Hash attack|10|start=2018-02-21T15:02:22.2577465Z app=Kerberos suser=Eugene Jenkins msg=Eugene Jenkins (Software Engineer)'s hash was stolen from one of the computers previously logged into by Eugene Jenkins (Software Engineer) and used from CLIENT1. externalId=2017 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd cs2Label=trigger cs2=update

### <a name="identity-theft-using-pass-the-ticket-attack"></a>Identitätsdiebstahl mithilfe eines Pass-the-Ticket-Angriffs
02-21-2018  17:04:47    Auth.Error  192.168.0.220   1 2018-02-21T15:04:33.537583+00:00 CENTER CEF 6076 PassTheTicketSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|PassTheTicketSecurityAlert|Identitätsdiebstahl mit Pass-the-Ticket-Angriff|10|start=2018-02-21T15:02:22.2577465Z app=Kerberos suser=Eugene Jenkins msg=Kerberos-Tickets von Eugene Jenkins (Softwareentwickler) wurden vom Administrator-PC zum Einsatz auf dem PC des Opfers gestohlen und für den Zugriff auf krbtgt/DOMAIN1.TEST.LOCAL verwendet. externalId=2018 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd cs2Label=trigger cs2=new

### <a name="kerberos-golden-ticket"></a>Kerberos Golden Ticket 
02-21-2018  16:22:39    Auth.Error  192.168.0.220   1 2018-02-21T14:22:34.274054+00:00 CENTER CEF 6076 GoldenTicketSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|GoldenTicketSecurityAlert|Kerberos Golden Ticket activity|10|start=2018-02-21T14:19:03.2416152Z app=Kerberos suser=Lanell Campos msg=Suspicious usage of Lanell Campos (Software Engineer)'s Kerberos ticket, indicating a potential Golden Ticket attack, was detected. externalId=2022 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/702c836e-6f49-4479-9892-80e8bccbfac0 cs2Label=trigger cs2=update

### <a name="kerberos-golden-ticket-non-existent-account"></a>Kerberos Golden Ticket, nicht vorhandenes Konto
07-01-2018  14:28:49    Auth.Error  192.168.0.100   1 2018-07-01T11:28:35.546638+00:00 CENTER CEF 38768 ForgedPrincipalSecurityAlert ï»¿0|Microsoft|Azure ATP|2.39.0.0|ForgedPrincipalSecurityAlert|Kerberos Golden Ticket – nicht vorhandenes Konto|10|start=2018-07-01T09:48:31.2567987Z app=Kerberos suser=domain1.test.local\fake msg=domain1.test.local\fake, das nicht in Active Directory vorhanden ist, hat ein Kerberos-Ticket verwendet. Das Ticket wurde von zwei Computern für den Zugriff auf drei Ressourcen erkannt. Dies kann auf einen potenziellen Golden Ticket-Angriff hinweisen. externalId=2027 cs1Label=url cs1=https://contoso-corp.atp.azure.com:13000/securityAlert/98f050d4-9134-429c-8e54-d8eeb19849c4 cs2Label=trigger cs2=update

### <a name="malicious-data-protection-private-information-request"></a>Böswillige Anforderung privater Informationen im Rahmen der Datensicherheit
10-29-2018  11:22:04    Auth.Error  192.168.0.202   1 2018-10-29T09:22:00.350864+00:00 DC3 CEF 3908 RetrieveDataProtectionBackupKeyS ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|RetrieveDataProtectionBackupKeySecurityAlert|Malicious Data Protection Private Information Request|10|start=2018-10-29T09:19:45.6307993Z app=LsaRpc shost=CLIENT1 msg=user1 performed 1 successful attempts from CLIENT1 to retrieve DPAPI domain backup key from DC1. externalId=2020 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/2f5717cb-2434-4d54-8af4-b2c6d14bc15c cs2Label=trigger cs2=new

### <a name="malicious-replication-of-directory-services"></a>Böswillige Replikation von Verzeichnisdiensten 
02-21-2018  16:20:06    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:54.254930+00:00 CENTER CEF 6076 MaliciousServiceCreationSecurity ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|MaliciousServiceCreationSecurityAlert|Suspicious service creation|5|start=2018-02-21T14:19:41.7897808Z app=ServiceInstalledEvent shost=CLIENT1 msg=user1 created MaliciousService in order to execute potentially malicious commands on CLIENT1. externalId=2026 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/179229b6-b791-4895-b5aa-fdf3747a325c cs2Label=trigger cs2=update

### <a name="privilege-escalation-using-forged-authorization-data"></a>Berechtigungsausweitung mithilfe von gefälschten Autorisierungsdaten
10-29-2018  11:22:04    Auth.Error  192.168.0.202   1 2018-10-29T09:21:59.288337+00:00 DC3 CEF 3908 ForgedPacSecurityAlert ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|ForgedPacSecurityAlert|Privilege escalation using forged authorization data|10|start=2018-10-29T09:19:43.6403358Z app=Kerberos suser=user1 msg=user1 failed to escalate privileges against DC1 to host/domain1.test.local from CLIENT1 by using forged authorization data. externalId=2013 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/b698d438-5013-4bca-be0b-f219f8b69108 cs2Label=trigger cs2=new

### <a name="reconnaissance-using-account-enumeration"></a>Reconnaissance mithilfe von Kontoenumeration
02-21-2018  16:19:35    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:27.540731+00:00 CENTER CEF 6076 AccountEnumerationSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AccountEnumerationSecurityAlert|Reconnaissance using account enumeration|5|start=2018-02-21T14:19:02.6045416Z app=Kerberos shost=CLIENT1 suser=LMaldonado msg=Suspicious account enumeration activity using the Kerberos protocol, originating from CLIENT1, was observed and successfully guessed Lamon Maldonado (Software Engineer). externalId=2003 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/eb6a35da-ff7f-4ab5-a1b5-a07529a89e6d cs2Label=trigger cs2=new

### <a name="reconnaissance-using-directory-services-queries"></a>Reconnaissance mithilfe von Verzeichnisdienstabfragen 
02-21-2018  16:22:08    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:54.267658+00:00 CENTER CEF 6076 SamrReconnaissanceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|SamrReconnaissanceSecurityAlert| Reconnaissance using directory services enumeration |5|start=2018-02-21T14:19:41.9912772Z app= Samr shost=CLIENT1 suser=user1 outcome=Success msg= The following directory services enumerations using SAMR protocol were attempted against DC1 from CLIENT1:\r\nSuccessful enumeration of all groups in domain1.test.local by user1. externalId=2019 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/f295029a-ffae-408b-9dd0-55424c81eac0 cs2Label=trigger cs2=new

### <a name="reconnaissance-using-dns"></a>Reconnaissance über DNS
02-21-2018  16:20:06    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:54.063994+00:00 CENTER CEF 6076 DnsReconnaissanceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|DnsReconnaissanceSecurityAlert|Reconnaissance using DNS|5|start=2018-02-21T14:19:41.9417776Z app=Dns shost=CLIENT1 request=demo query requestMethod=Axfr reason=NoError outcome=Success msg=Suspicious DNS activity was observed, originating from CLIENT1 (which is not a DNS server). Die Abfrage wurde als Demoabfrage gesendet (Typ „Axfr“). Als Antwort wurde „NoError“ zurückgegeben. externalId=2007 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/6f69e1e7-304a-4054-8edf-33f26c1f004c cs2Label=trigger cs2=update

### <a name="reconnaissance-using-smb-session-enumeration"></a>Reconnaissance mithilfe der SMB-Sitzungsenumeration
02-21-2018  16:21:22    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:13.962930+00:00 CENTER CEF 6076 EnumerateSessionsSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|EnumerateSessionsSecurityAlert|Reconnaissance using SMB Session Enumeration|5|start=2018-02-21T14:19:03.2071170Z app=SrvSvc shost=CLIENT1 msg=SMB session enumeration attempts were successfully performed by user1, from CLIENT1 against DC1, exposing Eugene Jenkins (user2-computer). externalId=2012 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/622c38ab-324f-4c1f-9caa-1fe85db3b440 cs2Label=trigger cs2=new

### <a name="remote-code-execution-attempt"></a>Versuchte Remote-Codeausführung
02-21-2018  16:22:08    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:54.267658+00:00 CENTER CEF 6076 RemoteExecutionSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|RemoteExecutionSecurityAlert|Remote execution attempt detected|5|start=2018-02-21T14:19:41.9912772Z app=Wmi shost=CLIENT1 suser=user1 outcome=Success msg=The following remote execution attempts were performed on DC1 from CLIENT1:\r\nSuccessful remote execution of one or more WMI methods by user1. externalId=2019 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/f295029a-ffae-408b-9dd0-55424c81eac0 cs2Label=trigger cs2=new

### <a name="suspicious-authentication-failures"></a>Verdächtige Authentifizierungsfehler
02-21-2018  16:19:20    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:15.397995+00:00 CENTER CEF 6076 BruteForceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|BruteForceSecurityAlert|Suspicious authentication failures|5|start=2018-02-21T14:19:03.3831122Z app=Kerberos shost=CLIENT1 msg=Suspicious authentication failures indicating a potential brute-force attack were detected from CLIENT1. externalId=2023 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/fea88fc7-4110-454d-816d-349032474fd6 cs2Label=trigger cs2=new

### <a name="suspicious-communication-over-dns"></a>Verdächtige Kommunikation über DNS
10-04-2018  14:49:38    Auth.Warning    192.168.0.202   1 2018-10-04T11:49:25.954059+00:00 DC3 CEF 3604 DnsSuspiciousCommunicationSecuri ï»¿0|Microsoft|Azure ATP|2.49.5589.58606|DnsSuspiciousCommunicationSecurityAlert|Suspicious Communication over DNS|5|start=2018-10-04T11:49:11.0822077Z app=DnsEvent dhost= suspiciousdomainname msg=CLIENT1 sent suspicious DNS queries resolving suspiciousdomainname externalId=2031 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/0fc77777-49ca-40b3-a7ba-7644f355539e cs2Label=trigger cs2=new

### <a name="suspicious-domain-controller-promotion-potential-dcshadow-attack"></a>Verdächtige Heraufstufung zu Domänencontrollern (potenzieller DcShadow-Angriff)
07-12-2018  11:18:07    Auth.Error  192.168.0.200    1 2018-07-12T08:18:06.883880+00:00 DC1 CEF 3868 DirectoryServicesRoguePromotionS ï»¿0|Microsoft|Azure ATP|2.40.0.0|DirectoryServicesRoguePromotionSecurityAlert| **Suspicious domain controller promotion (potential DcShadow attack)**|10|start=2018-07-12T08:17:55.4067092Z app=Ldap shost=CLIENT1 msg=CLIENT1, which is a computer in domain1.test.local, registered as a domain controller on DC1. externalId=2028 cs1Label=url cs1=https://contoso-corp.atp.azure.com:13000/securityAlert/97c59b43-dc18-44ee-9826-8fd5d03bd53 cs2Label=trigger cs2=update

### <a name="suspicious-modification-of-sensitive-groups"></a>Verdächtige Modifizierung von sensiblen Gruppen
10-29-2018  11:21:03    Auth.Warning    192.168.0.202   1 2018-10-29T09:20:49.667014+00:00 DC3 CEF 3908 AbnormalSensitiveGroupMembership ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|AbnormalSensitiveGroupMembershipChangeSecurityAlert|Suspicious modification of sensitive groups|5|start=2018-10-29T09:19:43.3013729Z app=GroupMembershipChangeEvent suser=user1 msg=user1 has uncharacteristically modified sensitive group memberships. externalId=2024 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/6f7e677e-f068-41e5-bada-708cd5a322b9 cs2Label=trigger cs2=new

### <a name="suspicious-replication-of-directory-services"></a>Verdächtige Replikation von Verzeichnisdiensten
02-21-2018  16:21:22    Auth.Error  192.168.0.220   1 2018-02-21T14:21:13.978554+00:00 CENTER CEF 6076 DirectoryServicesReplicationSecu ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|DirectoryServicesReplicationSecurityAlert|Malicious replication of directory services|10|start=2018-02-21T14:19:03.9975656Z app=Drsr shost=CLIENT1 msg=Malicious replication requests were successfully performed by user1, from CLIENT1 against DC1. outcome=Success externalId=2006 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/cb95648e-1b6f-4d3b-81b9-7605532787d7 cs2Label=trigger cs2=new

### <a name="suspicious-replication-request-potential-dcshadow-attack"></a>Verdächtige Replikationsanforderung (potenzieller DcShadow-Angriff)
07-12-2018  11:18:37    Auth.Error  192.168.0.200    1 2018-07-12T08:18:32.265989+00:00 DC1 CEF 3868 DirectoryServicesRogueReplicatio ï»¿0|Microsoft|Azure ATP|2.40.0.0|DirectoryServicesRogueReplicationSecurityAlert| **Suspicious replication request (potential DcShadow attack)**|10|start=2018-07-12T08:17:55.3816102Z **app=Replication Activity** shost=CLIENT1 msg=CLIENT1, which is not a valid domain controller in domain1.test.local, sent changes to directory objects on DC1. externalId=2029 cs1Label=url cs1=https://contoso-corp.atp.azure.com:13000/securityAlert/1d5d1444-12cf-4db9-be48-39ebc2f51515 cs2Label=trigger cs2=new

### <a name="suspicious-service-creation"></a>Erstellen eines verdächtigen Diensts 
10-29-2018  11:20:02    Auth.Warning    192.168.0.202   1 2018-10-29T09:19:59.164874+00:00 DC3 CEF 3908 MaliciousServiceCreationSecurity ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|MaliciousServiceCreationSecurityAlert|Suspicious service creation|5|start=2018-10-29T09:19:44.9471965Z app=ServiceInstalledEvent shost=CLIENT1 msg=user1 created MaliciousService in order to execute potentially malicious commands on CLIENT1. externalId=2026 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/118bbe3d-fe72-40de-80d0-2678b68aa027 cs2Label=trigger cs2=new

### <a name="suspicious-vpn-connection"></a>Verdächtige VPN-Verbindung
07-03-2018  13:13:12    Auth.Warning  192.168.0.200   1 2018-07-03T10:13:06.187834+00:00 DC1 CEF 2520 AbnormalVpnSecurityAlert ï»¿0|Microsoft|Azure ATP|2.39.0.0|AbnormalVpnSecurityAlert|Suspicious VPN Connection|5|start=2018-06-30T15:34:05.3887333Z app=VpnConnection suser=user1 msg=user1 connected to a VPN using 3 computers from 3 Locations.     externalId=2025 cs1Label=url cs1=https://contoso-corp.eng.atp.azure.com:13000/securityAlert/88c46b0e-372f-4c06-9935-67bd512c4f68 cs2Label=trigger cs2=new

### <a name="unusual-protocol-implementation---potential-use-of-malicious-tools-such-a-hydra"></a>Ungewöhnliche Protokollimplementierung (potenzielle Verwendung von schädlichen Tools wie Hydra)*
02-21-2018  16:21:22    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:13.916050+00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AbnormalProtocolSecurityAlert|Unusual protocol implementation|5|start=2018-02-21T14:19:03.1981155Z app=Ntlm shost=CLIENT2 outcome=Success msg=There were attempts to authenticate from CLIENT2 against DC1 using an unusual protocol implementation. Kann auf den Einsatz von schädlichen Tools zum Ausführen eines Pass-the-Hash- oder Brute-Force-Angriffs hinweisen. externalId=2002 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label=trigger cs2=new

### <a name="unusual-protocol-implementation--potential-use-of-malicious-tools-such-a-metasploit"></a>Ungewöhnliche Protokollimplementierung (potenzielle Verwendung von schädlichen Tools wie Metasploit)*
10-29-2018  11:22:04    Auth.Warning    192.168.0.202   1 2018-10-29T09:22:00.460233+00:00 DC3 CEF 3908 AbnormalProtocolSecurityAlert ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|AbnormalProtocolSecurityAlert|Unusual protocol implementation (potential use of Metasploit hacking tools)|5|start=2018-10-29T09:19:46.6092465Z app=Ntlm shost=CLIENT2 outcome=Success msg=There were attempts to authenticate from CLIENT2 against DC1 using an unusual protocol implementation. externalId=2002 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/573f10a1-6f8a-44b1-a5b1-212d40996363 cs2Label=trigger cs2=new

## <a name="see-also"></a>Weitere Informationen
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Azure ATP capacity planning (Azure ATP-Kapazitätsplanung)](atp-capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
