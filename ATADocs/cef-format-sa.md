---
title: Referenz zum ATA-SIEM-Protokoll | Microsoft-Dokumentation
description: Stellt Beispiele über Sicherheitswarnungsprotokolle bereit, die von ATA an SIEM gesendet werden.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 12/20/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 601b48ba-a327-4aff-a1f9-2377a2bb7a42
ms.reviewer: ort
ms.suite: ems
ms.openlocfilehash: fcab8aa33185b24f4ad1903c429b15decebf5e20
ms.sourcegitcommit: e844155ea57f73dfe2b47f4c5c1c7f5292ccbf1e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2020
ms.locfileid: "94690804"
---
# <a name="ata-siem-log-reference"></a>Referenz zum ATA-SIEM-Protokoll


[!INCLUDE [Banner for top of topics](includes/banner.md)]

ATA kann Sicherheits-und Integritäts Warn Ereignisse an Siem weiterleiten. Warnungen werden im CEF-Format weitergeleitet. Ein Beispiel zu jeder Art von Sicherheitswarnungsprotokoll, das an SIEM gesendet werden soll, finden Sie unten.

## <a name="sample-ata-security-alerts-in-cef-format"></a>Beispielsicherheitswarnungen von ATA im CEF-Format
Die folgenden Felder und deren Werte werden an Ihren SIEM-Agent weitergeleitet:

- start – Startzeit der Warnung
- suser – Konto (normalerweise das Benutzerkonto), das an der Warnung beteiligt ist
- shost – Quellcomputer der Warnung
- outcome – Warnungen mit definiertem Aktivitätserfolg oder Fehler, die in der Warnung ausgeführt wurden  
- msg – Beschreibung der Warnung
- cnt – Warnungen mit einer Anzahl der Zeiten, zu denen die Warnung erfolgt ist (z. B. Brute Force mit einer Anzahl geschätzter Kennwörter)
- app – Warnungsprotokoll
- externalId – Ereignis-ID, die ATA in das Ereignisprotokoll schreibt, das der Warnung entspricht*
- cs#label & cs# – Zeichenfolgen der Kunden, für die CEF zulässt, dass sie cs#label (Name des neuen Felds) und cs# (Wert) verwenden, z. B.: cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa

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
12-12-2018 19:52:18 auth. Warning 192.168.0.222 1 2018-12-12t17:52:18.899690 + 00:00 Center ATA 4688 ldapbruteforcesuspiciousactivity ‹ ~ ̈CEF: 0 | Microsoft | ATA | 1.9.0.0 | Ldapbruteforcesuspiciousactivity | Brute-Force-Angriff mithilfe von LDAP Simple BIND | 5 | Start = 2018-12-12t17:52:10.2350665 z app = LDAP msg = 10000 Kennwort-Raten bei 100-Konten von W2012R2-000000-Server. Ein Kontokennwort wurde erfolgreich geraten. externalId=2004 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114acb8ca1ec1250cacdcb

### <a name="encryption-downgrade-activity-golden-ticket"></a>Aktivität zur Herabstufung der Verschlüsselung (Golden Ticket)
12-12-2018 20:12:35 auth. Warning 192.168.0.222 1 2018-12-12t18:12:35.105942 + 00:00 Center ATA 4688 verschlüsselungsdowngrade verdächtiger ousact Microsoft | ATA | 1.9.0.0 | "Verschlüsselungsdowngradecoverdächtiger ousactivity" | Aktivität zur Herabstufung der Verschlüsselung | 5 | Start = 2018-12-12t18:10:35.0334169 z app = Kerberos msg = die Verschlüsselungsmethode des TGT-Felds TGS_REQ Nachricht von W2012R2-000000-Server wurde basierend auf dem zuvor gelernten Verhalten herabgestuft. Dies kann das Ergebnis eines auf W2012R2-000000-Server verwendeten Golden Ticket sein. externalId=2009 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114f938ca1ec1250cafcfa

