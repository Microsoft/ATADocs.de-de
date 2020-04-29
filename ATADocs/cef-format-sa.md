---
title: Referenz zum ATA-SIEM-Protokoll | Microsoft-Dokumentation
description: Stellt Beispiele über Sicherheitswarnungsprotokolle bereit, die von ATA an SIEM gesendet werden.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 12/20/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 601b48ba-a327-4aff-a1f9-2377a2bb7a42
ms.reviewer: ort
ms.suite: ems
ms.openlocfilehash: 12885e07707e458009025a551248af5ec68849d0
ms.sourcegitcommit: 8c0222dc8333b5aa47430c5daee9bc7f1d82df31
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2020
ms.locfileid: "81524836"
---
# <a name="ata-siem-log-reference"></a>Referenz zum ATA-SIEM-Protokoll


*Gilt für: Advanced Threat Analytics Version 1.9*

ATA kann Sicherheits-und Integritäts Warn Ereignisse an Siem weiterleiten. Warnungen werden im CEF-Format weitergeleitet. Ein Beispiel zu jeder Art von Sicherheitswarnungsprotokoll, das an SIEM gesendet werden soll, finden Sie unten.

## <a name="sample-ata-security-alerts-in-cef-format"></a>Beispielsicherheitswarnungen von ATA im CEF-Format
Die folgenden Felder und deren Werte werden an Ihren SIEM-Agent weitergeleitet:

-   start – Startzeit der Warnung
-   suser – Konto (normalerweise das Benutzerkonto), das an der Warnung beteiligt ist
-   shost – Quellcomputer der Warnung
-   outcome – Warnungen mit definiertem Aktivitätserfolg oder Fehler, die in der Warnung ausgeführt wurden  
-   msg – Beschreibung der Warnung
-   cnt – Warnungen mit einer Anzahl der Zeiten, zu denen die Warnung erfolgt ist (z. B. Brute Force mit einer Anzahl geschätzter Kennwörter)
-   app – Warnungsprotokoll
-   externalId – Ereignis-ID, die ATA in das Ereignisprotokoll schreibt, das der Warnung entspricht*
-   cs#label & cs# – Zeichenfolgen der Kunden, für die CEF zulässt, dass sie cs#label (Name des neuen Felds) und cs# (Wert) verwenden, z. B.: cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa

In diesem Beispiel ist cs1 ein Feld, das über eine URL für die Warnung verfügt.

*Wenn Sie Skripts oder Automatisierungen basierend auf Protokollen erstellen, verwenden Sie die permanente externe ID der einzelnen Protokolle anstelle der Protokollnamen, da die Protokollnamen ohne vorherige Ankündigung geändert werden können. 

|Warnungsnamen|Ereignis-IDs der Warnungen|
|---------|---------------|
|2001|Verdacht des Identitätsdiebstahls auf Grundlage von ungewöhnlichem Verhalten|
|2002|Ungewöhnliche Protokollimplementierung|
|2003|Reconnaissance mithilfe von Kontoenumeration|
|2004|Brute-Force-Angriff mithilfe einer einfachen LDAP-Bindung|
|2006|Böswillige Replikation von Verzeichnisdiensten|
|2007|Reconnaissance über DNS|
|2008|Aktivität zur Herabstufung der Verschlüsselung|
|2009|Aktivität zur Herabstufung der Verschlüsselung (potenzieller Golden Ticket-Angriff)|
|2010|Aktivität zur Herabstufung der Verschlüsselung (potenzieller Overpass-the-Hash-Angriff)|
|2011|Aktivität zur Herabstufung der Verschlüsselung (potenzieller Skeleton Key-Angriff)|
|2012|Reconnaissance mithilfe der SMB-Sitzungsenumeration|
|2013|Berechtigungsausweitung mithilfe von gefälschten Autorisierungsdaten|
|2014|Honeytoken-Aktivität|
|2016|Umfangreiche Objektlöschungen|
|2017|Identitätsdiebstahl mithilfe eines Pass-the-Hash-Angriffs|
|2018|Identitätsdiebstahl mithilfe eines Pass-the-Ticket-Angriffs|
|2019|Erkannter Remoteausführungsversuch|
|2020|Böswillige Anforderung privater Informationen im Rahmen der Datensicherheit|
|2021|Reconnaissance mithilfe von Verzeichnisdienstabfragen|
|2022|Golden Ticket-Aktivität von Kerberos|
|2023|Verdächtige Authentifizierungsfehler|
|2024|Ungewöhnliche Modifizierung von sensiblen Gruppen|
|2026|Erstellen eines verdächtigen Diensts|



