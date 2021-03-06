---
title: Bewertung der Identitäts Sicherheit für Identitäts Sicherheit in Microsoft Defender
description: Dieser Artikel bietet einen Überblick über die Status Bewertungsberichte von Microsoft Defender für Identity Security.
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: 3b3f20ac50e3b5b687dd6ece8b421c84288a3126
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533850"
---
# <a name="microsoft-defender-for-identitys-identity-security-posture-assessments"></a>Bewertung der Identitäts Sicherheit für Identitäts Sicherheit in Microsoft Defender

In der Regel haben Organisationen jeder Größenordnung nur eingeschränkte Informationen darüber, ob ihre lokalen Apps und Dienste ein Sicherheitsrisiko für die Organisation darstellen könnten. Dieses Problem trifft insbesondere bei nicht unterstützten oder veralteten Komponenten zu.

Auch wenn Ihr Unternehmen kontinuierlich viel Zeit und Arbeit in den erhöhten Schutz von Identitäten und Identitätsinfrastrukturen (z.B. Active Directory oder Active Directory Connect) investiert, werden häufige Fehlkonfigurationen sowie die Verwendung von Legacykomponenten – eine der größten Bedrohungen für Ihre Organisation – leicht übersehen. Sicherheitsuntersuchungen von Microsoft haben ergeben, dass die meisten Angriffe auf Identitäten häufige Fehlkonfigurationen in Active Directory und die fortgesetzte Verwendung von Legacykomponenten (z.B. das NTLMv1-Protokoll) ausnutzen, um Identitäten zu stehlen und erfolgreich in Ihre Organisation einzudringen. Um dies effektiv zu bekämpfen, [!INCLUDE [Product long](includes/product-long.md)] bietet jetzt proaktive Identitäts Sicherheitsstatus-Bewertungen, um Verbesserungsmaßnahmen in Ihren lokalen Active Directory Konfigurationen zu erkennen und vorzuschlagen.

## <a name="what-do-defender-for-identity-identity-security-posture-assessments-provide"></a>Welche Sicherheitsstatus Bewertungen werden von Defender für Identitäts Identitäten bereitgestellt?

- Ermittlungen und kontextbezogene Daten zu bekannten gefährdeten Komponenten und Fehlkonfigurationen sowie relevante Möglichkeiten zur Behebung.
- [!INCLUDE [Product short](includes/product-short.md)] erkennt nicht nur verdächtige Aktivitäten, sondern überwacht mithilfe des vorhandenen Sensors auch Ihre lokalen Identitäten und die Identitäts Infrastruktur für schwache Orte [!INCLUDE [Product short](includes/product-short.md)] .
- Genaue Bewertungsberichte zum aktuellen Sicherheitsstatus Ihrer Organisation ermöglichen eine schnelle Reaktion und eine effektive, kontinuierliche Überwachung.

## <a name="how-do-i-get-started"></a>Wie fange ich an?

### <a name="access"></a>Access

[!INCLUDE [Product short](includes/product-short.md)] Sicherheitsbewertungen sind nach dem Aktivieren der Integration über das Microsoft Cloud App Security-Portal verfügbar [!INCLUDE [Product short](includes/product-short.md)] . Informationen zur Integration [!INCLUDE [Product short](includes/product-short.md)] in Cloud App Security finden Sie unter [ [!INCLUDE [Product short](includes/product-short.md)] Integration](/cloud-app-security/aatp-integration).

### <a name="licensing"></a>Lizenzierung

Für den Zugriff [!INCLUDE [Product short](includes/product-short.md)] auf sicherheitsbewertungs Berichte in Cloud App Security ist keine Cloud App Security-Lizenz [!INCLUDE [Product short](includes/product-short.md)] erforderlich. es ist nur eine Lizenz erforderlich.

## <a name="access-defender-for-identity-using-cloud-app-security"></a>Zugreifen auf Defender für Identity mithilfe von Cloud App Security

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