### <a name="encryption-downgrade-activity-overpass-the-hash"></a>Aktivität zur Herabstufung der Verschlüsselung (Overpass-the-Hash)
12-12-2018 19:00:31 auth. Warning 192.168.0.222 1 2018-12-12t17:00:31.963485 + 00:00 Center ATA 4688 verschlüsselungsdowngrade verdächtiger ousact Microsoft | ATA | 1.9.0.0 | "Verschlüsselungsdowngradecoverdächtiger ousactivity" | Aktivität zur Herabstufung der Verschlüsselung | 5 | Start = 2018-12-12t17:00:31.2975188 z app = Kerberos msg = die Verschlüsselungsmethode des Encrypted_Timestamp Felds AS_REQ Meldung von W2012R2-000000-Server wurde basierend auf dem zuvor gelernten Verhalten herabgestuft. Grund dafür ist möglicherweise ein Diebstahl von Anmeldeinformationen bei einem Overpass-The-Hash-Angriff auf W2012R2-000000-Server. externalId=2010 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113eaf8ca1ec1250ca0883

###  <a name="encryption-downgrade-activity-skeleton-key"></a>Aktivität zur Herabstufung der Verschlüsselung (Skeleton Key)
12-12-2018 20:07:24 auth. Warning 192.168.0.222 1 2018-12-12t18:07:24.065140 + 00:00 Center ATA 4688 verschlüsselungsdowngradecoousact-̈CEF: 0 | Microsoft | ATA | 1.9.0.0 | "Verschlüsselungsdowngradecoverdächtiger ousactivity" | Aktivität zur Herabstufung der Verschlüsselung | 5 | Start = 2018-12-12t18:07:24.0222746 z app = Kerberos msg = die Verschlüsselungsmethode des ETYPE_INFO2 Felds KRB_ERR Meldung von W2012R2-000000-Server wurde basierend auf dem zuvor gelernten Verhalten herabgestuft. Grund dafür ist möglicherweise ein Skeleton Key auf DC1. externalId=2011 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114e5c8ca1ec1250cafafe

### <a name="honeytoken-activity"></a>Honeytoken-Aktivität
12-12-2018 19:51:52 auth. Warning 192.168.0.222 1 2018-12-12t17:51:52.659618 + 00:00 Center ATA 4688 honeytkenactivityverdächtiger ousacti. ~ ̈CEF: 0 | Microsoft | ATA | 1.9.0.0 | Honeytkenactivityverdächtiger ousactivity | Honeytoken-Aktivität | 5 | Start = 2018-12-12t17:51:52.5855994 z app = Kerberos suser = USR78982 msg = die folgenden Aktivitäten wurden von USR78982 LAST78982: \r\nauthenticated von CLIENT1 mithilfe von NTLM beim Zugriff auf domain1. Test. local\cifs auf DC1 ausgeführt. externalId=2014 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114ab88ca1ec1250ca7f76

### <a name="identity-theft-using-pass-the-hash-attack"></a>Identitätsdiebstahl mithilfe eines Pass-the-Hash-Angriffs
12-12-2018 19:56:02 auth. Error 192.168.0.222 1 2018-12-12t17:56:02.047236 + 00:00 Center ATA 4688 passthehashverdächtiger ousactivity. ~ ̈CEF: 0 | Microsoft | ATA | 1.9.0.0 | Passthehashverdächtiousactivity | Identitätsdiebstahl mithilfe eines Pass-the-Hash-Angriffs | 10 | Start = 2018-12-12t17:54:01.9582400 z app = NTLM suser = USR46829 LAST46829 msg = USR46829 LAST46829's Hash wurde von einem der Computer gestohlen, die zuvor von USR46829 LAST46829 angemeldet waren und von W2012R2-000000-Server verwendet wurden. externalId=2017 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114bb28ca1ec1250caf673

### <a name="identity-theft-using-pass-the-ticket-attack"></a>Identitätsdiebstahl mithilfe eines Pass-the-Ticket-Angriffs
12-12-2018 22:03:51 auth. Error 192.168.0.222 1 2018-12-12t20:03:51.643633 + 00:00 Center ATA 4688 passderticketargousactivity. ~ ̈CEF: 0 | Microsoft | ATA | 1.9.0.0 | Passderticketverdächtiousactivity | Identitätsdiebstahl mithilfe eines Pass-The-Ticket-Angriffs | 10 | Start = 2018-12-12t17:54:12.9960662 z app = Kerberos suser = Birder Lamm msg = die Kerberos-Tickets von Birder Lamm (Software Engineer) wurden von W2012R2-000106-Server an W2012R2-000051-Server gestohlen und für den Zugriff auf domain1 externalId=2018 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114b458ca1ec1250caf5b7

