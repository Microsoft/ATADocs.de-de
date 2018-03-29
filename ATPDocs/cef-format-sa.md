---
title: Referenz zum Azure ATP-SIEM-Protokoll | Microsoft-Dokumentation
description: Stellt Beispiele über verdächtige Aktivitätsprotokolle bereit, die von Azure ATP an SIEM gesendet werden.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/28/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 3261155c-3c72-4327-ba29-c113c63a4e6d
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 0a632473490d157e2b85a30bdb82947982da9551
ms.sourcegitcommit: 7c9fe4eb781bec71129310a6e0c5e76b022a0213
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
*Gilt für: Azure Advanced Threat Protection*


# <a name="azure-atp-siem-log-reference"></a>Referenz zum Azure ATP-SIEM-Protokoll

Azure ATP kann verdächtige Aktivitäten und die Überwachung von Warnereignissen an SIEM weiterleiten. Verdächtige Aktivitätsereignisse haben das CEF-Format. Dieser Verweisartikel bietet Beispiele verdächtiger Aktivitätsprotokolle, die an Ihren SIEM-Agent gesendet wurden.

## <a name="sample-azure-atp-suspicious-activities-in-cef-format"></a>Beispiel: verdächtige Azure ATP-Aktivitäten im CEF-Format
Die folgenden Felder und deren Werte werden an Ihren SIEM-Agent weitergeleitet:

-   start : die Startzeit der Warnung
-   suser: das Konto (normalerweise das Benutzerkonto), das in dieser Warnung mit einbezogen ist
-   shost: der Quellcomputer für diese Warnung
-   outcome: für Warnungen; die in der Warnung ausgeführte Aktivität ist erfolgreich/schlägt fehl  
-   msg: die Beschreibung für die Warnung
-   cnt: für Warnungen, die die Zeiten angeben, wann die Warnung aufgetreten ist (z.B. Brute Force mit einer Anzahl geschätzter Kennwörter)
-   app: das in dieser Warnung verwendete Protokoll
-   externalId: die Ereignis-ID, die Azure ATP in das Ereignisprotokoll schreibt, das dieser Warnung entspricht
-   cs#label & cs#: die Zeichenfolgen der Kunden, für die CEF zulässt, dass sie cs#label (Name des neuen Felds) und cs# (Wert) verwenden, z.B.: cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa

In diesem Beispiel ist cs1 ein Feld, das über eine URL für die Warnung verfügt.

## <a name="sample-logs"></a>Beispielprotokolle

Die folgenden Beispielprotokolle gelten zwar für RFC 5242, Azure ATP unterstützt jedoch auch RFC 3164.

Prioritäten:

- 3=Niedrig
- 5=Mittel
- 10=Hoch

### <a name="bruteforce--ldap"></a>BruteForce – LDAP
02-21-2018  16:20:21    Auth.Warning    192.168.0.220   1 2018-02-21T14:20:06.156238+00:00 CENTER CEF 6076 LdapBruteForceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|LdapBruteForceSecurityAlert|Brute force attack using LDAP simple bind|5|start=2018-02-21T14:19:41.7422810Z app=Ldap suser=Wofford Thurston shost=CLIENT1 msg=A brute force attack using the Ldap protocol was attempted on Wofford Thurston (Software Engineer) from CLIENT1 (100 guess attempts). cnt=100 externalId=2004 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/57b8ac96-7907-4971-9b27-ec77ad8c029a


