---
title: "Überwachen von Warnungen von Advanced Threat Analytics Health Center | Microsoft-Dokumentation"
description: "Mit ATA Health Center lässt sich die Integrität des ATA-Diensts überprüfen, und es werden Warnungen über mögliche Probleme angezeigt."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: d6c783b2-46c5-4211-b21a-d6b17f08d03d
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: e929714ca33dfaa82bdf93dbaf230abadef1b86d
ms.sourcegitcommit: 49e892a82275efa5146998764e850959f20d3216
translationtype: HT
---
*Gilt für: Advanced Threat Analytics Version 1.7*



# <a name="ata-health-center"></a>ATA Health Center
Mit ATA Health Center lässt sich die Leistung des ATA-Diensts überprüfen, und es werden Warnungen über Probleme angezeigt.

## <a name="working-with-the-ata-health-center"></a>Arbeiten mit dem ATA Health Center
Das ATA Health Center zeigt Probleme durch einen roten Punkt über dem Health Center-Symbol auf der Menüleiste an.

![Roter Punkt auf der Symbolleiste für das ATA-Integritätscenter](media/ATA-Health-Center-Alert-red-dot.png)

### <a name="managing-ata-health"></a>Verwalten der ATA-Integrität
Um den Gesamtzustand des Systems zu überprüfen, klicken Sie auf der Menüleiste auf das Health Center-Symbol. ![ATA Health Center-Symbol](media/ATA-red-dot.png)

-   Alle offenen Warnungen lassen sich über die Einstellungen **Aufgelöst** und **Verworfen** verwalten. Klicken Sie hierzu in der Warnung auf **Öffnen**, und scrollen Sie abwärts zu **Aufgelöst** oder **Verworfen**.

-   Wenn ein Problem als behoben markiert wird, ATA jedoch erkennt, dass das Problem weiterhin besteht, wird es automatisch erneut in die Liste der Probleme mit dem Zustand **Offen** aufgenommen. Wenn ATA erkennt, dass ein offenes Problem behoben wurde, wird dieses automatisch in die Liste **Aufgelöst** aufgenommen.

-   Probleme mit dem Status **Verworfen** sind solche, die ATA nicht länger überprüfen soll – beispielsweise bekannte Probleme, die derzeit nicht behoben werden sollen und nicht mehr in der Liste **Offen** aufgeführt werden sollen. Legen Sie für solche Probleme **Verworfen** fest.

![Abbildung eines ATA Health Center-Problems](media/ATA-Health-Issue.JPG)

## <a name="see-also"></a>Weitere Informationen
- [Arbeiten mit ATA-Erkennungseinstellungen](working-with-detection-settings.md)
- [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
