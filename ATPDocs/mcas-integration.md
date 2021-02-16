---
title: Microsoft Defender für Identity in Microsoft Cloud App Security
description: Übersicht über Microsoft Defender für Identitäts Features in Microsoft Cloud App Security.
ms.date: 01/24/2021
ms.topic: how-to
ms.openlocfilehash: 93ece5c8345929984473b057fdad2d4eec6fb9c0
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533833"
---
# <a name="using-microsoft-defender-for-identity-with-microsoft-cloud-app-security"></a>Verwenden von Microsoft Defender für Identity mit Microsoft Cloud App Security

Dieser Artikel soll Ihnen dabei helfen, die erweiterte Untersuchung zu verstehen und zu navigieren, wenn Sie das Microsoft Cloud App Security-Portal mit verwenden [!INCLUDE [Product long](includes/product-long.md)] .

Durch die Nutzung vorhandener lokaler Erkennungen und ungewöhnlicher Verhaltensanalysen ermöglicht der Zugriff auf [!INCLUDE [Product short](includes/product-short.md)] das Microsoft Cloud App Security-Portal die zusätzliche Möglichkeit, sensible Daten im gesamten Unternehmen zu erkennen und zu warnen. Außerdem werden die Aktivitäten gefiltert und Richtlinien erstellt. Dieses Hybridangebot analysiert Aktivitäten und Warnungen basierend auf User and Entity Behavior Analytics (UEBA), um riskante Verhaltensweisen zu ermitteln, und bietet eine Bewertung der Untersuchungspriorität, um Ihre Reaktion auf Incidents bei gefährdeten Identitäten zu optimieren.

In diesem Artikel finden Sie Informationen zu Folgendem:

> [!div class="checklist"]
>
> - Übersicht über die Dienste
> - Neue Zugriffsmöglichkeiten [!INCLUDE [Product short](includes/product-short.md)]
> - Voraussetzungen für die Lizenzierung
> - Wo finden Sie nach [!INCLUDE [Product short](includes/product-short.md)] verfolgte Aktivitäten in Cloud App Security

## <a name="service-overview"></a>Übersicht über die Dienste

Die Integration [!INCLUDE [Product short](includes/product-short.md)] von in ermöglicht das Cloud App Security-Portal Warnungen und Einblicke aus:

- Microsoft Cloud App Security, das Angriffe innerhalb einer Cloudsitzung identifiziert und sich dabei nicht nur mit Microsoft-Produkten, sondern auch mit Anwendungen von Drittanbietern befasst
- [!INCLUDE [Product long](includes/product-long.md)], der Machine Learning und Verhaltensanalysen verwendet, um Angriffe in Ihrem lokalen Netzwerk zu erkennen.
- Azure Active Directory Identity Protection, das Benutzer- und Anmelderisiken bei Identitäten in der Cloud erkennt und proaktiv verhindert

## <a name="access-defender-for-identity"></a>Auf Defender für Identität zugreifen

Wählen Sie weiter [!INCLUDE [Product short](includes/product-short.md)] im [!INCLUDE [Product short](includes/product-short.md)] Portal aus, oder greifen Sie [!INCLUDE [Product short](includes/product-short.md)] über das Microsoft Cloud App Security Portal auf Warnungen und Identitäts Bewertung zu. Im Workflow [!INCLUDE [Product short](includes/product-short.md)] werden die Einrichtungs-und Konfigurations Tasks weiterhin im [!INCLUDE [Product short](includes/product-short.md)] Portal verarbeitet.

## <a name="prerequisites"></a>Voraussetzungen

Zur Nutzung aller Features der Benutzeruntersuchung über die gesamte Hybridumgebung hinweg benötigen Sie Folgendes:

- Eine gültige Lizenz für Microsoft Cloud App Security
- Eine gültige Lizenz für [!INCLUDE [Product long](includes/product-long.md)] die Verbindung mit Ihrer Active Directory Instanz

>[!NOTE]
>
> - Wenn Sie nicht über ein Abonnement für Cloud App Security verfügen, können Sie weiterhin das Cloud App Security-Portal verwenden, um Warnungen zu untersuchen [!INCLUDE [Product short](includes/product-short.md)] und ausführliche Informationen zu Benutzern und Ihren lokalen, verwalteten Aktivitäten zu erhalten. Sie erhalten jedoch keine relevanten Einblicke in Ihre cloudanwendungen.
> - [!INCLUDE [Product short](includes/product-short.md)] Administratoren benötigen möglicherweise neue Berechtigungen für den Zugriff auf Cloud App Security. Informationen zum Zuweisen von Berechtigungen zu Cloud App Security finden Sie unter [Administratorzugriff verwalten](/cloud-app-security/manage-admins).

