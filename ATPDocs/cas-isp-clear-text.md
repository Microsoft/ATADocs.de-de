---
title: Bewertung von Microsoft Defender für die Identitäts offen Stellung von Text
description: Dieser Artikel bietet eine Übersicht über den Microsoft Defender for Identity-Bericht zur Bewertung der Identitäts Sicherheitslage.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 08/25/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6a5d110d35ad3b49205d4c0b7b03412fe26626ae
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2020
ms.locfileid: "94848787"
---
# <a name="security-assessment-entities-exposing-credentials-in-clear-text"></a>Sicherheitsbewertung: Verfügbarmachen von Anmeldeinformationen in Klartext durch Entitäten

![Verhindern von Risiken durch Anmeldeinformationen in Klartext in Cloud App Security](media/cas-isp-clear-text-1.png)

## <a name="what-information-does-the-prevent-clear-text-security-assessment-provide"></a>Welche Informationen stellt die Bewertung der Sicherheit von Klartextinformationen bereit?

Diese Sicherheitsbewertung überwacht Ihren Datenverkehr auf jegliche Entitäten, die Anmeldeinformationen in Klartext verfügbar machen, sendet Ihnen Warnungen zu den aktuellen Risiken (den am stärksten betroffenen Entitäten) in Ihrer Organisation und empfiehlt Maßnahmen zur Beseitigung der Risiken.

## <a name="why-is-clear-text-credential-exposure-risky"></a>Warum bergen Anmeldeinformationen in Klartext ein Risiko?

Entitäten, die Anmeldeinformationen in Klartext verfügbar machen, stellen nicht nur für die fragliche Entität ein Risiko dar, sondern für Ihre gesamte Organisation.

Das erhöhte Risiko liegt darin begründet, dass unsicherer Datenverkehr wie z.B. einfache LDAP-Bindungen hochgradig anfällig für Abfangaktionen durch Man-in-the-Middle-Angriffe sind. Diese Arten von Angriffen ziehen schädliche Aktivitäten nach sich, beispielsweise die Offenlegung von Anmeldeinformationen, die von einem Angreifer genutzt werden können, um Ihrer Organisation zu schaden.

## <a name="how-do-i-use-this-security-assessment-to-improve-my-organizational-security-posture"></a>Wie wird diese Sicherheitsbewertung verwendet, um den Sicherheitsstatus meiner Organisation zu verbessern?

1. Sehen Sie sich die Sicherheitsbewertung für betroffene Entitäten an.
    ![Überprüfen der wichtigsten betroffenen Entitäten und Erstellen eines Aktionsplans](media/cas-isp-clear-text-2.png)
1. Finden Sie heraus, warum diese Entitäten LDAP in Klartext verwenden.
1. Beheben Sie die Probleme, und beenden Sie die Offenlegung dieser Informationen.
1. Nachdem Sie sich vergewissert haben, dass das Problem behoben ist, empfiehlt es sich, LDAP-Signaturen auf Domänencontrollerebene als erforderlich festzulegen. Weitere Informationen über das Signieren auf LDAP-Servern finden Sie unter [Domänencontroller: Signaturanforderungen für LDAP-Server](/windows/security/threat-protection/security-policy-settings/domain-controller-ldap-server-signing-requirements).

> [!NOTE]
> Diese Bewertung wird nahezu in Echtzeit aktualisiert.

## <a name="next-steps"></a>Nächste Schritte

- [[!INCLUDE [Product short](includes/product-short.md)] Aktivitäten Filtern in Cloud App Security](activities-filtering-mcas.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)