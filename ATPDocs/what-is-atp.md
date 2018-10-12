---
title: Was ist Azure Advanced Threat Protection (ATP)? | Microsoft-Dokumentation
description: Hier wird erläutert, worum es sich bei Azure Advanced Threat Protection (ATP) handelt und welche Arten von verdächtigen Aktivitäten erkannt werden können
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 9/16/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 2d14d0e9-1b03-4bcc-ae97-8fd41526ffc5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f3e03f5307a9a09ffb2a62e7313be4629f4bc060
ms.sourcegitcommit: 5ff50807f855db1051b977a64eb6e90487ea196c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2018
ms.locfileid: "45750469"
---
*Gilt für: Azure Advanced Threat Protection*

# <a name="what-is-azure-advanced-threat-protection"></a>Was ist Azure Advanced Threat Protection?
Azure Advanced Threat Protection (ATP) ist eine cloudbasierte Sicherheitslösung, mit der Sie komplexe Bedrohungen, gefährdete Identitäten und schädliche Insider-Aktionen gegen Ihre Organisation identifizieren und erkennen können und die Sie bei der Untersuchung dieser Bedrohungen unterstützt. Azure ATP bietet SecOp-Analysten und Sicherheitsexperten, die Probleme beim Erkennen erweiterter Angriffe in Hybridumgebungen haben, folgende Funktionen:  
- Überwachung von Benutzern, Entitätsverhalten und -aktivitäten mit lernbasierter Analyse  
- Schutz von in Active Directory gespeicherten Benutzeridentitäten und Anmeldeinformationen  
- Identifikation und Untersuchung verdächtiger Benutzeraktivitäten und erweiterter Angriffe in der gesamten Kill Chain 
- Bereitstellung eindeutiger Informationen zu einem Incident in einer einfachen Zeitachse zur schnellen Selektierung 
 
## <a name="monitor-and-profile-user-behavior-and-activities"></a>Überwachung und Profiling von Benutzerverhalten und -aktivitäten  
Azure ATP überwacht und analysiert netzwerkübergreifend Benutzeraktivitäten und -informationen, wie z.B. Berechtigungen und Gruppenmitgliedschaften, und erstellt dabei für jeden Benutzer eine verhaltensbasierte Baseline. Anschließend identifiziert Azure ATP Anomalien bei integrierter adaptiver Intelligenz und gewährt Ihnen Einblicke in verdächtige Aktivitäten und Ereignisse. Dabei werden Ihnen komplexe Bedrohungen, gefährdete Benutzer und Insider-Bedrohungen Ihrer Organisation angezeigt. Mit den Sensoren von Azure ATP werden Domänencontroller der Organisation überwacht. Dadurch wird von jedem Gerät aus ein umfassender Überblick für alle Benutzeraktivitäten geboten. 
 
## <a name="protect-user-identities-and-reduce-the-attack-surface"></a>Schutz von Benutzeridentitäten und Verringern der Angriffsfläche   
Azure ATP gewährt Ihnen wertvolle Einblicke in Identitätskonfigurationen und stellt empfohlene Best Practices für die Sicherheit bereit. Mithilfe von Azure ATP können Sie durch Sicherheitsberichte und die Analyse von Benutzerprofilen die Angriffsfläche Ihrer Organisation deutlich reduzieren, wodurch auch die Gefährdung von Benutzeranmeldeinformationen sowie die Gefährdung durch einen Angriff verringert werden kann. Mithilfe der visuellen Lateral Movement-Pfade von ATP verstehen Sie schnell, wie genau sich ein Angreifer lateral innerhalb Ihrer Organisation bewegen kann, um sensible Konten zu gefährden. Die Lösung unterstützt Sie dabei, diese Risiken im Vorhinein zu vermeiden. Zudem können Sie mithilfe der Sicherheitsberichte von ATP Benutzer und Geräte identifizieren, die sich mit Klartextkennwörtern authentifizieren, und weitere Einblicke gewinnen, um den Sicherheitsstatus und die Richtlinien Ihrer Organisation zu verbessern.  
 
## <a name="identify-suspicious-activities-and-advanced-attacks-across-the-attack-kill-chain"></a>Identifizieren verdächtiger Aktivitäten und erweiterter Angriffe über die Kill Chain 
Angriffe werden in der Regel gegen eine beliebige zugängliche Entität gestartet, wie z.B. einen Benutzer mit geringfügigen Berechtigungen, und verschieben sich anschließend schnell seitwärts, bis der Angreifer Zugriff auf wertvolle Objekte erhält (z.B. sensible Konten, Domänenadministratoren und streng vertrauliche Daten). Azure ATP erkennt diese erweiterten Bedrohungen von Grund auf während der gesamten Kill Chain zur Angriffsabwehr: 
### <a name="reconnaissance"></a>Reconnaissance 
Identifizieren nicht autorisierter Benutzer und Angreifer, um über eine Vielzahl von Methoden Informationen zu Benutzernamen, der Gruppenmitgliedschaft von Benutzern, Geräten zugewiesenen IP-Adressen, Ressourcen und mehr zu erlangen.  
### <a name="compromised-users"></a>Gefährdete Benutzer
Identifizieren von Versuchen zur Gefährdung von Benutzeranmeldeinformationen über Angriffe durch Schlüsselsuche, fehlgeschlagene Authentifizierungen, Änderungen der Gruppenmitgliedschaft von Benutzern und weitere Methoden.  

