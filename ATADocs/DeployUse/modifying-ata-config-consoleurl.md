---
title: "Ändern der ATA-Konfiguration – IP-Adresse der ATA-Konsole | Microsoft Advanced Threat Analytics"
description: "Beschreibt, wie die IP-Adresse der ATA-Konsole geändert wird, über die eine Verknüpfung mit der ATA-Konsole auf den ATA-Gateways erstellt wird."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: stevenpo
ms.date: 11/29/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 50118465-df34-4e04-b0cc-48808b6a96b1
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: bc7af91a925928183d179391f15d3a24cda2b576
ms.openlocfilehash: 8f816c8eda0a1b11a42314a18b1c8c39ac6a7ba8


---

*Gilt für: Advanced Threat Analytics Version 1.7*



# <a name="change-ata-configuration---ata-console-url"></a>Ändern der ATA-Konfiguration – URL der ATA-Konsole

>[!div class="step-by-step"]
[« Zertifikat für ATA Center](modifying-ata-config-centercert.md)
[Domänenverbindungskennwort »](modifying-ata-config-dcpassword.md)

## <a name="change-the-ata-console-url"></a>Ändern der URL der ATA-Konsole
Standardmäßig ist die URL der ATA-Konsole die IP-Adresse, die Sie beim Installieren von ATA Center als IP-Adresse der ATA-Konsole ausgewählt haben.

Die URL wird in den folgenden Szenarios verwendet:

-   Installation von ATA-Gateways: Wenn ein ATA-Gateway installiert wird, registriert es sich bei ATA Center. Diese Registrierung erfolgt durch Herstellen einer Verbindung mit der ATA-Konsole. Wenn Sie einen vollqualifizierten Domänennamen (FQDN) für die URL der ATA-Konsole eingeben, müssen Sie sicherstellen, dass das ATA-Gateway den FQDN in die IP-Adresse auflösen kann, an die die ATA-Konsole gebunden ist.

-   Warnungen: Wenn ATA eine SIEM- oder E-Mail-Warnung sendet, enthält diese einen Link zur jeweiligen verdächtigen Aktivität. Dabei bildet die URL der ATA-Konsole den Hostteil des Links.

-   Wenn Sie ein Zertifikat von Ihrer internen Zertifizierungsstelle installiert haben, empfiehlt es sich, die URL mit dem Antragstellernamen im Zertifikat anzugleichen, sodass Benutzer beim Herstellen einer Verbindung mit der ATA-Konsole keine Warnmeldung erhalten.

-   Durch die Verwendung eines FQDN für die URL der ATA-Konsole können Sie die von der ATA-Konsole verwendete IP-Adresse ändern, ohne dass Warnungen, die in der Vergangenheit gesendet wurden, ungültig werden oder ohne das ATA-Gateway-Setuppaket erneut herunterladen zu müssen. Sie müssen lediglich den DNS mit der neuen IP-Adresse aktualisieren.

> [!NOTE]
> Nach dem Ändern der URL der ATA-Konsole sollten Sie vor der Installation neuer ATA-Gateways das ATA-Gateway-Setuppaket herunterladen.

Führen Sie zum Ändern der URL für die ATA-Konsole die folgenden Schritte auf dem ATA Center-Server aus.

1.  Öffnen Sie die ATA-Konsole.

2.  Wählen Sie auf der Symbolleiste die Einstellungsoption und dann **Konfiguration** aus.

    ![Symbol der ATA-Konfigurationseinstellungen](media/ATA-config-icon.JPG)

3.  Wählen Sie **Center** aus.

4.  Wählen Sie unter **IP-Adresse für Konsole** eine der vorhandenen IP-Adressen aus.

5.  Ändern Sie unter **Konsolen-URL** die URL nach Bedarf.

    ![URL der ATA-Konsole](media/ATA-chge-center-URL.png)
> [!NOTE]
> Am Ende der URL darf kein Schrägstrich (/) enthalten sein.

6.  Klicken Sie auf **Speichern**.

>[!div class="step-by-step"]
[« Zertifikat für ATA Center](modifying-ata-config-centercert.md)
[Domänenverbindungskennwort »](modifying-ata-config-dcpassword.md)


## <a name="see-also"></a>Siehe auch
- [Arbeiten mit der ATA-Konsole](working-with-ata-console.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://aka.ms/ata-forum)



<!--HONumber=Nov16_HO5-->


