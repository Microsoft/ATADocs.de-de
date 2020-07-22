---
title: 'Azure Advanced Threat Protection: Unsichere Bewertungen der SID-Verlaufsattribute'
description: Dieser Artikel bietet eine Übersicht über die Azure ATP-Entitäten mit unsicheren SID-Verlaufsattributen im Bericht zur Bewertung des Identitätssicherheitsstatus.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 04/30/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2fe62047-75ef-4b2e-b4aa-72860e39b4e4
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f10756f3b5fc009e2bd37fff9eff04d1c5c41585
ms.sourcegitcommit: 073154998f5fdfbefe276888ffb034dfce368662
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/23/2020
ms.locfileid: "85256268"
---
# <a name="security-assessment-unsecure-sid-history-attributes"></a>Sicherheitsbewertung: Unsichere SID-Verlaufsattribute

## <a name="what-is-an-unsecure-sid-history-attribute"></a>Was ist ein unsicheres SID-Verlaufsattribut?

Der SID-Verlauf ist ein Attribut, das [Migrationsszenarios](/previous-versions/windows/it-pro/windows-server-2003/cc779590(v=ws.10)) unterstützt. Jedes Benutzerkonto verfügt über eine zugeordnete [Sicherheitskennung](/windows/win32/secauthz/security-identifiers) (Security Identifier, SID), die zum Nachverfolgen des Sicherheitsprinzipals und den Zugriff des Kontos beim Herstellen einer Verbindung zu Ressourcen verwendet wird. Der SID-Verlauf ermöglicht einem anderen Konto Zugriff, damit es effektiv in ein anderes Konto geklont werden kann, und ist äußerst nützlich, um sicherzustellen, dass Benutzer beim Verschieben (Migrieren) von einer Domäne in eine andere den Zugriff beibehalten.

Die Bewertung überprüft Konten mit SID-Verlaufsattributen, bei denen Azure ATP-Profile riskant sein können.

## <a name="what-risk-does-unsecure-sid-history-attribute-pose"></a>Welches Risiko stellt ein unsicheres SID-Verlaufsattribut dar?

Organisationen, die ihre Kontoattribute nicht sichern können, lassen die Tür für böswillige Akteure offen.

Böswillige Akteure suchen ähnlich wie Diebe häufig in jeder Umgebung nach dem einfachsten und lautlosesten Weg. Konten, die mit einem unsicheren SID-Verlaufsattribut konfiguriert sind, stellen einen Einstieg für Angreifer dar und können Risiken ergeben.

Beispielsweise kann ein nicht sensibles Konto in einer Domäne die SID des Unternehmensadministrators und den SID-Verlauf aus einer anderen Domäne in der Active Directory-Gesamtstruktur enthalten, wodurch der Zugriff für das Benutzerkonto auf einen effektiven Domänenadministrator in allen Domänen in der Gesamtstruktur erhöht wird. Wenn Sie über eine Gesamtstruktur-Vertrauensstellung ohne aktivierten SID-Filter (auch als Quarantäne bezeichnet) verfügen, können Sie eine SID aus einer anderen Gesamtstruktur einfügen. Diese wird dann bei der Authentifizierung dem Benutzertoken hinzugefügt und für Zugriffsauswertungen verwendet.

## <a name="how-do-i-use-this-security-assessment"></a>Wie wird diese Sicherheitsbewertung verwendet?

1. Verwenden Sie die Berichtstabelle, um zu ermitteln, welches Ihrer Konten über ein unsicheres SID-Verlaufsattribut verfügt.
    ![Überprüfen der wichtigsten betroffenen Entitäten und Erstellen eines Aktionsplans](media/atp-cas-isp-unsecure-sid-history-attribute-1.png)
1. Nehmen Sie mithilfe von PowerShell und den folgenden Schritten geeignete Maßnahmen vor, um das SID-Verlaufsattribut aus den Konten zu entfernen:

    1. Identifizieren Sie die SID im SIDHistory-Attribut im Konto.

        ```powershell
        Get-ADUser -Identity <account> -Properties SidHistory | Select-Object -ExpandProperty SIDHistory
        ```

    2. Entfernen Sie das SIDHistory-Attribut, indem Sie die zuvor identifizierte SID verwenden.

        ```powershell
        Set-ADUser -Identity <account> -Remove @{SIDHistory='S-1-5-21-...'}
        ```

## <a name="see-also"></a>Weitere Informationen

- [Verwenden von Aktivitätsfiltern und Erstellen von Aktionsrichtlinien mit Azure ATP in Microsoft Cloud App Security](atp-activities-filtering-mcas.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)