## <a name="sample-logs"></a>Beispielprotokolle

Prioritäten: 3 = niedrig, 5 = mittel 10 = hoch

### <a name="abnormal-modification-of-sensitive-groups"></a>Ungewöhnliche Modifizierung von sensiblen Gruppen
1 2018-12-12T16:53:22.925757+00:00 CENTER ATA 4688 AbnormalSensitiveGroupMembership CEF:0|Microsoft|ATA|1.9.0.0|AbnormalSensitiveGroupMembershipChangeSuspiciousActivity|Ungewöhnliche Modifizierung von sensiblen Gruppen|5|start=2018-12-12T18:52:58.0000000Z app=GroupMembershipChangeEvent suser=krbtgt msg=krbtgt weist ungewöhnlich geänderte sensible Gruppenmitgliedschaften auf. externalId=2024 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113d028ca1ec1250ca0491

### <a name="brute-force-attack-using-ldap-simple-bind"></a>Brute-Force-Angriff mithilfe einer einfachen LDAP-Bindung
12-12-2018  19:52:18    Auth.Warning    192.168.0.222   1 2018-12-12T17:52:18.899690+00:00 CENTER ATA 4688 LdapBruteForceSuspiciousActivity ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|LdapBruteForceSuspiciousActivity|Brute-Force-Angriff mithilfe einer einfachen LDAP-Bindung|5|start=2018-12-12T17:52:10.2350665Z app=Ldap msg=10000 Versuche zum Raten von Kennwörtern wurden für 100 Konten von W2012R2-000000-Server durchgeführt. Ein Kontokennwort wurde erfolgreich geraten. externalId=2004 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114acb8ca1ec1250cacdcb

### <a name="encryption-downgrade-activity-golden-ticket"></a>Aktivität zur Herabstufung der Verschlüsselung (Golden Ticket)
12-12-2018  20:12:35    Auth.Warning    192.168.0.222   1 2018-12-12T18:12:35.105942+00:00 CENTER ATA 4688 EncryptionDowngradeSuspiciousAct ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|EncryptionDowngradeSuspiciousActivity|Aktivität zur Herabstufung der Verschlüsselung|5|start=2018-12-12T18:10:35.0334169Z app=Kerberos msg=Die Verschlüsselungsmethode des TGT-Felds der TGS_REQ-Nachricht von W2012R2-000000-Server wurde basierend auf dem zuvor erlernten Verhalten heruntergestuft. Dies kann das Ergebnis eines auf W2012R2-000000-Server verwendeten Golden Ticket sein. externalId=2009 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114f938ca1ec1250cafcfa

### <a name="encryption-downgrade-activity-overpass-the-hash"></a>Aktivität zur Herabstufung der Verschlüsselung (Overpass-the-Hash)
12-12-2018  19:00:31    Auth.Warning    192.168.0.222   1 2018-12-12T17:00:31.963485+00:00 CENTER ATA 4688 EncryptionDowngradeSuspiciousAct ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|EncryptionDowngradeSuspiciousActivity|Aktivität zur Herabstufung der Verschlüsselung|5|start=2018-12-12T17:00:31.2975188Z app=Kerberos msg=Die Verschlüsselungsmethode des Felds Encrypted_Timestamp der AS_REQ-Nachricht von W2012R2-000000-Server wurde basierend auf dem zuvor erlernten Verhalten heruntergestuft. Grund dafür ist möglicherweise ein Diebstahl von Anmeldeinformationen bei einem Overpass-The-Hash-Angriff auf W2012R2-000000-Server. externalId=2010 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113eaf8ca1ec1250ca0883

