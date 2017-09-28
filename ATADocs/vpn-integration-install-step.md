---
title: "Installieren von Advanced Threat Analytics – Schritt 7 | Microsoft-Dokumentation"
description: In diesem Schritt bei der ATA-Installation integrieren Sie Ihr VPN.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 09/19/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e0aed853-ba52-46e1-9c55-b336271a68e7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 384384ebd6b6fadcaa5636200ccd08667d9c41a5
ms.sourcegitcommit: 34c3d6f56f175994b672842c7576040956ceea69
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/19/2017
---
*Gilt für: Advanced Threat Analytics Version 1.8*



# <a name="install-ata---step-7"></a>Installieren von ATA – Schritt 7

>[!div class="step-by-step"]
[« Schritt 5](install-ata-step5.md)
[Schritt 8 »](install-ata-step7.md)

## <a name="step-7-integrate-vpn"></a>Schritt 7: Integrieren des VPN

### <a name="configuring-vpn"></a>Konfigurieren des VPN

ATA erfasst VPN-Daten zur Erstellung von Profilen der Standorte, über die Computer eine Verbindung mit dem Netzwerk herstellen und mit denen diese ungewöhnliche VPN-Verbindungen erkennen können.

So konfigurieren Sie VPN-Daten in ATA

1. Wechseln Sie zu **Konfiguration**, und klicken Sie dann auf die Registerkarte **VPN**.

2. Geben Sie einen Wert für **Gemeinsames Geheimnis** für das Konto Ihres RADIUS-Servers ein. Das gemeinsame Geheimnis finden Sie in der VPN-Dokumentation.

 ![Konfigurieren des ATA-VPN](media/vpn.png)

3.  Nachdem Sie diese Option aktiviert haben, hören alle ATA-Gateways und Lightweight-Gateways Port 1813 auf RADIUS-Buchhaltungsereignisse ab. 

4.  Nach Abschluss dieser Konfiguration sollten die RADIUS-Buchhaltungsereignisse des VPN an ATA-Gateways oder ATA-Lightweight-Gateways weitergeleitet werden.

5.  Nachdem das ATA-Gateway die VPN-Ereignisse empfängt und zur Verarbeitung an das ATA Center sendet, benötigt ATA Center Internetkonnektivität für HTTPS-Port 443, um die externen IP-Adressen in den VPN-Ereignissen an ihren jeweiligen geografischen Standorten aufzulösen.

Der Aufruf zum Auflösen einer externen IP-Adresse an einem Standort ist anonym. In diesem Aufruf wird kein persönlicher Bezeichner gesendet.

Die unterstützten VPN-Lieferanten sind folgende:
- Microsoft
- F5
- Check Point
- Cisco ASA




>[!div class="step-by-step"]
[« Schritt 6](install-ata-step5.md)
[Schritt 8 »](install-ata-step7.md)



## <a name="related-videos"></a>Verwandte Videos
- [Auswählen des richtigen ATA-Gatewaytyps](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Siehe auch
- [Handbuch für die ATA POC-Bereitstellung](http://aka.ms/atapoc)
- [Tool zur Bemessung von ATA-Gateways](http://aka.ms/atasizingtool)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Voraussetzungen für ATA](ata-prerequisites.md)