### <a name="bruteforce"></a>BruteForce
02-21-2018  16:19:20    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:15.397995+00:00 CENTER CEF 6076 BruteForceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|BruteForceSecurityAlert|Suspicious authentication failures|5|start=2018-02-21T14:19:03.3831122Z app=Kerberos shost=CLIENT1 msg=Suspicious authentication failures indicating a potential brute-force attack were detected from CLIENT1. externalId=2023 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/fea88fc7-4110-454d-816d-349032474fd6
### <a name="privilege-escalation"></a>Ausweitung von Berechtigungen
#### <a name="silver"></a>Silver
02-21-2018  16:19:20    Auth.Error  192.168.0.220   1 2018-02-21T14:19:15.186167+00:00 CENTER CEF 6076 ForgedPacSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|ForgedPacSecurityAlert|Privilege escalation using forged authorization data|10|start=2018-02-21T14:19:02.8595383Z app=Kerberos suser=user1 msg=user1 attempted to escalate privileges to host/domain1.test.local from CLIENT1 by using forged authorization data. externalId=2013 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/029189e1-6bb4-490b-bcaf-5fac4457e9f3
#### <a name="gold"></a>Gold
02-21-2018  16:19:20    Auth.Error  192.168.0.220   1 2018-02-21T14:19:14.358037+00:00 CENTER CEF 6076 ForgedPacSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|ForgedPacSecurityAlert|Privilege escalation using forged authorization data|10|start=2018-02-21T14:19:02.8595383Z app=Kerberos suser=user1 msg=user1 failed to escalate privileges against DC1 to host/domain1.test.local from CLIENT1 by using forged authorization data. externalId=2013 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/f3359eff-cb59-44b9-82b6-5e82ff06e6c8
### <a name="golden-ticket"></a>Golden Ticket
02-21-2018  16:22:39    Auth.Error  192.168.0.220   1 2018-02-21T14:22:34.274054+00:00 CENTER CEF 6076 GoldenTicketSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|GoldenTicketSecurityAlert|Kerberos Golden Ticket activity|10|start=2018-02-21T14:19:03.2416152Z app=Kerberos suser=Lanell Campos msg=Suspicious usage of Lanell Campos (Software Engineer)'s Kerberos ticket, indicating a potential Golden Ticket attack, was detected. externalId=2022 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/702c836e-6f49-4479-9892-80e8bccbfac0
### <a name="honey-token-activity"></a>Honeytokenaktivität
02-21-2018  16:20:36    Auth.Warning    192.168.0.220   1 2018-02-21T14:20:34.106162+00:00 CENTER CEF 6076 HoneytokenActivitySecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|HoneytokenActivitySecurityAlert|Honeytoken activity|5|start=2018-02-21T14:20:26.6705617Z app=Kerberos suser=honey msg=The following activities were performed by honey:\r\nLogged in to CLIENT2 via DC1. externalId=2014 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/9249fe9a-c883-46dd-a4da-2a1fca5f211c
### <a name="suspicious-replication-of-directory-services"></a>Verdächtige Replikation von Verzeichnisdiensten
02-21-2018  16:21:22    Auth.Error  192.168.0.220   1 2018-02-21T14:21:13.978554+00:00 CENTER CEF 6076 DirectoryServicesReplicationSecu ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|DirectoryServicesReplicationSecurityAlert|Malicious replication of directory services|10|start=2018-02-21T14:19:03.9975656Z app=Drsr shost=CLIENT1 msg=Malicious replication requests were successfully performed by user1, from CLIENT1 against DC1. outcome=Success externalId=2006 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/cb95648e-1b6f-4d3b-81b9-7605532787d7
### <a name="malicious-data-protection-private-information-request"></a>Böswillige Anforderung privater Informationen im Rahmen der Datensicherheit
02-21-2018  16:22:08    Auth.Error  192.168.0.220   1 2018-02-21T14:21:54.080266+00:00 CENTER CEF 6076 RetrieveDataProtectionBackupKeyS ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|RetrieveDataProtectionBackupKeySecurityAlert|Malicious Data Protection Private Information Request|10|start=2018-02-21T14:19:41.8382786Z app=LsaRpc shost=CLIENT1 msg=user1 performed 1 successful attempts from CLIENT1 to retrieve DPAPI domain backup key from DC1. externalId=2020 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/b22221d1-764a-4fae-a5ce-e6a0c69dc55a

### <a name="over-pass-the-hash"></a>Over-pass-the-hash
02-21-2018  16:21:07    Auth.Warning    192.168.0.220   1 2018-02-21T14:20:54.145833+00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|EncryptionDowngradeSecurityAlert|Encryption downgrade activity|5|start=2018-02-21T14:19:41.8737870Z app=Kerberos msg= The encryption method of the Encrypted_Timestamp field of AS_REQ message from CLIENT1 has been downgraded based on previously learned behavior. Grund dafür ist möglicherweise ein Diebstahl von Anmeldeinformationen bei einem Overpass-The-Hash-Angriff auf CLIENT1. externalId=2011 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2
### <a name="pass-the-hash"></a>Pass-the-hash
02-21-2018  17:04:47    Auth.Error  192.168.0.220   1 2018-02-21T15:04:33.537583+00:00 CENTER CEF 6076 PassTheHashSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|PassTheHashSecurityAlert|Identity theft using Pass-the-Hash attack|10|start=2018-02-21T15:02:22.2577465Z app=Kerberos suser=Eugene Jenkins msg=Eugene Jenkins (Software Engineer)'s hash was stolen from one of the computers previously logged into by Eugene Jenkins (Software Engineer) and used from CLIENT1. externalId=2017 cs1Label=url cs1=https://test-syslog.eng.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd
### <a name="account-enumeration"></a>Kontoenumeration
02-21-2018  16:19:35    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:27.540731+00:00 CENTER CEF 6076 AccountEnumerationSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AccountEnumerationSecurityAlert|Reconnaissance using account enumeration|5|start=2018-02-21T14:19:02.6045416Z app=Kerberos shost=CLIENT1 suser=LMaldonado msg=Suspicious account enumeration activity using the Kerberos protocol, originating from CLIENT1, was observed and successfully guessed Lamon Maldonado (Software Engineer). externalId=2003 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/eb6a35da-ff7f-4ab5-a1b5-a07529a89e6d
### <a name="dns-recon"></a>DNS-Reconnaissance
02-21-2018  16:20:06    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:54.063994+00:00 CENTER CEF 6076 DnsReconnaissanceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|DnsReconnaissanceSecurityAlert|Reconnaissance using DNS|5|start=2018-02-21T14:19:41.9417776Z app=Dns shost=CLIENT1 request=demo query requestMethod=Axfr reason=NoError outcome=Success msg=Suspicious DNS activity was observed, originating from CLIENT1 (which is not a DNS server). Die Abfrage wurde als Demoabfrage gesendet (Typ „Axfr“). Als Antwort wurde „NoError“ zurückgegeben. externalId=2007 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/6f69e1e7-304a-4054-8edf-33f26c1f004c


