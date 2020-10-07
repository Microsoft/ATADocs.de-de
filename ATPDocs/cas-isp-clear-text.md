---
title: Azure Advanced Threat Protection-Bewertungen des Risikos durch Klartextinformationen
description: Dieser Artikel bietet eine Übersicht über den Bericht von Azure ATP zur Bewertung des Identitätssicherheitsstatus von Klartext.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 08/25/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 124957bb-5882-4fcf-bab2-b74b0c69571d
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 413e7482900f34428056401085f04195ccb4e720
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2020
ms.locfileid: "90913226"
---
# <a name="security-assessment-entities-exposing-credentials-in-clear-text"></a>Sicherheitsbewertung: Verfügbarmachen von Anmeldeinformationen in Klartext durch Entitäten

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

![Verhindern von Risiken durch Anmeldeinformationen in Klartext in Cloud App Security](media/atp-cas-isp-clear-text-1.png)

## <a name="what-information-does-the-prevent-clear-text-security-assessment-provide"></a>Welche Informationen stellt die Bewertung der Sicherheit von Klartextinformationen bereit?

Diese Sicherheitsbewertung überwacht Ihren Datenverkehr auf jegliche Entitäten, die Anmeldeinformationen in Klartext verfügbar machen, sendet Ihnen Warnungen zu den aktuellen Risiken (den am stärksten betroffenen Entitäten) in Ihrer Organisation und empfiehlt Maßnahmen zur Beseitigung der Risiken.

## <a name="why-is-clear-text-credential-exposure-risky"></a>Warum bergen Anmeldeinformationen in Klartext ein Risiko?

Entitäten, die Anmeldeinformationen in Klartext verfügbar machen, stellen nicht nur für die fragliche Entität ein Risiko dar, sondern für Ihre gesamte Organisation.

Das erhöhte Risiko liegt darin begründet, dass unsicherer Datenverkehr wie z.B. einfache LDAP-Bindungen hochgradig anfällig für Abfangaktionen durch Man-in-the-Middle-Angriffe sind. Diese Arten von Angriffen ziehen schädliche Aktivitäten nach sich, beispielsweise die Offenlegung von Anmeldeinformationen, die von einem Angreifer genutzt werden können, um Ihrer Organisation zu schaden.

## <a name="how-do-i-use-this-security-assessment-to-improve-my-organizational-security-posture"></a>Wie wird diese Sicherheitsbewertung verwendet, um den Sicherheitsstatus meiner Organisation zu verbessern?

1. Sehen Sie sich die Sicherheitsbewertung für betroffene Entitäten an.
    ![Überprüfen der wichtigsten betroffenen Entitäten und Erstellen eines Aktionsplans](media/atp-cas-isp-clear-text-2.png)
1. Finden Sie heraus, warum diese Entitäten LDAP in Klartext verwenden.
1. Beheben Sie die Probleme, und beenden Sie die Offenlegung dieser Informationen.
1. Nachdem Sie sich vergewissert haben, dass das Problem behoben ist, empfiehlt es sich, LDAP-Signaturen auf Domänencontrollerebene als erforderlich festzulegen. Weitere Informationen über das Signieren auf LDAP-Servern finden Sie unter [Domänencontroller: Signaturanforderungen für LDAP-Server](/windows/security/threat-protection/security-policy-settings/domain-controller-ldap-server-signing-requirements).

> [!NOTE]
> Diese Bewertung wird nahezu in Echtzeit aktualisiert.

## <a name="next-steps"></a>Nächste Schritte

- [Azure ATP-Aktivitätsfilter in Cloud App Security](activities-filtering-mcas.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)