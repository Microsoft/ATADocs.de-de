---
title: Verschieben von Advanced Threat Analytics zu Azure Advanced Threat Protection
description: Erfahren Sie, wie Sie eine vorhandene Installation von Advanced Threat Analytics zu Azure ATP verschieben.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 07/13/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: e734e382-c4b1-43ca-9a8d-96c91daf2578
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 217f961a0c063d75ec73d2aa1b45c028ed5fbad3
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88956481"
---
# <a name="advanced-threat-analytics-ata-to-azure-advanced-threat-protection-azure-atp"></a>Advanced Threat Analytics (ATA) zu Azure Advanced Threat Protection (Azure ATP)

Folgen Sie dieser Anleitung, um eine vorhandene ATA-Installation zum Azure Advanced Threat Protection-Dienst zu verschieben. In der Anleitung sind sowohl Voraussetzungen und Anforderungen für Azure ATP beschrieben als auch Informationen zur Planung und Durchführung des Verschiebevorgangs enthalten. Zusätzlich finden Sie darin Überprüfungsschritte und Tipps zur Nutzung der neuesten Sicherheitslösungen und Schutzmöglichkeiten vor Bedrohungen mit Azure ATP nach der Installation.

Weitere Informationen zu den Unterschieden zwischen ATA und Azure ATP finden Sie unter [Häufig gestellte Fragen zu Azure ATP](atp-technical-faq.md#what-is-azure-atp).

In dieser Anleitung lernen Sie Folgendes:

> [!div class="checklist"]
>
> - Überprüfen und Bestätigen der Voraussetzungen für den Azure ATP-Dienst
> - Dokumentieren Ihrer vorhandenen ATA-Konfiguration
> - Planen des Verschiebevorgangs
> - Einrichten und Konfigurieren Ihres Azure ATP-Diensts
> - Ausführen von Überprüfungen nach dem Verschiebevorgang
> - Außer Betrieb nehmen von ATA nach dem Verschieben

> [!NOTE]
> Das Verschieben zu Azure ATP ist aus jeder beliebigen ATA-Version möglich. Beachten Sie aber dabei, dass keine Daten aus ATA zu Azure ATP verschoben werden können. Aus diesem Grund sollten Sie alle ATA Center-Daten und -Warnungen, die für laufende Untersuchungen erforderlich sind, zurückhalten, bis alle ATA-Warnungen geschlossen oder behoben wurden.

## <a name="prerequisites"></a>Voraussetzungen

- Ein Azure Active Directory-Mandant mit mindestens einem globalen Administrator oder einem Sicherheitsadministrator ist erforderlich, um eine Azure ATP-Instanz zu erstellen. Jede Azure ATP-Instanz unterstützt mehrere Active Directory-Gesamtstrukturbegrenzungen und die Gesamtstrukturfunktionsebene (Forest Functional Level, FFL) von Windows 2003 und höher.

- Azure ATP erfordert .NET Framework 4.7 oder höher und möglicherweise auch einen Domänencontroller (Neustart), falls Sie eine ältere Version als .NET Framework 4.7 verwenden.

- Stellen Sie sicher, dass Ihre Domänencontroller alle [Anforderungen für den Azure ATP-Sensor](atp-prerequisites.md#azure-atp-sensor-requirements) erfüllen und Ihre Umgebung alle [Anforderungen für Azure ATP](atp-prerequisites.md) erfüllt.

- Überprüfen Sie, ob alle Domänencontroller, die Sie verwenden möchten, über ausreichenden Internetzugriff auf den Azure ATP-Dienst verfügen. Überprüfen Sie, ob Ihre Domänencontroller die [Konfigurationsanforderungen für den Azure ATP-Proxy](configure-proxy.md) erfüllen, und bestätigen Sie dies.

> [!NOTE]
> Diese Migrationsanleitung bezieht sich ausschließlich auf Azure ATP-Sensoren.

## <a name="plan"></a>Plan

Stellen Sie sicher, dass Sie die folgenden Informationen gesichert haben, bevor Sie mit dem Verschieben beginnen:

1. Kontodetails für Ihr [Verzeichnisdienste](install-atp-step2.md)-Konto
1. [Einstellungen](setting-syslog.md) für Syslog-Benachrichtigungen
1. E-Mail-[Benachrichtigungsdetails](notifications.md)
1. Gruppenmitgliedschaft für ATA-Rollen
1. VPN-Integration
1. Warnungsausschlüsse
    - Ausschlüsse sind nicht von ATA zu Azure ATP übertragbar, daher müssen Details von jedem Ausschluss die [Ausschlüsse in Azure ATP replizieren](excluding-entities-from-detections.md).
1. Kontodetails für Honeytoken-Konten
    - Falls Sie noch keine Honeytoken-Konten dediziert haben, erfahren Sie mehr über [Honeytokens in Azure ATP](install-atp-step7.md), und erstellen Sie neue Konten für deren Verwendung.
1. Eine vollständige Liste aller Entitäten (Computer, Gruppen, Benutzer), die Sie manuell als „sensible Entitäten“ kennzeichnen möchten
    - Erfahren Sie mehr über die Bedeutung von [sensiblen Entitäten](sensitive-accounts.md) in Azure ATP.
1. [Details](reports.md) der Berichtsplanung (Liste der Berichte und geplante zeitliche Steuerung)

> [!NOTE]
> Deinstallieren Sie ATA Center erst, nachdem alle ATA-Gateways entfernt wurden. Wenn ATA Center deinstalliert wird, während ATA-Gateways noch ausgeführt werden, ist Ihre Organisation nicht mehr vor Bedrohungen geschützt.

## <a name="move"></a>Verschieben

Schließen Sie den Verschiebevorgang zu Azure ATP in zwei einfachen Schritten ab:

### <a name="step-1-create-and-install-azure-atp-instance-and-sensors"></a>Schritt 1: Erstellen und Installieren von Azure ATP-Instanz und -Sensoren

1. [Erstellen Sie Ihre neue Azure ATP-Instanz](install-atp-step1.md)

1. Deinstallieren Sie das ATA-Lightweight-Gateways auf allen Domänencontrollern.

1. Installieren Sie den Azure ATP-Sensor auf allen Domänencontrollern:
    - [Laden Sie die Dateien für den Azure ATP-Sensor herunter.](install-atp-step3.md)
    - [Rufen Sie Ihren Zugriffsschlüssel für Azure ATP ab.](install-atp-step3.md#download-the-setup-package)
    - [Installieren Sie Azure ATP-Sensoren auf Ihren Domänencontrollern.](install-atp-step4.md)

### <a name="step-2-configure-and-validate-azure-atp-instance"></a>Schritt 2: Konfigurieren und Überprüfen der Azure ATP-Instanz

- [Konfigurieren Sie den Sensor](install-atp-step5.md)

> [!NOTE]
> Bestimmte Aufgaben in der folgenden Liste, z. B. das Auswählen von Entitäten für manuelles **sensibles** Tagging, können erst abgeschlossen werden, nachdem Azure ATP-Sensoren installiert wurden und eine erste Synchronisierung erfolgt ist. Die erste Synchronisierung kann bis zu 2 Stunden dauern.

#### <a name="configuration"></a>Konfiguration

Melden Sie sich im Azure ATP-Portal an, und schließen Sie die folgenden Konfigurationsaufgaben ab.

| Schritt    | Aktion | Status |
|--------------|------------|------------------|
| 1  | Festlegen von [verzögerten Updates für bestimmte Domänencontroller](sensor-update.md) | - [ ] |
| 2  | Kontodetails für [Verzeichnisdienste](install-atp-step2.md)| - [ ] |
| 3  | Konfigurieren von [Syslog-Benachrichtigungen](setting-syslog.md) | - [ ] |
| 4  | [Integrieren von VPN](install-atp-step6-vpn.md)-Informationen| - [ ] |
| 5  | Konfigurieren der [WDATP-Integration](integrate-wd-atp.md)| - [ ] |
| 6  | Festlegen von [Honeytoken](install-atp-step7.md)-Konten| - [ ] |
| 7  | Tagging von [sensiblen Entitäten](sensitive-accounts.md)| - [ ] |
| 8  | Erstellen von [Sicherheitswarnungsausschlüssen](excluding-entities-from-detections.md)| - [ ] |
| 9 | [Aktivieren/Deaktivieren von E-Mail-Benachrichtigungen](notifications.md) | - [ ] |
| 10  | Einstellungen für [Berichtszeitplan](reports.md) (Liste der Berichte und geplante zeitliche Steuerung)| - [ ] |
| 11  | Konfigurieren von [rollenbasierten Berechtigungen](atp-role-groups.md) | - [ ] |
| 12  | [Konfigurieren von SIEM-Benachrichtigungen (IP-Adresse)](configure-event-collection.md#siemsyslog)| - [ ] |

#### <a name="validation"></a>Validation

Aufgaben im Azure ATP-Portal:

- Überprüfen Sie alle [Integritätswarnungen](atp-health-center.md) auf Anzeichen für Dienstprobleme.
- Überprüfen Sie [Fehlerprotokolle](troubleshooting-atp-using-logs.md) für den Azure ATP-Sensor auf ungewöhnliche Fehler.

## <a name="after-the-move"></a>Nach dem Verschieben

In diesem Abschnitt der Anleitung wird erläutert, welche Aktionen nach dem Verschieben ausgeführt werden können.

> [!NOTE]
> Das Importieren vorhandener Sicherheitswarnungen aus ATA zu ATP wird nicht unterstützt. Stellen Sie sicher, dass Sie alle vorhandenen ATA-Warnungen aufgezeichnet oder behoben haben, bevor Sie ATA Center außer Betrieb setzen.

- **ATA Center außer Betrieb nehmen**  
  - Es empfiehlt sich, die ATA Center-Daten noch für eine gewisse Zeit online zu speichern, um sie nach dem Verschieben zu referenzieren. Nach der Außerbetriebnahme von ATA Center hat sich die Anzahl der Ressourcen in der Regel verringert, besonders, wenn es sich dabei um virtuelle Computer handelt.

- **Sichern von Mongo DB**  
  - [Sichern Sie Mongo DB](/advanced-threat-analytics/ata-database-management#backing-up-the-ata-database), wenn Sie die ATA-Daten unbegrenzt speichern möchten.

## <a name="mission-accomplished"></a>Mission erfüllt.

Gratulation! Sie haben die Migration von ATA zu Azure ATP erfolgreich abgeschlossen.

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie mehr über Features, Funktionalität und [Sicherheitswarnungen](understanding-security-alerts.md) von [Azure ATP](what-is-atp.md).

## <a name="join-the-community"></a>Beitritt zur Community

Haben Sie weitere Fragen, oder möchten Sie mit anderen über Azure ATP und damit verbundene Sicherheitsaspekte diskutieren? Treten Sie noch heute der [Azure ATP-Community](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) bei!