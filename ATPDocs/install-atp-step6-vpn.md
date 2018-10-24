---
title: Installieren der VPN-Integration von Azure Advanced Threat Protection | Microsoft-Dokumentation
description: Sammeln von Kontoführungsinformationen für Azure ATP durch Integration einer VPN.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 0d9d2a1d-6c76-4909-b6f9-58523df16d4f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 382b0f31cbc24dde3905d99bab7ed8be8feb5cb4
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/04/2018
ms.locfileid: "48783745"
---
*Gilt für: Azure Advanced Threat Protection*



# <a name="integrate-vpn"></a>Integrieren des VPN

<<<<<<< KOPFTEIL Azure Advanced Threat Protection (ATP) kann Kontoführungsinformationen aus VPN-Lösungen erfassen. Nach der Konfiguration beinhaltet die Profilseite des Benutzers Informationen aus den VPN-Verbindungen, wie IP-Adressen und Standorte, aus denen die Verbindungen entstammen. Dadurch wird der Untersuchungsvorgang um zusätzliche Informationen zur Benutzeraktivität und einen neuen Ermittlungsvorgang für ungewöhnliche VPN-Verbindungen ergänzt. Der Aufruf zum Auflösen einer externen IP-Adresse an einem Standort ist anonym. In diesem Aufruf wird kein persönlicher Bezeichner gesendet.
=======
> [!div class="step-by-step"]
> [« Schritt 5](install-atp-step5.md)
> [Schritt 7 »](install-atp-step7.md)

## <a name="step-6-integrate-vpn"></a>Schritt 6: Integrieren des VPN

Azure Advanced Threat Protection kann Kontoführungsinformationen aus VPN-Lösungen erfassen. Nach der Konfiguration beinhaltet die Profilseite des Benutzers Informationen aus den VPN-Verbindungen, wie IP-Adressen und Standorte, aus denen die Verbindungen entstammen. Dadurch wird der Untersuchungsvorgang um zusätzliche Informationen zur Benutzeraktivität und einen neuen Ermittlungsvorgang für ungewöhnliche VPN-Verbindungen ergänzt. Der Aufruf zum Auflösen einer externen IP-Adresse an einem Standort ist anonym. In diesem Aufruf wird kein persönlicher Bezeichner gesendet.
>>>>>>> 209d7e7162816a4c9e6e0ec0ff8d02f771e12d04

Azure ATP arbeitet mit Ihrer VPN-Lösung zusammen, indem es an RADIUS-Buchhaltungsereignissen lauscht, die an die Azure ATP-Sensoren weitergeleitet werden. Dieser Mechanismus basiert auf einer standardmäßigen RADIUS-Kontoführung ([RFC 2866](https://tools.ietf.org/html/rfc2866)). Die folgenden VPN-Anbieter werden unterstützt:

-   Microsoft
-   F5
-   Check Point
-   Cisco ASA

## <a name="prerequisites"></a>Voraussetzungen

Stellen Sie für die Aktivierung der VPN-Integration sicher, dass die folgenden Parameter festgelegt werden:

-   Öffnen Sie Port UDP 1813 auf Ihre eigenständigen Azure ATP-Sensoren und bzw. oder die Azure ATP-Sensoren.


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

Azure ATP erfasst VPN-Daten zur Erstellung von Profilen der Standorte, über die Computer eine Verbindung mit dem Netzwerk herstellen und mit denen diese verdächtige VPN-Verbindungen erkennen können.

So konfigurieren Sie VPN-Daten in ATP:

1.  Klicken Sie im Azure ATP-Portal auf das Konfigurationszahnrad und anschließend auf **VPN**.
 

2.  Aktivieren Sie die **RADIUS-Kontoführung**, und geben Sie das **gemeinsame Geheimnis** ein, das Sie zuvor auf Ihrem RRAS-VPN-Server konfiguriert haben. Klicken Sie dann auf **Save** (Speichern).
 

  ![Konfigurieren von Azure ATP-VPN](./media/atp-vpn-radius.png)


Nachdem Sie diese Option aktiviert haben, lauschen alle Azure ATP-Sensoren und die eigenständigen Sensoren an Port 1813 für RADIUS-Buchhaltungsereignisse. Damit ist die Einrichtung abgeschlossen. 

 Nachdem der Azure ATP-Sensor die VPN-Ereignisse empfangen und an den Azure ATP-Clouddienst zur Verarbeitung gesendet hat, übergibt das Entitätsprofil verschiedene VPN-Standorte, auf die zugegriffen wurde, und die Aktivitäten im Profil enthalten Standorte.

<a name="-head"></a><<<<<<< HEAD
=======
> [!div class="step-by-step"]
> [« Schritt 6](install-atp-step5.md)
> [Schritt 7 »](install-atp-step7.md)
>>>>>>> 209d7e7162816a4c9e6e0ec0ff8d02f771e12d04


## <a name="see-also"></a>Weitere Informationen
- [Azure ATP sizing tool (Azure ATP-Tool zur Größenanpassung)](http://aka.ms/aatpsizingtool)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
