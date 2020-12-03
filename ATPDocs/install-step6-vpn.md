---
title: Installieren von Microsoft Defender für die Identitäts-VPN-Integration
description: Erfassen Sie Buchhaltungsinformationen für Microsoft Defender für die Identität, indem Sie ein VPN integrieren.
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: e7c406a198eb78c98c795ba43d9b4076610540c7
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/03/2020
ms.locfileid: "96543959"
---
# <a name="integrate-vpn"></a>Integrieren des VPN

[!INCLUDE [Product long](includes/product-long.md)] kann Buchhaltungsinformationen aus VPN-Lösungen erfassen. Nach der Konfiguration beinhaltet die Profilseite des Benutzers Informationen aus den VPN-Verbindungen, wie IP-Adressen und Standorte, aus denen die Verbindungen entstammen. Dadurch wird der Untersuchungsvorgang um zusätzliche Informationen zur Benutzeraktivität und einen neuen Ermittlungsvorgang für ungewöhnliche VPN-Verbindungen ergänzt. Der Aufruf zum Auflösen einer externen IP-Adresse an einem Standort ist anonym. In diesem Aufruf wird kein persönlicher Bezeichner gesendet.

[!INCLUDE [Product short](includes/product-short.md)] Integration in Ihre VPN-Lösung durch lauschen auf RADIUS-Buchhaltungs Ereignisse, die an die Sensoren weitergeleitet werden [!INCLUDE [Product short](includes/product-short.md)] . Dieser Mechanismus basiert auf einer standardmäßigen RADIUS-Kontoführung ([RFC 2866](https://tools.ietf.org/html/rfc2866)). Die folgenden VPN-Anbieter werden unterstützt:

- Microsoft
- F5
- Check Point
- Cisco ASA

## <a name="prerequisites"></a>Voraussetzungen

Stellen Sie für die Aktivierung der VPN-Integration sicher, dass die folgenden Parameter festgelegt werden:

- Öffnen Sie Port UDP 1813 auf Ihren [!INCLUDE [Product short](includes/product-short.md)] Sensoren und/oder [!INCLUDE [Product short](includes/product-short.md)] eigenständigen Sensoren.

> [!NOTE]
> Durch die Aktivierung der RADIUS-Konto **Führung** aktiviert der Sensor eine vorab bereitgestellte Windows-Firewallrichtlinie mit dem Namen " [!INCLUDE [Product short](includes/product-short.md)] **[!INCLUDE [Product long](includes/product-long.md)] Sensor** ", um die eingehende RADIUS-Kontoführung über Port UDP 1813 zuzulassen

Im untenstehenden Beispiel wird der Microsoft-Routing- und Remotezugriffsserver (RRAS) zur Beschreibung des VPN-Konfigurationsvorgangs verwendet.

Wenn Sie die VPN-Lösung eines Drittanbieters nutzen, greifen Sie auf dessen Dokumentation zurück, um zu erfahren, wie Sie die RADIUS-Kontoführung aktivieren.

## <a name="configure-radius-accounting-on-the-vpn-system"></a>Konfigurieren der RADIUS-Kontoführung auf dem VPN-System

Führen Sie auf Ihrem RRAS-Server die folgenden Schritte aus.

1. Öffnen Sie die Routing- und Remotezugriffs-Konsole.
1. Klicken Sie mit der rechten Maustaste auf den Server, und klicken Sie anschließend auf **Eigenschaften**.
1. Wählen Sie unter **Kontoführungsanbieter** in der Registerkarte **Sicherheit** **RADIUS-Kontoführung** aus, und klicken Sie auf **Konfigurieren**.

    ![RADIUS-Setup](media/radius-setup.png)

1. Geben Sie im Fenster **RADIUS-Server hinzufügen** den **Servernamen** des nächsten [!INCLUDE [Product short](includes/product-short.md)] Sensors ein (der über eine Netzwerkverbindung verfügt). Um Hochverfügbarkeit zu erreichen, können Sie zusätzliche [!INCLUDE [Product short](includes/product-short.md)] Sensoren als RADIUS-Server hinzufügen. Stellen Sie unter **Port** sicher, dass die Standardeinstellung 1813 konfiguriert ist. Klicken Sie auf **Ändern**, und tippen Sie eine neue, geheime Zeichenfolge von alphanumerischen Zeichen ein. Notieren Sie sich die neue Zeichenfolge für den gemeinsamen geheimen Schlüssel, da Sie Sie später während der Konfiguration ausfüllen müssen [!INCLUDE [Product short](includes/product-short.md)] . Prüfen Sie das Feld **„RADIUS-Kontoführung aktiviert“- und „RADIUS-Kontoführung deaktiviert“-Nachrichten senden**, und klicken Sie anschließend in allen geöffneten Dialogfeldern auf **OK**.

    ![VPN-Setup](media/vpn-set-accounting.png)

### <a name="configure-vpn-in-product-short"></a>Konfigurieren von VPN in [!INCLUDE [Product short](includes/product-short.md)]

[!INCLUDE [Product short](includes/product-short.md)] sammelt VPN-Daten, die die Profilerstellung für die Speicherorte erleichtern, von denen Computer eine Verbindung mit dem Netzwerk herstellen und verdächtige VPN-Verbindungen erkennen können.

So konfigurieren Sie VPN-Daten in [!INCLUDE [Product short](includes/product-short.md)] :

1. [!INCLUDE [Product short](includes/product-short.md)]Klicken Sie im Portal auf das konfigurationszahnrad und dann auf **VPN**.
1. Aktivieren Sie die **RADIUS-Kontoführung**, und geben Sie das **gemeinsame Geheimnis** ein, das Sie zuvor auf Ihrem RRAS-VPN-Server konfiguriert haben. Klicken Sie dann auf **Save** (Speichern).

    ![Konfigurieren [! INCLUDE [Product Short] (includes/Produkt-Short. MD)] VPN](media/vpn-radius.png)

Nachdem dies aktiviert ist, [!INCLUDE [Product short](includes/product-short.md)] lauschen alle Sensoren an Port 1813 für RADIUS-Buchhaltungs Ereignisse, und Ihr VPN-Setup ist vollständig.

 Nachdem der [!INCLUDE [Product short](includes/product-short.md)] Sensor die VPN-Ereignisse empfangen und zur Verarbeitung an den [!INCLUDE [Product short](includes/product-short.md)] clouddienst gesendet hat, gibt das Entitäts Profil unterschiedliche VPN-Speicherorte an, auf die zugegriffen wurde, und Aktivitäten im Profil geben Speicherorte an.

## <a name="see-also"></a>Weitere Informationen

- [[!INCLUDE [Product short](includes/product-short.md)]-Tool zur Größenanpassung](https://aka.ms/aatpsizingtool)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Voraussetzungen für [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