###  <a name="encryption-downgrade-activity-skeleton-key"></a>Aktivität zur Herabstufung der Verschlüsselung (Skeleton Key)
12-12-2018  20:07:24    Auth.Warning    192.168.0.222   1 2018-12-12T18:07:24.065140+00:00 CENTER ATA 4688 EncryptionDowngradeSuspiciousAct ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|EncryptionDowngradeSuspiciousActivity|Aktivität zur Herabstufung der Verschlüsselung|5|start=2018-12-12T18:07:24.0222746Z app=Kerberos msg=Die Verschlüsselungsmethode des ETYPE_INFO2-Felds der KRB_ERR-Nachricht von W2012R2-000000-Server wurde basierend auf dem zuvor erlernten Verhalten heruntergestuft. Grund dafür ist möglicherweise ein Skeleton Key auf DC1. externalId=2011 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114e5c8ca1ec1250cafafe

### <a name="honeytoken-activity"></a>Honeytoken-Aktivität
12-12-2018  19:51:52    Auth.Warning    192.168.0.222   1 2018-12-12T17:51:52.659618+00:00 CENTER ATA 4688 HoneytokenActivitySuspiciousActi ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|HoneytokenActivitySuspiciousActivity|Honeytoken activity|5|start=2018-12-12T17:51:52.5855994Z app=Kerberos suser=USR78982 msg=Die folgenden Aktivitäten wurden von USR78982 LAST78982 durchgeführt:\r\nVon CLIENT1 mit NTLM beim Zugriff auf domain1.test.local\cifs auf DC1 authentifiziert. externalId=2014 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114ab88ca1ec1250ca7f76

### <a name="identity-theft-using-pass-the-hash-attack"></a>Identitätsdiebstahl mithilfe eines Pass-the-Hash-Angriffs
12-12-2018  19:56:02    Auth.Error  192.168.0.222   1 2018-12-12T17:56:02.047236+00:00 CENTER ATA 4688 PassTheHashSuspiciousActivity ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|PassTheHashSuspiciousActivity|Identitätsdiebstahl mithilfe eines Pass-the-Hash-Angriffs|10|start=2018-12-12T17:54:01.9582400Z app=Ntlm suser=USR46829 LAST46829 msg=Hash von USR46829 LAST46829 wurde von einem der Computer gestohlen, die zuvor von USR46829 LAST46829 angemeldet und von W2012R2-000000-Server verwendet wurden. externalId=2017 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114bb28ca1ec1250caf673

### <a name="identity-theft-using-pass-the-ticket-attack"></a>Identitätsdiebstahl mithilfe eines Pass-the-Ticket-Angriffs
12-12-2018  22:03:51    Auth.Error  192.168.0.222   1 2018-12-12T20:03:51.643633+00:00 CENTER ATA 4688 PassTheTicketSuspiciousActivity ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|PassTheTicketSuspiciousActivity|Identitätsdiebstahl mithilfe eines Pass-the-Ticket-Angriffs|10|start=2018-12-12T17:54:12.9960662Z app=Kerberos suser=Birdie Lamb msg=Die Kerberos-Tickets von Birdie Lamb (Softwareentwickler) wurden von W2012R2-000106-Server bis W2012R2-000051-Server gestohlen und für den Zugriff auf domain1.test.local\host verwendet. externalId=2018 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114b458ca1ec1250caf5b7

### <a name="kerberos-golden-ticket-activity"></a>Golden Ticket-Aktivität von Kerberos
12-12-2018  19:53:26    Auth.Error  192.168.0.222   1 2018-12-12T17:53:26.869091+00:00 CENTER ATA 4688 GoldenTicketSuspiciousActivity ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|GoldenTicketSuspiciousActivity|Golden Ticket-Aktivität von Kerberos|10|start=2018-12-13T06:51:26.7290524Z app=Kerberos suser=Sonja Chadsey msg=Es wurde eine verdächtige Nutzung des Kerberos-Tickets von Sonja Chadsey (Softwareentwicklerin) erkannt, die auf einen möglichen Golden Ticket-Angriff hinweist. externalId=2022 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114b168ca1ec1250caf556

