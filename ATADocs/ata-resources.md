---
title: Roadmap für Advanced Threat Analytics-Ressourcen und-Bereitschaft
description: Stellt eine Liste von Links zu ATA-Ressourcen, Videos, ersten Schritten sowie zur Bereitstellung und zum Überblick für die Bereitschaft bereit.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 7/15/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 42a1a34f-ed6b-4538-befb-452168a30e8c
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 7f8413ba144196a4f64e21dfd688583a05b874ed
ms.sourcegitcommit: 5bf0c6a204b71126306a0c64108eaf9cb7fc042f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/18/2021
ms.locfileid: "101096997"
---
# <a name="ata-readiness-roadmap"></a>Überblick über die ATA-Bereitschaft

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Dieser Artikel bietet einen Überblick über die Roadmap für die Bereitschaft, die Ihnen beim Einstieg mit Advanced Threat Analytics hilft.

## <a name="understanding-ata"></a>Grundlegendes zu ATA

Advanced Threat Analytics (ATA) ist eine lokale Plattform, die Ihnen hilft, Ihr Unternehmen vor verschiedenen Typen von erweiterten gezielten Cyberangriffen und Insider Bedrohungen zu schützen. In den folgenden Artikeln finden Sie weitere Informationen zu ATA zu erhalten:

- [ATA-Übersicht](what-is-ata.md)

- [Einführungsvideo zu ATA (kurz)](https://aka.ms/ATAShort)

- [Einführungsvideo zu ATA (lang)](https://aka.ms/ATAVideo)

## <a name="deployment-decisions"></a>Entscheidungen für die Bereitstellung

ATA besteht aus ATA Center, das Sie auf einem Server installieren können, sowie aus ATA Gateways, die Sie auf separaten Computern oder mithilfe des Lightweight-Gateways direkt auf Ihren Domänencontrollern installieren können. Bevor Sie loslegen ist es wichtig, folgende Entscheidungen zur Bereitstellung zu treffen:

|Konfiguration | Entscheidung |
|----|----|
|Hardwaretyp|Physische, virtuelle, Azure-VM|
|Arbeitsgruppe oder Domäne|Arbeitsgruppe, Domäne|
|Festlegen der Gatewaygröße|Vollständiges Gateway, Lightweight-Gateway|
|Zertifikate|PKI, selbstsigniert|

Wenn Sie physische Server verwenden, sollten Sie die Kapazität planen. Sie können das Tool zur Größenanpassung zum Zuweisen von Speicherplatz für ATA verwenden:

[Tool zur Größen](ata-capacity-planning.md) Anpassung von ATA: das Tool zur Größenanpassung automatisiert die Erfassung der Menge an Datenverkehr, die ATA benötigt. Es stellt automatisch Empfehlungen zu Unterstützbarkeit und Ressourcen für ATA Center und ATA-Lightweight-Gateways bereit.

[ATA-Kapazitätsplanung](ata-capacity-planning.md)

## <a name="deploy-ata"></a>Bereitstellung von ATA

Diese Ressourcen unterstützen Sie beim Download und bei der Installation von ATA Center, bei der Verbindung zu Active Directory, beim Download des ATA Gatewaypakets, beim Einrichten der Ereignissammlung und optional bei der Integration in Ihr VPN sowie bei der Einrichtung von Honeytoken-Konten und -Ausschlüssen.

[Herunterladen von ATA](https://aka.ms/ataeval): Wenn Sie sich vor der Bereitstellung von ATA noch nicht dazu entschieden haben, ATA käuflich zu erwerben, können Sie die Evaluierungsversion herunterladen.

[ATA POC-Playbook](/samples/browse/?redirectedfrom=TechNet-Gallery): Anleitung für alle Schritte für eine erfolgreiche ATA POC-Bereitstellung.

[Video zur ATA-Bereitstellung](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes): Dieses Video bietet eine Übersicht über die Schritte für die ATA-Bereitstellung in weniger als zehn Minuten.

## <a name="ata-settings"></a>ATA-Einstellungen

Die grundlegenden, erforderlichen Einstellungen in ATA werden als Teil des Installations-Assistenten konfiguriert. Es gibt jedoch eine Reihe anderer Einstellungen, die Sie zur Optimierung von ATA verwenden können, um die Erkennungen für Ihre Umgebung präziser durchzuführen, z.B. die SIEM-Integration und Überwachungseinstellungen.

[Überwachungseinstellungen](https://aka.ms/ataauditingblog): Überwachen Sie die Integrität Ihres Domänencontrollers vor und nach der ATA-Bereitstellung.

[Allgemeine ATA-Dokumentation](index.yml)

## <a name="work-with-ata"></a>Arbeiten mit ATA

Sobald ATA einsatzbereit ist, können Sie verdächtige Aktivitäten anzeigen, die in der Angriffszeitleiste erkannt werden. Dies ist die Standardzielseite, auf die Sie gelangen, wenn Sie sich bei der ATA-Konsole anmelden. Standardmäßig werden alle offenen verdächtigen Aktivitäten auf der Angriffszeitachse angezeigt. Außerdem wird der Schweregrad angezeigt, der den einzelnen Aktivitäten zugewiesen wurde. Untersuchen Sie jede verdächtige Aktivität, indem Sie zu den Entitäten (Computer, Geräte, Benutzer) navigieren, um deren Profilseiten zu öffnen, die weitere Informationen bereitstellen. Mithilfe folgender Ressourcen können Sie mit den verdächtigen Aktivitäten von ATA arbeiten:

[Verdächtige ATA-Aktivitäten – Playbook](/samples/browse/?redirectedfrom=TechNet-Gallery): Dieser Artikel führt Sie durch die Angriffstechniken für den Diebstahl von Anmeldeinformationen durch jederzeit verfügbare Recherchetools aus dem Internet. Zu jedem Zeitpunkt des Angriffs sehen Sie, wie ATA Ihnen dabei hilft, weitere Einblicken in diese Bedrohungen zu erhalten.

[Handbuch zu verdächtigen ATA-Aktivitäten](suspicious-activity-guide.md)

## <a name="security-best-practices"></a>Bewährte Sicherheitsmethoden

[Bewährte Methoden für ATA](https://aka.ms/atasecbestpractices): Bewährte Methoden zum Sichern von ATA.

[Häufig gestellte Fragen zu ATA](ata-technical-faq.md): Dieser Artikel enthält eine Reihe häufig gestellter Fragen zu ATA sowie Hintergrundwissen und Antworten.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

[Seite zu Microsoft Security Channel 9](https://channel9.msdn.com/Shows/Microsoft-Security/)

## <a name="community-resources"></a>Communityressourcen

[ATA-Blog](https://aka.ms/ATABlog) 
 [ATA-Community](https://aka.ms/ATACommunity)