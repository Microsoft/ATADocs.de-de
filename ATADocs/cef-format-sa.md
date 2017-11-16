---
title: Referenz zum ATA-SIEM-Protokoll | Microsoft-Dokumentation
description: "Stellt Beispiele über verdächtige Aktivitätsprotokolle bereit, die von ATA an SIEM gesendet werden."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 601b48ba-a327-4aff-a1f9-2377a2bb7a42
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: d9e226f06c407cb16a3486f81658e05433b00fb1
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/07/2017
---
*Gilt für: Advanced Threat Analytics Version 1.8*


# <a name="ata-siem-log-reference"></a>Referenz zum ATA-SIEM-Protokoll

ATA kann verdächtige Aktivitäten und die Überwachung von Warnereignissen und Ihrem SIEM-Agent weiterleiten. Verdächtige Aktivitätsereignisse haben das CEF-Format. Dieser Verweisartikel bietet Beispiele verdächtiger Aktivitätsprotokolle, die an Ihren SIEM-Agent gesendet wurden.

## <a name="sample-ata-suspicious-activities-in-cef-format"></a>Beispiel verdächtiger ATA-Aktivitäten im CEF-Format
Die folgenden Felder und deren Werte werden an Ihren SIEM-Agent weitergeleitet:

-   start : die Startzeit der Warnung
-   suser: das Konto (normalerweise das Benutzerkonto), das in dieser Warnung mit einbezogen ist
-   shost: der Quellcomputer für diese Warnung
-   outcome: für Warnungen; die in der Warnung ausgeführte Aktivität ist erfolgreich/schlägt fehl  
-   msg: die Beschreibung für die Warnung
-   cnt: für Warnungen, die die Zeiten angeben, wann die Warnung aufgetreten ist (z.B. Brute Force mit einer Anzahl geschätzter Kennwörter)
-   app: das in dieser Warnung verwendete Protokoll
-   externalId: die Ereignis-ID, die ATA in das Ereignisprotokoll schreibt, das dieser Warnung entspricht
-   cs#label & cs#: die Zeichenfolgen der Kunden, für die CEF zulässt, dass sie cs#label (Name des neuen Felds) und cs# (Wert) verwenden, z.B.: cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa

In diesem Beispiel ist cs1 ein Feld, das über eine URL für die Warnung verfügt.

## <a name="sample-logs"></a>Beispielprotokolle

Prioritäten: 3 = niedrig, 5 = mittel 10 = hoch

### <a name="bruteforce--ldap"></a>BruteForce – LDAP
05-03-2017          13:35:01               Auth.Warning    192.168.0.220     Mai  3 10:35:01 CENTER ATA:CEF:0|Microsoft|ATA|.5942.64854|BruteForceSuspiciousActivity|Brute-Force-Angriff mithilfe einer einfachen LDAP-Bindung|5|start=2017-05-03T10:34:57.2785534Z app=Ldap suser=Darris Woods shost=CLIENT1 msg=Brute-Force-Angriffsversuch mithilfe des LDAP-Protokolls auf Darris Woods (Softwareingenieur) von CLIENT1 (76 geschätzte Versuche). cnt=76 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909b2458ca1ec04d05e6a70

05-03-2017          13:35:05               Auth.Warning    192.168.0.220     Mai  3 10:35:05 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|BruteForceSuspiciousActivity|Brute-Force-Angriff mithilfe einer einfachen LDAP-Bindung|5|start=2017-05-03T10:34:58.7004159Z app=Ldap suser=Dino Hopkins shost=CLIENT1 msg=Brute-Force-Angriffsversuch mithilfe des LDAP-Protokolls auf Dino Hopkins (Softwareingenieur) von CLIENT1 (3 geschätzte Versuche). cnt=3 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909b2458ca1ec04d05e6a70

