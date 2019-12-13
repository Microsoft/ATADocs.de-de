---
title: Was ist Azure Advanced Threat Protection (Azure ATP)? | Microsoft-Dokumentation
description: Hier wird erläutert, worum es sich bei Azure Advanced Threat Protection (Azure ATP) handelt und welche Arten von verdächtigen Aktivitäten erkannt werden können
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 05/07/2019
ms.topic: article
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2d14d0e9-1b03-4bcc-ae97-8fd41526ffc5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 1148e4644ac49da31f2ba62e7bb972f3f9cfbbdf
ms.sourcegitcommit: 6dd002b5a34f230aaada55a6f6178c2f9e1584d9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2019
ms.locfileid: "68484958"
---
# <a name="what-is-azure-advanced-threat-protection"></a>Was ist Azure Advanced Threat Protection?
Azure Advanced Threat Protection (ATP) ist eine cloudbasierte Sicherheitslösung, die Signale Ihres lokalen Active Directory nutzt, um komplexe Bedrohungen, gefährdete Identitäten und schädliche Insider-Aktionen gegen Ihre Organisation zu identifizieren und zu erkennen, und die Sie bei der Untersuchung dieser Bedrohungen unterstützt. Azure ATP bietet SecOp-Analysten und Sicherheitsexperten, die Probleme beim Erkennen erweiterter Angriffe in Hybridumgebungen haben, folgende Funktionen:  
- Überwachung von Benutzern, Entitätsverhalten und -aktivitäten mit lernbasierter Analyse  
- Schutz von in Active Directory gespeicherten Benutzeridentitäten und Anmeldeinformationen  
- Identifikation und Untersuchung verdächtiger Benutzeraktivitäten und erweiterter Angriffe in der gesamten Kill Chain 
- Bereitstellung eindeutiger Informationen zu einem Incident in einer einfachen Zeitachse zur schnellen Selektierung 
 
## <a name="monitor-and-profile-user-behavior-and-activities"></a>Überwachung und Profiling von Benutzerverhalten und -aktivitäten  
Azure ATP überwacht und analysiert netzwerkübergreifend Benutzeraktivitäten und -informationen, wie z.B. Berechtigungen und Gruppenmitgliedschaften, und erstellt dabei für jeden Benutzer eine verhaltensbasierte Baseline. Anschließend identifiziert Azure ATP Anomalien bei integrierter adaptiver Intelligenz und gewährt Ihnen Einblicke in verdächtige Aktivitäten und Ereignisse. Dabei werden Ihnen komplexe Bedrohungen, gefährdete Benutzer und Insider-Bedrohungen Ihrer Organisation angezeigt. Mit den Sensoren von Azure ATP werden Domänencontroller der Organisation überwacht. Dadurch wird von jedem Gerät aus ein umfassender Überblick für alle Benutzeraktivitäten geboten. 
 
## <a name="protect-user-identities-and-reduce-the-attack-surface"></a>Schutz von Benutzeridentitäten und Verringern der Angriffsfläche   
Azure ATP gewährt Ihnen wertvolle Einblicke in Identitätskonfigurationen und stellt empfohlene Best Practices für die Sicherheit bereit. Mithilfe von Azure ATP können Sie durch Sicherheitsberichte und die Analyse von Benutzerprofilen die Angriffsfläche Ihrer Organisation deutlich reduzieren, wodurch auch die Gefährdung von Benutzeranmeldeinformationen sowie die Gefährdung durch einen Angriff verringert werden kann. Mithilfe der visuellen Lateral Movement-Pfade von Azure ATP verstehen Sie schnell, wie genau sich ein Angreifer lateral innerhalb Ihrer Organisation bewegen kann, um sensible Konten zu gefährden. Die Lösung unterstützt Sie dabei, diese Risiken im Vorhinein zu vermeiden. Zudem können Sie mithilfe der Sicherheitsberichte von Azure ATP Benutzer und Geräte identifizieren, die sich mit Klartextkennwörtern authentifizieren, und weitere Einblicke gewinnen, um den Sicherheitsstatus und die Richtlinien Ihrer Organisation zu verbessern.  
 
## <a name="identify-suspicious-activities-and-advanced-attacks-across-the-cyber-attack-kill-chain"></a>Identifizieren verdächtiger Aktivitäten und erweiterter Angriffe über die Kill Chain des Cyberangriffs 

