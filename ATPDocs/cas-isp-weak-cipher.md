---
title: Sicherheitsstatus Bewertungsbericht von Microsoft Defender für Identity Weak
description: Dieser Artikel bietet eine Übersicht über den Bericht "Sicherheitsstatus Bewertung für schwache Chiffre Identität" von Microsoft Defender for Identity.
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: 9001fcc0aa871c14924fdd5c913e488e00104f3b
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/03/2020
ms.locfileid: "96543500"
---
# <a name="security-assessment-weak-cipher-usage"></a>Sicherheitsbewertung: Verwendung schwacher Verschlüsselungen

## <a name="what-are-weak-ciphers"></a>Was bedeutet schwache Verschlüsselung?

Kryptografie basiert auf Verschlüsselungen zum Verschlüsseln unserer Daten. RC4 (Rivest Cipher 4, auch bekannt als ARC4 oder ARCFOUR, was Alleged RC4 bedeutet) ist ein Beispiel dafür. Obwohl RC4 aus Gründen der Einfachheit und Geschwindigkeit bemerkenswert ist, wurden seit der ursprünglichen Version von RC4 mehrere Schwachstellen erkannt, die das System unsicher machen. RC4 ist besonders anfällig, wenn der Anfang des Ausgabeschlüsselstroms nicht verworfen wird, oder wenn nicht zufällige oder verwandte Schlüssel verwendet werden.

## <a name="how-do-i-use-this-security-assessment-to-improve-my-organizational-security-posture"></a>Wie wird diese Sicherheitsbewertung verwendet, um den Sicherheitsstatus meiner Organisation zu verbessern?

1. Sehen Sie sich die Sicherheitsbewertung für die Verwendung schwacher Verschlüsselungen an.
    ![Bewertung der Verwendung von schwacher Verschlüsselung](media/cas-isp-weak-cipher-2.png)
1. Überprüfen Sie, warum die identifizierten Clients und Server eine schwache Verschlüsselung verwenden.
1. Korrigieren Sie die Fehler, und deaktivieren Sie die Verwendung von RC4 und/oder anderen schwachen Verschlüsselungen (wie z. B. DES/3DES).
1. Weitere Informationen zur Deaktivierung von RC4 finden Sie in der [Microsoft-Sicherheitsempfehlung](https://support.microsoft.com/help/2868725/microsoft-security-advisory-update-for-disabling-rc4).

> [!NOTE]
> Diese Bewertung wird nahezu in Echtzeit aktualisiert.

## <a name="remediation"></a>Wiederherstellung

Deaktivieren Sie Client und Server, die nicht mehr RC4-Verschlüsselungssammlungen verwenden sollen, indem Sie die folgenden Registrierungsschlüssel festlegen. Nach der Deaktivierung kann jeder Server oder Client, der mit einem anderen Client oder Server kommuniziert, der die Verwendung von RC4 erfordert, verhindern, dass eine Verbindung stattfindet. Clients, auf denen diese Einstellung bereitgestellt wird, können keine Verbindung mit Standorten herstellen, die RC4 erfordern, und Server, die diese Einstellung bereitstellen, können keine Clients bedienen, die RC4 verwenden müssen.

> [!NOTE]
> Testen Sie daher unbedingt die folgenden Einstellungen in einer kontrollierten Umgebung, bevor Sie sie in der Produktion aktivieren.
>
> - [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128]   "Enabled"=dword:00000000
> - [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128]   "Enabled"=dword:00000000
> - [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128]   "Enabled"=dword:00000000

Weitere Informationen zum Download und Aktualisieren der Bearbeitungen für die Registrierung finden Sie in den [Microsoft-Sicherheitsempfehlungen](/security-updates/SecurityAdvisories/2013/2868725).

## <a name="next-steps"></a>Nächste Schritte

- [[!INCLUDE [Product short](includes/product-short.md)] Aktivitäten Filtern in Cloud App Security](activities-filtering-mcas.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