### <a name="malicious-data-protection-private-information-request"></a>Böswillige Anforderung privater Informationen im Rahmen der Datensicherheit
12-12-2018  20:03:49    Auth.Error  192.168.0.222   1 2018-12-12T18:03:49.814620+00:00 CENTER ATA 4688 RetrieveDataProtectionBackupKeyS ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|RetrieveDataProtectionBackupKeySuspiciousActivity|Böswillige Anforderung privater Informationen im Rahmen der Datensicherheit|10|start=2018-12-12T17:58:56.3537533Z app=LsaRpc shost=W2012R2-000000-Server msg=Ein unbekannter Benutzer hat einen erfolgreichen Versuch von W2012R2-000000-Server durchgeführt, den DPAPI-Domänensicherungsschlüssel von DC1 abzurufen. externalId=2020 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114d858ca1ec1250caf983

### <a name="malicious-replication-of-directory-services"></a>Böswillige Replikation von Verzeichnisdiensten
12-12-2018  19:56:49    Auth.Error  192.168.0.222   1 2018-12-12T17:56:49.312648+00:00 CENTER ATA 4688 DirectoryServicesReplicationSusp ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|DirectoryServicesReplicationSuspiciousActivity|Böswillige Replikation von Verzeichnisdiensten|10|start=2018-12-12T17:52:34.3287329Z app=Drsr shost=W2012R2-000000-Server msg=Es wurden erfolgreich böswillige Replikationsanforderungen von W2012R2-000000-Server für DC1 durchgeführt. outcome=Success externalId=2006 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114be18ca1ec1250caf6b8

### <a name="privilege-escalation-using-forged-authorization-data"></a>Berechtigungsausweitung mithilfe von gefälschten Autorisierungsdaten
12-12-2018  19:51:15    Auth.Error  192.168.0.222   1 2018-12-12T17:51:15.658608+00:00 CENTER ATA 4688 ForgedPacSuspiciousActivity ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|ForgedPacSuspiciousActivity|Berechtigungsausweitung mithilfe von gefälschten Autorisierungsdaten|10|start=2018-12-12T17:51:15.0261128Z app=Kerberos suser=triservice msg=triservice hat versucht, mithilfe gefälschter Autorisierungsdaten die Berechtigungen für DC1 von W2012R2-000000-Server auszuweiten. externalId=2013 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114a938ca1ec1250ca7f48

### <a name="reconnaissance-using-directory-services-queries"></a>Reconnaissance mithilfe von Verzeichnisdienstabfragen
12-12-2018  20:23:52    Auth.Warning    192.168.0.222   1 2018-12-12T18:23:52.155531+00:00 CENTER ATA 4688 SamrReconnaissanceSuspiciousActi ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|SamrReconnaissanceSuspiciousActivity|Reconnaissance mithilfe von Verzeichnisdienstabfragen|5|start=2018-12-12T18:04:12.9868815Z app=Samr shost=W2012R2-000000-Server msg=Die folgenden Verzeichnisdienstabfragen mit dem SAMR-Protokoll wurden bei DC1 von W2012R2-000000-Server versucht:\r\nErfolgreiche Abfrage zu Eingehende Gesamtstruktur-Vertrauensstellung (Mitglieder dieser Gruppe können eingehende, unidirektionale Vertrauensstellungen für diese Gesamtstruktur erstellen) in domain1.test.local externalId=2021 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114e758ca1ec1250cafb2e

