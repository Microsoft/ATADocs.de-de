---
title: Bewertungen der nicht überwachten Domänen Controller von Microsoft Defender
description: Dieser Artikel bietet eine Übersicht über den Microsoft Defender for Identity-Identitäts Sicherheitsstatus-Bewertungsbericht für nicht überwachte Domänen Controller.
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: 86a1e02b84cf874f23fbf7b69d50c482cd15713b
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/03/2020
ms.locfileid: "96544146"
---
# <a name="security-assessment-unmonitored-domain-controllers"></a>Sicherheitsbewertung: Nicht überwachte Domänencontroller

## <a name="what-are-unmonitored-domain-controllers"></a>Was sind nicht überwachte Domänencontroller?

Ein wesentlicher Bestandteil der [!INCLUDE [Product long](includes/product-long.md)] Lösung erfordert, dass die Sensoren auf allen Domänen Controllern der Organisation bereitgestellt werden, und bietet eine umfassende Ansicht für alle Benutzeraktivitäten von jedem Gerät.

Aus diesem Grund [!INCLUDE [Product short](includes/product-short.md)] überwacht Ihre Umgebung fortlaufend, um Domänen Controller ohne installierten [!INCLUDE [Product short](includes/product-short.md)] Sensor zu identifizieren, und meldet diese nicht überwachten Server, um Sie bei der Verwaltung der vollständigen Abdeckung Ihrer Umgebung zu unterstützen.

## <a name="what-risk-do-unmonitored-domain-controllers-pose-to-an-organization"></a>Welche Risiken entstehen durch nicht überwachte Domänencontroller für eine Organisation?

Alle Domänen Controller müssen mit Sensoren überwacht werden, um eine maximale Effizienz zu erzielen [!INCLUDE [Product short](includes/product-short.md)] . Organisationen, die keine Maßnahmen ergreifen, um nicht überwachte Domänencontroller mit Sensoren auszustatten, senken die Transparenz ihrer Umgebung und gehen das Risiko ein, dass ihre Assets für böswillige Benutzer zugänglich sind.

## <a name="how-do-i-use-this-security-assessment"></a>Wie wird diese Sicherheitsbewertung verwendet?

1. Anhand der Berichtstabelle können Sie ermitteln, welche Ihrer Domänencontroller nicht überwacht werden.
    ![Bereitstellen von Sensoren auf nicht überwachten Domänencontrollern](media/cas-isp-unmonitored-domain-controller-1.png)
1. Führen Sie auf den betroffenen Domänencontrollern entsprechende Maßnahmen durch, indem Sie [Überwachungssensoren installieren und konfigurieren](sensor-monitoring.md#domain-controller-status).

> [!NOTE]
> Diese Bewertung wird nahezu in Echtzeit aktualisiert.

## <a name="see-also"></a>Weitere Informationen

- [Überwachen der Domänencontrollerabdeckung](sensor-monitoring.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
