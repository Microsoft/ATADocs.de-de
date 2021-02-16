---
title: Microsoft Defender für die Identitäts Integration mit Microsoft Defender for Endpoint
description: Integrieren von Microsoft Defender für Identity in Microsoft Defender for Endpoint für die vollständige Bedrohungserkennung
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: 356f97509fe3af81a4d1c896e7b64b2779e6028a
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533867"
---
# <a name="integrate-microsoft-defender-for-identity-with-microsoft-defender-for-endpoint"></a>Integrieren von Microsoft Defender für Identity in Microsoft Defender for Endpoint

[!INCLUDE [Product long](includes/product-long.md)] ermöglicht die Integration in [!INCLUDE [Product long](includes/product-long.md)] Defender for Endpoint, um eine noch umfassendere Lösung für den Schutz vor Bedrohungen zu erhalten. Während [!INCLUDE [Product short](includes/product-short.md)] den Datenverkehr auf Ihren Domänen Controllern überwacht, überwacht Defender for Endpoint ihre Endpunkte und stellt eine einzige Schnittstelle bereit, über die Sie Ihre Umgebung schützen können.

Durch die Integration von Defender für Endpoint in [!INCLUDE [Product short](includes/product-short.md)] können Sie die volle Leistung beider Dienste nutzen und Ihre Umgebung schützen, einschließlich der folgenden:

- Endpunkt Verhaltens Sensoren: diese Sensoren werden in Windows 10 eingebettet und verarbeiten Verhaltens Signale des Betriebssystems (z. b. Prozess-, Registrierungs-, Datei-und Netzwerkkommunikation) und senden diese Sensordaten an Ihre private, isolierte cloudinstanz von Defender for Endpoint.