### <a name="reconnaissance-using-account-enumeration"></a>Reconnaissance mithilfe von Kontoenumeration
1 2018-12-12T16:57:09.661680+00:00 CENTER ATA 4688 AccountEnumerationSuspiciousActi CEF:0|Microsoft|ATA|1.9.0.0|AccountEnumerationSuspiciousActivity|Reconnaissance mithilfe von Kontoenumeration|5|start=2018-12-12T16:57:09.1706828Z app=Kerberos shost=W2012R2-000000-Server msg=Es wurde eine verdächtige Kontoenumerationsaktivität mithilfe des Kerberos-Protokolls (Ursprung W2012R2-000000-Server) beobachtet. Der Angreifer hat insgesamt 100 Versuche durchgeführt, Kontonamen zu erraten. Ein Versuch stimmte mit bestehenden Kontonamen in Active Directory überein. externalId=2003 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113de58ca1ec1250ca06d8

### <a name="reconnaissance-using-dns"></a>Reconnaissance über DNS
1 2018-12-12T16:57:20.743634+00:00 CENTER ATA 4688 DnsReconnaissanceSuspiciousActiv CEF:0|Microsoft|ATA|1.9.0.0|DnsReconnaissanceSuspiciousActivity|Reconnaissance über DNS|5|start=2018-12-12T16:57:20.2556472Z app=Dns shost=W2012R2-000000-Server msg=Eine verdächtige DNS-Aktivität (Ursprung: W2012R2 – kein DNS-Server) für W2012R2-000000-Server wurde beobachtet. externalId=2007 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113df08ca1ec1250ca074c

### <a name="reconnaissance-using-smb-session-enumeration"></a>Reconnaissance mithilfe der SMB-Sitzungsenumeration
12-12-2018  19:50:51    Auth.Warning    192.168.0.222   1 2018-12-12T17:50:51.090247+00:00 CENTER ATA 4688 EnumerateSessionsSuspiciousActiv ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|EnumerateSessionsSuspiciousActivity|Reconnaissance mithilfe der SMB-Sitzungsenumeration|5|start=2018-12-12T17:00:42.7234229Z app=SrvSvc shost=W2012R2-000000-Server msg=Fehlgeschlagene Versuche der SMB-Sitzungsenumeration von W2012R2-000000-Server für DC1. Es wurden keine Konten verfügbar gemacht. externalId=2012 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114a788ca1ec1250ca7735

### <a name="remote-execution-attempt-detected"></a>Erkannter Remoteausführungsversuch
12-12-2018  19:58:45    Auth.Warning    192.168.0.222   1 2018-12-12T17:58:45.082799+00:00 CENTER ATA 4688 RemoteExecutionSuspiciousActivit ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|RemoteExecutionSuspiciousActivity|Erkannter Remoteausführungsversuch|5|start=2018-12-12T17:54:23.9523766Z shost=W2012R2-000000-Server msg=Die folgenden Remoteausführungsversuche wurden auf DC1 von W2012R2-000000-Server durchgeführt:\r\nDie Remoteplanung ist für mindestens einen Task fehlgeschlagen. externalId=2019 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114c548ca1ec1250caf783

### <a name="unusual-protocol-implementation"></a>Ungewöhnliche Protokollimplementierung
1 2018-12-12T16:50:46.930234+00:00 CENTER ATA 4688 AbnormalProtocolSuspiciousActivi CEF:0|Microsoft|ATA|1.9.0.0|AbnormalProtocolSuspiciousActivity|Ungewöhnliche Protokollimplementierung|5|start=2018-12-12T16:48:46.6480337Z app=Ntlm shost=W2012R2-000000-Server outcome=Success msg=triservice hat sich von W2012R2-000000-Server mithilfe einer ungewöhnlichen Protokollimplementierung bei DC1 authentifiziert. Dies kann auf den Einsatz von schädlichen Tools zum Ausführen eines Pass-the-Hash- oder Brute-Force-Angriffs hinweisen. externalId=2002 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113c668ca1ec1250ca0397

