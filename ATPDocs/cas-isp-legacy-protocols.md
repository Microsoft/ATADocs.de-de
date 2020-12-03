---
title: Bewertung der Identitäts Sicherheit für Microsoft Defender für Identity-Legacy Protokolle
description: Dieser Artikel bietet eine Übersicht über den Microsoft Defender for Identity-Bericht zur Bewertung der Sicherheitsstatus Bewertung.
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: 54bc0aeca86acf30101cb3200c1c5c8a3d5041bd
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/03/2020
ms.locfileid: "96544180"
---
# <a name="security-assessment-legacy-protocols-usage"></a>Sicherheitsbewertung: Verwendung von Legacyprotokollen

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

Um Legacyprotokolle außer Betrieb nehmen zu können, muss Ihre Organisation zunächst herausfinden, welche internen Entitäten und Anwendungen diese Protokolle verwenden. Der Bewertungsbericht zur **Nutzung von Legacyprotokollen** gibt die wichtigsten Entitäten an, die Legacyprotokolle verwenden (z.B. NTLMv1). Anhand dieses Berichts können Sie sofort die am stärksten betroffenen Entitäten überprüfen und entsprechende Maßnahmen ergreifen, indem Sie die Verwendung dieser Protokolle beenden und die Protokolle letztendlich komplett deaktivieren. Informationen zu den potenziellen Gefahren durch Legacyprotokolle finden Sie unter [Beenden der Verwendung von LAN-Manager und NTLMv1](/archive/blogs/miriamxyra/stop-using-lan-manager-and-ntlmv1) und [Beenden von MIC 2 und Ausnutzen von LMv2-Clients](https://www.preempt.com/blog/active-directory-ntlm-attacks/).

## <a name="how-do-i-use-this-security-assessment"></a>Wie wird diese Sicherheitsbewertung verwendet?

1. Verwenden Sie die Berichtstabelle, um zu ermitteln, welche Ihrer wichtigsten ermittelten Entitäten Legacyprotokolle verwenden.

    ![Verhindern der Verwendung von Legacyprotokollen](media/cas-isp-legacy-protocols-2.png)
1. Ergreifen Sie entsprechende Maßnahmen für diese Entitäten, um Abhängigkeiten zu ermitteln.
1. Beenden Sie die Verwendung des Legacyprotokolls, und [deaktivieren Sie schließlich das Protokoll vollständig](/archive/blogs/miriamxyra/stop-using-lan-manager-and-ntlmv1).
1. [Löschen Sie MIC 2, und verwenden Sie keine LMv2-Clients mehr.](https://www.preempt.com/blog/active-directory-ntlm-attacks/)

> [!NOTE]
> Diese Bewertung wird nahezu in Echtzeit aktualisiert.

## <a name="next-steps"></a>Nächste Schritte

- [[!INCLUDE [Product short](includes/product-short.md)] Aktivitäten Filtern in Cloud App Security](activities-filtering-mcas.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)