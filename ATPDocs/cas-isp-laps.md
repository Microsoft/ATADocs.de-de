---
title: Azure Advanced Threat Protection:Verwendung von Microsoft LAPS
description: Dieser Artikel bietet eine Übersicht über die Verwendung von Microsoft LAPS von Azure ATP zur Bewertung des Identitätssicherheitsstatus von Klartext.
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
ms.openlocfilehash: fdc5ace86a48b78041e1a7fc8927ae24d64b00ff
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2020
ms.locfileid: "90913221"
---
# <a name="security-assessment-microsoft-laps-usage"></a>Sicherheitsbewertung: Verwendung von Microsoft LAPS

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

## <a name="what-is-microsoft-laps"></a>Was ist Microsoft LAPS?

Die „lokale Administratorkennwortlösung“ (Local Administrator Password Solution, LAPS) von Microsoft stellt die Verwaltung der Kennwörter lokaler Administratorkonten für in eine Domäne eingebundenen Computer bereit. Kennwörter werden zufällig in Active Directory (AD) angeordnet und gespeichert und durch ACLs geschützt. So können nur berechtigte Benutzer diese lesen oder ihre Zurücksetzung anfordern.

## <a name="what-risk-does-not-implementing-laps-pose-to-an-organization"></a>Welches Risiko birgt die Nichtimplementierung von LAPS für eine Organisation?

LAPS bietet eine Lösung für das Problem der Verwendung eines gemeinsamen lokalen Kontos mit einem identischen Kennwort auf jedem Computer in einer Domäne. LAPS löst dieses Problem, indem für das gemeinsame lokale Administratorkonto auf jedem Computer in der Domäne ein anderes rotiertes zufälliges Kennwort festgelegt wird.

LAPS vereinfacht die Kennwortverwaltung und hilft Kunden dabei, zusätzliche empfohlene Schutzmaßnahmen gegen Cyberangriffe zu implementieren. Die Lösung verringert insbesondere das Risiko der Lateralausweitung, die auftritt, wenn Kunden dasselbe lokale Administratorkonto und dieselbe Kennwortkombination auf ihren Computern verwenden. LAPS speichert das Kennwort für das lokale Administratorkonto jedes Computers in AD, das in einem vertraulichen Attribut im entsprechenden AD-Objekt auf dem Computer gesichert wird. Der Computer kann die eigenen Kennwortdaten in AD aktualisieren, und Domänenadministratoren können autorisierten Benutzern oder Gruppen wie Helpdeskadministratoren für Arbeitsstationen Lesezugriff zuweisen.

## <a name="how-do-i-use-this-security-assessment"></a>Wie wird diese Sicherheitsbewertung verwendet?

1. Verwenden Sie die Berichtstabelle, um zu ermitteln, welche Ihrer Domänen über einige (oder alle) kompatible Windows-Geräte verfügen, die nicht durch LAPS geschützt sind oder für die das durch LAPS verwaltete Kennwort in den letzten 60 Tagen noch nicht geändert wurde.
1. Wählen Sie für Domänen, die nur teilweise geschützt sind, die betreffende Zeile aus, um die Liste der Geräte anzuzeigen, die nicht von LAPS in dieser Domäne geschützt sind.
    ![Auswählen von Domänen mit LAPS-Geräten](media/atp-cas-isp-laps-1.png)
1. Ergreifen Sie entsprechende Maßnahmen auf diesen Geräten, indem Sie [Microsoft LAPS](https://go.microsoft.com/fwlink/?linkid=2104282) mithilfe der unter Download bereitgestellten Dokumentation herunterladen, installieren oder konfigurieren oder eine Problembehandlung durchführen.
    ![Wiederherstellen von LAPS-Geräten](media/atp-cas-isp-laps-2.png)

> [!NOTE]
> Diese Bewertung wird alle 24 Stunden aktualisiert.

## <a name="see-also"></a>Weitere Informationen

- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)