---
title: Liste nützlicher Ressourcen für Azure Advanced Threat Protection | Microsoft-Dokumentation
description: Dieser Artikel enthält eine Liste nützlicher Ressourcen für Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/29/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 34dc152c-6b7f-4128-93fe-aad56c282730
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b8d91468664a76436078772ad1fc8510ea56d67a
ms.sourcegitcommit: 5c0f914b44bfb8e03485f12658bfa9a7cd3d8bbc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/30/2018
ms.locfileid: "32298483"
---
*Gilt für: Azure Advanced Threat Protection*



# <a name="azure-atp-readiness-guide"></a>Handbuch für die Azure ATP-Bereitschaft

Dieser Artikel stellt einen Überblick über die Bereitschaft bereit, der eine Liste der Ressourcen enthält, die Sie bei den ersten Schritten mit Azure Advanced Threat Protection unterstützt. 

## <a name="understanding-azure-atp"></a>Grundlegendes zu Azure ATP

Bei Azure Advanced Threat Protection (ATP) handelt es sich um einen Clouddienst, mit dem Sie Ihr Unternehmen vor verschiedenen hochentwickelten und gezielten Cyberangriffen und Bedrohungen von innen schützen können. In den folgenden Artikeln finden Sie weitere Informationen zu Azure ATP: 
- [Übersicht über Azure ATP](what-is-atp.md)
- [Einführungsvideo zu Azure ATP (vollständig)](https://www.youtube.com/watch?v=KX-xpFc0sBw) 

## <a name="deployment-decisions"></a>Entscheidungen für die Bereitstellung

Azure ATP besteht aus dem Clouddienst von Azure sowie aus Sensoren, die auf einem Domänencontroller oder auf dedizierten Servern installiert werden können. Bevor Sie Azure ATP einrichten, sollten Sie auswählen, welche Sensoren am besten zu Ihrer Bereitstellung passen.<br>Wenn Sie physische Server verwenden, sollten Sie die Kapazität planen. Sie können das Tool zur Größenanpassung zum Zuweisen von Speicherplatz für Ihre Sensoren verwenden: 
- [Azure ATP-Tool zur Größenanpassung](http://aka.ms/aatpsizingtool): Das Tool zur Größenanpassung automatisiert die Auflistung der Menge an Datenverkehr, den Azure ATP überwacht. Es stellt automatisch Empfehlungen zur Unterstützbarkeit und Ressourcen für Sensoren bereit. 
- [Handbuch zur ATA-Kapazitätsplanung](atp-capacity-planning.md)

## <a name="deploy-azure-atp"></a>Bereitstellen von Azure ATP

Diese Ressourcen unterstützen Sie beim Einrichten von Azure ATP, bei der Verbindung zu Active Directory, beim Download des Sensorpakets, beim Einrichten der Ereignissammlung und optional bei der Integration in Ihr VPN und bei der Einrichtung von Honeytoken-Konten und -Ausschlüssen. 
- [Testen Sie Azure ATP (Teil von EMS E5):](http://aka.ms/aatptrial) Die Testversion ist 90 Tage gültig.
- [Bereitstellungshandbuch:](install-atp-step1.md) Stellen Sie Azure ATP in Ihrer Umgebung bereit, indem Sie diese Schritte befolgen.
- [Integrieren von Azure ATP in Windows Defender ATP](integrate-wd-atp.md)
- 
## <a name="azure-atp-settings"></a>Einstellungen für Azure ATP

Diese grundlegenden erforderlichen Einstellungen in Azure ATP werden bei der Erstellung des Arbeitsbereichs konfiguriert. Es gibt jedoch einige andere Einstellungen, die Sie zur Optimierung von Azure ATP verwenden können, um die Erkennungen für Ihre Umgebung präziser durchzuführen, z.B. die SIEM-Integration oder Überwachungseinstellungen. 

- [Allgemeine ATP-Dokumentation](what-is-atp.md)
- [Überwachungseinstellungen](https://blogs.technet.microsoft.com/positivesecurity/2017/08/18/ata-auditing-auditpol-advanced-audit-settings-enforcement-lightweight-gateway-service-discovery/): Überwachen Sie die Integrität Ihres Domänencontrollers vor und nach der ATA-Bereitstellung. 

## <a name="work-with-azure-atp"></a>Arbeiten mit Azure ATP

Sobald Azure ATP einsatzbereit ist, können Sie verdächtige Aktivitäten anzeigen, die in der Zeitachse für Aktivitäten erkannt werden. Dies ist die Standardseite, auf die Sie gelangen, wenn Sie sich im Azure ATP-Portal anmelden. Standardmäßig werden alle offenen verdächtigen Aktivitäten auf der Angriffszeitachse angezeigt. Außerdem wird der Schweregrad angezeigt, der den einzelnen Aktivitäten zugewiesen wurde. Untersuchen Sie jede verdächtige Aktivität, indem Sie zu den Entitäten (Computer, Geräte, Benutzer) navigieren, um deren Profilseiten zu öffnen, die weitere Informationen bereitstellen. Mithilfe folgender Ressourcen können Sie mit den verdächtigen Aktivitäten von Azure ATP arbeiten: 

- [Azure ATP suspicious activity guide (Handbuch zu verdächtigen Aktivitäten bei Azure ATP):](suspicious-activity-guide.md) Erfahren Sie mehr über die Selektierung und die nächsten Schritte mit Azure ATP-Erkennungen.
- [Tag groups as sensitive (Kennzeichnen von Gruppen als vertraulich):](sensitive-accounts.md) Erhalten Sie Einblicke in die Offenlegung von Anmeldeinformationen bei vertraulichen Sicherheitsgruppen.

## <a name="security-best-practices"></a>Bewährte Sicherheitsmethoden

- [Häufig gestellte Fragen zu Azure ATP:](atp-technical-faq.md) Dieser Artikel enthält einige häufig gestellter Fragen zu Azure ATP sowie Hintergrundwissen und Antworten. 
## <a name="community-resources"></a>Communityressourcen

Blog: [Azure ATP-Blog](https://aka.ms/aatpblog)

Öffentliche Community: [Tech Community für Azure ATP](https://aka.ms/AatpCom)

Private Community: [Yammer-Gruppe für Azure ATP](https://www.yammer.com/azureadvisors/#/threads/inGroup?type=in_group&feedId=9386893&view=all)

Channel 9: [Seite zu Microsoft Security Channel 9](https://channel9.msdn.com/Shows/Microsoft-Security/)



## <a name="see-also"></a>Siehe auch

- [Working with sensitive accounts (Arbeiten mit sensiblen Konten)](sensitive-accounts.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)