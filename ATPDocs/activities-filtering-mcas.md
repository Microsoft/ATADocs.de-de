---
title: Microsoft Defender für das Filtern von Identitäts Aktivitäten und Richtlinien in Microsoft Cloud App Security
description: Übersicht über Microsoft Defender für das Filtern von Identitäts Aktivitäten und Richtlinien mit Microsoft Cloud App Security.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 0f6a359745ae03ce0b982e00b7f4c06d556eb702
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2020
ms.locfileid: "94848821"
---
# <a name="use-activity-filters-and-create-action-policies-with-product-long-in-microsoft-cloud-app-security"></a>Verwenden von Aktivitäts Filtern und Erstellen von Aktions Richtlinien mit [!INCLUDE [Product long](includes/product-long.md)] in Microsoft Cloud App Security

Dieser Artikel soll Ihnen dabei helfen zu verstehen, wie Sie Aktions Richtlinien für Aktivitäten mithilfe von Microsoft Cloud App Security Filtern und erstellen können [!INCLUDE [Product short](includes/product-short.md)] .

Weitere Informationen zum Durchführen der Integration finden Sie unter [ [!INCLUDE [Product short](includes/product-short.md)] Integration mit Cloud App Security](/cloud-app-security/aatp-integration).

[!INCLUDE [Product short](includes/product-short.md)]Die Verwendung von mit Microsoft Cloud App Security bietet Aktivitäts Analysen und Warnungen auf der Grundlage von Benutzer-und Entitäts Verhaltensanalysen (ueba), identifiziert die riskanten Verhaltensweisen in Ihrem Unternehmen und bietet eine umfassende Untersuchung der Prioritäts Bewertung sowie Aktivitäts Filterung und anpassbare Aktivitätsrichtlinien.

## <a name="prerequisites"></a>Voraussetzungen

Zur Nutzung aller Features der Benutzeruntersuchung über die gesamte Hybridumgebung hinweg benötigen Sie Folgendes:

- Eine gültige Lizenz für Microsoft Cloud App Security
- Eine gültige Lizenz für [!INCLUDE [Product long](includes/product-long.md)] die Verbindung mit Ihrer Active Directory Instanz

>[!NOTE]
>Wenn Sie nicht über ein Abonnement für Cloud App Security verfügen, können Sie das Cloud App Security-Portal verwenden, um Warnungen zu untersuchen und ausführliche Informationen zu [!INCLUDE [Product short](includes/product-short.md)] Benutzern und Ihren lokalen Aktivitäten zu erhalten. allerdings bleiben Einblicke in Ihre cloudanwendungen nicht verfügbar.

## <a name="filter-product-short-activities-in-cloud-app-security"></a>[!INCLUDE [Product short](includes/product-short.md)]Aktivitäten in Cloud App Security Filtern

[!INCLUDE [Product short](includes/product-short.md)] Sie können über das Haupt Cloud App Security Menü **untersuchen** auf Aktivitäten zugreifen, indem Sie das Untermenü **Aktivitätsprotokoll** oder im Menü **Warnungen** nach Status, Kategorie, Schweregrad, Anwendung, Benutzername oder Richtlinie auswählen.

So greifen Sie [!INCLUDE [Product short](includes/product-short.md)] über den Benutzer auf Aktivitäten zu:

1. Filtern Sie die Warteschlange **Warnungen** mithilfe des Felds BENUTZERNAME.
    ![Filtern von Warnungen nach Benutzername](media/mcas-alerts-queue.png)
1. Klicken Sie in der Ergebnisliste in einer beliebigen Warnung auf den Benutzernamen, um die **Benutzerseite** des Benutzers zu öffnen, den Sie untersuchen möchten.

1. Filtern Sie Aktivitäten des Benutzers mithilfe der verfügbaren Felder, oder fügen Sie über die Schaltfläche „+“ eine neue Filterregel hinzu.
    ![Filtern von Aktivitäten des Benutzers](media/mcas-activity-filter.png)

## <a name="create-activity-policies-in-cloud-app-security"></a>Erstellen von Aktivitätsrichtlinien in Cloud App Security

Nach dem Filtern von Aktivitäten und dem Identifizieren der zu implementierenden Aktivitätsrichtlinien oder der Nichtkonformität in Ihrer Organisation verwenden Sie die Option **Neue Aktivitätsrichtlinie erstellen** im Filtermenü, um sofort eine neue benutzerdefinierte Richtlinie für einen Benutzer, ein Gerät oder einen Mandanten zu erstellen.

So erstellen Sie eine neue Aktivitätsrichtlinie:

1. Wenden Sie von jeder **Aktivitätsprotokoll**-Seite aus einen Filter an (z. B. APP, Benutzername, Aktivitätstyp usw.).
    - Wählen Sie zum Filtern von Aktivitäten aus [!INCLUDE [Product short](includes/product-short.md)] die Option **Active Directory** im App-Filter aus.
    ![Erstellen einer neuen Aktivitätsrichtlinie](media/mcas-create-new-policy.png)
1. Klicken Sie auf die Schaltfläche **Neue Richtlinie aus Suche**.
1. Fügen Sie einen **Richtliniennamen** hinzu.
    ![Erstellen einer neuen Aktivitätsrichtlinie, Schritt 2](media/mcas-create-policy.png)
1. Fügen Sie eine **Beschreibung** für die Richtlinie hinzu.
1. Weisen Sie den **Schweregrad** der Richtlinie zu.
1. Wählen Sie eine **Kategorie** für die Richtlinie aus.
1. Wählen Sie die Filter aus, die für die Richtlinie erstellt und dieser hinzugefügt werden sollen, oder ändern Sie sie.
1. Verfeinern Sie die Filter, oder fügen Sie neue hinzu.
1. Speichern Sie die neue Richtlinie, und wenden Sie sie an.

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie mehr über die Bewertung der Untersuchungspriorität sowie zusätzliche Features von [Microsoft Cloud App Security](/cloud-app-security/).

## <a name="join-the-community"></a>Beitritt zur Community

Haben Sie weitere Fragen, oder möchten Sie mit anderen über [!INCLUDE [Product short](includes/product-short.md)] und damit verbundene Sicherheitsaspekte diskutieren? Treten Sie noch heute der [[!INCLUDE [Product short](includes/product-short.md)]Community](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) bei.