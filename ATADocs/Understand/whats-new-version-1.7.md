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
ms.sourcegitcommit: e3b690767e5c6f5561a97a73eccfbf50ddb04148
ms.openlocfilehash: 579e49a8dd9a5cc67961af14259bb8bb27130de5


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

 > [!IMPORTANT]
 Die automatische Erneuerung der von ATA verwendeten Zertifikate wird nicht unterstützt. Die Verwendung dieser Zertifikate kann dazu führen, dass ATA bei einer automatischen Erneuerung der Zertifikate nicht mehr funktioniert. 


## Weitere Informationen
[Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Aktualisieren von ATA auf Version 1.7 – Migrationshandbuch](ata-update-1.7-migration-guide.md)




<!--HONumber=Aug16_HO5-->