### <a name="smb-session-enumeration"></a>SMB-Sitzungsauflistung
02-21-2018  16:21:22    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:13.962930+00:00 CENTER CEF 6076 EnumerateSessionsSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|EnumerateSessionsSecurityAlert|Reconnaissance using SMB Session Enumeration|5|start=2018-02-21T14:19:03.2071170Z app=SrvSvc shost=CLIENT1 msg=SMB session enumeration attempts were successfully performed by user1, from CLIENT1 against DC1, exposing Eugene Jenkins (user2-computer). externalId=2012 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/622c38ab-324f-4c1f-9caa-1fe85db3b440
### <a name="sam-r-enumeration"></a>SAM-R-Enumeration
02-21-2018  16:22:08    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:54.267658+00:00 CENTER CEF 6076 SamrReconnaissanceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|SamrReconnaissanceSecurityAlert| Reconnaissance using directory services enumeration |5|start=2018-02-21T14:19:41.9912772Z app= Samr shost=CLIENT1 suser=user1 outcome=Success msg= The following directory services enumerations using SAMR protocol were attempted against DC1 from CLIENT1:\r\nSuccessful enumeration of all groups in domain1.test.local by user1. externalId=2019 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/f295029a-ffae-408b-9dd0-55424c81eac0
### <a name="remote-execution"></a>Remoteausführung
02-21-2018  16:22:08    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:54.267658+00:00 CENTER CEF 6076 RemoteExecutionSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|RemoteExecutionSecurityAlert|Remote execution attempt detected|5|start=2018-02-21T14:19:41.9912772Z app=Wmi shost=CLIENT1 suser=user1 outcome=Success msg=The following remote execution attempts were performed on DC1 from CLIENT1:\r\nSuccessful remote execution of one or more WMI methods by user1. externalId=2019 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/f295029a-ffae-408b-9dd0-55424c81eac0
### <a name="skeleton-key"></a>Skeleton Key
02-21-2018  16:21:07    Auth.Warning    192.168.0.220   1 2018-02-21T14:20:54.145833+00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|EncryptionDowngradeSecurityAlert|Encryption downgrade activity|5|start=2018-02-21T14:19:41.8737870Z app=Kerberos msg=The encryption method of the ETYPE_INFO2 field of KRB_ERR message from CLIENT1 has been downgraded based on previously learned behavior. Grund dafür ist möglicherweise ein Skeleton Key auf DC1. externalId=2011 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2

### <a name="unusual-protocol-implementation"></a>Ungewöhnliche Protokollimplementierung
02-21-2018  16:21:22    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:13.916050+00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AbnormalProtocolSecurityAlert|Unusual protocol implementation|5|start=2018-02-21T14:19:03.1981155Z app=Ntlm shost=CLIENT2 outcome=Success msg=There were attempts to authenticate from CLIENT2 against DC1 using an unusual protocol implementation. Dies kann auf den Einsatz von schädlichen Tools zum Ausführen eines Pass-the-Hash- oder Brute-Force-Angriffs hinweisen. externalId=2002 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs1=https://192.168.0.220/suspiciousActivity/5909cce38ca1ec04d05f4ab4

### <a name="malicious-service-creation"></a>Erstellen eines schädlichen Diensts
02-21-2018  16:20:06    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:54.254930+00:00 CENTER CEF 6076 MaliciousServiceCreationSecurity ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|MaliciousServiceCreationSecurityAlert|Suspicious service creation|5|start=2018-02-21T14:19:41.7897808Z app=ServiceInstalledEvent shost=CLIENT1 msg=user1 created MaliciousService in order to execute potentially malicious commands on CLIENT1. externalId=2026 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/179229b6-b791-4895-b5aa-fdf3747a325c

### <a name="pass-the-ticket"></a>Pass-the-Ticket

02-21-2018  17:04:47    Auth.Error  192.168.0.220   1 2018-02-21T15:04:33.537583+00:00 CENTER CEF 6076 PassTheTicketSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|PassTheTicketSecurityAlert|Identity theft using Pass-the-Ticket attack|10|start=2018-02-21T15:02:22.2577465Z app=Kerberos suser=Eugene Jenkins msg=Eugene Jenkins (Software Engineer)'s Kerberos tickets were stolen from Admin-PC to Victom-PC and used to access krbtgt/DOMAIN1.TEST.LOCAL. externalId=2017 cs1Label=url cs1=https://contoso-corp.eng.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd


## <a name="see-also"></a>Weitere Informationen
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Azure ATP capacity planning (Azure ATP-Kapazitätsplanung)](atp-capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)