### <a name="suspicion-of-identity-theft-based-on-abnormal-behavior"></a>Verdacht des Identitätsdiebstahls auf Grundlage von ungewöhnlichem Verhalten
1 2018-12-12T16:50:35.746877+00:00 CENTER ATA 4688 AbnormalBehaviorSuspiciousActivi CEF:0|Microsoft|ATA|1.9.0.0|AbnormalBehaviorSuspiciousActivity|Verdacht des Identitätsdiebstahls auf Grundlage von ungewöhnlichem Verhalten|5|start=2018-12-12T16:48:35.5501183Z app=Kerberos suser=USR45964 msg=USR45964 LAST45964 wies bei der Durchführung von Aktivitäten, die im letzten Monat nicht beobachtet wurden und auch nicht in Übereinstimmung mit den Aktivitäten anderer Konten im Unternehmen standen, ein ungewöhnliches Verhalten auf. Das ungewöhnliche Verhalten basiert auf den folgenden Aktivitäten:\r\nDurchführung der interaktiven Anmeldung von 30 ungewöhnlichen Arbeitsplätzen aus.\r\nAngeforderter Zugriff auf 30 ungewöhnliche Ressourcen. externalId=2001 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113c5b8ca1ec1250ca0355

### <a name="suspicious-authentication-failures"></a>Verdächtige Authentifizierungsfehler
12-12-2018  19:50:34    Auth.Warning    192.168.0.222   1 2018-12-12T17:04:25.214067+00:00 CENTER ATA 4688 BruteForceSuspiciousActivity ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|BruteForceSuspiciousActivity|Verdächtige Authentifizierungsfehler|5|start=2018-12-12T17:03:58.5892462Z app=Kerberos shost=W2012R2-000106-Server msg=Verdächtige Authentifizierungsfehler, die auf einen möglichen Brute-Force-Angriff hinweisen, wurden von W2012R2-000106-Server beobachtet. externalId=2023 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113f988ca1ec1250ca5810

### <a name="suspicious-service-creation"></a>Erstellen eines verdächtigen Diensts
12-12-2018  19:53:49    Auth.Warning    192.168.0.222   1 2018-12-12T17:53:49.913034+00:00 CENTER ATA 4688 MaliciousServiceCreationSuspicio ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|MaliciousServiceCreationSuspiciousActivity|Erstellen eines verdächtigen Diensts|5|start=2018-12-12T19:53:49.0000000Z app=ServiceInstalledEvent shost=W2012R2-000000-Server msg=triservice hat FakeService erstellt, um potenziell schädliche Befehle auf W2012R2-000000-Server auszuführen. externalId=2026 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114b2d8ca1ec1250caf577

## <a name="health-alerts"></a>Integritätswarnungen

### <a name="gatewaydisconnectedmonitoringalert"></a>GatewayDisconnectedMonitoringAlert
1 2018-12-12T16:52:41.520759+00:00 CENTER ATA 4688 GatewayDisconnectedMonitoringAle CEF:0|Microsoft|ATA|1.9.0.0|GatewayDisconnectedMonitoringAlert|GatewayDisconnectedMonitoringAlert|5|externalId=1011 cs1Label=url cs1=https\://192.168.0.220/monitoring msg=Es gab seit 5 Minuten keine Kommunikation vom Gateway CENTER. Letzte Kommunikation erfolgte am 12/12/2018 4:47:03 PM UTC.

### <a name="gatewaystartfailuremonitoringalert"></a>GatewayStartFailureMonitoringAlert
1 2018-12-12T15:36:59.701097+00:00 CENTER ATA 1372 GatewayStartFailureMonitoringAle CEF:0|Microsoft|ATA|1.9.0.0|GatewayStartFailureMonitoringAlert|GatewayStartFailureMonitoringAlert|5|externalId=1018 cs1Label=url cs1=https\://192.168.0.220/monitoring msg=Der Gatewaydienst auf DC1 konnte nicht gestartet werden. Letzte beobachtete Ausführung am 12/12/2018 3:04:12 PM UTC.

> [!NOTE]
> Alle Integritäts Warnungen werden mit der gleichen Vorlage wie oben gesendet.


## <a name="see-also"></a>Weitere Informationen
- [Voraussetzungen für ATA](ata-prerequisites.md)
- [ATA-Kapazitätsplanung](ata-capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-collection.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
