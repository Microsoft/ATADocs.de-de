---
title: Advanced Threat Analytics-Rollen Gruppen für die Zugriffs Verwaltung
description: Führt Sie durch die Arbeit mit ATA-Rollengruppen.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 3715b69e-e631-449b-9aed-144d0f9bcee7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: cdb1d66513f785b71b73b21aaf096ab5b5d3ad81
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2020
ms.locfileid: "90908744"
---
# <a name="ata-role-groups"></a>ATA-Rollengruppen


[!INCLUDE [Banner for top of topics](includes/banner.md)]

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Rollengruppen erlauben die Zugriffsverwaltung für ATA. Sie können durch Verwendung von Rollengruppen Aufgaben in Ihrem Sicherheitsteam aufteilen und nur so viel Zugriff gewähren, wie Benutzer für die Ausführung ihrer Arbeit benötigen. Dieser Artikel beschreibt die Zugriffsverwaltung und die Berechtigungen der einzelnen ATA-Rollengruppen und hilft Ihnen bei der Einrichtung und Ausführung von Rollengruppen in ATA.

> [!NOTE]
> Jeder lokale Administrator im ATA-Center ist automatisch ein Microsoft Advanced Threat Analytics-Administrator.

## <a name="types-of-ata-role-groups"></a>Typen von ATA-Rollengruppen 

ATA führt drei Typen von Rollengruppen ein: ATA-Administratoren, ATA-Benutzer und ATA-Viewer. Die folgende Tabelle beschreibt den Zugriffstyp in ATA, der pro Rolle verfügbar ist. Je nachdem, welche Rolle Sie zuweisen, stehen verschiedene Bildschirme und Menüoptionen in ATA nicht zur Verfügung:

|Aktivität |Microsoft Advanced Threat Analytics-Administratoren|Microsoft Advanced Threat Analytics-Benutzer|Microsoft Advanced Threat Analytics-Viewer|
|----|----|----|----|
|Anmelden|Verfügbar|Verfügbar|Verfügbar|
|Bereitstellen von Eingaben für verdächtige Aktivitäten|Verfügbar|Verfügbar|Nicht verfügbar|
|Ändern des Status von verdächtigen Aktivitäten|Verfügbar|Verfügbar|Nicht verfügbar|
|Freigeben/Exportieren von verdächtiger Aktivität über E-Mail/Abruflink|Verfügbar|Verfügbar|Nicht verfügbar|
|Status von Integritäts Warnungen ändern|Verfügbar|Verfügbar|Nicht verfügbar|
|Aktualisieren der ATA-Konfiguration|Verfügbar|Nicht verfügbar|Nicht verfügbar|
|Gateway – Hinzufügen|Verfügbar|Nicht verfügbar|Nicht verfügbar|
|Gateway – Löschen |Verfügbar|Nicht verfügbar|Nicht verfügbar|
|Überwachter DC – Hinzufügen |Verfügbar|Nicht verfügbar|Nicht verfügbar|
|Überwachter DC – Löschen|Verfügbar|Nicht verfügbar|Nicht verfügbar|
|Anzeigen von Warnungen und verdächtigen Aktivitäten|Verfügbar|Verfügbar|Verfügbar|


Wenn Benutzer versuchen, auf eine Seite zuzugreifen, die nicht für deren Rollengruppe verfügbar ist, werden sie auf eine ATA-Seite weitergeleitet, die ihnen mitteilt, dass Sie für den Zugriff nicht autorisiert sind. 

## <a name="add--remove-users---ata-role-groups"></a>Hinzufügen/Entfernen von Benutzern – ATA-Rollengruppen 

ATA verwendet die lokalen Windows-Gruppen als Grundlage für Rollengruppen. Die Rollengruppen müssen auf dem Server von ATA-Center verwaltet werden.
Zum Hinzufügen oder Entfernen von Benutzern, verwenden Sie die MMC **Lokale Benutzer und Gruppen** (Lusrmgr.msc). Sie können auf einem Computer, der zu einer Domäne gehört, Domänenkonten sowie lokale Konten hinzufügen. 

