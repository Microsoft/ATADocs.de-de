---
title: "Ressourcen für Advanced Threat Analytics und Roadmap für die Bereitschaft | Microsoft-Dokumentation"
description: "Stellt eine Liste von Links zu ATA-Ressourcen, Videos, ersten Schritten sowie zur Bereitstellung und zum Überblick für die Bereitschaft bereit."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 1/15/2018
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 42a1a34f-ed6b-4538-befb-452168a30e8c
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 33aec9dd89fc189144387e59c3b48b9d440936d2
ms.sourcegitcommit: 55f7ac32bcd4ac8edb8b8b3b47993bf96b9acce2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/15/2018
---
*Gilt für: Advanced Threat Analytics Version 1.8*

# <a name="ata-readiness-roadmap"></a>Überblick über die ATA-Bereitschaft 
Dieses Dokument bietet einen Überblick über die Bereitschaft, der Ihnen beim Einstieg mit Advanced Threat Analytics hilft.

## <a name="understanding-ata"></a>Grundlegendes zu ATA

Advanced Threat Analytics (ATA) ist eine lokale Plattform, mit deren Hilfe Sie Ihr Unternehmen vor verschiedenen hochentwickelten und gezielten Cyberangriffen und Insiderbedrohungen schützen können. In den folgenden Artikeln finden Sie weitere Informationen zu ATA zu erhalten:

- [ATA-Übersicht](https://aka.ms/ATAOverview)

- [Einführungsvideo zu ATA (kurz)](https://aka.ms/ATAShort)

- [Einführungsvideo zu ATA (lang)](https://aka.ms/ATAVideo) 


## <a name="deployment-decisions"></a>Entscheidungen für die Bereitstellung

ATA besteht aus ATA Center, das Sie auf einem Server installieren können, sowie aus ATA Gateways, die Sie auf separaten Computern oder mithilfe von Lightweight-Gateways direkt auf Ihren Domänencontrollern installieren können. Bevor Sie loslegen ist es wichtig, folgende Entscheidungen zur Bereitstellung zu treffen:

|KONFIGURATION|ENTSCHEIDUNG|
|----|----|
|Hardwaretyp|Physische, virtuelle, Azure-VM|
|Arbeitsgruppe oder Domäne|Arbeitsgruppe, Domäne|
|Bemessung von Gateways|Vollständiges Gateway, Lightweight-Gateway|
|Zertifikate|PKI, selbstsigniert|

Wenn Sie physische Server verwenden, sollten Sie die Kapazität planen. Sie können das Tool zur Größenanpassung zum Zuweisen von Speicherplatz für ATA verwenden:

[ATA-Tool zur Größenanpassung](http://aka.ms/atasizing): Das Tool zur Größenanpassung automatisiert die Auflistung der Menge an Datenverkehr, die von ATA benötigt wird. Es stellt automatisch Empfehlungen zu Unterstützbarkeit und Ressourcen für ATA Center und ATA-Lightweight-Gateways bereit.

[ATA-Kapazitätsplanung](https://docs.microsoft.com/en-us/advanced-threat-analytics/ata-capacity-planning)

## <a name="deploy-ata"></a>Bereitstellung von ATA

Die folgenden Artikel enthalten Informationen zum Download und zur Installation von ATA Center, zur Verbindung zu Active Directory, beim Download des ATA-Gatewaypakets, zum Einrichten der Ereignissammlung und optional zur Integration in Ihr VPN und zur Einrichtung von Honeytokenkonten und -ausschlüssen.

[Herunterladen von ATA](http://aka.ms/ataeval): Wenn Sie sich vor der Bereitstellung von ATA noch nicht dazu entschieden haben, ATA käuflich zu erwerben, können Sie die Evaluierungsversion herunterladen. 

[ATA POC-Playbook](http://aka.ms/atapoc): Anleitung für alle Schritte für eine erfolgreiche ATA POC-Bereitstellung.

[Video zur ATA-Bereitstellung](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes): Dieses Video bietet eine Übersicht über die Schritte für die ATA-Bereitstellung in weniger als zehn Minuten.

## <a name="ata-settings"></a>ATA-Einstellungen

Die grundlegenden, erforderlichen Einstellungen in ATA werden als Teil des Installations-Assistenten konfiguriert. Es gibt jedoch eine Reihe anderer Einstellungen, die Sie zur Optimierung von ATA verwenden können, um die Erkennungen für Ihre Umgebung präziser durchzuführen, z.B. die SIEM-Integration oder Überwachungseinstellungen.

[Überwachungseinstellungen](https://aka.ms/ataauditingblog): Überwachen Sie die Integrität Ihres Domänencontrollers vor und nach der ATA-Bereitstellung.

[Allgemeine ATA-Dokumentation](https://docs.microsoft.com/en-us/advanced-threat-analytics/)

## <a name="work-with-ata"></a>Arbeiten mit ATA

Sobald ATA einsatzbereit ist, können Sie verdächtige Aktivitäten anzeigen, die in der Angriffszeitleiste erkannt werden. Dies ist die Standardzielseite, auf die Sie gelangen, wenn Sie sich bei der ATA-Konsole anmelden. Standardmäßig werden alle offenen verdächtigen Aktivitäten auf der Angriffszeitachse angezeigt. Außerdem wird der Schweregrad angezeigt, der den einzelnen Aktivitäten zugewiesen wurde. Untersuchen Sie jede verdächtige Aktivität, indem Sie zu den Entitäten (Computer, Geräte, Benutzer) navigieren, um deren Profilseiten zu öffnen, die weitere Informationen bereitstellen. Mithilfe folgender Ressourcen können Sie mit den verdächtigen Aktivitäten von ATA arbeiten:

[Verdächtige ATA-Aktivitäten – Playbook](http://aka.ms/ataplaybook): Dieser Artikel führt Sie durch die Angriffstechniken für den Diebstahl von Anmeldeinformationen durch jederzeit verfügbare Recherchetools aus dem Internet. Zu jedem Zeitpunkt des Angriffs sehen Sie, wie ATA Ihnen dabei hilft, weitere Einblicken in diese Bedrohungen zu erhalten.

[Handbuch zu verdächtigen ATA-Aktivitäten](http://aka.ms/atasaguide)



## <a name="security-best-practices"></a>Bewährte Methoden für die Sicherheit

[Bewährte Methoden für ATA](https://aka.ms/atasecbestpractices): Bewährte Methoden zum Sichern von ATA.

[Häufig gestellte Fragen zu ATA](http://aka.ms/atafaq): Dieser Artikel enthält eine Reihe häufig gestellter Fragen zu ATA sowie Hintergrundwissen und Antworten.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

[Seite zu Microsoft Security Channel 9](https://channel9.msdn.com/Shows/Microsoft-Security/)

## <a name="community-resources"></a>Communityressourcen

[ATA-Blog](https://aka.ms/ATABlog)
[ATA-Community](https://aka.ms/ATACommunity)
[Feedback zu ATA](https://aka.ms/ATAUserVoice)