### <a name="kerberos-golden-ticket-activity"></a>Golden Ticket-Aktivität von Kerberos
12-12-2018 19:53:26 auth. Error 192.168.0.222 1 2018-12-12t17:53:26.869091 + 00:00 Center ATA 4688 goldenticketverdächtiger ousactivity ‹ ~ ̈CEF: 0 | Microsoft | ATA | 1.9.0.0 | Goldenticketverdächtiger ousactivity | Kerberos Golden Ticket-Aktivität | 10 | Start = 2018-12-13t06:51:26.7290524 z app = Kerberos suser = Sonja chadsey msg = verdächtige Verwendung des Kerberos-Tickets von Sonja chadsey (Software Engineer), das auf einen potenziellen Golden Ticket-Angriff hinweist, wurde erkannt. externalId=2022 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114b168ca1ec1250caf556

### <a name="malicious-data-protection-private-information-request"></a>Böswillige Anforderung privater Informationen im Rahmen der Datensicherheit
12-12-2018 20:03:49 auth. Error 192.168.0.222 1 2018-12-12t18:03:49.814620 + 00:00 Center ATA 4688 retrievedataschutzbackupkeys ~ ~ ̈CEF: 0 | Microsoft | ATA | 1.9.0.0 | Retrievedataschützbackupkeyverdächtiger ousactivity | Böswillige Datenschutzanforderungen für private Informationen | 10 | Start = 2018-12-12t17:58:56.3537533 z app = Lsarpc shost = W2012R2-000000-Server msg = ein unbekannter Benutzer hat einen erfolgreichen Versuch von W2012R2-000000-Server ausgeführt, um den DPAPI-Domänen Sicherungs Schlüssel von DC1 abzurufen. externalId=2020 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114d858ca1ec1250caf983

### <a name="malicious-replication-of-directory-services"></a>Böswillige Replikation von Verzeichnisdiensten
12-12-2018 19:56:49 auth. Error 192.168.0.222 1 2018-12-12t17:56:49.312648 + 00:00 Center ATA 4688 Director yservicesreplicationsusp. ~ ̈CEF: 0 | Microsoft | ATA | 1.9.0.0 | Directoriyservicesreplicationverdächtiger ousactivity | Böswillige Replikation von Verzeichnisdiensten | 10 | Start = 2018-12-12t17:52:34.3287329 z app = drsr shost = W2012R2-000000-Server msg = böswillige Replikations Anforderungen wurden erfolgreich von W2012R2-000000-Server gegen DC1 ausgeführt. outcome=Success externalId=2006 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114be18ca1ec1250caf6b8

### <a name="privilege-escalation-using-forged-authorization-data"></a>Berechtigungsausweitung mithilfe von gefälschten Autorisierungsdaten
12-12-2018 19:51:15 auth. Error 192.168.0.222 1 2018-12-12t17:51:15.658608 + 00:00 Center ATA 4688 forgedpacverdächtiger ousactivity. ~ ̈CEF: 0 | Microsoft | ATA | 1.9.0.0 | Forgedpacverdächtiger ousactivity | Berechtigungs Ausweitung mithilfe gefälschter Autorisierungs Daten | 10 | Start = 2018-12-12t17:51:15.0261128 z app = Kerberos suser = TestService msg = "TestService" hat versucht, mithilfe gefälschter Autorisierungs Daten Berechtigungen für DC1 von W2012R2-000000-Server auszuweiten. externalId=2013 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114a938ca1ec1250ca7f48

### <a name="reconnaissance-using-directory-services-queries"></a>Reconnaissance mithilfe von Verzeichnisdienstabfragen
12-12-2018 20:23:52 auth. Warning 192.168.0.222 1 2018-12-12t18:23:52.155531 + 00:00 Center ATA 4688 samrreconnaissancesuspiciousacti ‹ ~ ̈CEF: 0 | Microsoft | ATA | 1.9.0.0 | Samrreconnaissancesuspiciousactivity | Reconnaissance mithilfe von Verzeichnisdienst Abfragen | 5 | Start = 2018-12-12t18:04:12.9868815 z app = SAMR shost = W2012R2-000000-Server msg = die folgenden Verzeichnisdienst Abfragen mithilfe des SAMR-Protokolls wurden für DC1 von W2012R2-000000-Server versucht: \ r\nerfolgreiche Abfrage über eingehende Gesamtstruktur-Vertrauensstellungs-Generatoren (Mitglieder dieser Gruppe können eingehende, unidirektionale Vertrauens Stellungen für diese Gesamtstruktur erstellen) in domain1. Test. local externalId = 2021 cs1Label = URL CS1 = HTTPS \: //192.168.0.220/suspiciousActivity/5c114e758ca1ec1250cafb2e