Weitere Informationen zum schnellen Aktivieren von in Cloud App Security finden Sie unter [ [!INCLUDE [Product short](includes/product-short.md)] Integration](/cloud-app-security/mdi-integration) [!INCLUDE [Product short](includes/product-short.md)] .

## <a name="defender-for-identity-in-cloud-app-security"></a>Defender für Identity in Cloud App Security

Lesen Sie die [Schnellstartanleitung für Cloud App Security](/cloud-app-security/getting-started-with-cloud-app-security), um sich mit den Grundlagen der Verwendung des Cloud App Security-Portals vertraut zu machen.

Greifen Sie [!INCLUDE [Product short](includes/product-short.md)] in Cloud App Security Warnungen, Aktivitäten und Benutzer Seiten auf Ihre Daten und ihre neuen Hybrid Features zu.

## <a name="alerts"></a>Alerts

[!INCLUDE [Product short](includes/product-short.md)] Warnungen werden in der Warteschlange Cloud App Security **Warnungen** angezeigt. Zusätzliche Filteroptionen stehen nur beim Anzeigen von Warnungen über Cloud App Security zur Verfügung. [!INCLUDE [Product short](includes/product-short.md)] Warnungen werden mithilfe des Anwendungs Filters gefiltert, um **Active Directory**.

## <a name="alert-management"></a>Alert Management

Wenn [!INCLUDE [Product short](includes/product-short.md)] Sie mit Cloud App Security verwenden, schließen Sie Warnungen in einem Dienst nicht automatisch im anderen Dienst. Genauer gesagt: durch das Schließen von Warnungen in Cloud App Security werden diese nicht in Defender für die Identität geschlossen, aber das Schließen von Warnungen in Defender für Identity synchronisiert die Schließung in Cloud App Security. Legen Sie fest, in welchem Dienst Warnungen verwaltet und behoben werden sollen, um doppelten Aufwand zu vermeiden.

## <a name="siem-notification"></a>SIEM-Benachrichtigungen

Wenn Ihre Dienste ( [!INCLUDE [Product short](includes/product-short.md)] und Cloud App Security) zurzeit so konfiguriert sind, dass Sie Warn Benachrichtigungen an eine Siem-Lösung sendet, [!INCLUDE [Product short](includes/product-short.md)] erhalten Sie nach dem Aktivieren der Integration in Cloud App Security doppelte Siem-Benachrichtigungen für die gleiche Warnung. Von jedem Dienst wird eine Warnung mit unterschiedlicher Warnungs-ID ausgegeben. Entscheiden Sie, in welchem Dienst Sie Warnungen verwalten möchten, und legen Sie anschließend fest, dass vom anderen Dienst keine SIEM-Benachrichtigungen mehr versendet werden. So vermeiden Sie Duplizierungen und Verwirrung.

## <a name="activities"></a>activities

[!INCLUDE [Product short](includes/product-short.md)] Warnungen werden innerhalb des Cloud App Security **Aktivitäts Protokolls** angezeigt. Zusätzliche Optionen und Features für die Aktivitätsfilterung stehen nur beim Anzeigen von Warnungen über Cloud App Security zur Verfügung. Weitere Informationen zum Filtern und Erstellen neuer Aktivitätsrichtlinien finden Sie unter [ [!INCLUDE [Product short](includes/product-short.md)] Aktivitäten mithilfe von Microsoft Cloud App Security](activities-filtering-mcas.md) .

## <a name="user-pages"></a>Benutzerseiten

Benutzerseiten enthalten die [Bewertung der Untersuchungspriorität](/cloud-app-security/tutorial-ueba) für jeden Benutzer sowie ein Aktivitätsprotokoll aller Aktionen.

So greifen Sie auf die Benutzerseite eines Systembenutzers zu:

1. Öffnen Sie im Hauptmenü die Option **Warnungen**.
1. Wählen Sie mithilfe des Felds **Benutzername** die Warnungswarteschlange für einen bestimmten Benutzer aus, und filtern Sie diese.

 oder

1. Wählen Sie im Menü **Untersuchen** die Option **Aktivitätsprotokoll** aus.
1. Filtern Sie die Warteschlange des Aktivitätsprotokolls nach Benutzer.

    ![Aktivitätsprotokoll](media/mcas-activity-filter.png)

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zum Filtern und Erstellen neuer Aktivitätsrichtlinien finden Sie unter [ [!INCLUDE [Product short](includes/product-short.md)] Aktivitäten mithilfe von Microsoft Cloud App Security](activities-filtering-mcas.md) .

## <a name="join-the-community"></a>Beitritt zur Community

Haben Sie weitere Fragen, oder möchten Sie mit anderen über [!INCLUDE [Product short](includes/product-short.md)] und damit verbundene Sicherheitsaspekte diskutieren? Treten Sie noch heute der [[!INCLUDE [Product short](includes/product-short.md)]Community](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) bei.
