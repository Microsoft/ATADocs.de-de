---
title: 'Installieren von Azure Advanced Threat Protection: Schritt 6 | Microsoft-Dokumentation'
description: In diesem Schritt der Installation von Azure ATP integrieren Sie Ihr VPN.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/14/2018
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 0d9d2a1d-6c76-4909-b6f9-58523df16d4f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: d29210983f3f9f879b462ef760d0b3fe6e53cd5d
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/21/2018
---
*Gilt für: Azure Advanced Threat Protection*



# <a name="install-azure-atp---step-6"></a>Installieren von Azure ATP: Schritt 6

>[!div class="step-by-step"]
[« Schritt 5](install-atp-step5.md)
[Schritt 7 »](install-atp-step7.md)

## <a name="step-6-integrate-vpn"></a>Schritt 6: Integrieren des VPN

Azure Advanced Threat Protection kann Kontoführungsinformationen aus VPN-Lösungen erfassen. Nach der Konfiguration beinhaltet die Profilseite des Benutzers Informationen aus den VPN-Verbindungen, wie IP-Adressen und Standorte, aus denen die Verbindungen entstammen. Dadurch wird der Untersuchungsvorgang um zusätzliche Informationen zur Benutzeraktivität und einen neuen Ermittlungsvorgang für ungewöhnliche VPN-Verbindungen ergänzt. Der Aufruf zum Auflösen einer externen IP-Adresse an einem Standort ist anonym. In diesem Aufruf wird kein persönlicher Bezeichner gesendet.

Azure ATP arbeitet mit Ihrer VPN-Lösung zusammen, indem es an RADIUS-Buchhaltungsereignissen lauscht, die an die Azure ATP-Sensoren weitergeleitet werden. Dieser Mechanismus basiert auf einer standardmäßigen RADIUS-Kontoführung ([RFC 2866](https://tools.ietf.org/html/rfc2866)). Die folgenden VPN-Anbieter werden unterstützt:

-   Microsoft
-   F5
-   Check Point
-   Cisco ASA

## <a name="prerequisites"></a>Voraussetzungen

Stellen Sie für die Aktivierung der VPN-Integration sicher, dass die folgenden Parameter festgelegt werden:

-   Öffnen Sie Port UDP 1813 auf Ihren eigenständigen Azure ATP-Sensoren und den Azure ATP-Sensor.


Im untenstehenden Beispiel wird der Microsoft-Routing- und Remotezugriffsserver (RRAS) zur Beschreibung des VPN-Konfigurationsvorgangs verwendet.

Wenn Sie die VPN-Lösung eines Drittanbieters nutzen, greifen Sie auf dessen Dokumentation zurück, um zu erfahren, wie Sie die RADIUS-Kontoführung aktivieren.

## <a name="configure-radius-accounting-on-the-vpn-system"></a>Konfigurieren der RADIUS-Kontoführung auf dem VPN-System

Führen Sie auf Ihrem RRAS-Server die folgenden Schritte aus.
 
1.  Öffnen Sie die Routing- und Remotezugriffs-Konsole.
2.  Klicken Sie mit der rechten Maustaste auf den Server, und klicken Sie anschließend auf **Eigenschaften**.
3.  Wählen Sie unter **Kontoführungsanbieter** in der Registerkarte **Sicherheit** **RADIUS-Kontoführung** aus, und klicken Sie auf **Konfigurieren**.

    ![RADIUS-Setup](./media/radius-setup.png)

4.  Geben Sie im Fenster **RADIUS-Server hinzufügen** den **Servernamen** des nächsten eigenständigen Azure ATP-Sensors oder Azure ATP-Sensors ein. Stellen Sie unter **Port** sicher, dass die Standardeinstellung 1813 konfiguriert ist. Klicken Sie auf **Ändern**, und tippen Sie eine neue, geheime Zeichenfolge von alphanumerischen Zeichen an, die Sie sich merken können, da Sie sie im weiteren Verlauf Ihrer Azure ATP-Konfiguration eingeben müssen. Prüfen Sie das Feld **Send RADIUS Account On and Accounting Off messages** („RADIUS-Kontoführung aktiviert“- und „RADIUS-Kontoführung deaktiviert“-Nachrichten senden), und klicken Sie anschließend in allen geöffneten Dialogfeldern auf **OK**.
 
     ![VPN-Setup](./media/vpn-set-accounting.png)
     
### <a name="configure-vpn-in-atp"></a>Konfigurieren von VPN in ATP

Azure ATP erfasst VPN-Daten zur Erstellung von Profilen der Standorte, über die Computer eine Verbindung mit dem Netzwerk herstellen und mit denen diese ungewöhnliche VPN-Verbindungen erkennen können.

So konfigurieren Sie VPN-Daten in ATP:

1.  Klicken Sie im Azure ATP-Arbeitsbereichsportal auf das Zahnrad „Konfiguration“ und anschließend auf **VPN**.
 

2.  Aktivieren Sie die **RADIUS-Kontoführung**, und geben Sie das **gemeinsame Geheimnis** ein, das Sie zuvor auf Ihrem RRAS-VPN-Server konfiguriert haben. Klicken Sie dann auf **Save** (Speichern).
 

  ![Konfigurieren von Azure ATP-VPN](./media/atp-vpn-radius.png)


Nachdem Sie diese Option aktiviert haben, lauschen alle eigenständigen Azure ATP-Sensoren und Sensoren an Port 1813 für RADIUS-Buchhaltungsereignisse. 

Damit ist Ihr Setup abgeschlossen. 

Nachdem der Azure ATP-Sensor die VPN-Ereignisse empfangen und an den Azure ATP-Clouddienst zur Verarbeitung gesendet hat, übergibt das Entitätsprofil verschiedene VPN-Standorte, auf die zugegriffen wurde, und die Aktivitäten im Profil enthalten Standorte.





>[!div class="step-by-step"]
[« Schritt 6](install-atp-step5.md)
[Schritt 7 »](install-atp-step7.md)


## <a name="see-also"></a>Weitere Informationen
- [Azure ATP sizing tool (Azure ATP-Tool zur Größenanpassung)](http://aka.ms/aatpsizingtool)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)
