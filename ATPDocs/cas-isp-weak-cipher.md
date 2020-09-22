---
title: Bericht zur Bewertung des Identitätssicherheitsstatus der schwachen Azure ATP-Verschlüsselung
description: Dieser Artikel bietet eine Übersicht über den Bericht zur Bewertung des Identitätssicherheitsstatus der schwachen Azure ATP-Verschlüsselung.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 08/25/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: cc82212b-7d25-4ec7-828d-2475ff40d685
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 728103079da513129a55875d28f360c5cd176b47
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2020
ms.locfileid: "90911942"
---
# <a name="security-assessment-weak-cipher-usage"></a>Sicherheitsbewertung: Verwendung schwacher Verschlüsselungen

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

## <a name="what-are-weak-ciphers"></a>Was bedeutet schwache Verschlüsselung?

Kryptografie basiert auf Verschlüsselungen zum Verschlüsseln unserer Daten. RC4 (Rivest Cipher 4, auch bekannt als ARC4 oder ARCFOUR, was Alleged RC4 bedeutet) ist ein Beispiel dafür. Obwohl RC4 aus Gründen der Einfachheit und Geschwindigkeit bemerkenswert ist, wurden seit der ursprünglichen Version von RC4 mehrere Schwachstellen erkannt, die das System unsicher machen. RC4 ist besonders anfällig, wenn der Anfang des Ausgabeschlüsselstroms nicht verworfen wird, oder wenn nicht zufällige oder verwandte Schlüssel verwendet werden.

## <a name="how-do-i-use-this-security-assessment-to-improve-my-organizational-security-posture"></a>Wie wird diese Sicherheitsbewertung verwendet, um den Sicherheitsstatus meiner Organisation zu verbessern?

1. Sehen Sie sich die Sicherheitsbewertung für die Verwendung schwacher Verschlüsselungen an.
    ![Bewertung der Verwendung von schwacher Verschlüsselung](media/atp-cas-isp-weak-cipher-2.png)
1. Überprüfen Sie, warum die identifizierten Clients und Server eine schwache Verschlüsselung verwenden.
1. Korrigieren Sie die Fehler, und deaktivieren Sie die Verwendung von RC4 und/oder anderen schwachen Verschlüsselungen (wie z. B. DES/3DES).
1. Weitere Informationen zur Deaktivierung von RC4 finden Sie in der [Microsoft-Sicherheitsempfehlung](https://support.microsoft.com/help/2868725/microsoft-security-advisory-update-for-disabling-rc4).

> [!NOTE]
> Diese Bewertung wird nahezu in Echtzeit aktualisiert.

## <a name="remediation"></a>Wiederherstellung

Deaktivieren Sie Client und Server, die nicht mehr RC4-Verschlüsselungssammlungen verwenden sollen, indem Sie die folgenden Registrierungsschlüssel festlegen. Nach der Deaktivierung kann jeder Server oder Client, der mit einem anderen Client oder Server kommuniziert, der die Verwendung von RC4 erfordert, verhindern, dass eine Verbindung stattfindet. Clients, bei denen die Einstellung bereitgestellt wird, können keine Verbindung zu Websites herstellen, die RC4 erfordern. Server, die diese Einstellung bereitstellen, können keine Clients bedienen, die RC4 erfordern.

> [!NOTE]
> Testen Sie daher unbedingt die folgenden Einstellungen in einer kontrollierten Umgebung, bevor Sie sie in der Produktion aktivieren.
>
> - [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128]   "Enabled"=dword:00000000
> - [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128]   "Enabled"=dword:00000000
> - [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128]   "Enabled"=dword:00000000

Weitere Informationen zum Download und Aktualisieren der Bearbeitungen für die Registrierung finden Sie in den [Microsoft-Sicherheitsempfehlungen](/security-updates/SecurityAdvisories/2013/2868725).

## <a name="next-steps"></a>Nächste Schritte

- [Azure ATP-Aktivitätsfilter in Cloud App Security](activities-filtering-mcas.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)