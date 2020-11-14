---
title: Was ist Microsoft Defender for Identity?
description: In diesem Artikel erfahren Sie, was Microsoft Defender for Identity ist und welche Arten von verdächtigen Aktivitäten dieser Clouddienst erkennen kann.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/27/2020
ms.topic: overview
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6bd5e8677a37555db09925d98d242334e1e4967c
ms.sourcegitcommit: 13d1ba61abae691d38d8e210b3adad71285d5c26
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/05/2020
ms.locfileid: "93380623"
---
# <a name="what-is-product-long"></a>Was ist [!INCLUDE [Product long](includes/product-long.md)]?

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

[!INCLUDE [Product long](includes/product-long.md)] (ehemals Azure Advanced Threat Protection bzw. Azure ATP) ist eine cloudbasierte Sicherheitslösung, die Signale Ihrer lokalen Active Directory-Instanz nutzt, um komplexe Bedrohungen, gefährdete Identitäten und schädliche Insideraktionen gegen Ihre Organisation zu identifizieren und zu erkennen, und die Sie bei der Untersuchung dieser Bedrohungen unterstützt.

[!INCLUDE [Product short](includes/product-short.md)] bietet SecOp-Analysten und -Sicherheitsexperten, die Probleme beim Erkennen erweiterter Angriffe in Hybridumgebungen haben, folgende Funktionen:

- Überwachung von Benutzern, Entitätsverhalten und -aktivitäten mit lernbasierter Analyse
- Schutz von in Active Directory gespeicherten Benutzeridentitäten und Anmeldeinformationen
- Identifikation und Untersuchung verdächtiger Benutzeraktivitäten und erweiterter Angriffe in der gesamten Kill Chain
- Bereitstellung eindeutiger Informationen zu einem Incident in einer einfachen Zeitachse zur schnellen Selektierung

## <a name="monitor-and-profile-user-behavior-and-activities"></a>Überwachung und Profiling von Benutzerverhalten und -aktivitäten

[!INCLUDE [Product short](includes/product-short.md)] überwacht und analysiert netzwerkübergreifend Benutzeraktivitäten und -informationen, z. B. Berechtigungen und Gruppenmitgliedschaften, und erstellt dabei für jeden Benutzer eine verhaltensbasierte Baseline. Anschließend identifiziert [!INCLUDE [Product short](includes/product-short.md)] Anomalien mit integrierter adaptiver Intelligenz und gewährt Ihnen Einblicke in verdächtige Aktivitäten und Ereignisse. Dadurch werden Ihnen komplexe Bedrohungen, gefährdete Benutzer und Insiderbedrohungen Ihrer Organisation angezeigt. Mit den proprietären Sensoren von [!INCLUDE [Product short](includes/product-short.md)] werden Domänencontroller der Organisation überwacht. Dadurch wird von jedem Gerät aus ein umfassender Überblick über alle Benutzeraktivitäten geboten.

## <a name="protect-user-identities-and-reduce-the-attack-surface"></a>Schutz von Benutzeridentitäten und Verringern der Angriffsfläche

[!INCLUDE [Product short](includes/product-short.md)] gewährt Ihnen wertvolle Einblicke in Identitätskonfigurationen und stellt empfohlene bewährte Methoden für die Sicherheit bereit. Mithilfe von [!INCLUDE [Product short](includes/product-short.md)] können Sie durch Sicherheitsberichte und die Analyse von Benutzerprofilen die Angriffsfläche Ihrer Organisation deutlich reduzieren, wodurch auch die Gefährdung von Benutzeranmeldeinformationen sowie die Gefährdung durch einen Angriff verringert werden kann. Mithilfe der visuellen Lateral Movement-Pfade von [!INCLUDE [Product short](includes/product-short.md)] verstehen Sie schnell, wie genau sich ein Angreifer lateral innerhalb Ihrer Organisation bewegen kann, um sensible Konten zu gefährden. Die Lösung unterstützt Sie dabei, diese Risiken im Voraus zu vermeiden. Zudem können Sie mithilfe der Sicherheitsberichte von [!INCLUDE [Product short](includes/product-short.md)] Benutzer und Geräte identifizieren, die sich mit Klartextkennwörtern authentifizieren, und weitere Einblicke gewinnen, um den Sicherheitsstatus und die Richtlinien Ihrer Organisation zu verbessern.