### <a name="reconnaissance-using-account-enumeration"></a>Reconnaissance mithilfe von Kontoenumeration
1 2018-12-12T16:57:09.661680+00:00 CENTER ATA 4688 AccountEnumerationSuspiciousActi CEF:0|Microsoft|ATA|1.9.0.0|AccountEnumerationSuspiciousActivity|Reconnaissance mithilfe von Kontoenumeration|5|start=2018-12-12T16:57:09.1706828Z app=Kerberos shost=W2012R2-000000-Server msg=Es wurde eine verdächtige Kontoenumerationsaktivität mithilfe des Kerberos-Protokolls (Ursprung W2012R2-000000-Server) beobachtet. Der Angreifer hat insgesamt 100 Versuche durchgeführt, Kontonamen zu erraten. Ein Versuch stimmte mit bestehenden Kontonamen in Active Directory überein. externalId=2003 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113de58ca1ec1250ca06d8

### <a name="reconnaissance-using-dns"></a>Reconnaissance über DNS
1 2018-12-12T16:57:20.743634+00:00 CENTER ATA 4688 DnsReconnaissanceSuspiciousActiv CEF:0|Microsoft|ATA|1.9.0.0|DnsReconnaissanceSuspiciousActivity|Reconnaissance über DNS|5|start=2018-12-12T16:57:20.2556472Z app=Dns shost=W2012R2-000000-Server msg=Eine verdächtige DNS-Aktivität (Ursprung: W2012R2 – kein DNS-Server) für W2012R2-000000-Server wurde beobachtet. externalId=2007 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113df08ca1ec1250ca074c

### <a name="reconnaissance-using-smb-session-enumeration"></a>Reconnaissance mithilfe der SMB-Sitzungsenumeration
12-12-2018 19:50:51 auth. Warning 192.168.0.222 1 2018-12-12t17:50:51.090247 + 00:00 Center ATA 4688 enumeratesessionssuspiciousactiv ‹ ~ ̈CEF: 0 | Microsoft | ATA | 1.9.0.0 | Enumeratesessionssuspiciousactivity | Reconnaissance mithilfe der SMB-sitzungsenumeration | 5 | Start = 2018-12-12t17:00:42.7234229 z app = srvsvc shost = W2012R2-000000-Server msg = SMB-sitzungsenumerationsversuche von W2012R2-000000-Server für DC1 fehlgeschlagen. Es wurden keine Konten verfügbar gemacht. externalId=2012 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114a788ca1ec1250ca7735

### <a name="remote-execution-attempt-detected"></a>Erkannter Remoteausführungsversuch
12-12-2018 19:58:45 auth. Warning 192.168.0.222 1 2018-12-12t17:58:45.082799 + 00:00 Center ATA 4688 remoteexecutionverdächtiger ousactivit ~ ~ ̈CEF: 0 | Microsoft | ATA | 1.9.0.0 | Remoteexecutionverdächtiger ousactivity | Versuch der Remote Ausführung erkannt | 5 | Start = 2018-12-12t17:54:23.9523766 z shost = W2012R2-000000-Server msg = die folgenden Remote Ausführungs Versuche wurden auf DC1 von W2012R2-000000-Server: \ r\nfehler bei der Remote Planung von mindestens einer Aufgabe ausgeführt. externalId=2019 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114c548ca1ec1250caf783

### <a name="unusual-protocol-implementation"></a>Ungewöhnliche Protokollimplementierung
1 2018-12-12T16:50:46.930234+00:00 CENTER ATA 4688 AbnormalProtocolSuspiciousActivi CEF:0|Microsoft|ATA|1.9.0.0|AbnormalProtocolSuspiciousActivity|Ungewöhnliche Protokollimplementierung|5|start=2018-12-12T16:48:46.6480337Z app=Ntlm shost=W2012R2-000000-Server outcome=Success msg=triservice hat sich von W2012R2-000000-Server mithilfe einer ungewöhnlichen Protokollimplementierung bei DC1 authentifiziert. Dies kann auf den Einsatz von schädlichen Tools zum Ausführen eines Pass-the-Hash- oder Brute-Force-Angriffs hinweisen. externalId=2002 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113c668ca1ec1250ca0397

