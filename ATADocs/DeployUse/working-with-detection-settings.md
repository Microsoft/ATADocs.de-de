---
title: Festlegen der Advanced Threat Analytics-Erkennungseinstellungen | Microsoft-Dokumentation
description: "Beschreibt, wie Sie eine Liste von IP-Adressen und Subnetzen konfigurieren, bei denen ungewöhnliche Umstände vorliegen und die anders als andere Entitäten in Ihrem Netzwerk behandelt werden sollen."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: f4f2ae30-4849-4a4f-8f6d-bfe99a32c746
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b28cb3a0da844b7c460c03726222bc775a9e47da
ms.openlocfilehash: c88d74793c6210704f2a187df6508bf525907118


---

*Gilt für: Advanced Threat Analytics Version 1.7*



# <a name="working-with-ata-detection-settings"></a>Arbeiten mit ATA-Erkennungseinstellungen
Auf der Konfigurationsseite **Erkennung** können Sie eine Liste von IP-Adressen und Subnetzen festlegen, bei denen ungewöhnliche Umstände vorliegen und die etwas anders als andere Entitäten in Ihrem Netzwerk behandelt werden sollen.

## <a name="setting-up-detection"></a>Einrichten der Erkennung
Im Bereich **Erkennung** können Sie die folgenden Elemente definieren:

-   **Honeytoken-Konto-SIDs:** ein Benutzerkonto, für das keine Netzwerkaktivitäten vorhanden sein sollten. Dieses Konto wird als ATA-Honeytoken-Benutzer konfiguriert. Wenn jemand dieses Benutzerkonto verwendet, erstellt ATA eine verdächtige Aktivität. Darüber hinaus weist dies auf schädliche Aktivitäten hin. Zum Konfigurieren des Honeytoken-Benutzers benötigen Sie die SID des Benutzerkontos und nicht den Benutzernamen.

>[!NOTE]
> Sie finden die SID des Benutzers auf der Registerkarte *Kontoinformationen* des Benutzerprofils in der ATA-Konsole.


![ATA detection settings honeytoken](media/ata-detection-settings-honeytoken-1.7.png)


**Ausnahmen für die Erkennung:** Sie können IP-Adressen aus den folgenden Erkennungen ausschließen. Wenn Sie eine IP-Adresse in eine dieser Listen eingeben, schließt ATA die IP-Adresse aus diesem spezifischen Typ von erkannter Aktivität aus.

-   IP-Adressausschlüsse bei DNS-Reconnaissance

-   IP-Adressausschlüsse bei Pass-the-Ticket

![ATA detection settings exclusions](media/ata-detection-settings-exclusions-1.7.png)


## <a name="see-also"></a>Siehe auch
- [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md)
- [Ändern der ATA-Konfiguration](modifying-ata-configuration.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Feb17_HO1-->


