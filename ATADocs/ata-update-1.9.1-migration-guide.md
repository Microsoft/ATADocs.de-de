---
title: Advanced Threat Analytics-Update für 1.9.1 Migration Guide
description: Verfahren zum Aktualisieren von ATA auf Version 1.9.1
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 12/10/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 2946310a-8e4e-48fc-9450-fc9647efeb22
ms.reviewer: ort
ms.suite: ems
ms.openlocfilehash: fdaf1e8e8a96e0f96098235d818f738528a7ab0e
ms.sourcegitcommit: 11fff9d4ebf1c50b04f7789a22c80cdbc3e4416a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2020
ms.locfileid: "79412311"
---
# <a name="ata-version-191"></a>ATA Version 1.9.1


Dieser Artikel beschreibt Probleme, die in Update 1 für Microsoft Advanced Threat Analytics (ATA), Version 1.9, behoben wurden. Die Buildnummer dieses Updates lautet 1.9.7412.

## <a name="fixed-issues-included-in-this-update"></a>In diesem Update enthaltene behobene Probleme

- Möglichkeit von Fehlern bei der Migration von ATA Version 1.8 auf Version 1.9 für große Datenbanken.
- Wenn Sie die neueste Version des Microsoft Edge-Browsers verwenden und zwischen Benutzern wechseln, reagiert der Browser möglicherweise nicht mehr.
- In einigen Szenarien fehlen Verzeichnisdateninformationen auf der Benutzerprofilseite.
- Wenn ein Benutzer zur Ausschlussliste für die Erkennung von ungewöhnlichem Verhalten hinzugefügt wird, wird der Ausschluss nicht immer angewendet. 
- Aktualisierte MongoDB-Datenbankversion.
- Inkonsistente Neusynchronisierung aller Active Directory-Entitäten für ATA nach einem Upgrade auf Version 1.9.
- Inkonsistente Exporte verdächtiger Aktivitäten nach Microsoft Excel. Gelegentliche Fehler bei der Fehlergenerierung.  


## <a name="improvements-included-in-this-update"></a>In diesem Update enthaltene Verbesserungen
- Änderungen erforderlich für die MAS-Zertifizierung (Microsoft Accessibility Standards).
- Enthält zusätzliche Fehlerbehebungen in Bezug auf die Leistung und Sicherheit.

## <a name="get-this-update"></a>Rufen Sie dieses Update ab

Updates für Microsoft Advanced Threat Analytics, Version 1.9, sind über Microsoft Update oder per manuellem Download verfügbar.

### <a name="microsoft-update"></a>Microsoft Update
Dieses Update ist über Microsoft Update verfügbar. Weitere Informationen zur Verwendung von Microsoft Update finden Sie unter [Beziehen von Updates über Windows Update](https://support.microsoft.com/help/3067639).

### <a name="manual-download"></a>Manueller Download
Um das eigenständige Paket für dieses Update zu erhalten, besuchen Sie die Microsoft Download Center-Website: [Laden Sie das ATA 1,9-Paket jetzt herunter](https://www.microsoft.com/en-us/download/details.aspx?id=56725).

### <a name="prerequisites"></a>Erforderliche Komponenten
Um dieses Update zu installieren, muss ATA Version 1.9 (1.9.7312), Update 1 für ATA Version 1.8 (1.8.6765) oder ATA Version 1.8 (1.8.6645) installiert sein.

### <a name="restart-requirement"></a>Neustart Anforderung
Nach dem Anwenden dieses Updates muss Ihr Computer möglicherweise neu gestartet werden.

### <a name="update-replacement-information"></a>Informationen zur Ersetzung durch dieses Update
Dieses Update ersetzt ATA Version 1.9 (1.9.7312).


## <a name="see-also"></a>Siehe auch

- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [ATA-Versionen](ata-versions.md)
