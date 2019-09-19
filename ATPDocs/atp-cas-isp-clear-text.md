---
title: Azure Advanced Threat Protection-Bewertungen des Risikos durch Klartextinformationen | Microsoft-Dokumentation
description: Dieser Artikel bietet eine Übersicht über den Bericht von Azure ATP zur Bewertung des Identitätssicherheitsstatus von Klartext.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 07/08/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 124957bb-5882-4fcf-bab2-b74b0c69571d
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 8e99ab22e65538aba6f645d6bb7929330244cafc
ms.sourcegitcommit: 475df3e87d8476ff13e48ebc7a722f46f29dab70
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71007551"
---
# <a name="security-assessment-entities-exposing-credentials-in-clear-text-----preview"></a>Sicherheitsbewertung: Verfügbarmachen von Anmeldeinformationen in Klartext durch Entitäten – Vorschau

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
1. Nachdem Sie sich vergewissert haben, dass das Problem behoben ist, empfiehlt es sich, LDAP-Signaturen auf Domänencontrollerebene als erforderlich festzulegen. Weitere Informationen über das Signieren auf LDAP-Servern finden Sie unter [Domänencontroller: Signaturanforderungen für LDAP-Server](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/domain-controller-ldap-server-signing-requirements). 
 

## <a name="next-steps"></a>Nächste Schritte
- [Azure ATP-Aktivitätsfilter in Cloud App Security](atp-activities-filtering-mcas.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
