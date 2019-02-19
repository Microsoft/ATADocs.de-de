---
title: Neuerungen in ATA 1.9 | Microsoft-Dokumentation
description: Listet Neuerungen sowie bekannte Probleme in ATA 1.9 auf.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: barbkess
ms.date: 3/25/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 51de491c-49ba-4aff-aded-cc133a8ccf0b
ms.reviewer: ''
ms.suite: ems
ms.openlocfilehash: 4a21dbf96ae7897c6ab45feb306f43986f84c5f2
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2019
ms.locfileid: "56077353"
---
# <a name="whats-new-in-ata-version-19"></a>Neuerungen in ATA 1.9

Die neueste Updateversion von ATA kann [aus dem Download Center heruntergeladen](https://www.microsoft.com/download/details.aspx?id=56725) werden. Die Vollversion kann aus dem [Evaluation Center](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics) heruntergeladen werden.

Die vorliegenden Anmerkungen zu dieser Version enthalten Informationen zu Updates, neuen Features, Fehlerbehebungen und bekannten Problemen in dieser Version von Advanced Threat Analytics.

## <a name="new--updated-detections"></a>Neue und aktualisierte Erkennung

-  **Erstellung von verdächtigen Diensten:** Angreifer versuchen, verdächtige Dienste auf Ihrem Netzwerk auszuführen. ATA gibt jetzt eine Warnung aus, wenn erkannt wird, dass jemand auf einem Domänencontroller einen neuen Dienst ausführt, der verdächtig erscheint. Dieser Erkennungsvorgang basiert nicht auf Netzwerkdatenverkehr, sondern auf Ereignissen. Weitere Informationen dazu finden Sie im [Advanced Threat Analytics-Leitfaden zu verdächtigen Aktivitäten](suspicious-activity-guide.md#suspicious-service-creation).


## <a name="new-reports-to-help-you-investigate"></a>Neue Berichte, um Sie bei der Untersuchung zu unterstützen 

-   Mithilfe der Option [**Kennwörter in Klartext offengelegt**](reports.md) können Sie feststellen, wenn Konten, die sowohl sensible als auch nicht sensible Daten enthalten können, Anmeldeinformationen für Konten in Klartext senden. Dadurch können Sie die Verwendung der einfachen LDAP-Bindung in Ihrer Umgebung untersuchen und reduzieren, um so die Sicherheitsstufe Ihres Netzwerks zu erhöhen. Der Bericht ersetzt die Klartextwarnungen über verdächtige Aktivitäten für Dienste und sensible Konten.

- Unter [**Lateral Movement-Pfade zu sensiblen Konten**](reports.md) werden die sensiblen Konten aufgeführt, die über Lateral Movement-Pfade zur Verfügung gestellt werden. Um die Angriffsfläche zu minimieren, kann so die Anzahl dieser Pfade verringert und die Sicherheit Ihres Netzwerks erhöht werden. Indem Lateral Movement-Vorgänge verhindert werden, können sich Angreifer nicht zwischen Benutzern und Computern in Ihrem Netzwerk bewegen, bis sie auf den Jackpot in Sachen virtuelle Sicherheit stoßen: die sensiblen Anmeldeinformationen Ihres Administratorkontos.

## <a name="improved-investigation"></a>Verbesserte Untersuchung

-  ATA 1.9 umfasst ein neues und verbessertes [Entitätsprofil](entity-profiles.md). Das Entitätsprofil umfasst ein Dashboard, das für eine detaillierte Untersuchung von Benutzern, den Ressourcen, auf die sie zugreifen können, sowie auf deren Verlauf, ausgerichtet ist. Außerdem können Sie mithilfe des Entitätsprofils sensible Benutzer ermitteln, auf die über Lateral Movement-Pfade zugegriffen werden kann. 

-   Mithilfe von ATA 1.9 können Sie [manuell Gruppen oder Konten als sensibel markieren](tag-sensitive-accounts.md), um den Erkennungsvorgang zu verbessern. Diese Markierungen wirken sich auf einige ATA-Erkennungsvorgänge aus, wie die Vorgänge zum Erkennen von Änderungen sensibler Gruppen und von Lateral Movement-Pfaden, für wichtig ist zu wissen, welche Gruppen und Konten als sensibel angesehen werden.

## <a name="performance-improvements"></a>Leistungsverbesserungen

- Die Infrastruktur von ATA Center wurde bezüglich der Leistung verbessert: Die aggregierte Datenverkehrsansicht ermöglicht Optimierungen der CPU- und Paketpipeline und verwendet Sockets zu Domänencontrollern erneut, um SSL-Sitzungen zum DC zu minimieren.



## <a name="additional-changes"></a>Weitere Änderungen

- Nach der Veröffentlichung einer neuen Version von ATA wird das Symbol [**Neuigkeiten**](working-with-ata-console.md) in der Symbolleiste angezeigt, und Sie erhalten Informationen darüber, was in der neusten Version geändert wurde. Außerdem erhalten Sie einen Link zu einem ausführlichen Änderungsprotokoll zu der Version.


## <a name="removed-and-deprecated-features"></a>Entfernte und veraltete Features

- Die Warnung für verdächtige Aktivitäten bei fehlerhafter Vertrauensstellung (**Broken trust suspicious activity**) wurde entfernt.
- Die verdächtige Aktivität „Kennwörter im Klartextformat“ wurde entfernt. Sie wurde durch die Option [**Passwords exposed in clear text report**](reports.md) (Bericht zu Kennwörtern im Klartextformat) ersetzt.



## <a name="see-also"></a>Weitere Informationen
[Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Aktualisieren von ATA auf Version 1.9: Migrationshandbuch](ata-update-1.9-migration-guide.md)

