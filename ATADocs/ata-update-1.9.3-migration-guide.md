---
title: Advanced Threat Analytics-Update für 1.9.3 Migration Guide
description: Vorgehensweise zum Aktualisieren von ATA auf Version 1.9.3
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 09/14/2020
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.assetid: 2946310a-8e4e-48fc-9450-fc9647efeb22
ms.reviewer: ort
ms.suite: ems
ms.openlocfilehash: 0148d8b37e116f1b2574fbedacfce6d02e0b88f2
ms.sourcegitcommit: e844155ea57f73dfe2b47f4c5c1c7f5292ccbf1e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2020
ms.locfileid: "94690821"
---
# <a name="ata-version-193"></a>ATA-Version 1.9.3

Wir freuen uns, die Verfügbarkeit von Microsoft Advanced Threat Analytics 1,9 Update 3 bekanntgeben zu können.

In diesem Artikel werden Probleme beschrieben, die in Update 3 von Microsoft Advanced Threat Analytics (ATA) Version 1,9 behoben wurden. Die Buildnummer dieses Updates lautet 1.9.7576.

## <a name="improvements-included-in-this-update"></a>In diesem Update enthaltene Verbesserungen

- Ein Upgrade von MongoDB auf Version 3.6.18 wurde durchgeführt, um verbesserte Support-und Sicherheitsupdates zu
- Aktualisieren von Bootstrap-und jQuery-NPM-Paketen auf Version 3.4.1 für Sicherheitsupdates.
- Die Funktionen für das Portal wurden verbessert.
- Erhöhter Hinweis für den Ablauf von Center-Zertifikaten auf drei Monate vor Ablauf (zuvor drei Wochen). Außerdem bietet der Hinweis nun eine klarere Beschreibung des schwere Grads, bei dem das Zertifikat nicht erneuert wird.
- Verbesserte Details mit Fehlern bei der Überprüfung der Anmelde Informationen beim Testen von Verzeichnisdienst Verbindungen.
- Das Fehlerprotokoll enthält jetzt ausführlichere Informationen, wenn Probleme mit Leistungsproblemen auftreten.
- Das Bereitstellungs Protokoll enthält jetzt ausführlichere Informationen zu Verbindungsproblemen während der Gatewaybereitstellung.
- Allgemeine Leistungsverbesserungen.

## <a name="fixed-issues-included-in-this-update"></a>In diesem Update enthaltene behobene Probleme

- Korrigiert eines Problems, bei dem die Sicherheitsprotokoll Berechtigungen für einige bereit Stellungen nicht ordnungsgemäß festgelegt sind.
- Korrigiert ein Problem, bei dem einige Übersetzungen für einige Sprachen fehlen.
- Korrigiert eines Problems, bei dem eine Fehlermeldung angezeigt wird, wenn Sie eine Konto Profilseite durchsuchen.
- Korrigiert eines Problems, bei dem einige Barrierefreiheits Funktionen nicht ordnungsgemäß funktionieren.

## <a name="how-to-get-this-update"></a>Beziehen dieses Updates

Updates für Microsoft ATA sind über Microsoft Update oder durch Manuelles Herunterladen verfügbar.

### <a name="microsoft-update"></a>Microsoft Update

Dieses Update ist über Microsoft Update verfügbar. Weitere Informationen zur Verwendung von Microsoft Update finden Sie unter [Beziehen von Updates über Windows Update](https://support.microsoft.com/help/3067639).

### <a name="microsoft-download-center"></a>Microsoft Download Center

Um das eigenständige Paket für dieses Update zu erhalten, besuchen Sie die Microsoft Download Center-Website: [Laden Sie das ATA 1.9.3-Paket jetzt herunter](https://www.microsoft.com/download/details.aspx?id=56725).

### <a name="prerequisites"></a>Voraussetzungen

Zum Installieren dieses Updates müssen Sie bereits eine der folgenden Versionen von ATA installiert haben:

- Update 2 für ATA 1,9 (Version 1.9.7478)
- Update 2 für ATA 1,9 (Version 1.9.7475)
- Update 1 für ATA 1.9 (Version 1.9.7412)
- ATA 1.9 (Version 1.9.7312)
- Update 1 für ATA 1.8 (Version 1.8.6765)
- ATA 1.8 (Version 1.8.6645)

### <a name="restart-requirement"></a>Erforderlicher Neustart

Nach dem Anwenden dieses Updates muss Ihr Computer möglicherweise neu gestartet werden.

### <a name="update-replacement-information"></a>Informationen zur Ersetzung durch dieses Update

Dieses Update ersetzt Update 2 für ATA 1,9 (Version 1.9.7478).

## <a name="see-also"></a>Siehe auch

- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [ATA-Versionen](ata-versions.md)