05-03-2017          13:35:05               Auth.Warning    192.168.0.220     Mai  3 10:35:05 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|BruteForceSuspiciousActivity|Brute-Force-Angriff mithilfe einer einfachen LDAP-Bindung|5|start=2017-05-03T10:34:59.7269332Z app=Ldap suser=Dino Hopkins shost=CLIENT1 msg=Erfolgreicher Brute-Force-Angriffsversuch mithilfe des LDAP-Protokolls auf Dino Hopkins (Softwareingenieur) von CLIENT1 (77 geschätzte Versuche). cnt=77 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909b2458ca1ec04d05e6a70
### <a name="bruteforce"></a>BruteForce
05-14-2017          13:27:05               Auth.Warning    192.168.0.220     1 2017-05- ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|BruteForceSuspiciousActivity|Verdächtige Authentifizierungsfehler|5|start=2017-05-14T10:27:04.3904739Z app=Kerberos shost=CLIENT1 msg= 	[Pre-Approved] 	Verdächtige Authentifizierungsfehler weisen darauf hin, dass ein potenzieller Brute-Force-Angriff von CLIENT1 aus erkannt wurde. externalId=2023 cs1Label=url cs1=https://center/suspiciousActivity/591830f98ca1ec11d0c0d7f5
### <a name="privilege-escalation"></a>Ausweitung von Berechtigungen
#### <a name="silver"></a>Silver
05-10-2017          17:14:15               Auth.Error           192.168.0.220     1 2017-05-10T14:14:15.589415+00:00 CENTER ATA 596 ForgedPacSuspiciousActivity ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|ForgedPacSuspiciousActivity|Berechtigungsausweitung mithilfe gefälschter Autorisierungsdaten|10|start=2017-05-10T14:11:51.8053059Z app=Kerberos suser=user1 msg=user1 hat von CLIENT2 aus versucht, mithilfe von gefälschten Autorisierungsdaten Berechtigungen auf HOST/client1 auszuweiten. externalId=2013 cs1Label=url cs1=https://center/suspiciousActivity/591320378ca1ec02543e4747
#### <a name="gold"></a>Gold
05-10-2017          17:13:30               Auth.Error           192.168.0.220     1 2017-05-10T14:13:30.244377+00:00 CENTER ATA 596 ForgedPacSuspiciousActivity ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|ForgedPacSuspiciousActivity|Berechtigungsausweitung mithilfe gefälschter Autorisierungsdaten|10|start=2017-05-10T14:11:27.6455273Z app=Kerberos suser=user1 msg=user1 hat von CLIENT1 aus versucht, mithilfe von gefälschten Autorisierungsdaten Berechtigungen für DC4 auszuweiten. externalId=2013 cs1Label=url cs1=https://center/suspiciousActivity/5913200a8ca1ec02543e3ea8
### <a name="golden-ticket"></a>Golden Ticket
05-14-2017          15:57:10               Auth.Warning    192.168.0.220     1 2017-05-14T12:57:10.392730+00:00 CENTER ATA 4732 EncryptionDowngradeSuspiciousAct ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|EncryptionDowngradeSuspiciousActivity|Encryption downgrade activity|5|start=2017-05-14T12:55:08.6913033Z app=Kerberos msg=Die Verschlüsselungsmethode für das Feld TGT der TGS_REQ-Nachricht auf CLIENT1 wurde auf Grundlage des zuvor gelernten Verhaltens heruntergestuft. Dies kann das Ergebnis eines auf CLIENT1 verwendeten Golden Ticket sein. externalId=2009 cs1Label=url cs1=https://center/suspiciousActivity/591854268ca1ec127ceec396
### <a name="honey-token-activity"></a>Honeytokenaktivität
05-11-2017          16:49:10               Auth.Warning    192.168.0.220     1 2017-05-11T13:49:10.725605+00:00 CENTER ATA 876 HoneytokenActivitySuspiciousActi ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|HoneytokenActivitySuspiciousActivity|Honeytokenaktivität|5|start=2017-05-11T13:49:09.6455794Z app=Kerberos suser=privtriservice msg=Folgende Aktivitäten wurden von privtriservice ausgeführt: Von \r\nAuthenticated von DC1 aus wurde über DC1 eine Authentifizierung mithilfe von NTLM bei einer Unternehmensressource durchgeführt. externalId=2014 cs1Label=url cs1=https://center/suspiciousActivity/59146bd68ca1ec036ce57d29
### <a name="suspicious-replication-of-directory-services"></a>Verdächtige Replikation von Verzeichnisdiensten
May  3 11:02:28 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|DirectoryServicesReplicationSuspiciousActivity|Böswillige Replikation von Verzeichnisdiensten|10|start=2017-05-03T11:00:13.6560919Z suser=user1 shost=CLIENT1 outcome=Failure msg= Von user1 von CLIENT1 aus wurde versucht, böswillige Replikationsanforderungen für DC1 auszuführen. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909b8c48ca1ec04d05ed28d
### <a name="malicious-data-protection-private-information-request"></a>Böswillige Anforderung privater Informationen im Rahmen der Datensicherheit
May  3 13:39:18 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|RetrieveDataProtectionBackupKeySuspiciousActivity|Böswillige Anforderung privater Informationen im Rahmen der Datensicherheit|10|start=2017-05-03T13:37:06.4039886Z app=LsaRpc shost=CLIENT1 suser= outcome=Success msg=Ein unbekannter Benutzer hat von CLIENT1 aus 4 erfolglose Versuche ausgeführt, einen DPAPI-Domänensicherungsschlüssel von DC1 abzurufen. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909dd868ca1ec04d05fb01d
### <a name="massive-object-deletion"></a>Umfangreiche Objektlöschungen
05-14-2017          14:38:34               Auth.Warning    192.168.0.220     1 2017-05-14T11:38:34.898810+00:00 CENTER ATA 3748 MassiveObjectDeletionSuspiciousA ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|MassiveObjectDeletionSuspiciousActivity|Umfangreiche Objektlöschungen|5|start=2017-05-14T11:33:32.0000000Z msg=496 Objekte (9,75 % der Gesamtzahl der AD-Objekte) wurden in einem Zeitraum von keiner Zeitdimension aus der Domäne domain1.test.local gelöscht. cnt=496 externalId=2016 cs1Label=url cs1=https://center/suspiciousActivity/591841ba8ca1ec0ea4ad587a
### <a name="over-pass-the-hash"></a>Over-pass-the-hash
05-14-2017          12:07:46               Auth.Warning    192.168.0.220     1 2017-05-14T09:07:46.652319+00:00 CENTER ATA 1116 EncryptionDowngradeSuspiciousAct ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|EncryptionDowngradeSuspiciousActivity|Encryption downgrade activity|5|start=2017-05-14T09:07:44.9933773Z app=Kerberos msg=Die Verschlüsselungsmethode für das Feld Encrypted_Timestamp der AS_REQ-Nachricht auf CLIENT1 wurde auf Grundlage des zuvor gelernten Verhaltens heruntergestuft. Grund dafür ist möglicherweise ein Diebstahl von Anmeldeinformationen bei einem Overpass-The-Hash-Angriff auf CLIENT1. externalId=2010 cs1Label=url cs1=https://center/suspiciousActivity/59181e628ca1ec045cdfa929
### <a name="pass-the-hash"></a>Pass-the-hash
05-10-2017          17:48:51               Auth.Error           192.168.0.220     1 2017-05-10T14:48:51.998620+00:00 CENTER ATA 596 PassTheHashSuspiciousActivity ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|PassTheHashSuspiciousActivity|Identitätsdiebstahl mithilfe eines Pass-the-Hash-Angriffs|10|start=2017-05-10T14:46:50.9463800Z app=Ntlm suser=user2 msg=Der Hash von user2 wurde aus einem der Computer gestohlen, die zuvor unter user2 angemeldet waren, und von CLIENT1 aus verwendet. externalId=2017 cs1Label=url cs1=https://center/suspiciousActivity/591328538ca1ec02543f9a1a
### <a name="account-enumeration"></a>Kontoenumeration
05-10-2017          16:44:22               Auth.Warning    192.168.0.220     1 2017-05-10T13:44:22.706381+00:00 CENTER ATA 596 AccountEnumerationSuspiciousActi ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|AccountEnumerationSuspiciousActivity|Reconnaissance mithilfe von Kontoenumeration|5|start=2017-05-10T13:44:20.9930644Z app=Kerberos shost=CLIENT3 msg=Eine verdächtige Kontoenumerationsaktivität mithilfe des Kerberos-Protokolls (Ursprung: CLIENT3) wurde beobachtet. Der Angreifer hat insgesamt 72 geschätzte Versuche für Kontonamen ausgeführt. 2 geschätzte Versuche ergaben eine Übereinstimmung mit vorhandenen Namen in Active Directory. externalId=2003 cs1Label=url cs1=https://center/suspiciousActivity/591319368ca1ec02543c56ee
### <a name="dns-recon"></a>DNS-Reconnaissance
05-03-2017          13:16:57               Auth.Warning    192.168.0.220     May  3 10:16:57 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|DnsReconnaissanceSuspiciousActivity|Reconnaissance mithilfe DNS|5|start=2017-05-03T10:16:41.8297467Z app=Dns shost=CLIENT1 msg=Eine verdächtige DNS-Aktivität (Ursprung: CLIENT1 - kein DNS-Server) für DC1 wurde beobachtet. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa 05-03-2017          13:24:21               Auth.Warning    192.168.0.220     May  3 10:24:21 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|DnsReconnaissanceSuspiciousActivity|Reconnaissance mithilfe DNS|5|start=2017-05-03T10:24:08.0950753Z app=Dns shost=CLIENT1 request=contoso.com requestMethod=Axfr reason=NameError outcome=Failure msg=Eine verdächtige DNS-Aktivität (Ursprung: CLIENT1- kein DNS-Server) wurde beobachtet. Die Abfrage erfolgte für contoso.com (Typ Axfr). Die Antwort war NameError. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa
### <a name="smb-session-enumeration"></a>SMB-Sitzungsauflistung
May  3 11:55:43 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|EnumerateSessionsSuspiciousActivity|Reconnaissance mithilfe von SMB-Sitzungsauflistung|5|start=2017-05-03T11:52:02.4360718Z app=SrvSvc shost=CLIENT1 msg=Es wurde von "CLIENT1" aus erfolgreich versucht, eine SMB-Sitzungsauflistung auf "DC1" durchzuführen. user1 (daf::1) wurde offengelegt. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909c53f8ca1ec04d05f1cf1
### <a name="samr-enumeration"></a>SAMR-Enumeration
May  3 11:44:48 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|SamrReconnaissanceSuspiciousActivity|Reconnaissance mithilfe von Verzeichnisdienstenumeration|5|start=2017-05-03T11:42:46.5911225Z app=Samr shost=CLIENT1 suser=user1 outcome=Success msg=Von CLIENT1 aus wurde versucht, für DC1 die folgenden Verzeichnisdienstenumerationen mithilfe des SAMR-Protokolls durchzuführen:\r\nErfolgreiche Enumeration aller Gruppen in domain1.test.local durch user1 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909c2b08ca1ec04d05f0e19
### <a name="remote-execution"></a>Remoteausführung
May  3 12:36:47 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|RemoteExecutionSuspiciousActivity|Versuch der Remoteausführung erkannt|3|start=2017-05-03T12:34:32.3714348Z app=ServiceControl shost=CLIENT1 suser=Administrator outcome=Success msg=Die folgenden Versuche zur Remoteausführung wurden von CLIENT1 auf DC1 durchgeführt:\r\nErfolgreiche Remoteerstellung von PSEXESVC durch Administrator. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909cedf8ca1ec04d05f5692
### <a name="skeleton-key"></a>Skeleton Key
05-14-2017          12:13:12               Auth.Warning    192.168.0.220     1 2017-05-14T09:13:12.102468+00:00 CENTER ATA 1116 EncryptionDowngradeSuspiciousAct ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|EncryptionDowngradeSuspiciousActivity|Encryption downgrade activity|5|start=2017-05-14T09:13:03.3509467Z app=Kerberos msg=Die Verschlüsselungsmethode für das Feld ETYPE_INFO2 der KRB_ERR-Nachricht auf CLIENT2 wurde auf Grundlage des zuvor gelernten Verhaltens heruntergestuft. Grund dafür ist möglicherweise ein Skeleton Key auf DC3. externalId=2011 cs1Label=url cs1=https://center/suspiciousActivity/59181fa88ca1ec045cdfe630
### <a name="unusual-protocol-implementation"></a>Ungewöhnliche Protokollimplementierung
May  3 12:28:19 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|AbnormalProtocolSuspiciousActivity|Ungewöhnliche Protokollimplementierung|5|start=2017-05-03T12:28:05.3561302Z app=Ntlm shost=CLIENT1 suser=Administratorergebnis=Success msg=Der Administrator hat sich von CLIENT1 mithilfe einer ungewöhnlichen Protokollimplementierung bei DC1 authentifiziert. Dies kann auf den Einsatz von schädlichen Tools zum Ausführen eines Pass-the-Hash- oder Brute-Force-Angriffs hinweisen. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909cce38ca1ec04d05f4ab4
### <a name="sensitive-account-credentials-exposed"></a>Sensible Anmeldeinformationen wurden offengelegt
May  3 13:23:18 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|LdapSimpleBindCleartextPasswordSuspiciousActivity|Sensible Anmeldeinformationen wurden offengelegt|3|start=2017-05-03T13:23:09.7798589Z app=Ldap shost=CLIENT1 suser=Administrator msg=Die Anmeldeinformationen des Administrators wurden als Klartext mithilfe einfacher LDAP-Bindung von CLIENT1 offengelegt. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909d9c68ca1ec04d05f9918
### <a name="services-exposing-account-credentials"></a>Dienste, die Kontoanmeldeinformationen offenlegen
May  3 13:34:23 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|LdapSimpleBindCleartextPasswordSuspiciousActivity|Dienste, die Kontoanmeldeinformationen offenlegen|3|start=2017-05-03T13:28:36.5159194Z app=Ldap shost=daf::220 msg=Auf daf::220 (daf::220) ausgeführte Dienste legen Kontoanmeldeinformationen in Klartext mithilfe einfacher LDAP-Bindung offen. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909dc5f8ca1ec04d05fa8b1
### <a name="pass-the-ticket"></a>Pass-the-Ticket
May  4 13:15:41 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|PassTheTicketSuspiciousActivity|Identitätsdiebstahl mithilfe eines Pass-the-Ticket-Angriffs|10|start=2017-05-04T13:13:44.5160000Z app=Kerberos shost=CLIENT1 suser=Administrator request=krbtgt/DOMAIN1.TEST.LOCAL msg=Die Kerberos-Tickets des Administrators wurden zwischen CLIENT2 und CLIENT1 gestohlen und für den Zugriff auf krbtgt/DOMAIN1.TEST.LOCAL verwendet. cs2Label=ticketSourceComputer cs2=CLIENT2 cs3Label=ticketSourceComputerIpAddress cs3= cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/590b29168ca1ec0ba438acf6

## <a name="see-also"></a>Weitere Informationen
- [Voraussetzungen für ATA](ata-prerequisites.md)
- [ATA-Kapazitätsplanung](ata-capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-collection.md#configuring-windows-event-forwarding)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