### <a name="lateral-movements"></a>Seitliche Verschiebungen
Erkennen von Versuchen zur seitlichen Verschiebung innerhalb des Netzwerks, um mithilfe von Methoden wie „Pass-the-Ticket“, „Pass-the-Hash“, „Overpass-the-Hash“ und mehr weitere Kontrolle über sensible Benutzer zu erlangen.  

### <a name="domain-dominance"></a>Domänendominanz
Hervorheben des Angreiferverhaltens bei Erreichen der Domänendominanz über die Ausführung von Remotecode auf dem Domänencontroller und Methoden wie „DC Shadow“, die böswillige Replikation des Domänencontrollers, Golden Ticket-Aktivitäten und mehr.   

## <a name="investigate-alerts-and-user-activities"></a>Untersuchen von Warnungen und Benutzeraktivitäten  
Azure ATP soll die Anzahl allgemeiner Warnungen reduzieren, damit nur relevante und wichtige Sicherheitswarnungen in einer übersichtlichen Zeitleiste mit gegen die Organisation gerichteten Angriffen in Echtzeit bereitgestellt werden können. Dank der Azure ATP-Ansicht mit der Zeitachse zu Angriffen können Sie sich problemlos aufs Wesentliche konzentrieren und intelligente Analysen wirksam einsetzen. Sicherheitsexperten, die Azure ATP verwenden, können Bedrohungen ohne großen Aufwand untersuchen und gewinnen organisationsübergreifend Einblicke für Benutzer, Geräte und Netzwerkressourcen. Die nahtlose Integration in Windows Defender ATP bietet durch zusätzliche Erkennung und Schutz vor erweiterten dauerhaften Bedrohungen für das Betriebssystem eine weitere erweiterte Sicherheitsebene.  

## <a name="additional-resources-for-azure-atp"></a>Zusätzliche Ressourcen für Azure ATP  
Starten Sie eine kostenlose Testversion: [https://signup.microsoft.com/Signup?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7&ali=1](https://signup.microsoft.com/Signup?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7&ali=1 "Enterprise Mobility + Security E5")
 
Folgen Sie Azure ATP in der Microsoft Tech Community  
[https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection "Azure ATP in Microsoft Tech Community")
 
Werden Sie Teil der Azure ATP Yammer-Community[https://www.yammer.com/azureadvisors/#/threads/inGroup?type=in_group&feedId=9386893](https://www.yammer.com/azureadvisors/#/threads/inGroup?type=in_group&feedId=9386893 "Azure ATP Yammer-Community")
 
Besuchen Sie die Azure ATP-Produktseite  
[https://azure.microsoft.com/en-us/features/azure-advanced-threat-protection/](https://azure.microsoft.com/en-us/features/azure-advanced-threat-protection/ "Azure ATP-Produktseite")

Weitere Informationen zur Azure ATP-Architektur finden Sie unter [Azure ATP-Architektur](atp-architecture.md).
 
## <a name="whats-next"></a>Wie geht es weiter? 

Es wird empfohlen, Azure ATP in 3 Phasen bereitzustellen:  

### <a name="phase-1"></a>Phase 1

1. Richten Sie Azure ATP zum Schutz Ihrer primären Umgebungen ein. Mit dem Azure ATP-Modell zur schnellen Bereitstellung können Sie mit dem Schutz Ihrer Organisation noch heute beginnen. [Install ATP (Installieren von ATP)](install-atp-step1.md)  
2. Legen Sie [Sensitive Accounts](sensitive-accounts.md) (sensible Konten) und [Honeytoken-Konten](install-atp-step7.md) fest.   
3. Überprüfen Sie die Berichte und [Lateral Movement-Pfade](use-case-lateral-movement-path.md).  


### <a name="phase-2"></a>Phase 2

1. Schützen Sie sämtliche Domänencontroller und [Gesamtstrukturen](atp-multi-forest.md) in Ihrer Organisation.  
2.  Überwachen Sie alle [Warnungen](working-with-suspicious-activities.md): Untersuchen Sie Warnungen bzgl. Lateral Movement und Domänendominanz.  
3. Nehmen Sie das [Leitfaden zu Sicherheitshinweisen](suspicious-activity-guide.md) zur Hilfe, um Bedrohungen zu verstehen und potenzielle Angriffe selektieren zu können.   


### <a name="phase-3"></a>Phase 3

1. Integrieren Sie Azure ATP-Warnungen in Ihre SecOp-Workflows. 

## <a name="see-also"></a>Weitere Informationen
- [Häufig gestellte Fragen zu Azure ATP](atp-technical-faq.md)
- [Arbeiten mit Sicherheitswarnungen](working-with-suspicious-activities.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)