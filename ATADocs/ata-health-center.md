---
title: "Überwachen von Systemintegrität und Ereignissen von Advanced Threat Analytics| Microsoft-Dokumentation"
description: "Mit ATA Health Center lässt sich die Integrität des ATA-Diensts überprüfen, und es werden Warnungen über mögliche Probleme sowie Systemereignisse in der Ereignisanzeige angezeigt."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/2/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: d6c783b2-46c5-4211-b21a-d6b17f08d03d
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 59e5cafcff7b84ffb9dc161cd0b50cd3014e455a
ms.sourcegitcommit: 3177d5894413fbd363b9aca8130f3f7a369223b8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2017
---
*Gilt für: Advanced Threat Analytics Version 1.8*


# Arbeiten mit der Systemintegrität und Ereignissen von ATA
<a id="working-with-ata-system-health-and-events" class="xliff"></a>

## ATA Health Center
<a id="ata-health-center" class="xliff"></a>
Mit ATA Health Center lässt sich die Leistung des ATA-Diensts überprüfen, und es werden Warnungen über Probleme angezeigt.

## Arbeiten mit dem ATA Health Center
<a id="working-with-the-ata-health-center" class="xliff"></a>
Das ATA Health Center zeigt Probleme durch einen roten Punkt über dem Health Center-Symbol auf der Menüleiste an.

![Roter Punkt auf der Symbolleiste für das ATA-Integritätscenter](media/ATA-Health-Center-Alert-red-dot.png)

### Verwalten der ATA-Integrität
<a id="managing-ata-health" class="xliff"></a>
Um den Gesamtzustand des Systems zu überprüfen, klicken Sie auf der Menüleiste auf das Health Center-Symbol. ![ATA Health Center-Symbol](media/ATA-red-dot.png)

-   Alle offenen Warnungen lassen sich über die Einstellungen **Aufgelöst** und **Verworfen** verwalten. Klicken Sie hierzu in der Warnung auf **Öffnen**, und scrollen Sie abwärts zu **Aufgelöst** oder **Verworfen**.

-   Wenn ein Problem als behoben markiert wird, ATA jedoch erkennt, dass das Problem weiterhin besteht, wird es automatisch erneut in die Liste der Probleme mit dem Zustand **Offen** aufgenommen. Wenn ATA erkennt, dass ein offenes Problem behoben wurde, wird dieses automatisch in die Liste **Aufgelöst** aufgenommen.

-   Probleme mit dem Status **Verworfen** sind solche, die ATA nicht länger überprüfen soll – beispielsweise bekannte Probleme, die derzeit nicht behoben werden sollen und nicht mehr in der Liste **Offen** aufgeführt werden sollen. Legen Sie für solche Probleme **Verworfen** fest.

![Abbildung eines ATA Health Center-Problems](media/ATA-Health-Issue.JPG)






## Siehe auch
<a id="see-also" class="xliff"></a>

- [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
