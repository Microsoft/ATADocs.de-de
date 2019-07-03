---
title: Azure Advanced Threat Protection in Microsoft Cloud App Security | Microsoft-Dokumentation
description: Übersicht über die Azure ATP-Features in Microsoft Cloud App Security.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 06/18/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 5169dffc-75c4-4eb0-b997-b5359cecda97
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 1e64ccfd3f559f59b0091e49a51e2016ef3f8745
ms.sourcegitcommit: 87756e27894570997b7039d128f223de0664639f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/18/2019
ms.locfileid: "67193495"
---
# <a name="using-azure-atp-with-microsoft-cloud-app-security"></a>Verwenden von Azure ATP mit Microsoft Cloud App Security 


Dieser Artikel bietet grundlegende Informationen sowie Tipps zur Navigation in der erweiterten Benutzeroberfläche für Untersuchungen, wenn Sie das Microsoft Cloud App Security-Portal mit Azure ATP verwenden. 

Beim Zugriff auf Azure ATP über das Microsoft Cloud App Security-Portal werden vorhandene lokale Ermittlungen und Analysen von ungewöhnlichen Verhaltensweisen genutzt – so können Sie eine Exfiltration von vertraulichen Daten in Ihrem gesamten Unternehmen erkennen und entsprechende Warnungen ausgeben. Darüber hinaus können Sie Aktivitäten filtern und umsetzbare Richtlinien erstellen. Dieses Hybridangebot analysiert Aktivitäten und Warnungen basierend auf User and Entity Behavior Analytics (UEBA), um riskante Verhaltensweisen zu ermitteln, und bietet eine Bewertung der Untersuchungspriorität, um Ihre Reaktion auf Incidents bei gefährdeten Identitäten zu optimieren. 

In diesem Artikel finden Sie Informationen zu Folgendem:

> [!div class="checklist"]
> * Dienstübersicht
> * Neue Möglichkeiten für den Zugriff auf Azure ATP
> * Voraussetzungen für die Lizenzierung
> * Von Azure ATP nachverfolgte Aktivitäten in Cloud App Security

## <a name="service-overview"></a>Dienstübersicht

Durch die Integration in Azure ATP bietet das Cloud App Security-Portal Warnungen und Erkenntnisse aus folgenden Diensten:
- Microsoft Cloud App Security, das Angriffe innerhalb einer Cloudsitzung identifiziert und sich dabei nicht nur mit Microsoft-Produkten, sondern auch mit Anwendungen von Drittanbietern befasst
- Azure Advanced Threat Protection – identifiziert Angriffe in Ihrem gesamten lokalen Netzwerk anhand von Verhaltensanalysen
- Azure Active Directory Identity Protection, das Benutzer- und Anmelderisiken bei Identitäten in der Cloud erkennt und proaktiv verhindert

## <a name="access-azure-atp"></a>Zugriff auf Azure ATP

Sie können weiterhin Azure ATP im Azure ATP-Portal nutzen oder über das Microsoft Cloud App Security-Portal auf Azure ATP-Warnungen und -Identitätsbewertungen zugreifen. In beiden Workflows werden Einrichtungs- und Konfigurationsaufgaben für Azure ATP weiterhin im Azure ATP-Portal ausgeführt. 

## <a name="prerequisites"></a>Voraussetzungen

Zur Nutzung aller Features der Benutzeruntersuchung über die gesamte Hybridumgebung hinweg benötigen Sie Folgendes:
- eine gültige Lizenz für Microsoft Cloud App Security
- eine gültige Lizenz für Azure ATP, die mit Ihrer Active Directory-Instanz verbunden ist
 
>[!NOTE]
>Wenn Sie kein Abonnement für Cloud App Security besitzen, können Sie das Cloud App Security-Portal verwenden, um Azure ATP-Warnungen zu untersuchen und Details zu Benutzern und ihren Aktivitäten in der lokalen verwalteten Umgebung anzuzeigen. Sie erhalten jedoch keine entsprechenden Erkenntnisse aus Ihren Cloudanwendungen.

Informationen zur schnellen Einrichtung und Nutzung von Azure ATP in Cloud App Security finden Sie unter [Azure ATP-Integration](https://docs.microsoft.com/cloud-app-security/aatp-integration/enable-azure-advanced-threat-protection).  
 
## <a name="azure-atp-in-cloud-app-security"></a>Azure ATP in Cloud App Security 

Lesen Sie die [Schnellstartanleitung für Cloud App Security](https://docs.microsoft.com/cloud-app-security/getting-started-with-cloud-app-security), um sich mit den Grundlagen der Verwendung des Cloud App Security-Portals vertraut zu machen. 

Greifen Sie in Cloud App Security-Warnungen, -Aktivitäten und -Benutzerseiten auf Ihre Azure ATP-Daten und neue Hybridfeatures zu. 

## <a name="alerts"></a>Warnungen

Azure ATP-Warnungen werden in der Cloud App Security-Warteschlange **Warnungen** angezeigt. Zusätzliche Filteroptionen stehen nur beim Anzeigen von Warnungen über Cloud App Security zur Verfügung. Azure ATP-Warnungen werden mithilfe des Anwendungsfilters in Azure ATP gefiltert. 


## <a name="activities"></a>Aktivitäten

Azure ATP-Warnungen werden im **Aktivitätsprotokoll** von Cloud App Security angezeigt. Zusätzliche Optionen und Features für die Aktivitätsfilterung stehen nur beim Anzeigen von Warnungen über Cloud App Security zur Verfügung. Informationen zum Filtern und Erstellen von Aktivitätsrichtlinien finden Sie unter [Azure ATP-Aktivitäten in Microsoft Cloud App Security](https://docs.microsoft.com/azure-advanced-threat-protection/atp-activities-filtering-mcas).  

## <a name="user-pages"></a>Benutzerseiten 

Benutzerseiten enthalten die [Bewertung der Untersuchungspriorität](https://docs.microsoft.com/cloud-app-security/tutorial-ueba) für jeden Benutzer sowie ein Aktivitätsprotokoll aller Aktionen. 

So greifen Sie auf die Benutzerseite eines Systembenutzers zu:
1. Öffnen Sie im Hauptmenü die Option **Warnungen**.
1. Wählen Sie mithilfe des Felds **Benutzername** die Warnungswarteschlange für einen bestimmten Benutzer aus, und filtern Sie diese.

 oder

1. Wählen Sie im Menü **Untersuchen** die Option **Aktivitätsprotokoll** aus. 
1. Filtern Sie die Warteschlange des Aktivitätsprotokolls nach Benutzer. 

    ![Aktivitätsprotokoll](media/atp-mcas-activity-filter.png)

## <a name="next-steps"></a>Nächste Schritte

Informationen zum Filtern und Erstellen von Aktivitätsrichtlinien finden Sie unter [Azure ATP-Aktivitäten in Microsoft Cloud App Security](https://docs.microsoft.com/azure-advanced-threat-protection/atp-activities-filtering-mcas). 
  
## <a name="join-the-community"></a>Beitritt zur Community

Haben Sie weitere Fragen, oder möchten Sie mit anderen über Azure ATP und damit verbundene Sicherheitsaspekte diskutieren? Treten Sie noch heute der [Azure ATP-Community](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) bei!