## <a name="identify-suspicious-activities-and-advanced-attacks-across-the-cyber-attack-kill-chain"></a>Identifizieren verdächtiger Aktivitäten und erweiterter Angriffe über die Kill Chain des Cyberangriffs

Angriffe werden in der Regel gegen eine beliebige zugängliche Entität gestartet, wie z.B. einen Benutzer mit geringfügigen Berechtigungen, und verschieben sich anschließend schnell seitwärts, bis der Angreifer Zugriff auf wertvolle Objekte erhält (z.B. sensible Konten, Domänenadministratoren und streng vertrauliche Daten). [!INCLUDE [Product short](includes/product-short.md)] erkennt diese erweiterten Bedrohungen von Grund auf während der gesamten Kill Chain des Cyberangriffs:

### <a name="reconnaissance"></a>Reconnaissance

Identifizieren nicht autorisierter Benutzer und der Versuche von Angreifern, Informationen zu erhalten. Angreifer suchen nach Informationen zu Benutzernamen, der Gruppenmitgliedschaft von Benutzern, Geräten zugewiesenen IP-Adressen, Ressourcen und mehr, wobei sie eine Vielzahl von Methoden verwenden.

### <a name="compromised-credentials"></a>Gefährdete Anmeldeinformationen

Identifizieren von Versuchen zur Gefährdung von Benutzeranmeldeinformationen über Brute-Force-Angriffe, fehlgeschlagene Authentifizierungen, Änderungen der Gruppenmitgliedschaft von Benutzern und weitere Methoden.

### <a name="lateral-movements"></a>Seitliche Verschiebungen

Erkennen von Versuchen zur seitlichen Verschiebung innerhalb des Netzwerks, um mithilfe von Methoden wie „Pass-the-Ticket“, „Pass-the-Hash“, „Overpass-the-Hash“ und mehr weitere Kontrolle über sensible Benutzer zu erlangen.

### <a name="domain-dominance"></a>Domänendominanz

Hervorheben des Angreiferverhaltens bei Erreichen der Domänendominanz über die Ausführung von Remotecode auf dem Domänencontroller und Methoden wie „DC Shadow“, die böswillige Replikation des Domänencontrollers, Golden Ticket-Aktivitäten und mehr.

## <a name="investigate-alerts-and-user-activities"></a>Untersuchen von Warnungen und Benutzeraktivitäten

[!INCLUDE [Product short](includes/product-short.md)] wurde dafür konzipiert, die Anzahl allgemeiner Warnungen zu reduzieren, damit nur relevante, wichtige Sicherheitswarnungen in einer übersichtlichen Zeitskala mit gegen die Organisation gerichteten Angriffen in Echtzeit bereitgestellt werden können. Dank der [!INCLUDE [Product short](includes/product-short.md)]-Ansicht mit der Zeitskala zu Angriffen können Sie sich problemlos aufs Wesentliche konzentrieren und intelligente Analysen wirksam einsetzen. Verwenden Sie [!INCLUDE [Product short](includes/product-short.md)], um Bedrohungen ohne großen Aufwand zu untersuchen und organisationsübergreifend Einblicke für Benutzer, Geräte und Netzwerkressourcen zu gewinnen. Die nahtlose Integration mit Microsoft Defender für Endpunkt bietet durch zusätzliche Erkennung und Schutz vor erweiterten dauerhaften Bedrohungen für das Betriebssystem eine weitere erweiterte Sicherheitsebene.

## <a name="additional-resources-for-product-short"></a>Zusätzliche Ressourcen für [!INCLUDE [Product short](includes/product-short.md)]

### <a name="start-a-free-trial"></a>Kostenlosen Test starten

