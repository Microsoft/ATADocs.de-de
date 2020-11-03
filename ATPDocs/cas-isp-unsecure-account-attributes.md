---
title: Bewertungen von Microsoft Defender für Identity-Konto Attribute
description: Dieser Artikel bietet eine Übersicht über die Entitäten von Microsoft Defender für Identitäts Entitäten mit unsicherem Attribute Identity Security-statusbewertung.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 034948a5a355012aad387aa4d46e6e3c8d342dee
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93277303"
---
# <a name="security-assessment-unsecure-account-attributes"></a>Sicherheitsbewertung: Unsichere Kontoattribute

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

## <a name="what-are-unsecure-account-attributes"></a>Was sind unsichere Kontoattribute?

[!INCLUDE [Product long](includes/product-long.md)] überwacht kontinuierlich Ihre Umgebung, um Konten mit Attributwerten zu identifizieren, die ein Sicherheitsrisiko darstellen, und meldet diese Konten, um Sie beim Schutz Ihrer Umgebung zu unterstützen.

## <a name="what-risk-do-unsecure-account-attributes-pose"></a>Welches Risiko stellen unsichere Kontoattribute dar?

Organisationen, die ihre Kontoattribute nicht sichern können, lassen die Tür für böswillige Akteure offen.

Böswillige Akteure suchen ähnlich wie Diebe häufig in jeder Umgebung nach dem einfachsten und lautlosesten Weg. Konten, die mit unsicheren Attributen konfiguriert sind, eröffnen Gelegenheiten für Angreifer und können Risiken darstellen.

Wenn das Attribut *PasswordNotRequired* beispielsweise aktiviert ist, kann ein Angreifer problemlos auf das Konto zugreifen. Das ist besonders riskant, wenn das Konto privilegierten Zugriff auf andere Ressourcen hat.

## <a name="how-do-i-use-this-security-assessment"></a>Wie wird diese Sicherheitsbewertung verwendet?

1. Verwenden Sie die Berichtstabelle, um zu ermitteln, welches Ihrer Konten über unsichere Attribute verfügt.
    ![Überprüfen der wichtigsten betroffenen Entitäten und Erstellen eines Aktionsplans](media/cas-isp-unsecure-account-attributes-1.png)
1. Ergreifen Sie für diese Benutzerkonten entsprechende Maßnahmen, indem Sie die relevanten Attribute ändern oder entfernen.

> [!NOTE]
> Diese Bewertung wird nahezu in Echtzeit aktualisiert.

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

- [[!INCLUDE [Product short](includes/product-short.md)] Aktivitäten Filtern in Cloud App Security](activities-filtering-mcas.md)
- [Sehen Sie sich das [!INCLUDE [Product short](includes/product-short.md)] Forum an!](https://aka.ms/MDIcommunity)
