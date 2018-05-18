---
title: Integration von Azure Advanced Threat Protection in Windows Defender ATP | Microsoft-Dokumentation
description: Integration von Azure Advanced Threat Protection in Windows Defender ATP, damit sämtliche Bedrohungen ermittelt werden können
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/16/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: f6f3ed75-d6bb-4966-a9a7-5339c4f3ebac
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 17ade33a55039eaf8abc98901cdab9ebeef850c5
ms.sourcegitcommit: 714a01edc9006b38d1163d03852dafc2a5fddb5f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/16/2018
---
*Gilt für: Azure Advanced Threat Protection*

# <a name="integrating-azure-atp-with-windows-defender-atp"></a>Integration von Azure ATP in Windows Defender ATP

Mithilfe von Azure Advanced Threat Protection können Sie Azure ATP in Windows Defender ATP integrieren, wodurch Sie eine noch umfangreichere Möglichkeit zum Schutz vor Bedrohungen erhalten. Während Azure ATP den Datenverkehr auf Ihren Domänencontrollern überwacht, überwacht Windows Defender ATP Ihre Endpunkte. Beide Dienste stellen gemeinsam eine Schnittstelle bereit, über die Sie Ihre Umgebung schützen können.

> [!NOTE]
> Die Integration ist derzeit nur aktiviert, wenn Sie ein Windows Defender ATP-Kunde für die private Vorschau sind.
 
Wenn Sie Windows Defender ATP in Azure ATP integrieren, können Sie beide Dienste in vollem Umfang nutzen und Ihre Umgebung einschließlich der folgenden Bestandteile sichern:

- Azure ATP-Sensoren und eigenständige Sensoren: Können sich auf Ihren Domänencontrollern direkt befinden oder eine Portspiegelung von Ihren Domänencontrollern auf ATP darstellen, um den Netzwerkdatenverkehr verschiedener Protokolle (wie Kerberos, DNS, RPC, NTLM) für die Authentifizierung, Autorisierung und das Sammeln von Informationen zu erfassen und zu analysieren. 

-   Verhaltenssensoren der Endpunkte: Diese Sensoren, die in Windows 10 eingebettet sind, sammeln und verarbeiten Signale zum Verhalten des Betriebssystems(z.B. Kommunikationen zum Prozess, zur Registrierung, zu den Dateien und zum Netzwerk) und senden diese Sensordaten an Ihre private, isolierte Cloudinstanz von Windows Defender ATP.

