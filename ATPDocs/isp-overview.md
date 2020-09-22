---
title: Azure Advanced Threat Protection-Bewertungen des Identitätssicherheitsstatus
description: Dieser Artikel bietet eine Übersicht über die Berichte von Azure ATP zur Bewertung des Identitätssicherheitsstatus.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 09/16/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 71b15bd9-3183-4e24-b18a-705023ccc313
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: eaef6571a11852e66634e9043daa25ec8fdbe2ef
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2020
ms.locfileid: "90910187"
---
# <a name="azure-atps-identity-security-posture-assessments"></a>Azure ATP-Bewertungen des Identitätssicherheitsstatus

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

In der Regel haben Organisationen jeder Größenordnung nur eingeschränkte Informationen darüber, ob ihre lokalen Apps und Dienste ein Sicherheitsrisiko für die Organisation darstellen könnten. Dieses Problem trifft insbesondere bei nicht unterstützten oder veralteten Komponenten zu.

Auch wenn Ihr Unternehmen kontinuierlich viel Zeit und Arbeit in den erhöhten Schutz von Identitäten und Identitätsinfrastrukturen (z.B. Active Directory oder Active Directory Connect) investiert, werden häufige Fehlkonfigurationen sowie die Verwendung von Legacykomponenten – eine der größten Bedrohungen für Ihre Organisation – leicht übersehen. Sicherheitsuntersuchungen von Microsoft haben ergeben, dass die meisten Angriffe auf Identitäten häufige Fehlkonfigurationen in Active Directory und die fortgesetzte Verwendung von Legacykomponenten (z.B. das NTLMv1-Protokoll) ausnutzen, um Identitäten zu stehlen und erfolgreich in Ihre Organisation einzudringen. Damit Sie solche Angriffe effektiv bekämpfen können, bietet Azure ATP jetzt proaktive Bewertungen des Identitätssicherheitsstatus, um Risiken zu erkennen und Aktionen zur Beseitigung für Ihre sämtlichen lokalen Active Directory-Konfigurationen zu empfehlen.

## <a name="what-do-azure-atp-identity-security-posture-assessments-provide"></a>Was bieten die Azure ATP-Bewertungen des Identitätssicherheitsstatus?

- Ermittlungen und kontextbezogene Daten zu bekannten gefährdeten Komponenten und Fehlkonfigurationen sowie relevante Möglichkeiten zur Behebung.
- Azure ATP erkennt nicht nur verdächtige Aktivitäten, sondern überwacht mithilfe des vorhandenen Azure ATP-Sensors auch aktiv Ihre lokalen Identitäten und Identitätsinfrastrukturen auf Schwachstellen.
- Genaue Bewertungsberichte zum aktuellen Sicherheitsstatus Ihrer Organisation ermöglichen eine schnelle Reaktion und eine effektive, kontinuierliche Überwachung.

## <a name="how-do-i-get-started"></a>Wie fange ich an?

### <a name="access"></a>Access

Azure ATP-Sicherheitsbewertungen stehen über das Microsoft Cloud App Security-Portal zur Verfügung. Aktivieren Sie vorher die Azure ATP-Integration. Informationen zur Integration von Azure ATP in Cloud App Security finden Sie unter [Azure ATP-Integration](/cloud-app-security/aatp-integration).

### <a name="licensing"></a>Lizenzierung

Für den Zugriff auf die Azure ATP-Sicherheitsbewertungsberichte in Cloud App Security ist keine Cloud App Security-Lizenz erforderlich, sondern nur eine Azure ATP-Lizenz.

## <a name="access-azure-atp-using-cloud-app-security"></a>Zugreifen auf Azure ATP über Cloud App Security

Lesen Sie die [Schnellstartanleitung für Cloud App Security](/cloud-app-security/getting-started-with-cloud-app-security), um sich mit den Grundlagen des Cloud App Security-Portals vertraut zu machen.

**Bewertungen des Identitätssicherheitsstatus**

Azure ATP bietet die folgenden Bewertungen des Identitätssicherheitsstatus. Jede Bewertung kann als Bericht heruntergeladen werden und enthält Anweisungen zur Verwendung sowie Tools zum Erstellen eines Aktionsplans zum Beheben des Problems.

**Bewertungsberichte**

- [Domänencontroller mit verfügbarem Druckspoolerdienst](cas-isp-print-spooler.md)
- [Ruhende Entitäten in sensiblen Gruppen](cas-isp-dormant-entities.md)
- [Verfügbarmachen von Anmeldeinformationen in Klartext durch Entitäten](cas-isp-clear-text.md)
- [Verwendung von Microsoft LAPS](cas-isp-laps.md)
- [Verwendung von Legacyprotokollen](cas-isp-legacy-protocols.md)
- [Lateral-Movement-Pfade mit dem höchsten Risiko](cas-isp-riskiest-lmp.md)
- [Nicht überwachte Domänencontroller](cas-isp-unmonitored-domain-controller.md)
- [Unsichere Kontoattribute](cas-isp-unsecure-account-attributes.md)
- [Unsichere Kerberos-Delegierung](cas-isp-unconstrained-kerberos.md)
- [Unsichere SID-Verlaufsattribute](cas-isp-unsecure-sid-history-attribute.md)
- [Verwendung schwacher Verschlüsselungen](cas-isp-weak-cipher.md)

So greifen Sie auf Bewertungen des Identitätssicherheitsstatus zu:

1. Öffnen Sie das **Microsoft Cloud App Security**-Portal.
    ![Zugreifen auf Azure ATP-Berichte zum Identitätssicherheitsstatus in Cloud App Security](media/atp-cas-isp-report-1.png)
1. Wählen Sie im linken Menü **Untersuchen** aus, und klicken Sie im Dropdownmenü auf **Identitätssicherheitsstatus**.
1. Klicken Sie in der Liste **Sicherheitsbewertungsberichte** auf die Statusbewertung, die Sie überprüfen möchten.

## <a name="next-steps"></a>Nächste Schritte

- [Weitere Informationen zur Verwendung von Cloud App Security mit Azure ATP](activities-filtering-mcas.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)