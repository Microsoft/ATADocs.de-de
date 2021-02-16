---
title: Liste der hilfreichen Ressourcen für Microsoft Defender für Identity
description: Dieser Artikel enthält eine Liste hilfreicher Ressourcen für Microsoft Defender für Identity.
ms.date: 10/27/2020
ms.topic: conceptual
ms.openlocfilehash: 8a814a51fdc63f59b36288922017280e0d7f3968
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533306"
---
# <a name="microsoft-defender-for-identity-readiness-guide"></a>Leitfaden für Microsoft Defender für die Identitäts Bereitschaft

In diesem Artikel erhalten Sie eine Roadmap-Liste mit Ressourcen, die Ihnen beim Einstieg in helfen [!INCLUDE [Product long](includes/product-long.md)] .

## <a name="understanding-microsoft-defender-for-identity"></a>Grundlegendes zu Microsoft Defender für Identity

[!INCLUDE [Product long](includes/product-long.md)] ist ein clouddienst, der Ihnen hilft, Ihr Unternehmen vor verschiedenen Typen von erweiterten gezielten Cyberangriffen und Insider Bedrohungen zu identifizieren und zu schützen.

Weitere Informationen zu [!INCLUDE [Product short](includes/product-short.md)] finden Sie unter:

- [[!INCLUDE [Product short](includes/product-short.md)] – Übersicht](what-is.md)
- [[!INCLUDE [Product short](includes/product-short.md)] Einführungsvideo (25 Minuten)-vollständig](https://www.youtube.com/watch?v=EGY2m8yU_KE)
- [[!INCLUDE [Product short](includes/product-short.md)] Deep Dive-Video (75 Minuten)-vollständig](https://www.youtube.com/watch?v=QXZIfH0wP3Q)

## <a name="deployment-decisions"></a>Entscheidungen für die Bereitstellung

[!INCLUDE [Product short](includes/product-short.md)] besteht aus einem clouddienst in Azure und integrierten Sensoren, die auf Domänen Controllern installiert werden können. Beim Einsatz physischer Server ist die Kapazitätsplanung von entscheidender Bedeutung. Sie können das Tool zur Größenanpassung zum Zuweisen von Speicherplatz für Ihre Sensoren verwenden:

- [ [!INCLUDE [Product short](includes/product-short.md)] Tool zur Größen](https://aka.ms/aatpsizingtool) Anpassung: das Tool zur Größenanpassung automatisiert die Erfassung der Menge an Datenverkehrs [!INCLUDE [Product short](includes/product-short.md)] Monitoren. Es stellt automatisch Empfehlungen zur Unterstützbarkeit und Ressourcen für Sensoren bereit.
- [[!INCLUDE [Product short](includes/product-short.md)] Leitfaden zur Kapazitätsplanung](capacity-planning.md)

## <a name="deploy-defender-for-identity"></a>Bereitstellen von Defender für Identity

Verwenden Sie diese Ressourcen, um die Einrichtung [!INCLUDE [Product short](includes/product-short.md)] , Verbindung mit Active Directory, das Herunterladen des Sensor Pakets, das Einrichten der Ereignis Sammlung und optional das integrieren in Ihr VPN und das Einrichten von honeytoken-Konten und-Ausschlüsse zu unterstützen.

- [Try [!INCLUDE [Product short](includes/product-short.md)] (Teil von EMS E5)](https://aka.ms/aatptrial)  die Testversion ist 90 Tage gültig.
- [ [!INCLUDE [Product short](includes/product-short.md)] ](install-step1.md) Führen Sie die folgenden Schritte aus, um [!INCLUDE [Product short](includes/product-short.md)] in Ihrer Umgebung bereitzustellen.
- [Integration [!INCLUDE [Product short](includes/product-short.md)] in Microsoft Defender for Endpoint](integrate-mde.md)

## <a name="defender-for-identity-settings"></a>Defender für Identitäts Einstellungen

Wenn Sie [!INCLUDE [Product short](includes/product-short.md)] die-Instanz erstellen, werden die grundlegenden Einstellungen automatisch konfiguriert. Es gibt mehrere zusätzliche konfigurierbare Einstellungen in, [!INCLUDE [Product short](includes/product-short.md)] um die Erkennung und Warnungs Genauigkeit für Ihre Umgebung zu verbessern, wie z. b. VPN-Integration, Sam required-Berechtigungen und erweiterte Überwachungs Richtlinien Einstellungen.

- [VPN-Integration](install-step6-vpn.md)
- [Erforderliche Berechtigungen für SAM-R](install-step8-samr.md)
- Überwachungs [Richtlinien Einstellungen](configure-windows-event-collection.md) – überwachen Sie die Integrität des Domänen Controllers vor und nach der [!INCLUDE [Product short](includes/product-short.md)] Bereitstellung.

## <a name="work-with-defender-for-identity"></a>Arbeiten mit Defender für Identity

Nachdem [!INCLUDE [Product short](includes/product-short.md)] ausgeführt wurde und ausgeführt wird, können Sie Sicherheitswarnungen auf der [!INCLUDE [Product short](includes/product-short.md)] Portal Aktivitäts Zeitachse anzeigen. Die Aktivitäts Zeitachse ist die Standard-Landing Page, nachdem Sie sich beim Portal angemeldet haben [!INCLUDE [Product short](includes/product-short.md)] . Standardmäßig werden alle offenen Sicherheitswarnungen auf der Aktivitätszeitachse angezeigt. Außerdem wird der Schweregrad angezeigt, der den einzelnen Warnungen zugewiesen wurde. Untersuchen Sie jede Warnung, indem Sie einen Drilldown zu den Entitäten (Computer, Geräte, Benutzer) ausführen, um deren Profilseiten mit weiteren Informationen zu öffnen. Lateral Movement-Pfade zeigen mögliche Bewegungen, die in Ihrem Netzwerk vorgenommen werden können, und gefährdete sensible Benutzer. Anhand der Graphs zur Erkennung des Lateral Movement-Pfads können Sie die Offenlegung erkennen und beheben. Diese Ressourcen helfen Ihnen bei der Arbeit mit [!INCLUDE [Product short](includes/product-short.md)] den Sicherheitswarnungen:

- [ [!INCLUDE [Product short](includes/product-short.md)] Sicherheits](suspicious-activity-guide.md) Warnungs Handbuch erlernen Sie die Selektierung, und führen Sie die nächsten Schritte mit Ihren [!INCLUDE [Product short](includes/product-short.md)] Erkennungen aus.
- [[!INCLUDE [Product short](includes/product-short.md)] Lateral Movement-Pfade](use-case-lateral-movement-path.md)
- [Tag groups as sensitive (Kennzeichnen von Gruppen als vertraulich):](sensitive-accounts.md) Erhalten Sie Einblicke in die Offenlegung von Anmeldeinformationen bei vertraulichen Sicherheitsgruppen.

## <a name="security-best-practices"></a>Bewährte Sicherheitsmethoden

- [ [!INCLUDE [Product short](includes/product-short.md)] Häufig gestellte Fragen](technical-faq.yml) : Dieser Artikel enthält eine Liste mit häufig gestellten Fragen zu [!INCLUDE [Product short](includes/product-short.md)] und bietet Einblicke und Antworten.

## <a name="community-resources"></a>Communityressourcen

Blog: [ [!INCLUDE [Product short](includes/product-short.md)] Blog](https://aka.ms/aatpblog)

Public Community: [ [!INCLUDE [Product short](includes/product-short.md)] Tech Community](https://aka.ms/AatpCom)

Private Community: [ [!INCLUDE [Product short](includes/product-short.md)] Yammer-Gruppe](https://www.yammer.com/azureadvisors/#/threads/inGroup?type=in_group&feedId=9386893&view=all&preserve-view=true)

Channel 9: [Seite zu Microsoft Security Channel 9](https://channel9.msdn.com/Shows/Microsoft-Security/)

## <a name="see-also"></a>Weitere Informationen

- [Working with sensitive accounts (Arbeiten mit sensiblen Konten)](sensitive-accounts.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
