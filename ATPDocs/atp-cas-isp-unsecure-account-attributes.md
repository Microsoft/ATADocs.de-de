---
title: 'Azure Advanced Threat Protection: Unsichere Bewertungen für Kontoattribute'
description: Dieser Artikel bietet eine Übersicht über die Azure ATP-Entitäten mit unsicheren Attributen im Bericht zur Bewertung des Identitätssicherheitsstatus.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 06/23/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2fe62047-75ef-4b2e-b4aa-72860e39b4e4
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 59f3f8a201b78667ef5c8d6d20da177104dc3a38
ms.sourcegitcommit: 073154998f5fdfbefe276888ffb034dfce368662
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/23/2020
ms.locfileid: "85256865"
---
# <a name="security-assessment-unsecure-account-attributes"></a>Sicherheitsbewertung: Unsichere Kontoattribute

## <a name="what-are-unsecure-account-attributes"></a>Was sind unsichere Kontoattribute?

Azure ATP überwacht Ihre Umgebung fortlaufend, um Konten mit Attributwerten zu identifizieren, die ein Sicherheitsrisiko darstellen, und erfasst Berichte zu diesen Konten, um Sie bei der Schutz Ihrer Umgebung zu unterstützen.

## <a name="what-risk-do-unsecure-account-attributes-pose"></a>Welches Risiko stellen unsichere Kontoattribute dar?

Organisationen, die ihre Kontoattribute nicht sichern können, lassen die Tür für böswillige Akteure offen.

Böswillige Akteure suchen ähnlich wie Diebe häufig in jeder Umgebung nach dem einfachsten und lautlosesten Weg. Konten, die mit unsicheren Attributen konfiguriert sind, eröffnen Gelegenheiten für Angreifer und können Risiken darstellen.

Wenn das Attribut *PasswordNotRequired* beispielsweise aktiviert ist, kann ein Angreifer problemlos auf das Konto zugreifen. Das ist besonders riskant, wenn das Konto privilegierten Zugriff auf andere Ressourcen hat.

## <a name="how-do-i-use-this-security-assessment"></a>Wie wird diese Sicherheitsbewertung verwendet?

1. Verwenden Sie die Berichtstabelle, um zu ermitteln, welches Ihrer Konten über unsichere Attribute verfügt.
    ![Überprüfen der wichtigsten betroffenen Entitäten und Erstellen eines Aktionsplans](media/atp-cas-isp-unsecure-account-attributes-1.png)
1. Ergreifen Sie für diese Benutzerkonten entsprechende Maßnahmen, indem Sie die relevanten Attribute ändern oder entfernen.

## <a name="remediation"></a>Wartung

Wenden Sie die geeigneten Behebungsmaßnahmen für die relevanten Attribute an, die in der folgenden Tabelle aufgeführt werden.

| Empfohlene Aktion | Wartung | Grund |
| --- | --- | --- |
| Kerberos-DES-Verschlüsselungstypen für dieses Konto entfernen| Einstellung aus den Kontoeigenschaften in Active Directory Domain Services (AD DS) entfernen | Zum Entfernen dieser Einstellung ist eine Kerberos-Vorauthentifizierung für das Konto erforderlich, wodurch die Sicherheit verbessert wird. |
| Gespeichertes Kennwort mit umkehrbarer Verschlüsselung entfernen | Einstellung aus den Kontoeigenschaften in AD DS entfernen | Wenn Sie diese Einstellung entfernen, ist keine einfache Entschlüsselung des Kennworts für das Konto mehr möglich. |
| Nicht erforderliches Kennwort entfernen | Einstellung aus den Kontoeigenschaften in AD DS entfernen | Zum Entfernen dieser Einstellung muss ein Kennwort für das Konto verwendet werden, um den unbefugten Zugriff auf Ressourcen zu verhindern. |
| Mit schwacher Verschlüsselung gespeichertes Kennwort entfernen | Kennwort für das Konto zurücksetzen | Wenn Sie das Kennwort des Kontos ändern, können stärkere Verschlüsselungsalgorithmen für dessen Schutz verwendet werden. |
| Kerberos-AES-Verschlüsselung aktivieren | AES-Features in den Kontoeigenschaften in AD DS aktivieren | Durch das Aktivieren von AES128_CTS_HMAC_SHA1_96 oder AES256_CTS_HMAC_SHA1_96 für das Konto wird die Verwendung schwächerer Verschlüsselungsverfahren für die Kerberos-Authentifizierung verhindert. |
| Kerberos-DES-Verschlüsselungstypen für dieses Konto entfernen | Einstellung aus den Kontoeigenschaften in AD DS entfernen | Wenn Sie diese Einstellung entfernen, können stärkere Verschlüsselungsalgorithmen für das Kennwort des Kontos verwendet werden. |

## <a name="see-also"></a>Weitere Informationen

- [Verwenden von Aktivitätsfiltern und Erstellen von Aktionsrichtlinien mit Azure ATP in Microsoft Cloud App Security](atp-activities-filtering-mcas.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
