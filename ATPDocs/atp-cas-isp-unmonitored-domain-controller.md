---
title: Azure Advanced Threat Protection – Bewertungen zu nicht überwachten Domänencontrollern
description: Dieser Artikel bietet eine Übersicht über die Berichte von Azure ATP zur Bewertung des Identitätssicherheitsstatus von nicht überwachten Domänencontrollern.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 08/25/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2fe62047-75ef-4b2e-b4aa-72860e39b4e4
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 878f251c1f2936a9207dc351adc9ae5680abe3c4
ms.sourcegitcommit: 098a20abe62e153372da4c96db256bc63c113bd1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/25/2020
ms.locfileid: "88809055"
---
# <a name="security-assessment-unmonitored-domain-controllers"></a>Sicherheitsbewertung: Nicht überwachte Domänencontroller

## <a name="what-are-unmonitored-domain-controllers"></a>Was sind nicht überwachte Domänencontroller?

Ein entscheidender Aspekt der Azure ATP-Lösung ist die Voraussetzung, dass die zugehörigen Sensoren auf allen Domänencontrollern einer Organisation bereitgestellt werden. Nur so lassen sich sämtliche Benutzeraktivitäten auf allen Geräten umfassend überwachen.

Aus diesem Grund überwacht Azure ATP Ihre Umgebung kontinuierlich auf nicht überwachte Domänencontroller, auf denen kein Azure ATP-Sensor installiert ist. Werden nicht überwachte Domänencontroller ermittelt, meldet Azure ATP die betroffenen Server. So werden Sie optimal bei der Verwaltung der vollständigen Abdeckung Ihrer Umgebung unterstützt.

## <a name="what-risk-do-unmonitored-domain-controllers-pose-to-an-organization"></a>Welche Risiken entstehen durch nicht überwachte Domänencontroller für eine Organisation?

Für maximale Effizienz müssen alle Domänencontroller mit Azure ATP-Sensoren überwacht werden. Organisationen, die keine Maßnahmen ergreifen, um nicht überwachte Domänencontroller mit Sensoren auszustatten, senken die Transparenz ihrer Umgebung und gehen das Risiko ein, dass ihre Assets für böswillige Benutzer zugänglich sind.

## <a name="how-do-i-use-this-security-assessment"></a>Wie wird diese Sicherheitsbewertung verwendet?

1. Anhand der Berichtstabelle können Sie ermitteln, welche Ihrer Domänencontroller nicht überwacht werden.
    ![Bereitstellen von Sensoren auf nicht überwachten Domänencontrollern](media/atp-cas-isp-unmonitored-domain-controller-1.png)
1. Führen Sie auf den betroffenen Domänencontrollern entsprechende Maßnahmen durch, indem Sie [Überwachungssensoren installieren und konfigurieren](atp-sensor-monitoring.md#domain-controller-status).

> [!NOTE]
> Diese Bewertung wird nahezu in Echtzeit aktualisiert.

## <a name="see-also"></a>Weitere Informationen

- [Überwachen der Domänencontrollerabdeckung](atp-sensor-monitoring.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
