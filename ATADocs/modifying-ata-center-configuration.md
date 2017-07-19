---
title: "Ändern der ATA Center-Konfiguration von Advanced Threat Analytics | Microsoft-Dokumentation"
description: "Beschreibt, wie die IP-Adresse, der Port, die URL der Konsole oder das Zertifikat für ATA Center geändert werden."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 93b27f15-f7e5-49bb-870a-d81d09dfe9fc
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1e9fa2d104c52087746e7c03fea27e3cb596adf0
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/30/2017
---
*Gilt für: Advanced Threat Analytics Version 1.8*



# <a name="modifying-the-ata-center-configuration"></a>Bearbeiten der ATA Center-Konfiguration


Nach der ersten Bereitstellung sollten Änderungen an ATA Center vorsichtig vorgenommen werden. Gehen Sie wie folgt vor, wenn Sie die IP-Adresse und den Port, die URL der Konsole oder das Zertifikat ändern.

## <a name="the-ata-center-ip-address"></a>Die IP-Adresse von ATA-Center

Die ATA-Gateways speichern die IP-Adresse der ATA Center-Instanz, mit der eine Verbindung hergestellt werden soll, lokal. Sie stellen in regelmäßigen Abständen eine Verbindung mit ATA Center her und rufen Konfigurationsänderungen ab. Änderungen im Hinblick auf die Herstellung der Verbindung mit ATA Center über die ATA-Gateways werden in zwei Stufen vorgenommen.

-   Erste Stufe: Aktualisieren Sie die IP-Adresse und den Port, die vom ATA Center-Dienst verwendet werden sollen. Zu diesem Zeitpunkt lauscht ATA Center noch auf die ursprüngliche IP-Adresse. Bei der nächsten Synchronisierung der Konfiguration des ATA-Gateways sind daher zwei IP-Adressen für ATA Center vorhanden. Solange das ATA-Gateway eine Verbindung über die ursprüngliche (erste) IP-Adresse herstellen kann, werden die neue IP-Adresse und der neue Port nicht verwendet.

-   Zweite Stufe: Nachdem alle ATA-Gateways mit der aktualisierten Konfiguration synchronisiert wurden, können Sie die neue IP-Adresse und den neuen Port aktivieren, auf die der ATA Center-Dienst lauscht. Wenn Sie die neue IP-Adresse aktivieren, wird der ATA Center-Dienst an die neue IP-Adresse gebunden. Die ATA-Gateways können keine Verbindung mit der ursprünglichen IP-Adresse herstellen und versuchen nun, eine Verbindung mit der zweiten (neuen) IP-Adresse für ATA Center herzustellen. Nach dem Herstellen der Verbindung mit dem ATA Center-Dienst über die neue IP-Adresse ruft das ATA-Gateway die neueste Konfiguration ab und verfügt über eine einzelne IP-Adresse für ATA Center. (Dies gilt, bis Sie den Vorgang erneut starten.)

> [!NOTE]
> -   Wenn ein ATA-Gateway während der ersten Stufe offline geschaltet war und die aktualisierte Konfiguration nicht abrufen konnte, müssen Sie die JSON-Konfigurationsdatei im ATA-Gateway manuell aktualisieren.
> -   Wenn die neue IP-Adresse auf dem ATA Center-Server installiert ist, können Sie sie beim Vornehmen der Änderung in der Liste der IP-Adressen auswählen. Wenn Sie die IP-Adresse jedoch aus bestimmten Gründen nicht auf dem ATA Center-Server installieren können, müssen Sie die benutzerdefinierte IP-Adresse manuell auswählen und hinzufügen. Sie können die neue IP-Adresse erst aktivieren, wenn sie auf dem Server installiert ist.
> -   Wenn Sie nach dem Aktivieren der neuen IP-Adresse ein neues ATA-Gateway bereitstellen möchten, müssen Sie das ATA-Gateway-Setuppaket erneut herunterladen.

## <a name="the-console-url"></a>URL der ATA-Konsole

Die URL wird in den folgenden Szenarios verwendet:

-   Installation von ATA-Gateways: Wenn ein ATA-Gateway installiert wird, registriert es sich bei ATA Center. Diese Registrierung erfolgt durch Herstellen einer Verbindung mit der ATA-Konsole. Wenn Sie einen vollqualifizierten Domänennamen (FQDN) für die URL der ATA-Konsole eingeben, müssen Sie sicherstellen, dass das ATA-Gateway den FQDN in die IP-Adresse auflösen kann, an die die ATA-Konsole gebunden ist.

-   Warnungen: Wenn ATA eine SIEM- oder E-Mail-Warnung sendet, enthält diese einen Link zur jeweiligen verdächtigen Aktivität. Dabei bildet die URL der ATA-Konsole den Hostteil des Links.

-   Wenn Sie ein Zertifikat von Ihrer internen Zertifizierungsstelle installiert haben, empfiehlt es sich, die URL mit dem Antragstellernamen im Zertifikat anzugleichen, sodass Benutzer beim Herstellen einer Verbindung mit der ATA-Konsole keine Warnmeldung erhalten.

-   Durch die Verwendung eines FQDN für die URL der ATA-Konsole können Sie die von der ATA-Konsole verwendete IP-Adresse ändern, ohne dass Warnungen, die in der Vergangenheit gesendet wurden, ungültig werden oder ohne das ATA-Gateway-Setuppaket erneut herunterladen zu müssen. Sie müssen lediglich den DNS mit der neuen IP-Adresse aktualisieren.

