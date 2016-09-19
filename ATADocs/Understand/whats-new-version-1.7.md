---
title: Neues in ATA Version 1.7 | Microsoft ATA
description: Listet Neuerungen sowie bekannte Probleme in ATA Version 1.7 auf
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 
ms.reviewer: 
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ae6a3295d2fffabdb8e5f713674379e4af499ac2
ms.openlocfilehash: af9101260b1a0d5d9da32398f638f76e0c8c40a7


---

# Neues in ATA Version 1.7
Die vorliegenden Anmerkungen zu dieser Version enthalten Informationen zu bekannten Problemen in dieser Version von Advanced Threat Analytics.

## Neuerungen beim Update auf ATA 1.7
Das Update auf ATA 1.7 bietet Verbesserungen in folgenden Bereichen:

-   Neue und aktualisierte Erkennung

-   Rollenbasierte Zugriffssteuerung

-   Unterstützung für Windows Server 2016 und Windows Server Core

-   Verbesserungen der Benutzeroberfläche


### Neue und aktualisierte Erkennung


- **Reconnaissance mithilfe von Verzeichnisdienstenumeration:** Im Rahmen dieser Phase der Reconnaissance sammeln Angreifer auf verschiedene Weise Informationen zu den Entitäten im Netzwerk. Die Verzeichnisdienstenumeration mit dem SAM-R-Protokoll ermöglicht es Angreifern, die Liste der Benutzer und Gruppen in einer Domäne zu erhalten und die Interaktion zwischen den verschiedenen Entitäten zu verstehen. 

- **Verbesserungen bei Pass-the-Hash-Angriffen:** Wir haben zusätzliche Verhaltensmodelle für Authentifizierungsmuster von Entitäten hinzugefügt, um die Pass-the-Hash-Erkennung zu verbessern. Dank dieser Modelle kann ATA das Verhalten von Entitäten verdächtigen NTLM-Authentifizierungen zuordnen und echte Pass-the-Hash-Angriffe vom Verhalten falsch-positiver Szenarien unterscheiden.

- **Verbesserungen bei Pass-the-Ticket-Angriffen:** Um hochentwickelte Attacken (allgemein, aber auch speziell Pass-the-Ticket-Angriffe) erfolgreich zu erkennen, muss die Korrelation zwischen einer IP-Adresse und dem Computerkonto präzise sein. Dies ist eine Herausforderung in Umgebungen, in denen IP-Adressen sich beabsichtigt schnell ändern, (z.B. Wi-Fi-Netzwerke und wenn mehrere virtuelle Maschinen einen gemeinsamen Host nutzen). Um diese Herausforderung zu überwinden und die Genauigkeit der Erkennung von Pass-the-Ticket-Angriffen zu verbessern, wurde der Mechanismus zur Auflösung des Netzwerknamens (Network Name Resolution; NNR) von ATA deutlich verbessert, um Fehlerquote zu reduzieren.

- **Verbesserungen bei ungewöhnlichem/nicht normalem Verhalten:** In ATA 1.7 wurden die NTLM-Authentifizierungsdaten als Datenquelle für nicht normales Verhalten hinzugefügt. Dazu decken die Algorithmen nun ein größeres Spektrum von Entitätsverhalten im Netzwerk ab. 

- **Verbesserungen bei der ungewöhnlichen Protokollimplementierung:** ATA erkennt nun die ungewöhnliche Protokollimplementierung im Kerberos-Protokoll, zusammen mit zusätzlichen Anomalien im NTLM-Protokoll. Diese neuen Kerberos-Anomalien werden gewöhnlicherweise für Overpass-the-Hash-Angriffe verwendet.


### Infrastruktur

- **Rollenbasierte Zugriffskontrolle:** die Funktion für die rollenbasierte Zugriffskontrolle (Role-Based Access Control; RBAC) ATA 1.7 enthält drei Rollen: ATA Administrator, ATA Analyst und ATA Executive.

- **Unterstützung für Windows Server 2016 und Windows Server Core:** ATA 1.7 unterstützt die Bereitstellung von Lightweight-Gateways auf Domänencontrollern unter Server Core für Windows Server 2012 und Server Core für Windows Server 2012 R2. Darüber hinaus unterstützt dieses Release Windows Server 2016 sowohl für die ATA Center- als auch die ATA-Gatewaykomponenten.

### Benutzererfahrung
- **Einfache Konfiguration:** Die ATA-Konfigurationsbenutzeroberfläche wurde in dieser Version neu gestaltet, um eine höhere Benutzerfreundlichkeit und eine bessere Unterstützung für Umgebungen mit mehreren ATA-Gateways zu gewährleisten. Mit diesem Release wird auch die Updateseite für das ATA-Gateway eingeführt, um die Verwaltung von automatische Updates für die verschiedenen Gateways zu erleichtern.

## Bekannte Probleme
In dieser Version bestehen die folgenden bekannten Probleme.

### Die automatische Aktualisierung des Gateways kann fehlschlagen.
**Symptome:** Das ATA-Gateway kann in einer Umgebung mit langsamen WAN-Verbindungen das Update-Timeout (100 Sekunden) erreichen. Updates können daraufhin nicht erfolgreich abgeschlossen werden.
In der ATA-Konsole zeigt das ATA-Gateway über längere Zeit den Status „Wird aktualisiert (Paket wird heruntergeladen)“ an und schlägt schließlich fehl.

**Problemumgehung:** Laden Sie das neueste ATA-Gateway-Paket aus der ATA-Konsole herunter, und aktualisieren das ATA-Gateway manuell, um dieses Problem zu umgehen.

