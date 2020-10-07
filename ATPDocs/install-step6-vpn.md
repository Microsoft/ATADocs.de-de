---
title: Installieren der VPN-Integration von Azure Advanced Threat Protection
description: Sammeln von Kontoführungsinformationen für Azure ATP durch Integration einer VPN.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 07/05/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 0d9d2a1d-6c76-4909-b6f9-58523df16d4f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 589e8f647abc4654d48006dd1e9b3d6a9538660f
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2020
ms.locfileid: "90913000"
---
# <a name="integrate-vpn"></a>Integrieren des VPN

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Azure Advanced Threat Protection (ATP) kann Kontoinformationen aus VPN-Lösungen erfassen. Nach der Konfiguration beinhaltet die Profilseite des Benutzers Informationen aus den VPN-Verbindungen, wie IP-Adressen und Standorte, aus denen die Verbindungen entstammen. Dadurch wird der Untersuchungsvorgang um zusätzliche Informationen zur Benutzeraktivität und einen neuen Ermittlungsvorgang für ungewöhnliche VPN-Verbindungen ergänzt. Der Aufruf zum Auflösen einer externen IP-Adresse an einem Standort ist anonym. In diesem Aufruf wird kein persönlicher Bezeichner gesendet.

Azure ATP arbeitet mit Ihrer VPN-Lösung zusammen, indem es an RADIUS-Buchhaltungsereignissen lauscht, die an die Azure ATP-Sensoren weitergeleitet werden. Dieser Mechanismus basiert auf einer standardmäßigen RADIUS-Kontoführung ([RFC 2866](https://tools.ietf.org/html/rfc2866)). Die folgenden VPN-Anbieter werden unterstützt:

- Microsoft
- F5
- Check Point
- Cisco ASA

## <a name="prerequisites"></a>Voraussetzungen

Stellen Sie für die Aktivierung der VPN-Integration sicher, dass die folgenden Parameter festgelegt werden:

- Öffnen Sie Port UDP 1813 auf Ihre eigenständigen Azure ATP-Sensoren und bzw. oder die Azure ATP-Sensoren.

> [!NOTE]
> Durch die Aktivierung der **RADIUS-Kontoführung** aktiviert der Azure ATP-Sensor eine vorab bereitgestellte Windows-Firewallrichtlinie mit dem Namen **Azure Advanced Threat Protection-Sensor**, um eingehende RADIUS-Kontoführung am Port UDP 1813 zuzulassen.

Im untenstehenden Beispiel wird der Microsoft-Routing- und Remotezugriffsserver (RRAS) zur Beschreibung des VPN-Konfigurationsvorgangs verwendet.

Wenn Sie die VPN-Lösung eines Drittanbieters nutzen, greifen Sie auf dessen Dokumentation zurück, um zu erfahren, wie Sie die RADIUS-Kontoführung aktivieren.

## <a name="configure-radius-accounting-on-the-vpn-system"></a>Konfigurieren der RADIUS-Kontoführung auf dem VPN-System

Führen Sie auf Ihrem RRAS-Server die folgenden Schritte aus.

1. Öffnen Sie die Routing- und Remotezugriffs-Konsole.
1. Klicken Sie mit der rechten Maustaste auf den Server, und klicken Sie anschließend auf **Eigenschaften**.
1. Wählen Sie unter **Kontoführungsanbieter** in der Registerkarte **Sicherheit** **RADIUS-Kontoführung** aus, und klicken Sie auf **Konfigurieren**.

    ![RADIUS-Setup](media/radius-setup.png)

1. Geben Sie im Fenster **RADIUS-Server hinzufügen** den **Servernamen** des nächsten Azure ATP-Sensors (mit Netzwerkkonnektivität) ein. Um Hochverfügbarkeit sicherzustellen, können Sie zusätzliche Azure ATP-Sensoren als RADIUS-Server hinzufügen. Stellen Sie unter **Port** sicher, dass die Standardeinstellung 1813 konfiguriert ist. Klicken Sie auf **Ändern**, und tippen Sie eine neue, geheime Zeichenfolge von alphanumerischen Zeichen ein. Notieren Sie die neue freigegebene geheime Zeichenfolge, da Sie sie später während der Azure ATP-Konfiguration eingeben müssen. Prüfen Sie das Feld **„RADIUS-Kontoführung aktiviert“- und „RADIUS-Kontoführung deaktiviert“-Nachrichten senden**, und klicken Sie anschließend in allen geöffneten Dialogfeldern auf **OK**.

    ![VPN-Setup](media/vpn-set-accounting.png)

### <a name="configure-vpn-in-atp"></a>Konfigurieren von VPN in ATP

Azure ATP erfasst VPN-Daten zur Erstellung von Profilen der Standorte, über die Computer eine Verbindung mit dem Netzwerk herstellen und mit denen diese verdächtige VPN-Verbindungen erkennen können.

So konfigurieren Sie VPN-Daten in ATP:

1. Klicken Sie im Azure ATP-Portal auf das Konfigurationszahnrad und anschließend auf **VPN**.
1. Aktivieren Sie die **RADIUS-Kontoführung**, und geben Sie das **gemeinsame Geheimnis** ein, das Sie zuvor auf Ihrem RRAS-VPN-Server konfiguriert haben. Klicken Sie dann auf **Save** (Speichern).

    ![Konfigurieren von Azure ATP-VPN](media/atp-vpn-radius.png)

Nachdem Sie diese Option aktiviert haben, lauschen alle Azure ATP-Sensoren an Port 1813 für RADIUS-Buchhaltungsereignisse. Damit ist die VPN-Einrichtung abgeschlossen.

 Nachdem der Azure ATP-Sensor die VPN-Ereignisse empfangen und an den Azure ATP-Clouddienst zur Verarbeitung gesendet hat, übergibt das Entitätsprofil verschiedene VPN-Standorte, auf die zugegriffen wurde, und die Aktivitäten im Profil enthalten Standorte.

## <a name="see-also"></a>Weitere Informationen

- [Azure ATP sizing tool (Azure ATP-Tool zur Größenanpassung)](https://aka.ms/aatpsizingtool)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](prerequisites.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)