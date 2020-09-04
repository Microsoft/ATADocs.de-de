---
title: Integration von Azure Advanced Threat Protection in Microsoft Defender ATP
description: Integration von Azure Advanced Threat Protection in Microsoft Defender ATP, damit sämtliche Bedrohungen ermittelt werden können
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 02/19/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: f6f3ed75-d6bb-4966-a9a7-5339c4f3ebac
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: cd8e17d48af6958367f0514caaad3acee8477c35
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88956753"
---
# <a name="integrate-azure-atp-with-microsoft-defender-atp"></a>Integration von Azure ATP in Microsoft Defender ATP

Mithilfe von Azure Advanced Threat Protection können Sie Azure ATP in Microsoft Defender ATP integrieren, wodurch Sie eine noch umfangreichere Möglichkeit zum Schutz vor Bedrohungen erhalten. Während Azure ATP den Datenverkehr auf Ihren Domänencontrollern überwacht, überwacht Microsoft Defender ATP Ihre Endpunkte. Beide Dienste stellen gemeinsam eine Schnittstelle bereit, über die Sie Ihre Umgebung schützen können.

Wenn Sie Microsoft Defender ATP in Azure ATP integrieren, können Sie beide Dienste in vollem Umfang nutzen und Ihre Umgebung einschließlich der folgenden Bestandteile sichern:

- Verhaltenssensoren der Endpunkte: Diese Sensoren, die in Windows 10 eingebettet sind, sammeln und verarbeiten Signale zum Verhalten des Betriebssystems (z. B. Kommunikation zum Prozess, zur Registrierung, zu den Dateien und zum Netzwerk) und senden diese Sensordaten an Ihre private, isolierte Cloudinstanz von Microsoft Defender ATP.