### <a name="suspicion-of-identity-theft-based-on-abnormal-behavior"></a>Verdacht des Identitätsdiebstahls auf Grundlage von ungewöhnlichem Verhalten
1 2018-12-12T16:50:35.746877+00:00 CENTER ATA 4688 AbnormalBehaviorSuspiciousActivi CEF:0|Microsoft|ATA|1.9.0.0|AbnormalBehaviorSuspiciousActivity|Verdacht des Identitätsdiebstahls auf Grundlage von ungewöhnlichem Verhalten|5|start=2018-12-12T16:48:35.5501183Z app=Kerberos suser=USR45964 msg=USR45964 LAST45964 wies bei der Durchführung von Aktivitäten, die im letzten Monat nicht beobachtet wurden und auch nicht in Übereinstimmung mit den Aktivitäten anderer Konten im Unternehmen standen, ein ungewöhnliches Verhalten auf. Das ungewöhnliche Verhalten basiert auf den folgenden Aktivitäten:\r\nDurchführung der interaktiven Anmeldung von 30 ungewöhnlichen Arbeitsplätzen aus.\r\nAngeforderter Zugriff auf 30 ungewöhnliche Ressourcen. externalId=2001 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113c5b8ca1ec1250ca0355

### <a name="suspicious-authentication-failures"></a>Verdächtige Authentifizierungsfehler
12-12-2018 19:50:34 auth. Warning 192.168.0.222 1 2018-12-12t17:04:25.214067 + 00:00 Center ATA 4688 bruteforcesuspiciousactivity ‹ ~ ̈CEF: 0 | Microsoft | ATA | 1.9.0.0 | Bruteforcesuspiciousactivity | Verdächtige Authentifizierungsfehler | 5 | Start = 2018-12-12t17:03:58.5892462 z app = Kerberos shost = W2012R2-000106-Server msg = verdächtige Authentifizierungsfehler. Dies deutet darauf hin, dass ein potenzieller Brute-Force-Angriff von W2012R2-000106-Server erkannt wurde. externalId=2023 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113f988ca1ec1250ca5810

### <a name="suspicious-service-creation"></a>Erstellen eines verdächtigen Diensts
12-12-2018 19:53:49 auth. Warning 192.168.0.222 1 2018-12-12t17:53:49.913034 + 00:00 Center ATA 4688 maliciousservicecreationverdächticio ‹ ~ ̈CEF: 0 | Microsoft | ATA | 1.9.0.0 | Maliciousservicecreationverdächtiger ousactivity | Verdächtige Dienst Erstellung | 5 | Start = 2018-12-12t19:53:49.0000000 z app = serviceinstalledevent shost = W2012R2-000000-Server msg = der Dienst hat fakeservice erstellt, um potenziell schädliche Befehle auf W2012R2-000000-Server auszuführen. externalId=2026 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114b2d8ca1ec1250caf577

## <a name="health-alerts"></a>Integritätswarnungen

### <a name="gatewaydisconnectedmonitoringalert"></a>GatewayDisconnectedMonitoringAlert
1 2018-12-12T16:52:41.520759+00:00 CENTER ATA 4688 GatewayDisconnectedMonitoringAle CEF:0|Microsoft|ATA|1.9.0.0|GatewayDisconnectedMonitoringAlert|GatewayDisconnectedMonitoringAlert|5|externalId=1011 cs1Label=url cs1=https\://192.168.0.220/monitoring msg=Es gab seit 5 Minuten keine Kommunikation vom Gateway CENTER. Letzte Kommunikation erfolgte am 12/12/2018 4:47:03 PM UTC.

### <a name="gatewaystartfailuremonitoringalert"></a>GatewayStartFailureMonitoringAlert
1 2018-12-12T15:36:59.701097+00:00 CENTER ATA 1372 GatewayStartFailureMonitoringAle CEF:0|Microsoft|ATA|1.9.0.0|GatewayStartFailureMonitoringAlert|GatewayStartFailureMonitoringAlert|5|externalId=1018 cs1Label=url cs1=https\://192.168.0.220/monitoring msg=Der Gatewaydienst auf DC1 konnte nicht gestartet werden. Letzte beobachtete Ausführung am 12/12/2018 3:04:12 PM UTC.

> [!NOTE]
> Alle Integritäts Warnungen werden mit der gleichen Vorlage wie oben gesendet.


## <a name="see-also"></a>Weitere Informationen
- [ATA-Voraussetzungen](ata-prerequisites.md)
- [ATA-Kapazitätsplanung](ata-capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-collection.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