Angriffe werden in der Regel gegen eine beliebige zugängliche Entität gestartet, wie z.B. einen Benutzer mit geringfügigen Berechtigungen, und verschieben sich anschließend schnell seitwärts, bis der Angreifer Zugriff auf wertvolle Objekte erhält (z.B. sensible Konten, Domänenadministratoren und streng vertrauliche Daten). Azure ATP erkennt diese erweiterten Bedrohungen von Grund auf während der gesamten Kill Chain des Cyberangriffs: 

### <a name="reconnaissance"></a>Reconnaissance 
Identifizieren nicht autorisierter Benutzer und der Versuche von Angreifern, Informationen zu erhalten. Angreifer suchen nach Informationen zu Benutzernamen, der Gruppenmitgliedschaft von Benutzern, Geräten zugewiesenen IP-Adressen, Ressourcen und mehr, wobei sie eine Vielzahl von Methoden verwenden.  

### <a name="compromised-credentials"></a>Gefährdete Anmeldeinformationen
Identifizieren von Versuchen zur Gefährdung von Benutzeranmeldeinformationen über Brute-Force-Angriffe, fehlgeschlagene Authentifizierungen, Änderungen der Gruppenmitgliedschaft von Benutzern und weitere Methoden.  

### <a name="lateral-movements"></a>Seitliche Verschiebungen
Erkennen von Versuchen zur seitlichen Verschiebung innerhalb des Netzwerks, um mithilfe von Methoden wie „Pass-the-Ticket“, „Pass-the-Hash“, „Overpass-the-Hash“ und mehr weitere Kontrolle über sensible Benutzer zu erlangen.  

### <a name="domain-dominance"></a>Domänendominanz
Hervorheben des Angreiferverhaltens bei Erreichen der Domänendominanz über die Ausführung von Remotecode auf dem Domänencontroller und Methoden wie „DC Shadow“, die böswillige Replikation des Domänencontrollers, Golden Ticket-Aktivitäten und mehr.

## <a name="investigate-alerts-and-user-activities"></a>Untersuchen von Warnungen und Benutzeraktivitäten  
Azure ATP soll die Anzahl allgemeiner Warnungen reduzieren, damit nur relevante, wichtige Sicherheitswarnungen in einer übersichtlichen Zeitleiste mit gegen die Organisation gerichteten Angriffen in Echtzeit bereitgestellt werden können. Dank der Azure ATP-Ansicht mit der Zeitachse zu Angriffen können Sie sich problemlos aufs Wesentliche konzentrieren und intelligente Analysen wirksam einsetzen. Verwenden Sie Azure ATP, um Bedrohungen ohne großen Aufwand zu untersuchen und organisationsübergreifend Einblicke für Benutzer, Geräte und Netzwerkressourcen zu gewinnen. Die nahtlose Integration in Windows Defender ATP bietet durch zusätzliche Erkennung und Schutz vor erweiterten dauerhaften Bedrohungen für das Betriebssystem eine weitere erweiterte Sicherheitsebene.  

