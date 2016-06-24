---
# required metadata

title: Arbeiten mit ATA-Erkennungseinstellungen | Microsoft Advanced Threat Analytics
description: Beschreibt, wie Sie eine Liste von IP-Adressen und Subnetzen konfigurieren, bei denen ungewöhnliche Umstände vorliegen und die anders als andere Entitäten in Ihrem Netzwerk behandelt werden sollen.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: f4f2ae30-4849-4a4f-8f6d-bfe99a32c746

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Arbeiten mit ATA-Erkennungseinstellungen
Auf der Konfigurationsseite **Erkennung** können Sie eine Liste von IP-Adressen und Subnetzen festlegen, bei denen ungewöhnliche Umstände vorliegen und die etwas anders als andere Entitäten in Ihrem Netzwerk behandelt werden sollen.

## Einrichten der Erkennung
Auf der Seite **Erkennung** können Sie die folgenden Elemente definieren:

-   **Subnetze mit kurzer Leasedauer:** Wenn Ihre Organisation über Subnetze verfügt, in denen die IP-Adressen nur sehr kurzzeitig zugewiesen werden, z. B. VPN-IP-Adresssubnetze oder WLAN-Subnetze, ist es wichtig, diese IP-Adressen und Subnetze in ATA einzugeben. Auf diese Weise weiß ATA, dass es die Zuordnung zwischen einem Computer und einer IP-Adresse aus diesen Bereichen für einen kürzeren Zeitraum als für andere IP-Adressen speichern muss.

-   **Honeytoken-Konto-SIDs:** ein Benutzerkonto, für das keine Netzwerkaktivitäten vorhanden sein sollten. Dieses Konto wird als ATA-Honeytoken-Benutzer konfiguriert. Wenn jemand dieses Benutzerkonto verwendet, erstellt ATA eine verdächtige Aktivität. Darüber hinaus weist dies auf schädliche Aktivitäten hin. Zum Konfigurieren des Honeytoken-Benutzers benötigen Sie die SID des Benutzerkontos und nicht den Benutzernamen.

Sie können IP-Adressen aus den folgenden Erkennungen ausschließen. Wenn Sie eine IP-Adresse in eine dieser Listen eingeben, schließt ATA die IP-Adresse aus diesem spezifischen Typ von erkannter Aktivität aus.

-   IP-Adressausschlüsse bei DNS-Reconnaissance

-   IP-Adressausschlüsse bei Pass-the-Ticket

## Siehe auch
- [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md)
- [Ändern der ATA-Konfiguration](modifying-ata-configuration.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


