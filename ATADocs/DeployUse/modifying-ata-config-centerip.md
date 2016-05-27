---
# required metadata

title: Ändern der ATA-Konfiguration – IP-Adresse für ATA Center | Microsoft Advanced Threat Analytics
description: Beschreibt, wie die IP-Adresse, der Port oder das Zertifikat für ATA Center geändert werden.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 93b27f15-f7e5-49bb-870a-d81d09dfe9fc

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Ändern der ATA-Konfiguration – IP-Adresse für ATA Center

>[!div class="step-by-step"]
[Zertifikat für ATA Center »](modifying-ata-config-centercert.md)

Nach der ersten Bereitstellung sollten Änderungen an ATA Center vorsichtig vorgenommen werden. Gehen Sie wie folgt vor, wenn Sie die IP-Adresse und den Port oder das Zertifikat ändern.

## Ändern der vom ATA Center-Server verwendeten IP-Adresse
Berücksichtigen Sie beim Ändern der IP-Adresse und des Ports oder des Zertifikats für ATA Center die folgenden Punkte.

Die ATA-Gateways speichern die IP-Adresse der ATA Center-Instanz, mit der eine Verbindung hergestellt werden soll, lokal. Sie stellen in regelmäßigen Abständen eine Verbindung mit ATA Center her und rufen Konfigurationsänderungen ab. Änderungen im Hinblick auf die Herstellung der Verbindung mit ATA Center über die ATA-Gateways werden in zwei Stufen vorgenommen.

-   Erste Stufe: Aktualisieren Sie die IP-Adresse und den Port, die vom ATA Center-Dienst verwendet werden sollen. Zu diesem Zeitpunkt lauscht ATA Center noch auf die ursprüngliche IP-Adresse. Bei der nächsten Synchronisierung der Konfiguration des ATA-Gateways sind daher zwei IP-Adressen für ATA Center vorhanden. Solange das ATA-Gateway eine Verbindung über die ursprüngliche (erste) IP-Adresse herstellen kann, werden die neue IP-Adresse und der neue Port nicht verwendet.

-   Zweite Stufe: Nachdem alle ATA-Gateways mit der aktualisierten Konfiguration synchronisiert wurden, können Sie die neue IP-Adresse und den neuen Port aktivieren, auf die der ATA Center-Dienst lauscht. Wenn Sie die neue IP-Adresse aktivieren, wird der ATA Center-Dienst an die neue IP-Adresse gebunden. Die ATA-Gateways können keine Verbindung mit der ursprünglichen IP-Adresse herstellen und versuchen nun, eine Verbindung mit der zweiten (neuen) IP-Adresse für ATA Center herzustellen. Nach dem Herstellen der Verbindung mit dem ATA Center-Dienst über die neue IP-Adresse ruft das ATA-Gateway die neueste Konfiguration ab und verfügt über eine einzelne IP-Adresse für ATA Center. (Dies gilt, bis Sie den Vorgang erneut starten.)

> [!NOTE]
> -   Wenn ein ATA-Gateway während der ersten Stufe offline geschaltet war und die aktualisierte Konfiguration nicht abrufen konnte, müssen Sie die JSON-Konfigurationsdatei im ATA-Gateway manuell aktualisieren.
> -   Wenn die neue IP-Adresse auf dem ATA Center-Server installiert ist, können Sie sie beim Vornehmen der Änderung in der Liste der IP-Adressen auswählen. Wenn Sie die IP-Adresse jedoch aus bestimmten Gründen nicht auf dem ATA Center-Server installieren können, müssen Sie die benutzerdefinierte IP-Adresse manuell auswählen und hinzufügen. Sie können die neue IP-Adresse erst aktivieren, wenn sie auf dem Server installiert ist.
> -   Wenn Sie nach dem Aktivieren der neuen IP-Adresse ein neues ATA-Gateway bereitstellen möchten, müssen Sie das ATA-Gateway-Setuppaket erneut herunterladen.

1.  Öffnen Sie die ATA-Konsole.

2.  Wählen Sie auf der Symbolleiste die Einstellungsoption aus, und wählen Sie **Konfiguration** aus..

    ![Symbol der ATA-Konfigurationseinstellungen](media/ATA-config-icon.JPG)

3.  Wählen Sie **Allgemein** aus..

4.  Wählen Sie unter **ATA Center-Dienst – IP-Adresse: Port** eine der vorhandenen IP-Adressen aus, oder wählen Sie **Benutzerdefinierte IP-Adresse hinzufügen** aus, und geben Sie eine IP-Adresse ein.

5.  Klicken Sie auf **Speichern**..

6.  Daraufhin wird eine Benachrichtigung über die Anzahl der ATA-Gateways angezeigt, die mit der neuesten Konfiguration synchronisiert wurden.

    ![Abbildung – synchronisierte ATA Center-Gateways](media/ATA-chge-IP-after-clicking-save.png)

    >[!IMPORTANT]
    >Bevor Sie die neue Konfiguration aktivieren, vergewissern Sie sich, dass alle ATA-Gateways mit der neuesten Konfiguration synchronisiert sind. Wird die neue Konfiguration aktiviert, bevor alle ATA-Gateways synchronisiert sind, kann es passieren, dass die ATA-Gateway nicht mehr ordnungsgemäß funktionieren. Ist mindestens eines der ATA-Gateways nicht synchronisiert, erhalten Sie diesen Fehler, wenn Sie auf „Aktivieren“ klicken:
    >
    >    ![Synchronisierungsfehler bei ATA-Gateways](media/ataGW-not-synced.png)


7.  Nachdem alle ATA-Gateways synchronisiert wurden, klicken Sie auf **Aktivieren**, um die neue IP-Adresse zu aktivieren.

    > [!NOTE]
    > Wenn Sie eine benutzerdefinierte IP-Adresse eingegeben haben, können Sie erst auf **Aktivieren** klicken, nachdem die IP-Adresse auf dem ATA Center-Server installiert wurde.

8.  Stellen Sie sicher, dass die Konfiguration aller ATA-Gateways nach Aktivierung der Änderung synchronisiert werden kann. Auf der Benachrichtigungsleiste wird angegeben, bei wie vielen ATA-Gateways die Konfiguration erfolgreich synchronisiert wurde.

>[!div class="step-by-step"]
[Ändern des Zertifikats für ATA Center »](modifying-ata-config-centercert.md)


## Siehe auch
- [Arbeiten mit der ATA-Konsole](working-with-ata-console.md)
- [Installieren von ATA](install-ata.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


