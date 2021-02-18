---
title: 'Tutorialübersicht: Microsoft Defender for Identity-Sicherheitswarnungsumgebung'
description: Diese Tutorialübersicht beschreibt die vier Teile der Microsoft Defender for Identity-Sicherheitswarnungsumgebung zur Simulation von Bedrohungen für die Erkennung durch Microsoft Defender for Identity.
ms.date: 10/26/2020
ms.topic: tutorial
ms.openlocfilehash: 61602a6bb7d3037d2278c2f492395ed058e8910b
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533561"
---
# <a name="tutorial-overview-microsoft-defender-for-identity-security-alert-lab"></a>Übersicht über das Tutorial: Lab für Microsoft Defender for Identity-Sicherheitswarnungen

Das Tutorial zur [!INCLUDE [Product long](includes/product-long.md)]-Sicherheitswarnungsumgebung soll die Funktionen von **[!INCLUDE [Product short](includes/product-short.md)]** zum Identifizieren und Erkennen verdächtiger Aktivitäten und potenzieller Angriffe auf Ihr Netzwerk veranschaulichen. Dieses vierteilige Tutorial erklärt, wie Sie eine Arbeitsumgebung installieren und konfigurieren, um *diskrete* Erkennungen von [!INCLUDE [Product short](includes/product-short.md)] zu testen. Die Testumgebung konzentriert sich auf *signaturbasierte* Funktionen von [!INCLUDE [Product short](includes/product-short.md)]. Die Testumgebung enthält keine erweiterten Verhaltenserkennungen auf Machine Learning-, Benutzer- oder Entitätsbasis, da diese Erkennungen eine Lernphase mit echtem Netzwerkverkehr von bis zu 30 Tagen erfordern.

## <a name="lab-setup"></a>Setup der Übungsumgebung

Dieses erste Tutorial dieser vierteiligen Reihe führt Sie durch die Erstellung einer Testumgebung für diskrete Erkennungen durch [!INCLUDE [Product short](includes/product-short.md)]. Das Tutorial enthält Informationen über Computer, Benutzer und Tools, die zum Einrichten der Testumgebung und zum Abschluss der Playbooks benötigt werden. Die Anleitung geht davon aus, dass Sie einen Domänencontroller und Arbeitsstationen für die Verwendung in der Testumgebung sowie andere administrative Aufgaben sicher einrichten können. Je mehr Ihre Testumgebung dem vorgeschlagenen Testumgebungssetup entspricht, desto einfacher können Sie die [!INCLUDE [Product short](includes/product-short.md)]-Testverfahren befolgen. Wenn Ihre Testumgebung eingerichtet ist, verwenden Sie zum Testen die Playbooks für [!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnungen.

> [!div class="nextstepaction"]
> [Setup einer ATP-Sicherheitswarnungsumgebung](playbook-setup-lab.md)

## <a name="reconnaissance-playbook"></a>Playbook zu Reconnaissance

Das zweite Tutorial in dieser vierteiligen Reihe ist ein Playbook zu Reconnaissance. Mit Reconnaissanceaktivitäten können Angreifer umfassende Kenntnisse und eine vollständige Zuordnung Ihrer Umgebung für die spätere Verwendung erzielen. Das Playbook zeigt Ihnen anhand von Beispielen für gängige, öffentlich zugängliche Hacking- und Angriffstools einige der Möglichkeiten von [!INCLUDE [Product short](includes/product-short.md)], verdächtige Aktivitäten aus potenziellen Angriffen zu identifizieren und zu erkennen.

> [!div class="nextstepaction"]
> [Playbook zu Reconnaissance](playbook-reconnaissance.md)

## <a name="lateral-movement-playbook"></a>Lateral Movement-Playbook

Das Lateral Movement-Playbook ist das dritte Tutorial der vierteiligen Reihe. Seitliche Verschiebungen werden von Angreifern durchgeführt, um die Domänendominanz zu erhalten. Während der Ausführung dieses Playbooks werden Bedrohungserkennungen für den Lateral Movement-Pfad und Sicherheitswarnungen von [!INCLUDE [Product short](includes/product-short.md)] aus den simulierten seitlichen Verschiebungen angezeigt, die Sie in Ihrer Testumgebung ausführen.  

> [!div class="nextstepaction"]
> [Lateral Movement-Playbook](playbook-lateral-movement.md)

## <a name="domain-dominance-playbook"></a>Playbook zu Domänendominanz

Das letzte Tutorial in der vierteiligen Reihe ist das Tutorial zum Playbook zu Domänendominanz. Während der Phase der Domänendominanz hat ein Angreifer bereits legitime Anmeldedaten für den Zugriff auf Ihren Domänencontroller erlangt, und versucht, eine dauerhafte Domänendominanz zu erreichen. Sie simulieren einige gängige Domänendominanzmethoden, um die domänendominanzorientierte Bedrohungserkennung und die Sicherheitswarnungsdienste von [!INCLUDE [Product short](includes/product-short.md)] zu demonstrieren.

> [!div class="nextstepaction"]
> [Playbook zu Domänendominanz](playbook-domain-dominance.md)


## <a name="join-the-community"></a>Beitritt zur Community

Haben Sie weitere Fragen, oder möchten Sie mit anderen über [!INCLUDE [Product short](includes/product-short.md)] und damit verbundene Sicherheitsaspekte diskutieren? Treten Sie noch heute der [[!INCLUDE [Product short](includes/product-short.md)]Community](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) bei.
