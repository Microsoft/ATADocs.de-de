---
title: Bewertungen von Microsoft Defender für die Identitäts-und risikoreichere lateral Movement-Pfade
description: Dieser Artikel bietet eine Übersicht über die sensiblen Entitäten von Microsoft Defender für Identitäten mit dem riskanten Bericht zur Identitäts Sicherheitsstatus-Bewertung.
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: 0c40159818e9526eb3cdf0259fbcb45c54fa5482
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/03/2020
ms.locfileid: "96544163"
---
# <a name="security-assessment-riskiest-lateral-movement-paths-lmp"></a>Sicherheitsbewertung: Lateral-Movement-Pfade mit dem höchsten Risiko

## <a name="what-are-risky-lateral-movement-paths"></a>Was sind riskante Lateral-Movement-Pfade?

[!INCLUDE [Product long](includes/product-long.md)] überwacht kontinuierlich Ihre Umgebung, um **sensible** Konten mit den riskanten lateral Movement-Pfaden zu identifizieren, die ein Sicherheitsrisiko darstellen, und meldet Berichte zu diesen Konten, um Sie bei der Verwaltung Ihrer Umgebung zu unterstützen. Pfade werden als riskant eingestuft, wenn sie über drei oder mehr nicht sensible Konten verfügen, die das **sensible** Konto dem Diebstahl von Anmeldeinformationen durch Angreifer aussetzen.

Hier erfahren Sie mehr über Lateral-Movement-Pfade:

- [[!INCLUDE [Product short](includes/product-short.md)] Lateral Movement-Pfade (LMPS)](use-case-lateral-movement-path.md)
- [MITRE ATT&CK: Lateral Movement](https://attack.mitre.org/tactics/TA0008/)

## <a name="what-risk-do-risky-lateral-movement-paths-pose"></a>Welches Risiko stellen riskante Lateral-Movement-Pfade dar?

Organisationen, die ihre **sensiblen** Konten nicht sichern, ermöglichen Angreifern den Zugang zu diesen.

Böswillige Akteure suchen ähnlich wie Diebe häufig in jeder Umgebung nach dem einfachsten und lautlosesten Weg. Sensible Konten mit riskanten Lateral-Movement-Pfaden eröffnen Gelegenheiten für Angreifer und können Risiken darstellen.

Beispielsweise sind die riskanten Pfade leichter für Angreifer sichtbar und können diesen im Fall einer Kompromittierung Zugriff auf die sensibelsten Entitäten Ihrer Organisation verschaffen.

## <a name="how-do-i-use-this-security-assessment"></a>Wie wird diese Sicherheitsbewertung verwendet?

1. Verwenden Sie die Berichtstabelle, um zu ermitteln, welche Ihrer **sensiblen** Konten riskante Lateral-Movement-Pfade aufweisen.
    ![Überprüfen der wichtigsten betroffenen Entitäten und Erstellen eines Aktionsplans](media/cas-isp-riskiest-lmp-1.png)
1. Ergreifen Sie entsprechende Maßnahmen:
    - Entfernen Sie die Entität aus der Gruppe, die in der Empfehlung angegeben wird.
    - Entfernen Sie die lokalen Administratorberechtigungen für die Entität von dem Gerät, das in der Empfehlung angegeben wird.

    > [!NOTE]
    > Warten Sie 24 Stunden, und überprüfen Sie dann, ob die Empfehlung nicht mehr in der Liste angezeigt wird.

> [!NOTE]
> Diese Bewertung wird alle 24 Stunden aktualisiert.

## <a name="see-also"></a>Weitere Informationen

- [[!INCLUDE [Product short](includes/product-short.md)] Aktivitäten Filtern in Cloud App Security](activities-filtering-mcas.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