- Analyse der Cloudsicherheit: Signale zum Verhalten verwenden Big Data, Machine Learning und eindeutige Microsoft-Ansichten des gesamten Windows-Ökosystems (z. B. das [Microsoft-Tool zum Entfernen bösartiger Software](https://www.microsoft.com/download/malicious-software-removal-tool-details.aspx)), Cloudprodukte des Unternehmens (wie Microsoft 365) und Online Assets (wie die URL-Bewertung von Bing und SmartScreen). Diese Signale werden in Einblicke, Erkennungsvorgänge und empfohlene Reaktionen auf komplexe Bedrohungen übersetzt.

- Bedrohungs Intelligenz: wird von Microsoft-Jägern und Sicherheitsteams generiert und durch die von Partnern bereitgestellten Bedrohungs Informationen ergänzt, ermöglicht die Bedrohungsanalyse dem Defender für den Endpunkt, Angreifer-Tools,-Verfahren und-Prozeduren zu identifizieren und Warnungen zu generieren, wenn diese Aktivitäten in den gesammelten Sensordaten

[!INCLUDE [Product short](includes/product-short.md)] die Technologie erkennt mehrere verdächtige Aktivitäten und konzentriert sich auf verschiedene Phasen der Kill-Kette von Cyberangriffen, darunter:

- Reconnaissance, während der die Angreifer Informationen zum Aufbau der Umgebung, zu den verschiedenen Assets und zu den vorhandenen Entitäten erfassen. Hier erstellen sie ganz allgemein einen Plan für die nächsten Phasen ihres Angriffs.

- Der Zyklus der Seitwärtsbewegung: Die Angreifer investieren Zeit und Mühe in die Verbreiterung ihrer Angriffsfläche in Ihrem Netzwerk.

- Domänendominanz (-persistenz): Die Angreifer sammeln die Informationen, mithilfe derer sie ihren Angriff fortsetzen und dabei eine Vielzahl von Einstiegspunkten, Anmeldeinformationen und Techniken anwenden können.

Gleichzeitig nutzt Defender for Endpoint Microsoft-Technologie und-Know-how, um ausgereifte Cyberangriffe zu erkennen und Folgendes bereitzustellen:

- Verhaltens-, cloudbasierte und erweiterte Angriffserkennung  
Sucht die Angriffe, die alle anderen Schutzmaßnahmen durchgeführt haben (Erkennung nach der Verletzung), bietet Handlungs relevante, korrelierte Warnungen für bekannte und unbekannte Angreifer, die versuchen, ihre Aktivitäten auf Endpunkten auszublenden.

- Umfangreiche Zeitachsen für die forensische Untersuchung und Risikominderung  
Sie können ganz leicht auf jedem Computer den Umfang von Sicherheitsverletzungen oder verdächtigen Verhaltensweisen über eine umfangreiche Computerzeitachse untersuchen. Sie können über das Netzwerk auf Dateien, URLs und die Netzwerkverbindung zugreifen. Sie erhalten mithilfe von umfangreichen Auflistungen und Analysen („Detonation“) zu den einzelnen Dateien oder URLs zusätzliche Informationen.

- Integrierte, eindeutige Wissensdatenbank mit Bedrohungs Intelligenz  
Einmalige Informationen zu Bedrohungen stellen Akteurdetails und Kontext zur Absicht jeder einzelnen informationsbasierten Ermittlung von Bedrohungen bereit. Dabei werden Microsoft-eigene Informationsquellen sowie Quellen von Drittanbietern verwendet.

## <a name="prerequisites"></a>Voraussetzungen

Um dieses Feature zu aktivieren, benötigen Sie eine Lizenz für [!INCLUDE [Product short](includes/product-short.md)] und Defender for Endpoint.

<a name="how-to-integrate-azure-atp-with-microsoft-defender-atp"></a>

## <a name="how-to-integrate-defender-for-identity-with-defender-for-endpoint"></a>Integrieren von Defender für Identity in Defender for Endpoint

1. Wählen Sie im [!INCLUDE [Product short](includes/product-short.md)]-Portal **Konfiguration** aus.

    ![[! INCLUDE [Product Short] (includes/Produkt-Short. MD)] Konfigurationsmenü](media/msde-configuration.png)
1. Wählen Sie in der Liste Konfigurationen die Option **Microsoft Defender für Endpunkt aus** , und legen Sie die Integration **auf** ein fest.

    ![Aktivieren der Windows Defender-Integration](media/msde-enable-integration.png)

1. Wechseln Sie im [Defender für Endpoint-Portal](https://securitycenter.windows.com/preferences/advanced)zu **Einstellungen** und **Erweiterte Features** , und legen Sie **[!INCLUDE [Product long](includes/product-long.md)] Integration** **auf ein fest.**

    ![Defender for Endpoint enable-Integration](media/msde-enable.png)

1. Wechseln Sie im [!INCLUDE [Product short](includes/product-short.md)] Portal zu **Einstellungen**  >  **Microsoft Defender für Endpunkt Integration**, um den Status der Integration zu überprüfen. Dann wird Ihnen der Status der Integration angezeigt, und wenn ein Fehler ausgelöst wird, wird er angezeigt.

## <a name="how-it-works"></a>Funktionsweise

Nachdem [!INCLUDE [Product short](includes/product-short.md)] und Defender for Endpoint vollständig integriert wurden, enthält die in [!INCLUDE [Product short](includes/product-short.md)] Defender for Endpoint vorhandene Entität im Portal in der Popup-und Entitäts Profilseite einen Badge, um anzuzeigen, dass Sie in Defender for Endpoint integriert ist.

 ![Defender for Endpoint Alerts-Profil](media/profile-alerts-msde.png)

Wenn die Entität Warnungen in Defender for Endpoint enthält, gibt es eine Zahl neben dem Badge, damit Sie wissen, wie viele Warnungen ausgelöst wurden.

 ![[! Warnungen einschließen [Product Short] (includes/Produkt-Short. MD)]](media/msde-icon-alerts.png)

Wenn Sie auf das Badge klicken, gelangen Sie zum Defender for Endpoint-Portal, wo Sie die Warnungen anzeigen und mindern können. Wenn die Entität nicht von Defender for Endpoint erkannt wird, ist der Badge abgeblendet.

 ![Defender für Endpunkt grau](media/msde-grey.png)

Klicken Sie im Defender for Endpoint-Portal auf einen Endpunkt, um [!INCLUDE [Product short](includes/product-short.md)] Warnungen anzuzeigen. Wenn Sie in Defender for Endpoint auf die Warnungen für diese Entität klicken, wird die Profilseite der Entität in geöffnet [!INCLUDE [Product short](includes/product-short.md)] .

 > [!NOTE]
 > Derzeit [!INCLUDE [Product short](includes/product-short.md)] unterstützt die Integration in Defender for Endpoint nur Benutzer und Computer aus dem lokalen Active Directory. Benutzer von Azure AD mit virtuellen Computern, die in Azure verwaltet werden, werden nicht als Teil der Integration angezeigt.

![Defender für Endpunkt Warnungen](media/msde-alerts.png)

## <a name="see-also"></a>Weitere Informationen

- [Untersuchen von Lateral Movement-Pfaden mit [!INCLUDE [Product short](includes/product-short.md)]](use-case-lateral-movement-path.md)
- [[!INCLUDE [Product short](includes/product-short.md)]-Tool zur Größenanpassung](https://aka.ms/aatpsizingtool)
- [[!INCLUDE [Product short](includes/product-short.md)]-Architektur](architecture.md)
- [Installieren von [!INCLUDE [Product short](includes/product-short.md)]](install-step1.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
