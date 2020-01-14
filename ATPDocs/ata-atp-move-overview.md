---
title: Verschieben von Advanced Threat Analytics zu Azure Advanced Threat Protection | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie eine vorhandene Installation von Advanced Threat Analytics zu Azure ATP verschieben.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 10/16/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: e734e382-c4b1-43ca-9a8d-96c91daf2578
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 5c784226b8cf9ee19797103d3e0b9cfe23a629bd
ms.sourcegitcommit: 9673eb49729a06d3a25d52c0f43c76ac61b9cf89
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/12/2020
ms.locfileid: "75908345"
---
# <a name="advanced-threat-analytics-ata-to-azure-advanced-threat-protection-azure-atp"></a>Advanced Threat Analytics (ATA) zu Azure Advanced Threat Protection (Azure ATP) 


Folgen Sie dieser Anleitung, um eine vorhandene ATA-Installation zum Azure Advanced Threat Protection-Dienst zu verschieben. In der Anleitung sind sowohl Voraussetzungen und Anforderungen für Azure ATP beschrieben als auch Informationen zur Planung und Durchführung des Verschiebevorgangs enthalten. Zusätzlich finden Sie darin Überprüfungsschritte und Tipps zur Nutzung der neuesten Sicherheitslösungen und Schutzmöglichkeiten vor Bedrohungen mit Azure ATP nach der Installation. 

