---
title: Behandeln von Problemen im ATA-Fehlerprotokoll | Microsoft ATA
description: "Beschreibt, wie Sie übliche Fehler in ATA beheben können"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 15c1a0d7ae213876c0e3a955eaeea8887281b4e6
ms.openlocfilehash: b073a1b969f8841c9bbe540722349a5ef70340d4


---

*Gilt für: Advanced Threat Analytics Version 1.7*



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
|Fehler beim Start von Live-Consumer  ---> Microsoft.Opn.Runtime.Monitoring.MessageSessionException: Der PEFNDIS-Ereignisanbieter ist nicht bereit.|PEF (Nachrichtenanalyse) wurde nicht ordnungsgemäß installiert.|Wenn Sie Hyper-V verwenden, versuchen Sie, die Hyper-V-Integrationsdienste zu aktualisieren. Kontaktieren Sie alternativ den Support für eine Problemumgehung.|
|Installationsfehler: 0x80070652|Auf Ihrem Computer stehen weitere Installationen aus.|Warten Sie, bis die anderen Installationen abgeschlossen sind, und starten Sie den Computer gegebenenfalls neu.|
|System.InvalidOperationException: Die Instanz „Microsoft.Tri.Gateway“ existiert nicht in der angegebenen Kategorie.|Die PIDs wurden für Prozessnamen im ATA-Gateway aktiviert.|Verwenden Sie [KB281884](https://support.microsoft.com/en-us/kb/281884), um die PIDs in den Prozessnamen zu deaktivieren.|
|System.InvalidOperationException: Die Kategorie ist nicht vorhanden.|Möglicherweise wurden die Leistungsindikatoren in der Registrierung deaktiviert.|Verwenden Sie [KB2554336](https://support.microsoft.com/en-us/kb/2554336), um die Leistungsindikatoren neu zu erstellen.|
|System.ApplicationException: Die ETW-Sitzung „MMA-ETW-Livecapture-a4f595bd-f567-49a7-b963-20fa4e370329“ kann nicht gestartet werden.|In der HOSTS-Datei existiert ein Hosteintrag, der auf den Kurznamen des Computers verweist.|Entfernen Sie den Hosteintrag aus „C:\Windows\System32\drivers\etc\HOSTS“, oder ändern Sie ihn in einen eindeutigen Domänennamen um.|


## ATA-IIS-Fehler (gilt nicht für ATA Version 1.7 und höher)
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
- [Konfigurieren der Windows-Ereignisweiterleitung](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Aug16_HO5-->