[https://signup.microsoft.com/Signup?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7&ali=1](https://signup.microsoft.com/Signup?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7&ali=1 "Enterprise Mobility + Security E5")

### <a name="follow-product-short-on-microsoft-tech-community"></a>[!INCLUDE [Product short](includes/product-short.md)] in der Microsoft Tech Community

[https://aka.ms/MDIcommunity](https://aka.ms/MDIcommunity "[!INCLUDE [Product short](includes/product-short.md)] on Microsoft Tech Community")

### <a name="join-the-product-short-yammer-community"></a>Yammer-Community für [!INCLUDE [Product short](includes/product-short.md)]

[https://www.yammer.com/azureadvisors/#/threads/inGroup?type=in_group&feedId=9386893](https://www.yammer.com/azureadvisors/#/threads/inGroup?type=in_group&feedId=9386893 "[!INCLUDE [Product short](includes/product-short.md)] Yammer community")

### <a name="visit-the-product-short-product-page"></a>Produktseite für [!INCLUDE [Product short](includes/product-short.md)]

[https://www.microsoft.com/microsoft-365/security/identity-defender](https://www.microsoft.com/microsoft-365/security/identity-defender "[!INCLUDE [Product short](includes/product-short.md)] product page")

### <a name="learn-more-about-product-short-architecture"></a>Weitere Informationen über die [!INCLUDE [Product short](includes/product-short.md)]-Architektur

[[!INCLUDE [Product short](includes/product-short.md)]-Architektur](architecture.md)

### <a name="watch-our-videos"></a>Videos

[Stärken Ihres Sicherheitsstatus mit [!INCLUDE [Product short](includes/product-short.md)]](https://techcommunity.microsoft.com/t5/video-hub/bolster-your-security-posture-with-microsoft-defender-for/m-p/1698841) – Erfahren Sie, wie Sie bekannte schlechte Methoden identifizieren und proaktiv lösen, um einen besseren Integritätszustand für Ihre Umgebung und mehr Schutz vor böswilligen Akteuren zu erzielen. [YouTube-Video ansehen](https://youtu.be/nx5rrxVuRTk)

[Untersuchen von Incidents mit [!INCLUDE [Product short](includes/product-short.md)]](https://techcommunity.microsoft.com/t5/video-hub/incident-investigation-with-microsoft-defender-for-identity/m-p/1698840) – Erfahren Sie, wie Sie erweiterte Bedrohungen für Identitäten und Domänencontrollern mit [!INCLUDE [Product short](includes/product-short.md)] erkennen, untersuchen und behandeln. Beginnend mit einer Warnung in [!INCLUDE [Product short](includes/product-short.md)] wird veranschaulicht, wie Informationen zu einem Incident korreliert werden, wie mithilfe der von [!INCLUDE [Product short](includes/product-short.md)] erfassten Informationen nach Bedrohungen gesucht wird und wie automatische Maßnahmen für Incidents initiiert werden können, um den Incident entgegenzuwirken, bevor größere Probleme entstehen. [YouTube-Video ansehen](https://youtu.be/geWU4It6S48)

## <a name="whats-next"></a>Ausblick

Es wird empfohlen, [!INCLUDE [Product short](includes/product-short.md)] in drei Phasen bereitzustellen:

### <a name="phase-1"></a>Phase 1

1. Richten Sie [!INCLUDE [Product short](includes/product-short.md)] zum Schutz Ihrer primären Umgebungen ein. Mit dem [!INCLUDE [Product short](includes/product-short.md)]-Modell zur schnellen Bereitstellung können Sie mit dem Schutz Ihrer Organisation noch heute beginnen. [Installieren von [!INCLUDE [Product short](includes/product-short.md)]](install-step1.md)
1. Legen Sie [Sensitive Accounts](sensitive-accounts.md) (sensible Konten) und [Honeytoken-Konten](install-step7.md) fest.
1. Überprüfen Sie die Berichte und [Lateral Movement-Pfade](use-case-lateral-movement-path.md).

### <a name="phase-2"></a>Phase 2

1. Schützen Sie sämtliche Domänencontroller und [Gesamtstrukturen](multi-forest.md) in Ihrer Organisation.
1. Überwachen Sie alle [Warnungen](working-with-suspicious-activities.md): Untersuchen Sie Warnungen bzgl. Lateral Movement und Domänendominanz.
1. Nehmen Sie das [Leitfaden zu Sicherheitshinweisen](suspicious-activity-guide.md) zur Hilfe, um Bedrohungen zu verstehen und potenzielle Angriffe selektieren zu können.

### <a name="phase-3"></a>Phase 3

1. Integrieren Sie [!INCLUDE [Product short](includes/product-short.md)]-Warnungen in Ihre SecOp-Workflows.

## <a name="see-also"></a>Weitere Informationen

- [Häufig gestellte Fragen zu [!INCLUDE [Product short](includes/product-short.md)]](technical-faq.md)
- [Arbeiten mit Sicherheitswarnungen](working-with-suspicious-activities.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
