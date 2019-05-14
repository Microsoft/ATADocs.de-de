---
title: Installieren von Advanced Threat Analytics – Schritt 7 | Microsoft-Dokumentation
description: In diesem Schritt bei der ATA-Installation integrieren Sie Ihr VPN.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: rkarlin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: e0aed853-ba52-46e1-9c55-b336271a68e7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: f98dfb3f5688f143a490a8ab7abb7eea7d8da5d9
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2019
ms.locfileid: "65197028"
---
# <a name="install-ata---step-7"></a>Installieren von ATA – Schritt 7

*Gilt für: Advanced Threat Analytics Version 1.9*

> [!div class="step-by-step"]
> [« Schritt 5](install-ata-step5.md)
> [Schritt 8 »](install-ata-step7.md)

## <a name="step-7-integrate-vpn"></a>Schritt 7: Integrieren des VPN

Die Version 1.8 von Microsoft Advanced Threat Analytics (ATA) kann Kontoführungsinformationen aus VPN-Lösungen erfassen. Nach der Konfiguration beinhaltet die Profilseite des Benutzers Informationen aus den VPN-Verbindungen, wie IP-Adressen und Standorte, aus denen die Verbindungen entstammen. Dadurch wird der Untersuchungsvorgang durch zusätzliche Informationen zur Benutzeraktivität ergänzt. Der Aufruf zum Auflösen einer externen IP-Adresse an einem Standort ist anonym. In diesem Aufruf wird kein persönlicher Bezeichner gesendet.

ATA arbeitet mit Ihrer VPN-Lösung zusammen, indem es RADIUS-Buchhaltungsereignisse abhört, die an die ATA-Gateways weitergeleitet werden. Dieser Mechanismus basiert auf einer standardmäßigen RADIUS-Kontoführung ([RFC 2866](https://tools.ietf.org/html/rfc2866)). Die folgenden VPN-Anbieter werden unterstützt:

-   Microsoft
-   F5
-   Cisco ASA

## <a name="prerequisites"></a>Voraussetzungen

Stellen Sie für die Aktivierung der VPN-Integration sicher, dass die folgenden Parameter festgelegt werden:

-   Öffnen Sie den Port UDP 1813 für Ihre ATA-Gateways und ATA-Lightweight-Gateways.

-   ATA Center muss mithilfe von HTTPS (Port 443) auf *ti.ata.azure.com* zugreifen können, sodass der Standort eingehender IP-Adressen abgefragt werden kann.

Im untenstehenden Beispiel wird der Microsoft-Routing- und Remotezugriffsserver (RRAS) zur Beschreibung des VPN-Konfigurationsvorgangs verwendet.

Wenn Sie die VPN-Lösung eines Drittanbieters nutzen, greifen Sie auf dessen Dokumentation zurück, um zu erfahren, wie Sie die RADIUS-Kontoführung aktivieren.

## <a name="configure-radius-accounting-on-the-vpn-system"></a>Konfigurieren der RADIUS-Kontoführung auf dem VPN-System

Führen Sie auf Ihrem RRAS-Server die folgenden Schritte aus.
 
1.  Öffnen Sie die Routing- und Remotezugriffs-Konsole.
2.  Klicken Sie mit der rechten Maustaste auf den Server, und klicken Sie anschließend auf **Eigenschaften**.
3.  Wählen Sie unter **Kontoführungsanbieter** in der Registerkarte **Sicherheit** **RADIUS-Kontoführung** aus, und klicken Sie auf **Konfigurieren**.

    ![RADIUS-Setup](./media/radius-setup.png)

4.  Tippen Sie im Fenster **RADIUS-Server hinzufügen** den **Servernamen** des nächsten ATA-Gateways oder ATA-Lightweight-Gateways ein. Stellen Sie unter **Port** sicher, dass die Standardeinstellung 1813 konfiguriert ist. Klicken Sie auf **Ändern**, und tippen Sie eine neue, geheime Zeichenfolge von alphanumerischen Zeichen an, die Sie sich merken können, da Sie sie im weiteren Verlauf Ihrer ATA-Konfiguration eingeben müssen. Prüfen Sie das Feld **Send RADIUS Account On and Accounting Off messages** („RADIUS-Kontoführung aktiviert“- und „RADIUS-Kontoführung deaktiviert“-Nachrichten senden), und klicken Sie anschließend in allen geöffneten Dialogfeldern auf **OK**.
 
     ![VPN-Setup](./media/vpn-set-accounting.png)
     
### <a name="configure-vpn-in-ata"></a>Konfigurieren von VPN in ATA

ATA sammelt VPN-Daten und erkennt, wann und wo Anmeldeinformationen über VPN verwendet werden, und bezieht diese Daten in Ihre Untersuchung ein. Dies bietet zusätzliche Informationen, die Ihnen bei der Suche von Warnungen helfen, die von ATA gemeldet werden.

So konfigurieren Sie VPN-Daten in ATA

1. Öffnen Sie in der ATA-Konsole die ATA-Konfigurationsseite, und gehen Sie auf **VPN**.
 
   ![ATA-Konfigurationsmenü](./media/config-menu.png)

2. Aktivieren Sie die **RADIUS-Kontoführung**, und geben Sie das **gemeinsame Geheimnis** ein, das Sie zuvor auf Ihrem RRAS-VPN-Server konfiguriert haben. Klicken Sie dann auf **Save** (Speichern).
 

  ![Konfigurieren des ATA-VPN](./media/vpn.png)


Nachdem Sie diese Option aktiviert haben, lauschen alle ATA-Gateways und ATA-Lightweight-Gateways an Port 1813 für RADIUS-Buchhaltungsereignisse. 

Ihr Setup ist nun vollständig, und Sie sehen jetzt die VPN-Aktivität auf der Profilseite des Benutzers:
 
   ![VPN-Setup](./media/vpn-user.png)

Nachdem das ATA-Gateway die VPN-Ereignisse empfängt und zur Verarbeitung an das ATA Center sendet, benötigt ATA Center Zugriff über HTTPS (Port 443) auf *ti.ata.azure.com*, um die externen IP-Adressen in den VPN-Ereignissen an ihrem jeweiligen geografischen Standorten aufzulösen.




> [!div class="step-by-step"]
> [« Schritt 6](install-ata-step5.md)
> [Schritt 8 »](install-ata-step7.md)



## <a name="related-videos"></a>Verwandte Videos
- [Übersicht über die ATA-Bereitstellung](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Auswählen des richtigen ATA-Gatewaytyps](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Weitere Informationen
- [Handbuch für die ATA POC-Bereitstellung](http://aka.ms/atapoc)
- [Tool zur Bemessung von ATA-Gateways](http://aka.ms/aatpsizingtool)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Voraussetzungen für ATA](ata-prerequisites.md)