- Analyse der Cloudsicherheit: Signale zum Verhalten verwenden Big Data, Machine Learning und eindeutige Microsoft-Ansichten des gesamten Windows-Ökosystems (z.B. das [Microsoft-Tool zum Entfernen bösartiger Software](https://www.microsoft.com/download/malicious-software-removal-tool-details.aspx)), Cloudprodukte des Unternehmens (wie Office 365) und Online Assets (wie die URL-Bewertung von Bing und SmartScreen). Diese Signale werden in Einblicke, Erkennungsvorgänge und empfohlene Antworten auf erweiterte Bedrohungen übersetzt.

- Informationen zu Bedrohungen: Mithilfe von Informationen zu Bedrohungen kann Windows Defender ATP Angriffstools, Techniken und Prozeduren ermitteln sowie Warnungen generieren, wenn diese in den erfassten Sensordaten gefunden werden. Die Informationen werden von Microsoft Hunters und Sicherheitsteams generiert und durch Informationen erweitert, die von Partnern bereitgestellt werden.

Die Azure ATP-Technologie erkennt verschiedene verdächtige Aktivitäten und konzentriert sich dabei auf die verschiedenen Phasen der Angriffskette von Cyberangriffen, so z.B.:

- Reconnaissance, während der die Angreifer Informationen zum Aufbau der Umgebung, zu den verschiedenen Assets und zu den vorhandenen Entitäten erfassen. Sie erstellen ganz allgemein einen Plan für die nächsten Phasen ihres Angriffs.

- Der Zyklus der Seitwärtsbewegung: Die Angreifer investieren Zeit und Mühe in die Verbreiterung ihrer Angriffsfläche in Ihrem Netzwerk.

- Domänendominanz (-persistenz): Die Angreifer sammeln die Informationen, mithilfe derer sie ihren Angriff fortsetzen und dabei eine Vielzahl von Einstiegspunkten, Anmeldeinformationen und Techniken anwenden können.

Gleichzeitig nutzt Windows Defender ATP die Technologie und das Fachwissen von Microsoft, um raffinierte Cyberangriffe zu ermitteln. Dabei wird Folgendes bereitgestellt:

- Verhaltens-, cloudbasierte und erweiterte Angriffserkennung<br></br>Es werden die Angriffe gefunden, die alle anderen Schutzmaßnahmen umgangen haben (Ermittlung nach dem Sicherheitsverstoß). Außerdem werden handlungsrelevante und korrelierte Warnungen für bekannte und unbekannte Angreifer ausgegeben, die versuchen, ihre Aktivitäten vor den Endpunkten zu verbergen.

- Umfangreiche Zeitachsen für die forensische Untersuchung und Risikominderung<br></br>Sie können ganz leicht auf jedem Computer den Umfang von Sicherheitsverletzungen oder verdächtigen Verhaltensweisen über eine umfangreiche Computerzeitachse untersuchen. Sie können über das Netzwerk auf Dateien, URLs und die Netzwerkverbindung zugreifen. Sie erhalten mithilfe von umfangreichen Auflistungen und Analysen („Detonation“) zu den einzelnen Dateien oder URLs zusätzliche Informationen.

- Integrierte, eindeutige Informationen zu Bedrohungen aus der Wissensdatenbank<br></br>Einmalige Informationen zu Bedrohungen stellen Akteurdetails und Kontext zur Absicht jeder einzelnen Intel-basierten Ermittlung von Bedrohungen bereit. Dabei werden Microsoft-eigene Informationsquellen sowie Quellen von Drittanbietern verwendet.

## <a name="prerequisites"></a>Voraussetzungen

Zur Aktivierung dieses Features benötigen Sie Lizenzen für Azure ATP und Windows Defender ATP. 


## <a name="how-to-integrate-azure-atp-with-windows-defender-atp"></a>Integrieren von Azure ATP in Windows Defender ATP

1. Legen Sie den Arbeitsbereich, den Sie integrieren möchten, als **Primär** fest. Nur ein Arbeitsbereich kann als „Primär“ gekennzeichnet sein, und nur ein primärer Arbeitsbereich kann in andere Dienste integriert werden. Wenn Sie zu einem späteren Zeitpunkt dem Arbeitsbereich die Kennzeichnung als „Primär“ entziehen möchten, müssen Sie zunächst die Integration entfernen, bevor Sie diesen als „Nicht primär“ kennzeichnen können.

 ![Primärer Arbeitsbereich](./media/primary-workspace.png)

2. Klicken Sie zunächst auf **Konfiguration** und anschließend unter **Datenquellen** auf **Windows Defender ATP**. Klicken Sie dann auf den Link zur **Verwaltung von Arbeitsbereichen**. Dies ist nur möglich, wenn Sie über eine Windows Defender ATP-Lizenz verfügen und Sie bereits den Integrationsvorgang für Windows Defender ATP durchgeführt haben. 

3. Klicken Sie in Ihrem primären Arbeitsbereich auf das Zahnrad „Einstellungen“.

 ![Integration des Arbeitsbereichs](./media/edit-workspace.png)
 
3. Legen Sie die Integration auf **On** (Aktiviert) fest. 

 ![Aktivieren der Integration](./media/enable-integration.png)

4. Gehen Sie im [Windows Defender ATP-Portal](https://beta.securitycenter.windows.com/preferences/advanced) auf **Einstellungen** > **Erweiterte Features**, und legen Sie **Azure ATP integration** (Azure ATP-Integration) auf **On** (Aktiviert) fest. 

 ![Aktivieren der Windows Defender-ATP-Integration](./media/wd-atp-enable.png)

5. Wenn Sie den Status der Integration im Azure ATP-Arbeitsbereichsportal überprüfen möchten, gehen Sie zu **Einstellungen** > **Windows Defender ATP integration** (Windows Defender ATP-Integration). Dann wird Ihnen der Status der Integration angezeigt. Wenn ein Fehler ausgelöst wird, wird dieser angezeigt. Außerdem wird Ihnen angezeigt, welcher Arbeitsbereich in Windows Defender ATP integriert wird.

## <a name="how-it-works"></a>Funktionsweise

Nach der vollständigen Integration von Azure ATP und Windows Defender ATP umfasst jede Entität in Windows Defender ATP (im Azure ATP-Arbeitsbereichsportal und im Popupelement „Miniprofil“) einen Badge, der dafür steht, dass diese Entität in Windows Defender ATP integriert ist. 

 ![Windows Defender ATP-Warnungen](./media/profile-alerts-wd.png)

Wenn die Entität Warnungen in Windows Defender ATP enthält, sehen Sie eine Ziffer neben dem Badge, die Sie über die Anzahl der ausgelösten Warnungen informiert.

 ![Azure ATP-Warnungen](./media/atp-integrated-wd-icon-alerts.png)

Wenn Sie auf den Badge klicken, gelangen Sie zum Windows Defender ATP-Portal, in dem Sie Warnungen anzeigen und behandeln können. Wenn die Entität nicht von Windows Defender ATP erkannt wird, wird der Badge ausgegraut. 

 ![Windows Defender ATP (ausgegraut)](./media/wd-grey.png)

Im Windows Defender ATP-Portal können Sie Azure ATP-Warnungen anzeigen lassen, wenn Sie auf einen Endpunkt klicken. Wenn Sie auf die Warnungen für diese Entität in Windows Defender ATP klicken, öffnet sich die Profilseite der Entität in Azure ATP. 
 
 > ![HINWEIS] Die Integration von Azure Advanced Threat Protection mit Windows Defender ATP unterstützt nur Benutzer und Computer aus dem lokalen Azure Active Directory. Benutzer von Azure AD mit virtuellen Computern, die in Azure verwaltet werden, werden nicht als Teil der Integration angezeigt. 

![Windows Defender ATP-Warnungen](./media/wd-atp-alerts.png)


## <a name="see-also"></a>Weitere Informationen

- [Investigating lateral movement paths with Azure ATP (Untersuchen von Lateral Movement-Pfaden mit Azure ATP)](use-case-lateral-movement-path.md)
- [Azure ATP sizing tool (Azure ATP-Tool zur Größenanpassung)](http://aka.ms/aatpsizingtool)
- [Azure ATP architecture (Azure ATP-Architektur)](atp-architecture.md)
- [Install ATP (Installieren von ATP)](install-atp-step1.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)