- Analyse der Cloudsicherheit: Signale zum Verhalten verwenden Big Data, Machine Learning und eindeutige Microsoft-Ansichten des gesamten Windows-Ökosystems (z. B. das [Microsoft-Tool zum Entfernen bösartiger Software](https://www.microsoft.com/download/malicious-software-removal-tool-details.aspx)), Cloudprodukte des Unternehmens (wie Microsoft 365) und Online Assets (wie die URL-Bewertung von Bing und SmartScreen). Diese Signale werden in Einblicke, Erkennungsvorgänge und empfohlene Reaktionen auf komplexe Bedrohungen übersetzt.

- Informationen zu Bedrohungen: Mithilfe von Informationen zu Bedrohungen kann Microsoft Defender ATP Angriffstools, Techniken und Prozeduren ermitteln sowie Warnungen generieren, wenn diese Aktivitäten in den erfassten Sensordaten gefunden werden. Die Informationen werden von Microsoft Hunters und Sicherheitsteams generiert und durch Informationen zu Bedrohungen ergänzt, die von Partnern bereitgestellt werden.

Die Azure ATP-Technologie erkennt verschiedene verdächtige Aktivitäten und konzentriert sich dabei auf die verschiedenen Phasen der Angriffskette von Cyberangriffen, so z.B.:

- Reconnaissance, während der die Angreifer Informationen zum Aufbau der Umgebung, zu den verschiedenen Assets und zu den vorhandenen Entitäten erfassen. Hier erstellen sie ganz allgemein einen Plan für die nächsten Phasen ihres Angriffs.

- Der Zyklus der Seitwärtsbewegung: Die Angreifer investieren Zeit und Mühe in die Verbreiterung ihrer Angriffsfläche in Ihrem Netzwerk.

- Domänendominanz (-persistenz): Die Angreifer sammeln die Informationen, mithilfe derer sie ihren Angriff fortsetzen und dabei eine Vielzahl von Einstiegspunkten, Anmeldeinformationen und Techniken anwenden können.

Gleichzeitig nutzt Microsoft Defender ATP die Technologie und das Fachwissen von Microsoft, um raffinierte Cyberangriffe zu ermitteln. Dabei wird Folgendes bereitgestellt:

- Verhaltens-, cloudbasierte und erweiterte Angriffserkennung  
Es werden die Angriffe gefunden, die alle anderen Schutzmaßnahmen umgangen haben (Ermittlung nach dem Sicherheitsverstoß). Außerdem werden handlungsrelevante und korrelierte Warnungen für bekannte und unbekannte Angreifer ausgegeben, die versuchen, ihre Aktivitäten vor den Endpunkten zu verbergen.

- Umfangreiche Zeitachsen für die forensische Untersuchung und Risikominderung  
Sie können ganz leicht auf jedem Computer den Umfang von Sicherheitsverletzungen oder verdächtigen Verhaltensweisen über eine umfangreiche Computerzeitachse untersuchen. Sie können über das Netzwerk auf Dateien, URLs und die Netzwerkverbindung zugreifen. Sie erhalten mithilfe von umfangreichen Auflistungen und Analysen („Detonation“) zu den einzelnen Dateien oder URLs zusätzliche Informationen.

- Integrierte, eindeutige Informationen zu Bedrohungen aus der Wissensdatenbank  
Einmalige Informationen zu Bedrohungen stellen Akteurdetails und Kontext zur Absicht jeder einzelnen informationsbasierten Ermittlung von Bedrohungen bereit. Dabei werden Microsoft-eigene Informationsquellen sowie Quellen von Drittanbietern verwendet.

## <a name="prerequisites"></a>Voraussetzungen

Zur Aktivierung dieses Features benötigen Sie Lizenzen für Azure ATP und Microsoft Defender ATP.

## <a name="how-to-integrate-azure-atp-with-microsoft-defender-atp"></a>Integration von Azure ATP in Microsoft Defender ATP

1. Öffnen Sie im Azure ATP-Portal **Konfiguration**.

    ![Azure ATP-Menü „Konfiguration“](media/atp-configuration-wd.png)
1. Wählen Sie in der Konfigurationsliste **Microsoft Defender ATP** aus, und schalten Sie die Integrationsumschaltfläche auf **Ein**.

    ![Aktivieren der Windows Defender-Integration](media/enable-integration.png)

1. Gehen Sie im [Microsoft Defender ATP-Portal](https://securitycenter.windows.com/preferences/advanced) auf **Einstellungen** > **Erweiterte Features**, und setzen Sie die **Azure ATP-Integration** auf **Ein**.

    ![Aktivieren der Microsoft Defender-ATP-Integration](media/wd-atp-enable.png)

1. Wenn Sie den Status der Integration im Azure ATP-Portal überprüfen möchten, gehen Sie zu **Einstellungen** > **Microsoft Defender ATP-Integration**. Dann wird Ihnen der Status der Integration angezeigt, und wenn ein Fehler ausgelöst wird, wird er angezeigt.

## <a name="how-it-works"></a>Funktionsweise

Nach der vollständigen Integration von Azure ATP und Microsoft Defender ATP umfasst jede Entität in Microsoft Defender ATP (im Azure ATP-Portal und im Popupelement „Miniprofil“) einen Badge, der dafür steht, dass diese Entität in Microsoft Defender ATP integriert ist.

 ![Microsoft Defender ATP-Warnungsprofil](media/profile-alerts-wd.png)

Wenn die Entität Warnungen in Microsoft Defender ATP enthält, sehen Sie eine Ziffer neben dem Badge, die Sie über die Anzahl der ausgelösten Warnungen informiert.

 ![Azure ATP-Warnungen](media/atp-integrated-wd-icon-alerts.png)

Wenn Sie auf den Badge klicken, gelangen Sie zum Microsoft Defender ATP-Portal, in dem Sie Warnungen anzeigen und behandeln können. Wenn die Entität nicht von Microsoft Defender ATP erkannt wird, wird der Badge ausgegraut.

 ![Microsoft Defender ATP grau](media/wd-grey.png)

Klicken Sie im Microsoft Defender ATP-Portal auf einen Endpunkt, um Azure ATP-Warnungen anzuzeigen. Wenn Sie in Microsoft Defender ATP auf die Warnungen für diese Entität klicken, öffnet sich die Profilseite der Entität in Azure ATP.

 > [!NOTE]
 > Die Integration von Azure ATP in Microsoft Defender ATP unterstützt nur Benutzer und Computer aus dem lokalen Azure Active Directory. Benutzer von Azure AD mit virtuellen Computern, die in Azure verwaltet werden, werden nicht als Teil der Integration angezeigt.

![Microsoft Defender ATP-Warnungen](media/wd-atp-alerts.png)

## <a name="see-also"></a>Weitere Informationen

- [Investigating lateral movement paths with Azure ATP (Untersuchen von Lateral Movement-Pfaden mit Azure ATP)](use-case-lateral-movement-path.md)
- [Azure ATP sizing tool (Azure ATP-Tool zur Größenanpassung)](https://aka.ms/aatpsizingtool)
- [Azure ATP architecture (Azure ATP-Architektur)](atp-architecture.md)
- [Install ATP (Installieren von ATP)](install-atp-step1.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
