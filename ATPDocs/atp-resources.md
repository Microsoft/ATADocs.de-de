---
title: Liste nützlicher Ressourcen für Azure Advanced Threat Protection | Microsoft-Dokumentation
description: Dieser Artikel enthält eine Liste nützlicher Ressourcen für Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/24/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 34dc152c-6b7f-4128-93fe-aad56c282730
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2249505a80eca230e9b5b54689414c445f169afc
ms.sourcegitcommit: 0f3ee3241895359d5cecd845827cfba1fdca9317
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/29/2019
ms.locfileid: "75544354"
---
# <a name="azure-atp-readiness-guide"></a>Handbuch für die Azure ATP-Bereitschaft

Dieser Artikel stellt einen Überblick über die Bereitschaft bereit, der eine Liste der Ressourcen enthält, die Sie bei den ersten Schritten mit Azure Advanced Threat Protection unterstützt. 

## <a name="understanding-azure-atp"></a>Grundlegendes zu Azure ATP

Bei Azure Advanced Threat Protection (ATP) handelt es sich um einen Clouddienst, mit dem Sie Ihr Unternehmen vor verschiedenen hochentwickelten und gezielten Cyberangriffen und Bedrohungen von innen schützen können.
 
Weitere Informationen zu Azure ATP: 
- [Übersicht über Azure ATP](what-is-atp.md)
- [Einführungsvideo zu Azure ATP (vollständig, 25 Minuten)](https://www.youtube.com/watch?v=EGY2m8yU_KE)
- [Ausführliches Video zu Azure ATP (vollständig, 75 Minuten)](https://www.youtube.com/watch?v=QXZIfH0wP3Q)

## <a name="deployment-decisions"></a>Entscheidungen für die Bereitstellung

Azure ATP besteht aus dem Clouddienst von Azure sowie aus integrierten Sensoren, die auf einem Domänencontroller oder auf eigenständigen Sensoren auf dedizierten Servern installiert werden können. Bevor Sie Azure ATP einrichten, sollten Sie den Typ der Sensoren auswählen, der am besten zu Ihrer Bereitstellung und Ihren Anforderungen passen. In Azure ATP integrierte Sensoren (bzw. Azure ATP-Sensoren) zeichnen sich durch eine höhere Sicherheit, niedrige Betriebskosten und eine einfachere Bereitstellung als eigenständige Azure ATP-Sensoren aus. Eigenständige Azure ATP-Sensoren erfordern physische Hardware, zusätzliche Konfigurationsschritte und umfangreichere Betriebskosten. <br>Beim Einsatz physischer Server ist die Kapazitätsplanung von entscheidender Bedeutung. Sie können das Tool zur Größenanpassung zum Zuweisen von Speicherplatz für Ihre Sensoren verwenden: 
- [Azure ATP-Tool zur Größenanpassung](https://aka.ms/aatpsizingtool): Das Tool zur Größenanpassung automatisiert die Auflistung der Menge an Datenverkehr, den Azure ATP überwacht. Es stellt automatisch Empfehlungen zur Unterstützbarkeit und Ressourcen für Sensoren bereit. 
- [Handbuch zur ATP-Kapazitätsplanung](atp-capacity-planning.md)

## <a name="deploy-azure-atp"></a>Bereitstellen von Azure ATP

Diese Ressourcen unterstützen Sie beim Einrichten von Azure ATP, bei der Verbindung zu Active Directory, beim Download des Sensorpakets, beim Einrichten der Ereignissammlung und optional bei der Integration in Ihr VPN und bei der Einrichtung von Honeytoken-Konten und -Ausschlüssen. 
- [Testen Sie Azure ATP (Teil von EMS E5):](https://aka.ms/aatptrial) Die Testversion ist 90 Tage gültig.
- [Azure ATP-Setup:](install-atp-step1.md) Führen Sie diese Schritte aus, um Azure ATP in Ihrer Umgebung bereitzustellen.
- [Integrieren von Azure ATP in Windows Defender ATP](integrate-wd-atp.md)

## <a name="azure-atp-settings"></a>Einstellungen für Azure ATP

Beim Erstellen der Azure ATP werden die erforderlichen Grundeinstellungen automatisch konfiguriert. Es gibt einige zusätzliche konfigurierbare Einstellungen in Azure ATP, um die Erkennungen und Warnung für Ihre Umgebung präziser durchzuführen, z.B. VPN-Integration, erforderliche Berechtigungen für SAM (Software Asset Management) sowie erweiterte Einstellungen für Überwachungsrichtlinien. 

- [VPN-Integration](install-atp-step6-vpn.md)
- [Erforderliche Berechtigungen für SAM-R](install-atp-step8-samr.md)
- [Überwachungsrichtlinieneinstellungen:](atp-advanced-audit-policy.md) Überwachen Sie die Integrität Ihres Domänencontrollers vor und nach einer ATP-Bereitstellung. 

## <a name="work-with-azure-atp"></a>Arbeiten mit Azure ATP

Sobald Azure ATP einsatzbereit ist, können Sie Sicherheitswarnungen in der Aktivitätszeitachse des Azure ATP-Portals anzeigen. Die Zeitachse für Aktivitäten ist die standardmäßige Landing Page nach der Anmeldung beim Azure ATP-Portal. Standardmäßig werden alle offenen Sicherheitswarnungen auf der Aktivitätszeitachse angezeigt. Außerdem wird der Schweregrad angezeigt, der den einzelnen Warnungen zugewiesen wurde. Untersuchen Sie jede Warnung, indem Sie einen Drilldown zu den Entitäten (Computer, Geräte, Benutzer) ausführen, um deren Profilseiten mit weiteren Informationen zu öffnen. Lateral Movement-Pfade zeigen mögliche Bewegungen, die in Ihrem Netzwerk vorgenommen werden können, und gefährdete sensible Benutzer. Anhand der Graphs zur Erkennung des Lateral Movement-Pfads können Sie die Offenlegung erkennen und beheben. Mithilfe folgender Ressourcen können Sie mit den Sicherheitswarnungen von Azure ATP arbeiten: 

- [ (Handbuch zu Sicherheitswarnungen bei Azure ATP):](suspicious-activity-guide.md) Erfahren Sie mehr über die Selektierung und die nächsten Schritte mit Azure ATP-Erkennungen.
- [Azure ATP-Lateral Movement-Pfade](use-case-lateral-movement-path.md)
- [Tag groups as sensitive (Kennzeichnen von Gruppen als vertraulich):](sensitive-accounts.md) Erhalten Sie Einblicke in die Offenlegung von Anmeldeinformationen bei vertraulichen Sicherheitsgruppen.

## <a name="security-best-practices"></a>Bewährte Sicherheitsmethoden

- [Häufig gestellte Fragen zu Azure ATP:](atp-technical-faq.md) Dieser Artikel enthält einige häufig gestellter Fragen zu Azure ATP sowie Hintergrundwissen und Antworten. 

## <a name="community-resources"></a>Communityressourcen

Blog: [Azure ATP-Blog](https://aka.ms/aatpblog)

Öffentliche Community: [Tech-Community für Azure ATP](https://aka.ms/AatpCom)

Private Community: [Yammer-Gruppe für Azure ATP](https://www.yammer.com/azureadvisors/#/threads/inGroup?type=in_group&feedId=9386893&view=all)

Channel 9: [Seite zu Microsoft Security Channel 9](https://channel9.msdn.com/Shows/Microsoft-Security/)



## <a name="see-also"></a>Weitere Informationen

- [Working with sensitive accounts (Arbeiten mit sensiblen Konten)](sensitive-accounts.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
