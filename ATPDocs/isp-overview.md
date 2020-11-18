---
title: Bewertung der Identitäts Sicherheit für Identitäts Sicherheit in Microsoft Defender
description: Dieser Artikel bietet einen Überblick über die Status Bewertungsberichte von Microsoft Defender für Identity Security.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 58e079764c2e59623b94b78f29f0ad00d6219dcc
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2020
ms.locfileid: "94847427"
---
# <a name="product-longs-identity-security-posture-assessments"></a>[!INCLUDE [Product long](includes/product-long.md)]Bewertung der Identitäts Sicherheitslage

In der Regel haben Organisationen jeder Größenordnung nur eingeschränkte Informationen darüber, ob ihre lokalen Apps und Dienste ein Sicherheitsrisiko für die Organisation darstellen könnten. Dieses Problem trifft insbesondere bei nicht unterstützten oder veralteten Komponenten zu.

Auch wenn Ihr Unternehmen kontinuierlich viel Zeit und Arbeit in den erhöhten Schutz von Identitäten und Identitätsinfrastrukturen (z.B. Active Directory oder Active Directory Connect) investiert, werden häufige Fehlkonfigurationen sowie die Verwendung von Legacykomponenten – eine der größten Bedrohungen für Ihre Organisation – leicht übersehen. Sicherheitsuntersuchungen von Microsoft haben ergeben, dass die meisten Angriffe auf Identitäten häufige Fehlkonfigurationen in Active Directory und die fortgesetzte Verwendung von Legacykomponenten (z.B. das NTLMv1-Protokoll) ausnutzen, um Identitäten zu stehlen und erfolgreich in Ihre Organisation einzudringen. Um dies effektiv zu bekämpfen, [!INCLUDE [Product long](includes/product-long.md)] bietet jetzt proaktive Identitäts Sicherheitsstatus-Bewertungen, um Verbesserungsmaßnahmen in Ihren lokalen Active Directory Konfigurationen zu erkennen und vorzuschlagen.

## <a name="what-do-product-short-identity-security-posture-assessments-provide"></a>Welche [!INCLUDE [Product short](includes/product-short.md)] Identitäts Sicherheitsstatus-Bewertungen werden bereitgestellt?

- Ermittlungen und kontextbezogene Daten zu bekannten gefährdeten Komponenten und Fehlkonfigurationen sowie relevante Möglichkeiten zur Behebung.
- [!INCLUDE [Product short](includes/product-short.md)] erkennt nicht nur verdächtige Aktivitäten, sondern überwacht mithilfe des vorhandenen Sensors auch Ihre lokalen Identitäten und die Identitäts Infrastruktur für schwache Orte [!INCLUDE [Product short](includes/product-short.md)] .
- Genaue Bewertungsberichte zum aktuellen Sicherheitsstatus Ihrer Organisation ermöglichen eine schnelle Reaktion und eine effektive, kontinuierliche Überwachung.

## <a name="how-do-i-get-started"></a>Wie fange ich an?

### <a name="access"></a>Access

[!INCLUDE [Product short](includes/product-short.md)] Sicherheitsbewertungen sind nach dem Aktivieren der Integration über das Microsoft Cloud App Security-Portal verfügbar [!INCLUDE [Product short](includes/product-short.md)] . Informationen zur Integration [!INCLUDE [Product short](includes/product-short.md)] in Cloud App Security finden Sie unter [ [!INCLUDE [Product short](includes/product-short.md)] Integration](/cloud-app-security/aatp-integration).

### <a name="licensing"></a>Lizenzierung

Für den Zugriff [!INCLUDE [Product short](includes/product-short.md)] auf sicherheitsbewertungs Berichte in Cloud App Security ist keine Cloud App Security-Lizenz [!INCLUDE [Product short](includes/product-short.md)] erforderlich. es ist nur eine Lizenz erforderlich.

## <a name="access-product-short-using-cloud-app-security"></a>Zugriff [!INCLUDE [Product short](includes/product-short.md)] mit Cloud App Security

Lesen Sie die [Schnellstartanleitung für Cloud App Security](/cloud-app-security/getting-started-with-cloud-app-security), um sich mit den Grundlagen des Cloud App Security-Portals vertraut zu machen.

**Bewertungen des Identitätssicherheitsstatus**

[!INCLUDE [Product short](includes/product-short.md)] bietet die folgenden Bewertungen der Identitäts Sicherheitslage. Jede Bewertung kann als Bericht heruntergeladen werden und enthält Anweisungen zur Verwendung sowie Tools zum Erstellen eines Aktionsplans zum Beheben des Problems.

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
    ![Zugriff [! INCLUDE [Product Short] (includes/Product-Short. MD)] Identitäts Sicherheitsstatus-Berichte in Cloud App Security](media/cas-isp-report-1.png)
1. Wählen Sie im linken Menü **Untersuchen** aus, und klicken Sie im Dropdownmenü auf **Identitätssicherheitsstatus**.
1. Klicken Sie in der Liste **Sicherheitsbewertungsberichte** auf die Statusbewertung, die Sie überprüfen möchten.

## <a name="next-steps"></a>Nächste Schritte

- [Weitere Informationen zur Verwendung von Cloud App Security mit [!INCLUDE [Product short](includes/product-short.md)]](activities-filtering-mcas.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
