---
title: Azure Advanced Threat Protection-Bewertung des Identitätssicherheitsstatus von Legacyprotokollen | Microsoft-Dokumentation
description: Dieser Artikel bietet eine Übersicht über den Bericht von Azure ATP zur Bewertung des Identitätssicherheitsstatus von Legacyprotokollen.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 07/08/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 6597b8c7-f83e-43c6-8149-fb4a914a845b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 55783934a609577bf34fe1034903f2d5e6f97fc5
ms.sourcegitcommit: 475df3e87d8476ff13e48ebc7a722f46f29dab70
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71007499"
---
# <a name="security-assessment-legacy-protocols-usage---preview"></a>Sicherheitsbewertung: Verwendung von Legacyprotokollen – Vorschau
 
## <a name="what-are-legacy-protocols"></a>Was sind Legacyprotokolle?

Unternehmen haben viele Standardvorgänge eingerichtet, um ihre Infrastrukturen durch Patchen und Serverhärtung zu schützen. Dabei wird ein Bereich häufig übersehen: die Außerbetriebnahme von Legacyprotokollen. Wenn die Verwendung von Legacyprotokollen nicht eingedämmt wird, ist dem Diebstahl von Anmeldeinformationen Tür und Tor geöffnet. 

Als die meisten Legacyprotokolle entworfen und erstellt wurden, existierten die heutigen Sicherheitsanforderungen noch nicht. Und die Implementierung erfolgte, bevor die Sicherheitsanforderungen in modernen Unternehmen ersichtlich wurden. Dennoch sind Legacyprotokolle nach wie vor unverändert vorhanden und können sich in jeder modernen Organisation im Handumdrehen in anfällige Zugriffspunkte verwandeln. 

## <a name="what-risks-do-retained-legacy-protocols-introduce"></a>Welche Risiken entstehen durch beibehaltene Legacyprotokolle? 

Moderne Cyberangriffsmethoden zielen häufig speziell auf Legacyprotokolle ab und nutzen sie, um Organisationen anzugreifen, die noch keine angemessene Risikominderung implementiert haben. 

Eine Verringerung der Angriffsfläche lässt sich erreichen, indem die Unterstützung für unsichere Legacyprotokolle wie z.B. die folgenden deaktiviert wird: 

- TLS 1.0 und 1.1 (ebenso alle Versionen von SSL)
- Server Message Block v1 (SMBv1)
- LanMan (LM) / NTLMv1
- Digestauthentifizierung

Um Legacyprotokolle außer Betrieb nehmen zu können, muss Ihre Organisation zunächst herausfinden, welche internen Entitäten und Anwendungen diese Protokolle verwenden. Der Bewertungsbericht zur **Nutzung von Legacyprotokollen** gibt die wichtigsten Entitäten an, die Legacyprotokolle verwenden (z.B. NTLMv1). Anhand dieses Berichts können Sie sofort die am stärksten betroffenen Entitäten überprüfen und entsprechende Maßnahmen ergreifen, indem Sie die Verwendung dieser Protokolle beenden und die Protokolle letztendlich komplett deaktivieren. Informationen zu den potenziellen Gefahren durch Legacyprotokolle finden Sie unter [Stop using LAN manager and NTLMv1!](https://blogs.technet.microsoft.com/miriamxyra/2017/11/07/stop-using-lan-manager-and-ntlmv1/) (Beenden Sie die Verwendung von LAN-Manager und NTLMv1!).


## <a name="how-do-i-use-this-security-assessment"></a>Wie wird diese Sicherheitsbewertung verwendet? 
1. Verwenden Sie die Berichtstabelle, um zu ermitteln, welche Ihrer wichtigsten ermittelten Entitäten Legacyprotokolle verwenden.  
    <br>![Verhindern der Verwendung von Legacyprotokollen](media/atp-cas-isp-legacy-protocols-2.png)
1. Ergreifen Sie für diese Entitäten entsprechende Maßnahmen, um Abhängigkeiten zu ermitteln, die Verwendung von Legacyprotokollen zu beenden und [die Protokolle letztendlich komplett zu deaktivieren](https://blogs.technet.microsoft.com/miriamxyra/2017/11/07/stop-using-lan-manager-and-ntlmv1/). 

## <a name="next-steps"></a>Nächste Schritte
- [Azure ATP-Aktivitätsfilter in Cloud App Security](atp-activities-filtering-mcas.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)