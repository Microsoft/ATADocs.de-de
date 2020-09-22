---
title: Advanced Threat Analytics-Update für 1.9.1 Migration Guide
description: Verfahren zum Aktualisieren von ATA auf Version 1.9.1
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 12/10/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 2946310a-8e4e-48fc-9450-fc9647efeb22
ms.reviewer: ort
ms.suite: ems
ms.openlocfilehash: e5a3c40ccc82434d7eb98e26bfd1290df55f1fd1
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2020
ms.locfileid: "90911712"
---
# <a name="ata-version-191"></a>ATA Version 1.9.1

[!INCLUDE [Rebranding notice](includes/rebranding.md)]
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

### <a name="manual-download"></a>Manuelles Herunterladen
Um das eigenständige Paket für dieses Update zu erhalten, besuchen Sie die Microsoft Download Center-Website: [Laden Sie das ATA 1,9-Paket jetzt herunter](https://www.microsoft.com/en-us/download/details.aspx?id=56725).

### <a name="prerequisites"></a>Voraussetzungen
Um dieses Update zu installieren, muss ATA Version 1.9 (1.9.7312), Update 1 für ATA Version 1.8 (1.8.6765) oder ATA Version 1.8 (1.8.6645) installiert sein.

### <a name="restart-requirement"></a>Erforderlicher Neustart
Nach dem Anwenden dieses Updates muss Ihr Computer möglicherweise neu gestartet werden.

### <a name="update-replacement-information"></a>Informationen zur Ersetzung durch dieses Update
Dieses Update ersetzt ATA Version 1.9 (1.9.7312).


## <a name="see-also"></a>Weitere Informationen

- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [ATA-Versionen](ata-versions.md)