> [!NOTE]
> Nach dem Ändern der URL der ATA-Konsole sollten Sie vor der Installation neuer ATA-Gateways das ATA-Gateway-Setuppaket herunterladen.

## <a name="the-ata-center-certificate"></a>Zertifikat für ATA Center
Wenn Ihr Zertifikate bald abläuft und nach dem Installieren des neuen Zertifikats im lokalen Computerspeicher auf dem ATA Center-Server erneuert oder ersetzt werden muss, können Sie das Zertifikat in einem zweistufigen Vorgang ersetzen:

-   Erste Stufe: Aktualisieren Sie das Zertifikat, das vom ATA Center-Dienst verwendet werden soll. Zu diesem Zeitpunkt ist der ATA Center-Dienst noch an das ursprüngliche Zertifikat gebunden. Beim Synchronisieren der Konfiguration der ATA-Gateways sind zwei mögliche Zertifikate vorhanden, die für die gegenseitige Authentifizierung gültig sind. Solange ein ATA-Gateway eine Verbindung über das ursprüngliche Zertifikat herstellen kann, wird das neue Zertifikat nicht verwendet.

-   Zweite Stufe: Nachdem alle ATA-Gateways mit der aktualisierten Konfiguration synchronisiert wurden, können Sie das neue Zertifikat aktivieren, an das der ATA Center-Dienst gebunden ist. Wenn Sie das neue Zertifikat aktivieren, wird der ATA Center-Dienst an das Zertifikat gebunden. Die ATA-Gateways können den ATA Center-Dienst nicht ordnungsgemäß gegenseitig authentifizieren und versuchen, das zweite Zertifikat zu authentifizieren. Nach dem Herstellen der Verbindung mit dem ATA Center-Dienst ruft das ATA-Gateway die neueste Konfiguration ab und verfügt über ein einzelnes Zertifikat für ATA Center. (Dies gilt, bis Sie den Vorgang erneut starten.)

> [!NOTE]
> -   Wenn ein ATA-Gateway während der ersten Stufe offline geschaltet war und die aktualisierte Konfiguration nicht abrufen konnte, müssen Sie die JSON-Konfigurationsdatei im ATA-Gateway manuell aktualisieren.
> -   Das verwendete Zertifikat muss von den ATA-Gateways als vertrauenswürdig eingestuft werden.
> -   Das Zertifikat wird auch für die ATA-Konsole verwendet, deshalb sollte es der Adresse der ATA-Konsole entsprechen, um Browserwarnungen zu vermeiden.
> -   Wenn Sie nach dem Aktivieren des neuen Zertifikats ein neues ATA-Gateway bereitstellen möchten, müssen Sie das ATA-Gateway-Setuppaket erneut herunterladen.

## <a name="changing-the-ata-center-configuration"></a>Ändern der ATA Center-Konfiguration

1.  Öffnen Sie die ATA-Konsole.

2.  Wählen Sie auf der Symbolleiste die Einstellungsoption und dann **Konfiguration** aus.

    ![Symbol der ATA-Konfigurationseinstellungen](media/ATA-config-icon.png)

3.  Wählen Sie **Center** aus.

  ![Ändern der ATA-Konfiguration](media/change-center-config.png)

4.  Wählen Sie unter **URL** die Option **Add custom DNS name / IP address** (Benutzerdefinierten DNS-Namen/IP-Adresse hinzufügen) sowie die neue DNS- oder IP-Adresse aus. Wählen Sie alternativ unter **Zertifikat** das neue Zertifikat aus.

5.  Klicken Sie auf **Speichern**.

6.  Daraufhin wird eine Benachrichtigung über die Anzahl der ATA-Gateways angezeigt, die mit der neuesten Konfiguration synchronisiert wurden.

    >[!IMPORTANT]
    >Bevor Sie die neue Konfiguration aktivieren, vergewissern Sie sich, dass alle ATA-Gateways mit der neuesten Konfiguration synchronisiert sind. Wird die neue Konfiguration aktiviert, bevor alle ATA-Gateways synchronisiert sind, kann es passieren, dass die ATA-Gateway nicht mehr ordnungsgemäß funktionieren. Ist mindestens eines der ATA-Gateways nicht synchronisiert, erhalten Sie diesen Fehler, wenn Sie auf „Aktivieren“ klicken:


7.  Nachdem alle ATA-Gateways synchronisiert wurden, klicken Sie auf **Aktivieren**, um die neue IP-Adresse oder das Zertifikat zu aktivieren.

    > [!NOTE]
    > Wenn Sie eine benutzerdefinierte IP-Adresse eingegeben haben, können Sie erst auf **Aktivieren** klicken, nachdem die IP-Adresse auf dem ATA Center-Server installiert wurde.

8.  Stellen Sie sicher, dass die Konfiguration aller ATA-Gateways nach Aktivierung der Änderung synchronisiert werden kann. Auf der Benachrichtigungsleiste wird angegeben, bei wie vielen ATA-Gateways die Konfiguration erfolgreich synchronisiert wurde.




## <a name="see-also"></a>Siehe auch
- [Arbeiten mit der ATA-Konsole](working-with-ata-console.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://aka.ms/ata-forum)
