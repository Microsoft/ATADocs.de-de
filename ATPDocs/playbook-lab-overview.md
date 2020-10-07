---
title: Übersicht über Azure ATP Security Alert Lab-Tutorial
description: Diese Tutorialübersicht beschreibt die vier Teile der Azure ATP-Sicherheitswarnungsumgebung zur Simulation von Bedrohungen für die Erkennung durch Azure ATP.
ms.service: azure-advanced-threat-protection
ms.topic: how-to
author: shsagir
ms.author: shsagir
ms.date: 02/28/2019
ms.reviewer: itargoet
ms.openlocfilehash: 380c24fad44cc8af83a98aa5da61cd835bbe7653
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2020
ms.locfileid: "90912617"
---
# <a name="tutorial-overview-atp-security-alert-lab"></a>Tutorial (Übersicht): ATP-Sicherheits Warnungs Labor

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Das Tutorial zur Azure ATP-Sicherheitswarnungsumgebung soll die Funktionen von **Azure ATP** zum Identifizieren und Erkennen verdächtiger Aktivitäten und potenzieller Angriffe auf Ihr Netzwerk veranschaulichen. Dieses vierteilige Tutorial erklärt, wie Sie eine Arbeitsumgebung installieren und konfigurieren, um *diskrete* Erkennungen durch Azure ATP zu testen. Die Testumgebung konzentriert sich auf *signaturbasierte* Funktionen von Azure ATP. Die Testumgebung enthält keine erweiterten Verhaltenserkennungen auf Machine Learning-, Benutzer- oder Entitätsbasis, da diese Erkennungen eine Lernphase mit echtem Netzwerkverkehr von bis zu 30 Tagen erfordern.

## <a name="lab-setup"></a>Setup der Übungsumgebung

Dieses erste Tutorial dieser vierteiligen Reihe führt Sie durch die Erstellung einer Testumgebung für diskrete Erkennungen durch Azure ATP. Das Tutorial enthält Informationen über Computer, Benutzer und Tools, die zum Einrichten der Testumgebung und zum Abschluss der Playbooks benötigt werden. Die Anleitung geht davon aus, dass Sie einen Domänencontroller und Arbeitsstationen für die Verwendung in der Testumgebung sowie andere administrative Aufgaben sicher einrichten können. Je mehr Ihre Testumgebung dem vorgeschlagenen Testumgebungssetup entspricht, desto einfacher können Sie die Azure ATP-Testverfahren befolgen. Wenn Ihre Testumgebung eingerichtet ist, verwenden Sie zum Testen die Playbooks für Azure ATP-Sicherheitswarnungen.

> [!div class="nextstepaction"]
> [Setup einer ATP-Sicherheitswarnungsumgebung](playbook-setup-lab.md)

## <a name="reconnaissance-playbook"></a>Playbook zu Reconnaissance

Das zweite Tutorial in dieser vierteiligen Reihe ist ein Playbook zu Reconnaissance. Mit Reconnaissanceaktivitäten können Angreifer umfassende Kenntnisse und eine vollständige Zuordnung Ihrer Umgebung für die spätere Verwendung erzielen. Das Playbook zeigt Ihnen anhand von Beispielen für gängige, öffentlich zugängliche Hacking- und Angriffstools einige der Möglichkeiten von Azure ATP, verdächtige Aktivitäten aus potenziellen Angriffen zu identifizieren und zu erkennen.

> [!div class="nextstepaction"]
> [Playbook zu Reconnaissance](playbook-reconnaissance.md)


## <a name="lateral-movement-playbook"></a>Lateral Movement-Playbook

Das Lateral Movement-Playbook ist das dritte Tutorial der vierteiligen Reihe. Seitliche Verschiebungen werden von Angreifern durchgeführt, um die Domänendominanz zu erhalten. Während der Ausführung dieses Playbooks werden Bedrohungserkennungen für den Lateral Movement-Pfad und Sicherheitswarnungen von Azure ATP aus den simulierten seitlichen Verschiebungen angezeigt, die Sie in Ihrer Testumgebung ausführen.  

> [!div class="nextstepaction"]
> [Lateral Movement-Playbook](playbook-lateral-movement.md)

## <a name="domain-dominance-playbook"></a>Playbook zu Domänendominanz

Das letzte Tutorial in der vierteiligen Reihe ist das Tutorial zum Playbook zu Domänendominanz. Während der Phase der Domänendominanz hat ein Angreifer bereits legitime Anmeldedaten für den Zugriff auf Ihren Domänencontroller erlangt, und versucht, eine dauerhafte Domänendominanz zu erreichen. Sie simulieren einige gängige Domänendominanzmethoden, um die domänendominanzorientierte Bedrohungserkennung und die Sicherheitswarnungsdienste von Azure ATP zu demonstrieren.

> [!div class="nextstepaction"]
> [Playbook zu Domänendominanz](playbook-domain-dominance.md)


## <a name="join-the-community"></a>Beitritt zur Community

Haben Sie weitere Fragen, oder möchten Sie mit anderen über Azure ATP und damit verbundene Sicherheitsaspekte diskutieren? Treten Sie noch heute der [Azure ATP-Community](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) bei!