---
title: 'Tutorialübersicht: Azure ATP-Sicherheitswarnungsumgebung | Microsoft-Dokumentation'
description: Diese Tutorialübersicht beschreibt die vier Teile der Azure ATP-Sicherheitswarnungsumgebung zur Simulation von Bedrohungen für die Erkennung durch Azure ATP.
ms.service: azure-advanced-threat-protection
ms.topic: tutorial
author: shsagir
ms.author: shsagir
ms.date: 02/28/2019
ms.reviewer: itargoet
ms.openlocfilehash: 644b934622c20fa1be640120fe9c04ea6a89e08c
ms.sourcegitcommit: 9673eb49729a06d3a25d52c0f43c76ac61b9cf89
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/12/2020
ms.locfileid: "75908494"
---
# <a name="tutorial-overview-atp-security-alert-lab"></a>Übersicht über das Tutorial: Lab für ATP-Sicherheitswarnungen

Das Tutorial zur Azure ATP-Sicherheitswarnungsumgebung soll die Funktionen von **Azure ATP** zum Identifizieren und Erkennen verdächtiger Aktivitäten und potenzieller Angriffe auf Ihr Netzwerk veranschaulichen. Dieses vierteilige Tutorial erklärt, wie Sie eine Arbeitsumgebung installieren und konfigurieren, um *diskrete* Erkennungen durch Azure ATP zu testen. Die Testumgebung konzentriert sich auf *signaturbasierte* Funktionen von Azure ATP. Die Testumgebung enthält keine erweiterten Verhaltenserkennungen auf Machine Learning-, Benutzer- oder Entitätsbasis, da diese Erkennungen eine Lernphase mit echtem Netzwerkverkehr von bis zu 30 Tagen erfordern.

## <a name="lab-setup"></a>Einrichten des Labs

Dieses erste Tutorial dieser vierteiligen Reihe führt Sie durch die Erstellung einer Testumgebung für diskrete Erkennungen durch Azure ATP. Das Tutorial enthält Informationen über Computer, Benutzer und Tools, die zum Einrichten der Testumgebung und zum Abschluss der Playbooks benötigt werden. Die Anleitung geht davon aus, dass Sie einen Domänencontroller und Arbeitsstationen für die Verwendung in der Testumgebung sowie andere administrative Aufgaben sicher einrichten können. Je mehr Ihre Testumgebung dem vorgeschlagenen Testumgebungssetup entspricht, desto einfacher können Sie die Azure ATP-Testverfahren befolgen. Wenn Ihre Testumgebung eingerichtet ist, verwenden Sie zum Testen die Playbooks für Azure ATP-Sicherheitswarnungen.

> [!div class="nextstepaction"]
> [Setup einer ATP-Sicherheitswarnungsumgebung](atp-playbook-setup-lab.md)

## <a name="reconnaissance-playbook"></a>Playbook zu Reconnaissance

Das zweite Tutorial in dieser vierteiligen Reihe ist ein Playbook zu Reconnaissance. Mit Reconnaissance-Aktivitäten können Angreifer umfassende Kenntnisse zu eine vollständige Zuordnung Ihrer Umgebung für die spätere Verwendung erzielen. Das Playbook zeigt Ihnen anhand von Beispielen für gängige, öffentlich zugängliche Hacking- und Angriffstools einige der Möglichkeiten von Azure ATP, verdächtige Aktivitäten aus potenziellen Angriffen zu identifizieren und zu erkennen.

> [!div class="nextstepaction"]
> [Playbook zu Reconnaissance](atp-playbook-reconnaissance.md)


## <a name="lateral-movement-playbook"></a>Lateral Movement-Playbook

Das Lateral Movement-Playbook ist das dritte Tutorial der vierteiligen Reihe. Seitliche Verschiebungen werden von Angreifern durchgeführt, um die Domänendominanz zu erhalten. Während der Ausführung dieses Playbooks werden Bedrohungserkennungen für den Lateral Movement-Pfad und Sicherheitswarnungen von Azure ATP aus den simulierten seitlichen Verschiebungen angezeigt, die Sie in Ihrer Testumgebung ausführen.  

> [!div class="nextstepaction"]
> [Lateral Movement-Playbook](atp-playbook-lateral-movement.md)

## <a name="domain-dominance-playbook"></a>Playbook zu Domänendominanz

Das letzte Tutorial in der vierteiligen Reihe ist das Tutorial zum Playbook zu Domänendominanz. Während der Phase der Domänendominanz hat ein Angreifer bereits legitime Anmeldedaten für den Zugriff auf Ihren Domänencontroller erlangt, und versucht, eine dauerhafte Domänendominanz zu erreichen. Sie simulieren einige gängige Domänendominanzmethoden, um die domänendominanzorientierte Bedrohungserkennung und die Sicherheitswarnungsdienste von Azure ATP zu demonstrieren.

> [!div class="nextstepaction"]
> [Playbook zu Domänendominanz](atp-playbook-domain-dominance.md)


## <a name="join-the-community"></a>Beitritt zur Community

Haben Sie weitere Fragen, oder möchten Sie mit anderen über Azure ATP und damit verbundene Sicherheitsaspekte diskutieren? Treten Sie noch heute der [Azure ATP-Community](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) bei!
