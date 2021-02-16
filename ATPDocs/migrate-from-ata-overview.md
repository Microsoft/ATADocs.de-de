---
title: Advanced Threat Analytics für Microsoft Defender zum Verschieben von Identitäten
description: Erfahren Sie, wie Sie eine vorhandene Advanced Threat Analytics-Installation in Microsoft Defender für Identity verschieben.
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: 45b9004bc439a28e144686e3147b94b6019a7a0f
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533799"
---
# <a name="advanced-threat-analytics-ata-to-microsoft-defender-for-identity"></a>Advanced Threat Analytics (ATA) bei Microsoft Defender für Identity

> [!NOTE]
> Die endgültige Version von ATA ist [allgemein verfügbar](https://support.microsoft.com/help/4568997/update-3-for-microsoft-advanced-threat-analytics-1-9). ATA wird die grundlegende Unterstützung am 12. Januar 2021 beenden. Der erweiterte Support wird bis zum 2026. Januar fortgesetzt. Weitere Informationen finden Sie in [unserem Blog](https://techcommunity.microsoft.com/t5/microsoft-security-and/end-of-mainstream-support-for-advanced-threat-analytics-january/ba-p/1539181).

Verwenden Sie dieses Handbuch, um von einer vorhandenen ATA-Installation zum ()-Dienst zu wechseln [!INCLUDE [Product long](includes/product-long.md)] . In diesem Handbuch [!INCLUDE [Product short](includes/product-short.md)] werden die Voraussetzungen und Anforderungen erläutert, und es wird erläutert, wie Sie Ihre Umstellung planen und dann vervollständigen. Überprüfungs Schritte und Tipps für die Verwendung der neuesten Bedrohungsschutz-und Sicherheitslösungen von [!INCLUDE [Product short](includes/product-short.md)] nach der Installation sind ebenfalls enthalten.

Weitere Informationen zu den Unterschieden zwischen ATA und [!INCLUDE [Product short](includes/product-short.md)] finden Sie in den [ [!INCLUDE [Product short](includes/product-short.md)] häufig gestellten Fragen](technical-faq.yml).

In dieser Anleitung lernen Sie Folgendes:

> [!div class="checklist"]
>
> - Überprüfen und bestätigen der [!INCLUDE [Product short](includes/product-short.md)] Dienst Voraussetzungen
> - Dokumentieren Ihrer vorhandenen ATA-Konfiguration
> - Planen des Verschiebevorgangs
> - Einrichten und Konfigurieren des [!INCLUDE [Product short](includes/product-short.md)]  Dienstanbieter
> - Ausführen von Überprüfungen nach dem Verschiebevorgang
> - Außer Betrieb nehmen von ATA nach dem Verschieben

> [!NOTE]
> Die Umstellung auf [!INCLUDE [Product short](includes/product-short.md)] aus ATA ist aus jeder ATA-Version möglich. Da Daten jedoch nicht von ATA nach verschoben werden können [!INCLUDE [Product short](includes/product-short.md)] , wird empfohlen, die ATA Center-Daten und-Warnungen beizubehalten, die für laufende Ermittlungen erforderlich sind, bis alle ATA-Warnungen geschlossen oder wieder hergestellt wurden.

## <a name="prerequisites"></a>Voraussetzungen

- Zum Erstellen einer-Instanz ist ein Azure Active Directory Mandanten mit mindestens einem globalen/Sicherheitsadministrator erforderlich [!INCLUDE [Product short](includes/product-short.md)] . Jede [!INCLUDE [Product short](includes/product-short.md)]-Instanz unterstützt mehrere Active Directory-Gesamtstrukturbegrenzungen und die Gesamtstrukturfunktionsebene (Forest Functional Level, FFL) von Windows 2003 und höher.

- [!INCLUDE [Product short](includes/product-short.md)] erfordert .NET Framework 4,7 oder höher und erfordert möglicherweise einen Domänen Controller (Neustart), wenn Ihre aktuelle .NET Framework-Version nicht 4,7 oder höher ist.

- Stellen Sie sicher, dass Ihre Domänen Controller alle [ [!INCLUDE [Product short](includes/product-short.md)] Sensor Anforderungen](prerequisites.md#azure-atp-sensor-requirements) erfüllen und dass Ihre Umgebung alle [ [!INCLUDE [Product short](includes/product-short.md)] Anforderungen](prerequisites.md)erfüllt.

- Überprüfen Sie, ob alle Domänen Controller, die Sie verwenden möchten, über ausreichende Internet Zugriffe auf den [!INCLUDE [Product short](includes/product-short.md)] Dienst verfügen. Überprüfen und bestätigen Sie, dass Ihre Domänen Controller die [ [!INCLUDE [Product short](includes/product-short.md)] Proxy Konfigurations Anforderungen](configure-proxy.md)erfüllen.

> [!NOTE]
> Dieses Migrations Handbuch ist nur für [!INCLUDE [Product short](includes/product-short.md)] Sensoren konzipiert.

## <a name="plan"></a>Plan

Stellen Sie sicher, dass Sie die folgenden Informationen gesichert haben, bevor Sie mit dem Verschieben beginnen:

1. Kontodetails für Ihr [Verzeichnisdienste](install-step2.md)-Konto
1. [Einstellungen](setting-syslog.md) für Syslog-Benachrichtigungen
1. E-Mail-[Benachrichtigungsdetails](notifications.md)
1. Gruppenmitgliedschaft für ATA-Rollen
1. VPN-Integration
1. Warnungsausschlüsse
    - Ausschlüsse können nicht von ATA auf übertragen werden [!INCLUDE [Product short](includes/product-short.md)] . Daher sind Details zu jedem Ausschluss erforderlich, um [die Ausschlüsse in [!INCLUDE [Product short](includes/product-short.md)] zu replizieren ](excluding-entities-from-detections.md).
1. Kontodetails für Honeytoken-Konten
    - Wenn Sie noch nicht über dedizierte honeytoken-Konten verfügen, erfahren Sie mehr über [honeytokens in [!INCLUDE [Product short](includes/product-short.md)] ](install-step7.md) , und erstellen Sie neue Konten, die zu diesem Zweck verwendet werden können.
1. Eine vollständige Liste aller Entitäten (Computer, Gruppen, Benutzer), die Sie manuell als „sensible Entitäten“ kennzeichnen möchten
    - Erfahren Sie mehr über die Wichtigkeit [sensibler Entitäten](sensitive-accounts.md) in [!INCLUDE [Product short](includes/product-short.md)] .
1. [Details](reports.md) der Berichtsplanung (Liste der Berichte und geplante zeitliche Steuerung)

> [!NOTE]
> Deinstallieren Sie ATA Center erst, nachdem alle ATA-Gateways entfernt wurden. Wenn ATA Center deinstalliert wird, während ATA-Gateways noch ausgeführt werden, ist Ihre Organisation nicht mehr vor Bedrohungen geschützt.

## <a name="move"></a>Verschieben

Schließen Sie den Umstieg auf [!INCLUDE [Product short](includes/product-short.md)] in zwei einfachen Schritten ab:

### <a name="step-1-create-and-install-defender-for-identity-instance-and-sensors"></a>Schritt 1: Erstellen und Installieren von Defender für Identitäts Instanz und-Sensoren

1. [Erstellen der neuen [!INCLUDE [Product short](includes/product-short.md)] Instanz](install-step1.md)

1. Deinstallieren Sie das ATA-Lightweight-Gateways auf allen Domänencontrollern.

1. Installieren Sie den [!INCLUDE [Product short](includes/product-short.md)] Sensor auf allen Domänen Controllern:
    - [Laden Sie die [!INCLUDE [Product short](includes/product-short.md)] Sensor Dateien herunter](install-step3.md).
    - [Rufen Sie Ihre [!INCLUDE [Product short](includes/product-short.md)] Zugriffstaste](install-step3.md#download-the-setup-package).
    - [Installieren [!INCLUDE [Product short](includes/product-short.md)] Sie Sensoren auf Ihren Domänen Controllern](install-step4.md).

### <a name="step-2-configure-and-validate-defender-for-identity-instance"></a>Schritt 2: Konfigurieren und Überprüfen von Defender für die Identitäts Instanz

- [Konfigurieren Sie den Sensor](install-step5.md)

> [!NOTE]
> Bestimmte Tasks in der folgenden Liste können nicht vor der Installation von [!INCLUDE [Product short](includes/product-short.md)] Sensoren abgeschlossen und dann eine anfängliche Synchronisierung abgeschlossen werden, z.  b. das Auswählen von Entitäten für manuelles, vertrauliches markieren Die erste Synchronisierung kann bis zu 2 Stunden dauern.

#### <a name="configuration"></a>Konfiguration

Melden Sie sich beim Portal an, und führen Sie [!INCLUDE [Product short](includes/product-short.md)] die folgenden Konfigurationsaufgaben aus.

| Schritt    | Aktion | Status |
|--------------|------------|------------------|
| 1  | Festlegen von [verzögerten Updates für bestimmte Domänencontroller](sensor-update.md) | - [ ] |
| 2  | Kontodetails für [Verzeichnisdienste](install-step2.md)| - [ ] |
| 3  | Konfigurieren von [Syslog-Benachrichtigungen](setting-syslog.md) | - [ ] |
| 4  | [Integrieren von VPN](install-step6-vpn.md)-Informationen| - [ ] |
| 5  | Konfigurieren der [WDATP-Integration](integrate-mde.md)| - [ ] |
| 6  | Festlegen von [Honeytoken](install-step7.md)-Konten| - [ ] |
| 7  | Tagging von [sensiblen Entitäten](sensitive-accounts.md)| - [ ] |
| 8  | Erstellen von [Sicherheitswarnungsausschlüssen](excluding-entities-from-detections.md)| - [ ] |
| 9 | [Aktivieren/Deaktivieren von E-Mail-Benachrichtigungen](notifications.md) | - [ ] |
| 10  | Einstellungen für [Berichtszeitplan](reports.md) (Liste der Berichte und geplante zeitliche Steuerung)| - [ ] |
| 11  | Konfigurieren von [rollenbasierten Berechtigungen](role-groups.md) | - [ ] |
| 12  | [Konfigurieren von SIEM-Benachrichtigungen (IP-Adresse)](configure-event-collection.md#siemsyslog)| - [ ] |

#### <a name="validation"></a>Validation

Im [!INCLUDE [Product short](includes/product-short.md)] Portal:

- Überprüfen Sie alle [Integritätswarnungen](health-center.md) auf Anzeichen für Dienstprobleme.
- Überprüfen Sie die [!INCLUDE [Product short](includes/product-short.md)] [Sensor Fehlerprotokolle](troubleshooting-using-logs.md) auf ungewöhnliche Fehler.

## <a name="after-the-move"></a>Nach dem Verschieben

In diesem Abschnitt der Anleitung wird erläutert, welche Aktionen nach dem Verschieben ausgeführt werden können.

> [!NOTE]
> Der Import vorhandener Sicherheitswarnungen von ATA in wird [!INCLUDE [Product short](includes/product-short.md)] nicht unterstützt. Stellen Sie sicher, dass Sie alle vorhandenen ATA-Warnungen aufgezeichnet oder behoben haben, bevor Sie ATA Center außer Betrieb setzen.

- **ATA Center außer Betrieb nehmen**  
  - Es empfiehlt sich, die ATA Center-Daten noch für eine gewisse Zeit online zu speichern, um sie nach dem Verschieben zu referenzieren. Nach der Außerbetriebnahme von ATA Center hat sich die Anzahl der Ressourcen in der Regel verringert, besonders, wenn es sich dabei um virtuelle Computer handelt.

- **Sichern von Mongo DB**  
  - [Sichern Sie Mongo DB](/advanced-threat-analytics/ata-database-management#backing-up-the-ata-database), wenn Sie die ATA-Daten unbegrenzt speichern möchten.

## <a name="mission-accomplished"></a>Mission erfüllt.

Gratulation! Die Umstellung von ATA auf [!INCLUDE [Product short](includes/product-short.md)] ist fertiggestellt.

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie mehr über [[!INCLUDE [Product short](includes/product-short.md)]](what-is.md) Features, Funktionen und [Sicherheitswarnungen](understanding-security-alerts.md).

## <a name="join-the-community"></a>Beitritt zur Community

Haben Sie weitere Fragen, oder möchten Sie mit anderen über [!INCLUDE [Product short](includes/product-short.md)] und damit verbundene Sicherheitsaspekte diskutieren? Treten Sie noch heute der [[!INCLUDE [Product short](includes/product-short.md)]Community](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) bei.