Weitere Informationen zu den Unterschieden zwischen ATA und Azure ATP finden Sie in den [Häufig gestellten Fragen zu Azure ATP] (https://docs.microsoft.com/azure-advanced-threat-protection/atp-technical-faq#what-is-azure-atp).

In dieser Anleitung lernen Sie Folgendes: 

> [!div class="checklist"]
> * Überprüfen und Bestätigen der Voraussetzungen für den Azure ATP-Dienst
> * Dokumentieren Ihrer vorhandenen ATA-Konfiguration
> * Planen des Verschiebevorgangs
> * Einrichten und Konfigurieren Ihres Azure ATP-Diensts
> * Ausführen von Überprüfungen nach dem Verschiebevorgang
> * Außer Betrieb nehmen von ATA nach dem Verschieben 

>[!NOTE]
> Das Verschieben zu Azure ATP ist aus jeder beliebigen ATA-Version möglich. Beachten Sie aber dabei, dass keine Daten aus ATA zu Azure ATP verschoben werden können. Aus diesem Grund sollten Sie alle ATA Center-Daten und -Warnungen, die für laufende Untersuchungen erforderlich sind, zurückhalten, bis alle ATA-Warnungen geschlossen oder behoben wurden. 

## <a name="prerequisites"></a>Voraussetzungen

- Ein Azure Active Directory-Mandant mit mindestens einem globalen Administrator oder einem Sicherheitsadministrator ist erforderlich, um eine Azure ATP-Instanz zu erstellen. Jede Azure ATP-Instanz unterstützt mehrere Active Directory-Gesamtstrukturbegrenzungen und die Gesamtstrukturfunktionsebene (Forest Functional Level, FFL) von Windows 2003 und höher.

- Azure ATP erfordert .NET Framework 4.7 und möglicherweise auch einen Domänencontroller (Neustart), falls Sie eine ältere Version als .NET Framework 4.7 verwenden.

- Stellen Sie sicher, dass Ihre Domänencontroller alle [Anforderungen für den Azure ATP-Sensor](https://docs.microsoft.com/azure-advanced-threat-protection/atp-prerequisites#azure-atp-sensor-requirements) erfüllen und Ihre Umgebung alle [Anforderungen für Azure ATP](https://docs.microsoft.com/azure-advanced-threat-protection/atp-prerequisites) erfüllt.

- Überprüfen Sie, ob alle Domänencontroller, die Sie verwenden möchten, über ausreichenden Internetzugriff auf den Azure ATP-Dienst verfügen. Überprüfen Sie, ob Ihre Domänencontroller die [Konfigurationsanforderungen für den Azure ATP-Proxy](https://docs.microsoft.com/azure-advanced-threat-protection/configure-proxy) erfüllen, und bestätigen Sie dies.

>[!NOTE]
> Diese Migrationsanleitung bezieht sich ausschließlich auf Azure ATP-Sensoren. Weitere Informationen finden Sie unter [Choosing the right sensor for your deployment (Auswählen des richtigen Sensortyps für die Bereitstellung)](https://docs.microsoft.com/azure-advanced-threat-protection/atp-capacity-planning#choosing-the-right-sensor-type-for-your-deployment). 

## <a name="plan"></a>Plan 

Stellen Sie sicher, dass Sie die folgenden Informationen gesichert haben, bevor Sie mit dem Verschieben beginnen: 
1. Kontodetails für Ihr [Verzeichnisdienste](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step2)-Konto
1. [Einstellungen](https://docs.microsoft.com/azure-advanced-threat-protection/setting-syslog) für Syslog-Benachrichtigungen
1. E-Mail-[Benachrichtigungsdetails](https://docs.microsoft.com/azure-advanced-threat-protection/notifications)
1. Gruppenmitgliedschaft für ATA-Rollen
1. VPN-Integration
1. Warnungsausschlüsse 
    - Ausschlüsse sind nicht von ATA zu Azure ATP übertragbar, daher müssen Details von jedem Ausschluss die [Ausschlüsse in Azure ATP replizieren](https://docs.microsoft.com/azure-advanced-threat-protection/excluding-entities-from-detections).
1. Kontodetails für Honeytoken-Konten 
    - Falls Sie noch keine Honeytoken-Konten dediziert haben, erfahren Sie mehr über [Honeytokens in Azure ATP](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step7), und erstellen Sie neue Konten für deren Verwendung.
1. Eine vollständige Liste aller Entitäten (Computer, Gruppen, Benutzer), die Sie manuell als „sensible Entitäten“ kennzeichnen möchten 
    - Erfahren Sie mehr über die Bedeutung von [sensiblen Entitäten](https://docs.microsoft.com/azure-advanced-threat-protection/sensitive-accounts) in Azure ATP.
1. [Details](https://docs.microsoft.com/azure-advanced-threat-protection/reports) der Berichtsplanung (Liste der Berichte und geplante zeitliche Steuerung) 
1. Identifizierung und Details zu jedem ATA-Lightweight-Gateway, das ein Kandidat für die Domänensynchronisierung in Azure ATP ist 
   - Erfahren Sie mehr über die Bedeutung von [Kandidaten für die Domänensynchronisierung](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step5#configure-sensor-settings) in Azure ATP.

> [!NOTE]
> Deinstallieren Sie ATA Center erst, nachdem alle ATA-Gateways entfernt wurden. Wenn ATA Center deinstalliert wird, während ATA-Gateways noch ausgeführt werden, ist Ihre Organisation nicht mehr vor Bedrohungen geschützt.

## <a name="move"></a>Verschieben 

Schließen Sie den Verschiebevorgang zu Azure ATP in zwei einfachen Schritten ab:

### <a name="step-1-create-and-install-azure-atp-instance-and-sensors"></a>Schritt 1: Erstellen und Installieren von Azure ATP-Instanz und -Sensoren

1. [Erstellen Sie Ihre neue Azure ATP-Instanz](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step1)

2. Deinstallieren Sie das ATA-Lightweight-Gateways auf allen Domänencontrollern.  

3. Installieren Sie den Azure ATP-Sensor auf allen Domänencontrollern:
     - [Laden Sie die Dateien für den Azure ATP-Sensor herunter.](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step3)
     - [Rufen Sie Ihren Zugriffsschlüssel für Azure ATP ab.](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step3#download-the-setup-package)
     - [Installieren Sie Azure ATP-Sensoren auf Ihren Domänencontrollern.](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step4) 

### <a name="step-2-configure-and-validate-azure-atp-instance"></a>Schritt 2: Konfigurieren und Überprüfen der Azure ATP-Instanz  

- [Konfigurieren Sie den Sensor](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step5)

>[!NOTE]
> Bestimmte Aufgaben in der folgenden Liste, z. B. das Auswählen von Entitäten für manuelles **sensibles** Tagging, können erst abgeschlossen werden, nachdem Azure ATP-Sensoren installiert wurden und eine erste Synchronisierung erfolgt ist. Die erste Synchronisierung kann bis zu 2 Stunden dauern. 

#### <a name="configuration"></a>Konfiguration

Melden Sie sich im Azure ATP-Portal an, und schließen Sie die folgenden Konfigurationsaufgaben ab.

| Schritt    | Aktion | Status |
|--------------|------------|------------------|
| 1  | Festlegen von [verzögerten Updates für bestimmte Domänencontroller](https://docs.microsoft.com/azure-advanced-threat-protection/sensor-update) | - [ ] |
| 2  | Kontodetails für [Verzeichnisdienste](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step2)| - [ ] |
| 3  | Konfigurieren von [Kandidaten für die Domänensynchronisierung](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step5#configure-sensor-settings) | - [ ] |
| 4  | Konfigurieren von [Syslog-Benachrichtigungen](https://docs.microsoft.com/azure-advanced-threat-protection/setting-syslog) | - [ ] |
| 5  | [Integrieren von VPN](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step6-vpn)-Informationen| - [ ] |
| 6  | Konfigurieren der [WDATP-Integration](https://docs.microsoft.com/azure-advanced-threat-protection/integrate-wd-atp)| - [ ] |
| 7  | Festlegen von [Honeytoken](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step7)-Konten| - [ ] |
| 8  | Tagging von [sensiblen Entitäten](https://docs.microsoft.com/azure-advanced-threat-protection/sensitive-accounts)| - [ ] |
| 9  | Erstellen von [Sicherheitswarnungsausschlüssen](https://docs.microsoft.com/azure-advanced-threat-protection/excluding-entities-from-detections)| - [ ] |
| 10 | [Aktivieren/Deaktivieren von E-Mail-Benachrichtigungen](https://docs.microsoft.com/azure-advanced-threat-protection/notifications) | - [ ] |
| 11  | Einstellungen für [Berichtszeitplan](https://docs.microsoft.com/azure-advanced-threat-protection/reports) (Liste der Berichte und geplante zeitliche Steuerung)| - [ ] |
| 12  | Konfigurieren von [rollenbasierten Berechtigungen](https://docs.microsoft.com/azure-advanced-threat-protection/atp-role-groups) | - [ ] |
| 12  | [Konfigurieren von SIEM-Benachrichtigungen (IP-Adresse)](https://docs.microsoft.com/azure-advanced-threat-protection/configure-event-collection#siemsyslog)| - [ ] | 

#### <a name="validation"></a>Validation

Aufgaben im Azure ATP-Portal:
- Überprüfen Sie alle [Integritätswarnungen](https://docs.microsoft.com/azure-advanced-threat-protection/atp-health-center) auf Anzeichen für Dienstprobleme. 
- Überprüfen Sie [Fehlerprotokolle](https://docs.microsoft.com/azure-advanced-threat-protection/troubleshooting-atp-using-logs) für den Azure ATP-Sensor auf ungewöhnliche Fehler.

## <a name="after-the-move"></a>Nach dem Verschieben

In diesem Abschnitt der Anleitung wird erläutert, welche Aktionen nach dem Verschieben ausgeführt werden können. 

>[!NOTE]
> Das Importieren vorhandener Sicherheitswarnungen aus ATA zu ATP wird nicht unterstützt. Stellen Sie sicher, dass Sie alle vorhandenen ATA-Warnungen aufgezeichnet oder behoben haben, bevor Sie ATA Center außer Betrieb setzen.  

- **ATA Center außer Betrieb nehmen** 
    - Es empfiehlt sich, die ATA Center-Daten noch für eine gewisse Zeit online zu speichern, um sie nach dem Verschieben zu referenzieren. Nach der Außerbetriebnahme von ATA Center hat sich die Anzahl der Ressourcen in der Regel verringert, besonders, wenn es sich dabei um virtuelle Computer handelt.  

- **Sichern von Mongo DB** 
    - [Sichern Sie Mongo DB](https://docs.microsoft.com/advanced-threat-analytics/ata-database-management#backing-up-the-ata-database), wenn Sie die ATA-Daten unbegrenzt speichern möchten.  

## <a name="mission-accomplished"></a>Mission erfüllt.

Gratulation! Sie haben die Migration von ATA zu Azure ATP erfolgreich abgeschlossen. 

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie mehr über Features, Funktionalität und [Sicherheitswarnungen](https://docs.microsoft.com/azure-advanced-threat-protection/understanding-security-alerts) von [Azure ATP](https://docs.microsoft.com/azure-advanced-threat-protection/what-is-atp).  
## <a name="join-the-community"></a>Beitritt zur Community

Haben Sie weitere Fragen, oder möchten Sie mit anderen über Azure ATP und damit verbundene Sicherheitsaspekte diskutieren? Treten Sie noch heute der [Azure ATP-Community](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) bei!




