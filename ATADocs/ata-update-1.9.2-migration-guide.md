---
title: Advanced Threat Analytics-Update für 1.9.2 Migration Guide
description: Verfahren für das Update von ATA auf Version 1.9.2
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 04/02/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.assetid: 2946310a-8e4e-48fc-9450-fc9647efeb22
ms.reviewer: ort
ms.suite: ems
ms.openlocfilehash: b2aa29f2818216b13116173f0872d9108e168c19
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2020
ms.locfileid: "90910992"
---
# <a name="ata-version-192"></a>ATA Version 1.9.2

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Wir freuen uns, die Verfügbarkeit von Microsoft Advanced Threat Analytics 1.9 Update 2 bekanntzugeben.

Dieser Artikel beschreibt Probleme, die in Update 2 für Microsoft Advanced Threat Analytics (ATA), Version 1.9, behoben wurden. Die Buildnummer dieses Updates lautet 1.9.7478.

## <a name="improvements-included-in-this-update"></a>In diesem Update enthaltene Verbesserungen

Dieses Update schließt Windows Server 2019 (einschließlich Core-Versionen, aber ausgenommen Nano) als unterstütztes Betriebssystem für die Komponenten Center, Gateway und Lightweight Gateway ein.

Dieses Update umfasst auch Verbesserungen der Leistung und Stabilität sowie Korrekturen für von Kunden gemeldete Probleme.

## <a name="fixed-issues-included-in-this-update"></a>In diesem Update enthaltene behobene Probleme

- Behebt ein Problem, bei dem die Verzeichnisdatenanzeige direkte Manager- und rekursive Mitgliedschaften anzeigt.
- Behebt ein Problem, bei dem die URL-Konfiguration von ATA Center nicht immer lokale IP-Adressen oder den Namen des lokalen Computers zeigt.
- Beseitigt eine integritätsbezogene Benachrichtigung zu einem Downloadproblem, bei dem die integritätsbezogene Benachrichtigung ein nicht vorhandenes Gateway enthält.
- Behebt Übersetzungsprobleme.
- Behebt ein Problem, bei dem die Version der MongoDB-Datenbank nicht aktualisiert wurde.
- Beseitigt ein seltenes Szenario, bei dem bei der Synchronisierung von Active Directory Probleme mit hoher Arbeitsspeicherauslastung auftraten.
- Beseitigt ein seltenes Szenario, bei dem die Konsole nur die Auswahl eines nicht unterstützten Zertifikats zuließ.
- Beseitigt ein seltenes Szenario, bei dem die Falschmeldung zu einem „Verdacht auf Identitätsdiebstahl aufgrund von anormalem Verhalten“ empfangen wurde.
- Korrigiert einen seltenen Fall, bei dem es zu einem Sprung auf der Zeitachse kam, wenn Benachrichtigungen automatisch aktualisiert wurden.

## <a name="get-this-update"></a>Rufen Sie dieses Update ab

Um das eigenständige Paket für dieses Update zu erhalten, besuchen Sie die Microsoft Download Center-Website: [Laden Sie das ATA 1.9.2-Paket jetzt herunter](https://www.microsoft.com/en-us/download/details.aspx?id=56725).

### <a name="prerequisites"></a>Voraussetzungen

Zum Installieren dieses Updates müssen Sie bereits eine der folgenden Versionen von ATA installiert haben: 
- Update 1 für ATA 1.9 (Version 1.9.7412)
- ATA 1.9 (Version 1.9.7312)
- Update 1 für ATA 1.8 (Version 1.8.6765)
- ATA 1.8 (Version 1.8.6645)

### <a name="restart-requirement"></a>Erforderlicher Neustart

Nach dem Anwenden dieses Updates muss Ihr Computer möglicherweise neu gestartet werden.

### <a name="update-replacement-information"></a>Informationen zur Ersetzung durch dieses Update

Dieses Update ersetzt ATA Version 1.9.1 (1.9.7412).


## <a name="see-also"></a>Weitere Informationen

- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [ATA-Versionen](ata-versions.md)