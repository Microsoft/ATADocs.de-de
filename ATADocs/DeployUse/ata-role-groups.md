---
title: "Arbeiten mit Rollengruppen – Vollständig | Microsoft ATA"
description: "Führt Sie durch die Arbeit mit ATA-Rollengruppen."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 09/20/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 3715b69e-e631-449b-9aed-144d0f9bcee7
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d47d9e7be294c68d764710c15c4bb78539e42f62
ms.openlocfilehash: 869d8f830d5dc70c927f172d77642b0c97bdcd84


---

*Gilt für: Advanced Threat Analytics Version 1.7*




# ATA-Rollengruppen

Rollengruppen erlauben die Zugriffsverwaltung für ATA. Sie können durch Verwendung von Rollengruppen Aufgaben in Ihrem Sicherheitsteam aufteilen und nur so viel Zugriff gewähren, wie Benutzer für die Ausführung ihrer Arbeit benötigen. Dieser Artikel beschreibt die Zugriffsverwaltung und die Berechtigungen der einzelnen ATA-Rollengruppen und hilft Ihnen bei der Einrichtung und Ausführung von Rollengruppen in ATA.
## Typen von ATA-Rollengruppen 

ATA führt drei Typen von Rollengruppen ein: ATA Administrator, ATA Analyst und ATA Executive. Die folgende Tabelle beschreibt den Zugriffstyp in ATA, der pro Rolle verfügbar ist. Je nachdem welche Rolle Sie zuweisen, stehen verschiedene Bildschirme und Menüoptionen in ATA nicht zur Verfügung:

|Aktivität |Microsoft Advanced Threat Analytics Administrator|Microsoft Advanced Threat Analytics Analyst|Microsoft Advanced Threat Analytics Executive|
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

Wenn Benutzer versuchen, auf eine Seite zuzugreifen, die nicht für deren Rollengruppe verfügbar ist, werden Sie auf eine ATA-Seite weitergeleitet, die Ihnen mitteilt, dass Sie für den Zugriff nicht autorisiert sind. 

## Hinzufügen/Entfernen von Benutzern – ATA-Rollengruppen 

ATA verwendet die lokalen Windows-Gruppen als Grundlage für Rollengruppen. Zum Hinzufügen oder Entfernen von Benutzern, verwenden Sie die MMC **Lokale Benutzer und Gruppen** (Lusrmgr.msc). Sie können auf einem Computer, der zu einer Domäne gehört, Domänenkonten sowie lokale Konten hinzufügen. 




<!--HONumber=Sep16_HO4-->


