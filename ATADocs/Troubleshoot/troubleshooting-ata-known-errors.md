---
title: Behandeln von Problemen im ATA-Fehlerprotokoll | Microsoft Advanced Threat Analytics
description: "Beschreibt, wie Sie übliche Fehler in ATA beheben können"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: 351541d28e0f30a33d76990f2ac00a4d506f5450


---

# Behandeln von Problemen im ATA-Fehlerprotokoll
In diesem Abschnitt sind mögliche Fehler, die es in den Bereitstellungen von ATA geben kann, und die Schritte zu deren Behebung aufgeführt.
## ATA-Gateway-Fehler
|Fehler|Beschreibung|Lösung|
|-------------|----------|---------|
|System.DirectoryServices.Protocols.LdapException: Lokaler Fehler.|Die ATA-Gateway konnte sich nicht beim Domänencontroller authentifizieren.|1. Vergewissern Sie sich, dass der DNS-Eintrag des Domänencontrollers im DNS-Server ordnungsgemäß konfiguriert ist. <br>2. Vergewissern Sie sich, dass die Zeit des ATA-Gateways mit der Zeit des Domänencontrollers synchronisiert ist.|
|System.IdentityModel.Tokens.SecurityTokenValidationException: Die Zertifikatkette kann nicht überprüft werden.|Das ATA-Gateway konnte das Zertifikat von ATA Center nicht überprüfen.|1. Vergewissern Sie sich, dass das Zertifikat der Stammzertifizierungsstelle im Zertifikatspeicher für vertrauenswürdige Zertifikate auf dem ATA-Gateway installiert ist. <br>2. Überprüfen Sie, ob die Zertifikatsperrliste (Certificate Revocation List, CRL) verfügbar ist und ob die Überprüfung auf Zertifikatssperrung ausgeführt werden kann.|
|Microsoft.Common.ExtendedException: Erstellungszeit konnte nicht analysiert werden.|Das ATA-Gateway konnte Syslog-Meldungen, die vom SIEM weitergeleitet wurden, nicht analysieren.|Stellen Sie sicher, dass das SIEM so konfiguriert ist, dass es die Meldungen in einem der Formate weiterleitet, die von ATA unterstützt werden.|
|System.ServiceModel.FaultException: Fehler beim Überprüfen der Sicherheit für die Nachricht.|Die ATA-Gateway konnte sich nicht bei ATA Center authentifizieren.|Vergewissern Sie sich, dass die Zeit des ATA-Gateways mit der Zeit von ATA-Center synchronisiert ist.|
|System.ServiceModel.EndpointNotFoundException: Es konnte keine Verbindung mit net.tcp://center.ip.addr:443/IEntityReceiver hergestellt werden.|Das ATA-Gateway konnte keine Verbindung mit ATA Center herstellen.|Vergewissern Sie sich, dass die Netzwerkeinstellungen richtig sind und dass die Verbindung zwischen dem ATA-Gateway und ATA Center aktiv ist.|
|System.DirectoryServices.Protocols.LdapException: Der LDAP-Server ist nicht verfügbar.|Das ATA-Gateway konnte den Domänencontroller nicht über das LDAP-Protokoll abfragen.|1. Vergewissern Sie sich, dass das Benutzerkonto, das von ATA zum Herstellen einer Verbindung mit der Active Directory-Domäne verwendet wird, vollen Lesezugriff auf alle Objekte in der Active Directory-Struktur hat. <br>2. Stellen Sie sicher, dass der Domänencontroller nicht so eingestellt ist, dass er LDAP-Abfragen von dem Benutzerkonto ablehnt, das von ATA verwendet wird.|
|Microsoft.Tri.Infrastructure.ContractException: Vertragsausnahme|Die ATA-Gateway konnte die Konfiguration von ATA Center nicht synchronisieren.|Schließen Sie die Konfiguration des ATA-Gateways in der ATA-Konsole ab.|
|System.Reflection.ReflectionTypeLoadException: Mindestens ein angeforderter Typ kann nicht geladen werden. Weitere Informationen erhalten Sie durch Abrufen der LoaderExceptions-Eigenschaft.|Auf dem ATA-Gateway ist die Nachrichtenanalyse installiert.| Deinstallieren Sie die Nachrichtenanalyse.|
|Fehler [Layout] System.OutOfMemoryException: Ausnahme vom Typ „System.OutOfMemoryException“ ausgelöst.|Auf dem ATA-Gateway ist nicht genügend Arbeitsspeicher verfügbar.|Erhöhen Sie die Arbeitsspeicherkapazität auf dem Domänencontroller.|
|Fehler beim Start von Live-Consumer  ---> Microsoft.Opn.Runtime.Monitoring.MessageSessionException: Der PEFNDIS-Ereignisanbieter ist nicht bereit.|PEF (Nachrichtenanalyse) wurde nicht ordnungsgemäß installiert.|Wenden Sie sich für eine Problemumgehung an den Support.|
|Installationsfehler: 0x80070652|Auf Ihrem Computer stehen weitere Installationen aus.|Warten Sie, bis die anderen Installationen abgeschlossen sind, und starten Sie den Computer gegebenenfalls neu.|

## Fehler der ATA-Konsole
|Fehler|Beschreibung|Lösung|
|-------------|----------|---------|
|HTTP-Fehler 500.19 – Interner Serverfehler|Das IIS URL Rewrite-Modul konnte nicht ordnungsgemäß installiert werden.|Deinstallieren Sie das IIS URL Rewrite-Modul, und installieren Sie es dann erneut.<br>[Laden Sie das IIS URL Rewrite-Modul herunter.](http://go.microsoft.com/fwlink/?LinkID=615137)|

## Bereitstellungsfehler
|Fehler|Beschreibung|Lösung|
|-------------|----------|---------|
|Fehler bei der Installation von .NET Framework 4.6.1. Fehlernummer ist 0x800713ec.|Die erforderlichen Komponenten für .NET Framework 4.6.1 sind nicht auf dem Server installiert. |Stellen Sie vor der Installation von ATA sicher, dass die Windows-Updates [KB2919442](https://www.microsoft.com/download/details.aspx?id=42135) und [KB2919355](https://support.microsoft.com/kb/2919355) auf dem Server installiert sind.|

![Bild zu ATA-.NET-Installationsfehler](media/netinstallerror.png)


## Weitere Informationen
- [ATA-Voraussetzungen](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA-Kapazitätsplanung](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Konfigurieren der Ereignissammlung](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Konfigurieren der Windows-Ereignisweiterleitung](/advanced-threat-analytics/deploy-use/configure-event-collection#ATA_event_WEF)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jun16_HO4-->


