---
title: 'Azure Advanced Threat Protection: Lateral-Movement-Pfade mit dem höchsten Risiko'
description: Dieser Artikel bietet eine Übersicht über die sensibelsten Azure ATP-Entitäten mit den Lateral-Movement-Pfade mit dem höchsten Risiko im Bericht zur Bewertung des Identitätssicherheitsstatus.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 08/25/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2fe62047-75ef-4b2e-b4aa-72860e39b4e4
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 301dc36032950733784b928198fa5b092ccd6f10
ms.sourcegitcommit: 098a20abe62e153372da4c96db256bc63c113bd1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/25/2020
ms.locfileid: "88809089"
---
# <a name="security-assessment-riskiest-lateral-movement-paths-lmp"></a>Sicherheitsbewertung: Lateral-Movement-Pfade mit dem höchsten Risiko

## <a name="what-are-risky-lateral-movement-paths"></a>Was sind riskante Lateral-Movement-Pfade?

Azure ATP überwacht Ihre Umgebung fortlaufend, um **sensible** Konten mit den riskantesten Lateral-Movement-Pfaden zu identifizieren, die ein Sicherheitsrisiko darstellen, und erfasst Berichte zu diesen Konten, um Sie bei der Verwaltung Ihrer Umgebung zu unterstützen. Pfade werden als riskant eingestuft, wenn sie über drei oder mehr nicht sensible Konten verfügen, die das **sensible** Konto dem Diebstahl von Anmeldeinformationen durch Angreifer aussetzen.

Hier erfahren Sie mehr über Lateral-Movement-Pfade:

- [Azure ATP-Lateral Movement-Pfade (LMPs)](use-case-lateral-movement-path.md)
- [MITRE ATT&CK: Lateral Movement](https://attack.mitre.org/tactics/TA0008/)

## <a name="what-risk-do-risky-lateral-movement-paths-pose"></a>Welches Risiko stellen riskante Lateral-Movement-Pfade dar?

Organisationen, die ihre **sensiblen** Konten nicht sichern, ermöglichen Angreifern den Zugang zu diesen.

Böswillige Akteure suchen ähnlich wie Diebe häufig in jeder Umgebung nach dem einfachsten und lautlosesten Weg. Sensible Konten mit riskanten Lateral-Movement-Pfaden eröffnen Gelegenheiten für Angreifer und können Risiken darstellen.

Beispielsweise sind die riskanten Pfade leichter für Angreifer sichtbar und können diesen im Fall einer Kompromittierung Zugriff auf die sensibelsten Entitäten Ihrer Organisation verschaffen.

## <a name="how-do-i-use-this-security-assessment"></a>Wie wird diese Sicherheitsbewertung verwendet?

1. Verwenden Sie die Berichtstabelle, um zu ermitteln, welche Ihrer **sensiblen** Konten riskante Lateral-Movement-Pfade aufweisen.
    ![Überprüfen der wichtigsten betroffenen Entitäten und Erstellen eines Aktionsplans](media/atp-cas-isp-riskiest-lmp-1.png)
1. Ergreifen Sie entsprechende Maßnahmen:
    - Entfernen Sie die Entität aus der Gruppe, die in der Empfehlung angegeben wird.
    - Entfernen Sie die lokalen Administratorberechtigungen für die Entität von dem Gerät, das in der Empfehlung angegeben wird.

    > [!NOTE]
    > Warten Sie 24 Stunden, und überprüfen Sie dann, ob die Empfehlung nicht mehr in der Liste angezeigt wird.

> [!NOTE]
> Diese Bewertung wird alle 24 Stunden aktualisiert.

## <a name="see-also"></a>Weitere Informationen

- [Verwenden von Aktivitätsfiltern und Erstellen von Aktionsrichtlinien mit Azure ATP in Microsoft Cloud App Security](atp-activities-filtering-mcas.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