## <a name="additional-resources-for-azure-atp"></a>Zusätzliche Ressourcen für Azure ATP  
### <a name="start-a-free-trial"></a>Kostenlosen Test starten  
[https://signup.microsoft.com/Signup?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7&ali=1](https://signup.microsoft.com/Signup?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7&ali=1 "Enterprise Mobility + Security E5")
 
### <a name="follow-azure-atp-on-microsoft-tech-community"></a>Folgen Sie Azure ATP in der Microsoft Tech Community  
[https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection "Azure ATP on Microsoft Tech Community")
 
### <a name="join-the-azure-atp-yammer-community"></a>Der Azure ATP Yammer-Community beitreten 
[https://www.yammer.com/azureadvisors/#/threads/inGroup?type=in_group&feedId=9386893](https://www.yammer.com/azureadvisors/#/threads/inGroup?type=in_group&feedId=9386893 "Azure ATP Yammer community")
 
### <a name="visit-the-azure-atp-product-page"></a>Besuchen Sie die Azure ATP-Produktseite  
[https://azure.microsoft.com/features/azure-advanced-threat-protection/](https://azure.microsoft.com/features/azure-advanced-threat-protection/ "Azure ATP product page")

### <a name="learn-more-about-azure-atp-architecture"></a>Weitere Informationen zur Azure ATP-Architektur
 [Azure ATP-Architektur](atp-architecture.md)
 
## <a name="microsoft-ignite"></a>Microsoft Ignite
Bei der Microsoft Ignite 2018 gab es mehrere Sitzungen zum Schwerpunkt [Azure Advanced Threat Protection](https://myignite.techcommunity.microsoft.com/sessions?q=Azure%2520Advanced%2520Threat%2520Protection&t=%257B%2522from%2522%253A%25222018-09-23T08%253A00%253A00-04%253A00%2522%252C%2522to%2522%253A%25222018-09-28T19%253A00%253A00-04%253A00%2522%257D). Die Sitzungen wurden aufgezeichnet. Wenn Sie das Ereignis verpasst haben, sollten Sie hier nachsehen:

### <a name="azure-atp"></a>Azure ATP 
[BRK3117](https://myignite.techcommunity.microsoft.com/sessions/65780?source=sessions#ignite-html-anchor) – SecOp and incident response with Azure ATP (SecOp und Reaktion auf Incidents mit Azure ATP) – sehen Sie sich das [Video auf YouTube](https://www.youtube.com/watch?v=QXZIfH0wP3Q) an.

### <a name="azure-atp-and-azure-ad-ip-active-directory-identity-protection"></a>Azure ATP und Azure AD IP (Active Directory Identity Protection)
[BRK3237](https://myignite.techcommunity.microsoft.com/sessions/64523?source=sessions#ignite-html-anchor) – Securing your hybrid cloud environment with Azure AD Identity Protection and Azure ATP (Sichern Ihrer Hybrid Cloud-Umgebung mit Azure AD Identity Protection und Azure ATP) – sehen Sie sich das [Video auf YouTube](https://www.youtube.com/watch?v=X7CXaok6GbM) an.

[BRK2157](https://myignite.techcommunity.microsoft.com/sessions/65776?source=sessions#ignite-html-anchor) – Accelerate deployment and adoption of Microsoft Information Protection solutions (Beschleunigen der Bereitstellung und der Einführung von Microsoft Information Protection-Lösungen) – sehen Sie sich das [Video auf YouTube](https://www.youtube.com/watch?v=Foh-XDVbPog) an.

Eine Zusammenfassung der Azure ATP-Ankündigungen, die auf der Ignite 2018 erfolgten, finden Sie im Blogbeitrag [Azure Advanced Threat Protection Expands Integrations, Detections, and Forensic Capabilities](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Azure-Advanced-Threat-Protection-Expands-Integrations-Detections/ba-p/262409) (Azure Advanced Threat Protection erweitert Integrationen, Erkennungen und forensische Möglichkeiten).

## <a name="whats-next"></a>Wie geht es weiter? 

Es wird empfohlen, Azure ATP in drei Phasen bereitzustellen:  

### <a name="phase-1"></a>Phase 1

1. Richten Sie Azure ATP zum Schutz Ihrer primären Umgebungen ein. Mit dem Azure ATP-Modell zur schnellen Bereitstellung können Sie mit dem Schutz Ihrer Organisation noch heute beginnen. [Install Azure ATP (Installieren von Azure ATP)](install-atp-step1.md)  
2. Legen Sie [Sensitive Accounts](sensitive-accounts.md) (sensible Konten) und [Honeytoken-Konten](install-atp-step7.md) fest.
3. Überprüfen Sie die Berichte und [Lateral Movement-Pfade](use-case-lateral-movement-path.md).  


### <a name="phase-2"></a>Phase 2

1. Schützen Sie sämtliche Domänencontroller und [Gesamtstrukturen](atp-multi-forest.md) in Ihrer Organisation.  
2. Überwachen Sie alle [Warnungen](working-with-suspicious-activities.md): Untersuchen Sie Warnungen bzgl. Lateral Movement und Domänendominanz.  
3. Nehmen Sie das [Leitfaden zu Sicherheitshinweisen](suspicious-activity-guide.md) zur Hilfe, um Bedrohungen zu verstehen und potenzielle Angriffe selektieren zu können.


### <a name="phase-3"></a>Phase 3

1. Integrieren Sie Azure ATP-Warnungen in Ihre SecOp-Workflows.

## <a name="see-also"></a>Weitere Informationen
- [Häufig gestellte Fragen zu Azure ATP](atp-technical-faq.md)
- [Arbeiten mit Sicherheitswarnungen](working-with-suspicious-activities.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
