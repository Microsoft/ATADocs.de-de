---
title: Aktivitätsfilterung und Richtlinien für Azure Advanced Threat Protection in Microsoft Cloud App Security
description: Übersicht über die Aktivitätsfilterung und Richtlinien für Azure Advanced Threat Protection in Microsoft Cloud App Security.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 07/01/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 397e5a77-2bc7-454c-9fe5-649ebaab16b3
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: bffad5454cbc1f9216333f44af9a7cfd39ce5433
ms.sourcegitcommit: 63be53de5b84eabdeb8c006438dab45bd35a4ab7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "79414470"
---
# <a name="use-activity-filters-and-create-action-policies-with-azure-atp-in-microsoft-cloud-app-security"></a>Verwenden von Aktivitätsfiltern und Erstellen von Aktionsrichtlinien mit Azure ATP in Microsoft Cloud App Security 

Dieser Artikel bietet grundlegende Informationen dazu, wie Aktionsrichtlinien für Azure ATP-Aktivitäten in Microsoft Cloud App Security gefiltert und erstellt werden. 

Weitere Informationen zum Abschließen der Integration finden Sie unter [Integration von Azure ATP in Cloud App Security](https://docs.microsoft.com/cloud-app-security/aatp-integration/enable-azure-advanced-threat-protection).  

Die Verwendung von Azure ATP mit Microsoft Cloud App Security bietet Aktivitätsanalysen und -warnungen basierend auf „User and Entity Behavior Analytics“ (UEBA). Hierbei werden die Verhaltensweisen mit dem höchsten Risiko in Ihrem Unternehmen ermittelt. Zudem werden eine umfassende Bewertung der Priorität bei Untersuchungen sowie eine aktive Filterung und anpassbare Aktivitätsrichtlinien bereitgestellt. 

## <a name="prerequisites"></a>Voraussetzungen

Zur Nutzung aller Features der Benutzeruntersuchung über die gesamte Hybridumgebung hinweg benötigen Sie Folgendes:
- Eine gültige Lizenz für Microsoft Cloud App Security
- eine gültige Lizenz für Azure ATP, die mit Ihrer Active Directory-Instanz verbunden ist

>[!NOTE]
>Wenn Sie kein Abonnement für Cloud App Security besitzen, können Sie das Cloud App Security-Portal verwenden, um Azure ATP-Warnungen zu untersuchen und Details zu Benutzern und ihren Aktivitäten in der lokalen verwalteten Umgebung anzuzeigen. Erkenntnisse in Zusammenhang mit Ihren Cloudanwendungen sind jedoch nicht verfügbar.

## <a name="filter-azure-atp-activities-in-cloud-app-security"></a>Filtern von Azure ATP-Aktivitäten in Cloud App Security  
 
Sie können über das Cloud App Security-Hauptmenü **Untersuchen** auf Azure ATP-Aktivitäten zugreifen, indem Sie das Untermenü **Aktivitätsprotokoll** auswählen. Alternativ dazu können Sie im Menü **Warnungen** anhand von Status, Kategorie, Schweregrad, Anwendung, Benutzername oder Richtlinie auf diese Aktivitäten zugreifen.  

So greifen Sie auf Azure ATP-Aktivitäten von Benutzern zu:

1. Filtern Sie die Warteschlange **Warnungen** mithilfe des Felds BENUTZERNAME. 
    ![Warteschlange für Warnungen](media/atp-mcas-alerts-queue.png)
1. Klicken Sie in der Ergebnisliste in einer beliebigen Warnung auf den Benutzernamen, um die **Benutzerseite** des Benutzers zu öffnen, den Sie untersuchen möchten. 
    
1. Filtern Sie Aktivitäten des Benutzers mithilfe der verfügbaren Felder, oder fügen Sie über die Schaltfläche „+“ eine neue Filterregel hinzu.
    ![Warteschlange für Warnungen](media/atp-mcas-activity-filter.png)

## <a name="create-activity-policies-in-cloud-app-security"></a>Erstellen von Aktivitätsrichtlinien in Cloud App Security

Nach dem Filtern von Aktivitäten und dem Identifizieren der zu implementierenden Aktivitätsrichtlinien oder der Nichtkonformität in Ihrer Organisation verwenden Sie die Option **Neue Aktivitätsrichtlinie erstellen** im Filtermenü, um sofort eine neue benutzerdefinierte Richtlinie für einen Benutzer, ein Gerät oder einen Mandanten zu erstellen. 

So erstellen Sie eine neue Aktivitätsrichtlinie:

1. Wenden Sie von jeder **Aktivitätsprotokoll**-Seite aus einen Filter an (z. B. APP, Benutzername, Aktivitätstyp usw.). 
    - Wählen Sie die Option **Active Directory Domain Services** im APP-Filter aus, um aus Azure ATP heraus nach Aktivitäten zu filtern. 
    ![Erstellen einer neuen Aktivitätsrichtlinie](media/atp-mcas-create-new-policy.png)
1. Klicken Sie auf die Schaltfläche **Neue Richtlinie aus Suche**.    
1. Fügen Sie einen **Richtliniennamen** hinzu. 
    ![Erstellen einer neuen Aktivitätsrichtlinie, Schritt 2](media/atp-mcas-create-policy.png)
1. Fügen Sie eine **Beschreibung** für die Richtlinie hinzu.  
1. Weisen Sie den **Schweregrad** der Richtlinie zu.
1. Wählen Sie eine **Kategorie** für die Richtlinie aus.
1. Wählen Sie die Filter aus, die für die Richtlinie erstellt und dieser hinzugefügt werden sollen, oder ändern Sie sie.
1. Verfeinern Sie die Filter, oder fügen Sie neue hinzu. 
1. Speichern Sie die neue Richtlinie, und wenden Sie sie an.  


## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie mehr über die Bewertung der Untersuchungspriorität sowie zusätzliche Features von [Microsoft Cloud App Security](https://docs.microsoft.com/cloud-app-security/).
  
## <a name="join-the-community"></a>Beitritt zur Community

Haben Sie weitere Fragen, oder möchten Sie mit anderen über Azure ATP und damit verbundene Sicherheitsaspekte diskutieren? Treten Sie noch heute der [Azure ATP-Community](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) bei!




