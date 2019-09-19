---
title: Azure Advanced Threat Protection-Bewertungen des Identitätssicherheitsstatus | Microsoft-Dokumentation
description: Dieser Artikel bietet eine Übersicht über die Berichte von Azure ATP zur Bewertung des Identitätssicherheitsstatus.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 09/16/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 71b15bd9-3183-4e24-b18a-705023ccc313
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: cb562e8d9dc21d8fa5fcce70ea2020be22796621
ms.sourcegitcommit: 475df3e87d8476ff13e48ebc7a722f46f29dab70
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71007504"
---
# <a name="azure-atps-identity-security-posture-assessments"></a>Azure ATP-Bewertungen des Identitätssicherheitsstatus
 
In der Regel haben Organisationen jeder Größenordnung nur eingeschränkte Informationen darüber, ob ihre lokalen Apps und Dienste ein Sicherheitsrisiko für die Organisation darstellen könnten. Dieses Problem trifft insbesondere bei nicht unterstützten oder veralteten Komponenten zu. 

Auch wenn Ihr Unternehmen kontinuierlich viel Zeit und Arbeit in den erhöhten Schutz von Identitäten und Identitätsinfrastrukturen (z.B. Active Directory oder Active Directory Connect) investiert, werden häufige Fehlkonfigurationen sowie die Verwendung von Legacykomponenten – eine der größten Bedrohungen für Ihre Organisation – leicht übersehen. Sicherheitsuntersuchungen von Microsoft haben ergeben, dass die meisten Angriffe auf Identitäten häufige Fehlkonfigurationen in Active Directory und die fortgesetzte Verwendung von Legacykomponenten (z.B. das NTLMv1-Protokoll) ausnutzen, um Identitäten zu stehlen und erfolgreich in Ihre Organisation einzudringen. Damit Sie solche Angriffe effektiv bekämpfen können, bietet Azure ATP jetzt proaktive Bewertungen des Identitätssicherheitsstatus, um Risiken zu erkennen und Aktionen zur Beseitigung für Ihre sämtlichen lokalen Active Directory-Konfigurationen zu empfehlen. 

## <a name="what-do-azure-atp-identity-security-posture-assessments-provide"></a>Was bieten die Azure ATP-Bewertungen des Identitätssicherheitsstatus?  
- Ermittlungen und kontextbezogene Daten zu bekannten gefährdeten Komponenten und Fehlkonfigurationen sowie relevante Möglichkeiten zur Behebung.
- Azure ATP erkennt nicht nur verdächtige Aktivitäten, sondern überwacht mithilfe des vorhandenen Azure ATP-Sensors auch aktiv Ihre lokalen Identitäten und Identitätsinfrastrukturen auf Schwachstellen. 
- Genaue Bewertungsberichte zum aktuellen Sicherheitsstatus Ihrer Organisation ermöglichen eine schnelle Reaktion und eine effektive, kontinuierliche Überwachung. 

## <a name="how-do-i-get-started"></a>Wie fange ich an? 

### <a name="access"></a>Zugriff

Azure ATP-Sicherheitsbewertungen stehen über das Microsoft Cloud App Security-Portal zur Verfügung. Aktivieren Sie vorher die Azure ATP-Integration. Informationen zur Integration von Azure ATP in Cloud App Security finden Sie unter [Azure ATP-Integration](https://docs.microsoft.com/cloud-app-security/aatp-integration). 

### <a name="licensing"></a>Lizenzierung

Für den Zugriff auf die Azure ATP-Sicherheitsbewertungsberichte in Cloud App Security ist keine Cloud App Security-Lizenz erforderlich, sondern nur eine Azure ATP-Lizenz. 

## <a name="access-azure-atp-using-cloud-app-security"></a>Zugreifen auf Azure ATP über Cloud App Security 

Lesen Sie die [Schnellstartanleitung für Cloud App Security](https://docs.microsoft.com/cloud-app-security/getting-started-with-cloud-app-security), um sich mit den Grundlagen des Cloud App Security-Portals vertraut zu machen. 

**Bewertungen des Identitätssicherheitsstatus**

Azure ATP bietet die folgenden Bewertungen des Identitätssicherheitsstatus. Jede Bewertung kann als Bericht heruntergeladen werden und enthält Anweisungen zur Verwendung sowie Tools zum Erstellen eines Aktionsplans zum Beheben des Problems. 

**Bewertungsberichte**
- Verhindern des [Verfügbarmachens von Anmeldeinformationen in Klartext durch Entitäten](atp-cas-isp-clear-text.md)
- Verhindern der [Verwendung von Legacyprotokollen](atp-cas-isp-legacy-protocols.md)
- Verhindern der [Verwendung schwacher Verschlüsselungen](atp-cas-isp-weak-cipher.md)
- Verhindern [unsicherer Kerberos-Delegierungen](atp-cas-isp-unconstrained-kerberos.md)
- Deaktivieren des [Druckspoolerdiensts auf Domänencontrollern](atp-cas-isp-print-spooler.md)
- Entfernen [ruhender Entitäten aus sensiblen Gruppen](atp-cas-isp-dormant-entities.md)

So greifen Sie auf Bewertungen des Identitätssicherheitsstatus zu:
1. Öffnen Sie das **Microsoft Cloud App Security**-Portal. 
    ![Zugreifen auf Azure ATP-Berichte zum Identitätssicherheitsstatus in Cloud App Security](media/atp-cas-isp-report-1.png)
1. Wählen Sie im linken Menü **Untersuchen** aus, und klicken Sie im Dropdownmenü auf **Identitätssicherheitsstatus**. 
1. Klicken Sie in der Liste **Sicherheitsbewertungsberichte** auf die Statusbewertung, die Sie überprüfen möchten.  


## <a name="next-steps"></a>Nächste Schritte
- [Weitere Informationen zur Verwendung von Cloud App Security mit Azure ATP](atp-activities-filtering-mcas.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)

