---
title: "Advanced Threat Analytics-Rollengruppen für die Zugangsverwaltung | Microsoft-Dokumentation"
description: "Führt Sie durch die Arbeit mit ATA-Rollengruppen."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/30/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 3715b69e-e631-449b-9aed-144d0f9bcee7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 6243c03af9e40b8774b2ce7089a47e54569ba45e
ms.sourcegitcommit: cb2a4df6805d41bf030d3439ef87281fc6acc98f
ms.translationtype: HT
ms.contentlocale: de-DE
---
*Gilt für: Advanced Threat Analytics Version 1.7*




# <a name="ata-role-groups"></a>ATA-Rollengruppen

Rollengruppen erlauben die Zugriffsverwaltung für ATA. Sie können durch Verwendung von Rollengruppen Aufgaben in Ihrem Sicherheitsteam aufteilen und nur so viel Zugriff gewähren, wie Benutzer für die Ausführung ihrer Arbeit benötigen. Dieser Artikel beschreibt die Zugriffsverwaltung und die Berechtigungen der einzelnen ATA-Rollengruppen und hilft Ihnen bei der Einrichtung und Ausführung von Rollengruppen in ATA.

> [!NOTE]
> Jeder lokale Administrator im ATA-Center ist automatisch ein Microsoft Advanced Threat Analytics-Administrator.

## <a name="types-of-ata-role-groups"></a>Typen von ATA-Rollengruppen 

ATA führt 3 Typen von Rollengruppen ein: ATA-Administratoren, ATA-Benutzer und ATA-Viewer. Die folgende Tabelle beschreibt den Zugriffstyp in ATA, der pro Rolle verfügbar ist. Je nachdem welche Rolle Sie zuweisen, stehen verschiedene Bildschirme und Menüoptionen in ATA nicht zur Verfügung:

|Aktivität |Microsoft Advanced Threat Analytics-Administratoren|Microsoft Advanced Threat Analytics-Benutzer|Microsoft Advanced Threat Analytics-Viewer|
|----|----|----|----|
|Anmeldung|Verfügbar|Verfügbar|Verfügbar|
|Bereitstellen von Eingaben für verdächtige Aktivitäten|Verfügbar|Verfügbar|Nicht verfügbar|
|Ändern des Status von verdächtigen Aktivitäten|Verfügbar|Verfügbar|Nicht verfügbar|
|Freigeben/Exportieren von verdächtiger Aktivität über E-Mail/Abruflink|Verfügbar|Verfügbar|Nicht verfügbar|
|Hinzufügen/Bearbeiten von Hinweisen für verdächtige Aktivitäten|Verfügbar|Verfügbar|Nicht verfügbar|
|Ändern des Status der Überwachung von Warnungen|Verfügbar|Verfügbar|Nicht verfügbar|
|Aktualisieren der ATA-Konfiguration|Verfügbar|Nicht verfügbar|Nicht verfügbar|
|Gateway – Hinzufügen|Verfügbar|Nicht verfügbar|Nicht verfügbar|
|Gateway – Löschen |Verfügbar|Nicht verfügbar|Nicht verfügbar|
|Überwachter DC – Hinzufügen |Verfügbar|Nicht verfügbar|Nicht verfügbar|
|Überwachter DC – Löschen|Verfügbar|Nicht verfügbar|Nicht verfügbar|
|Anzeigen von Warnungen und verdächtigen Aktivitäten|Verfügbar|Verfügbar|Verfügbar|


Wenn Benutzer versuchen, auf eine Seite zuzugreifen, die nicht für deren Rollengruppe verfügbar ist, werden Sie auf eine ATA-Seite weitergeleitet, die Ihnen mitteilt, dass Sie für den Zugriff nicht autorisiert sind. 

## <a name="add--remove-users---ata-role-groups"></a>Hinzufügen/Entfernen von Benutzern – ATA-Rollengruppen 

ATA verwendet die lokalen Windows-Gruppen als Grundlage für Rollengruppen. Die Rollengruppen müssen auf dem Server von ATA-Center verwaltet werden.
Zum Hinzufügen oder Entfernen von Benutzern, verwenden Sie die MMC **Lokale Benutzer und Gruppen** (Lusrmgr.msc). Sie können auf einem Computer, der zu einer Domäne gehört, Domänenkonten sowie lokale Konten hinzufügen. 