### Migrationsfehler beim Update von ATA 1.6 auf 1.7
Beim Update auf ATA 1.7 kann der Aktualisierungsvorgang mit dem folgenden Fehlercode misslingen *0x80070643*:

![Fehler beim Update auf ATA 1.7](media/ata-update-error.png)

Überprüfen Sie das Bereitstellungsprotokoll, um die Ursache des Fehlers zu finden. Das Bereitstellungsprotokoll befindet sich am folgenden Speicherort: **%temp%\..\Microsoft Advanced Thread Analytics Center_{Datumsstempel}_MsiPackage.log**. 

Die folgende Tabelle enthält die Fehler, nach denen Sie suchen sollten, und das entsprechende Mongo-Skript, um den Fehler zu beheben. Siehe das Beispiel unter der Tabelle, um zu erfahren, wie das Mongo-Skript ausgeführt wird:

| Fehler in Bereitstellungsprotokolldatei                                                                                                                  | Mongo-Skript                                                                                                                                                                         |
|---|---|
| „System.FormatException: Size {Größe}“ ist größer als MaxDocumentSize 16777216 <br>Weiter unten in der Datei:<br>  Microsoft.Tri.Center.Deployment.Package.Actions.DatabaseActions.MigrateUniqueEntityProfiles(Boolean isPartial)                                                                                        | db.UniqueEntityProfile.find().forEach(function(obj){if(Object.bsonsize(obj) > 12582912) {print(obj._id);print(Object.bsonsize(obj));db.UniqueEntityProfile.remove({_id:obj._id});}}) |
| System.OutOfMemoryException: Ausnahme des Typs 'System.OutOfMemoryException' ausgelöst<br>Weiter unten in der Datei:<br>Microsoft.Tri.Center.Deployment.Package.Actions.DatabaseActions.ReduceSuspiciousActivityDetailsRecords(IMongoCollection`1 suspiciousActivityCollection, Int32 deletedDetailRecordMaxCount) | db.SuspiciousActivity.find().forEach(function(obj){if(Object.bsonsize(obj) > 500000),{print(obj._id);print(Object.bsonsize(obj));db.SuspiciousActivity.remove({_id:obj._id});}})     |
|System.Security.Cryptography.CryptographicException: Ungültige Länge<br>Weiter unten in der Datei:<br> Microsoft.Tri.Center.Deployment.Package.Actions.DatabaseActions.MigrateCenterSystemProfile(IMongoCollection`1 systemProfileCollection)| CenterThumbprint=db.SystemProfile.find({_t:"CenterSystemProfile"}).toArray()[0].Configuration.SecretManagerConfiguration.CertificateThumbprint;db.SystemProfile.update({_t:"CenterSystemProfile"},{$set:{"Configuration.ManagementClientConfiguration.ServerCertificateThumbprint":CenterThumbprint}})|


Um das entsprechende Skript auszuführen, führen Sie die folgenden Schritte durch. 

1.  Navigieren Sie an einer Eingabeaufforderung mit erhöhten Rechten zum folgenden Verzeichnis: **C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**
2.  Geben Sie „– **Mongo.exe ATA-**“ ein (*Hinweis*: ATA muss in Großbuchstaben angegeben werden.)
3.  Fügen Sie das Skript ein, das dem Fehler im Bereitstellungsprotokoll in der obigen Tabelle entspricht.

![ATA Mongo-Skript](media/ATA-mongoDB-script.png)

An diesem Punkt sollten Sie das Upgrade neu starten können.

### ATA meldet eine große Anzahl verdächtiger Aktivitäten des Typs *Reconnaissance mithilfe einer Verzeichnisdienstenumeration*:
 
Dies passiert am ehesten, wenn auf allen (bzw. vielen) Clientcomputern in der Organisation ein Tool zum Scannen des Netzwerks ausgeführt wird. Wenn dieses Problem auftritt:

1. Falls Sie den Grund oder die jeweilige Anwendung bestimmen können, die auf den Clientcomputern ausgeführt wird, senden Sie eine E-Mail mit den Informationen an ATAEval bei Microsoft.com.
2. Verwenden Sie das folgende Mongo-Skript, um alle diese Ereignisse zu verwerfen (siehe oben, um zu erfahren, wie Sie das Mongo-Skript ausführen):

db.SuspiciousActivity.update({_t: "SamrReconnaissanceSuspiciousActivity"}, {$set: {Status: "Dismissed"}}, {multi: true})

### ATA sendet Benachrichtigungen bei verworfenen verdächtigen Aktivitäten:
Wenn Benachrichtigungen konfiguriert wurden, sendet ATA möglicherweise weiterhin Benachrichtigungen (E-Mail, Syslog und Ereignisprotokolle) für verworfene verdächtige Aktivitäten.
Für dieses Problem ist derzeit keine Problemumgehung bekannt. 

### Das ATA-Gateway registriert sich ggf. nicht bei ATA Center, wenn TLS 1.0 und TLS 1.1 deaktiviert sind:
Wenn TLS 1.0 und 1.1 von TLS auf dem ATA-Gateway (oder Lightweight Gateway) deaktiviert sind, kann sich das Gateway möglicherweise nicht beim ATA Center registrieren

### Die automatische Erneuerung von Zertifikaten, die von ATA verwendet werden, wird nicht unterstützt
Die Verwendung der automatischen Zertifikatserneuerung kann dazu führen, dass ATA bei einer automatischen Erneuerung der Zertifikate nicht mehr funktioniert. 


## Weitere Informationen
[Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Aktualisieren von ATA auf Version 1.7 – Migrationshandbuch](ata-update-1.7-migration-guide.md)




<!--HONumber=Sep16_HO2-->


