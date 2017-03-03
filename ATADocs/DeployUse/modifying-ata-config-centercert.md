---
title: "Ändern der Advanced Threat Analytics-Konfiguration – Zertifikat für Center | Microsoft-Dokumentation"
description: Beschreibt den zweistufigen Vorgang zum Erneuern oder Ersetzen des Zertifikats im lokalen Computerspeicher auf dem ATA Center-Server.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 1/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: c8855287-de3b-4cdd-be8f-2128f48a6f27
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b28cb3a0da844b7c460c03726222bc775a9e47da
ms.openlocfilehash: 9d3e4a76c37fcd3cd90afe068e904e64cd9f45b0


---

*Gilt für: Advanced Threat Analytics Version 1.7*



# <a name="change-ata-configuration---ata-center-certificate"></a>Ändern der ATA-Konfiguration – Zertifikat für ATA Center

>[!div class="step-by-step"]
[« IP-Adresse von ATA Center](modifying-ata-config-centerip.md)
[URL der ATA-Konsole »](modifying-ata-config-consoleurl.md)

## <a name="change-the-ata-center-certificate"></a>Ändern des Zertifikats für ATA Center
Wenn Ihr Zertifikate bald abläuft und nach dem Installieren des neuen Zertifikats im lokalen Computerspeicher auf dem ATA Center-Server erneuert oder ersetzt werden muss, können Sie das Zertifikat in einem zweistufigen Vorgang ersetzen:

-   Erste Stufe: Aktualisieren Sie das Zertifikat, das vom ATA Center-Dienst verwendet werden soll. Zu diesem Zeitpunkt ist der ATA Center-Dienst noch an das ursprüngliche Zertifikat gebunden. Beim Synchronisieren der Konfiguration der ATA-Gateways sind zwei mögliche Zertifikate vorhanden, die für die gegenseitige Authentifizierung gültig sind. Solange ein ATA-Gateway eine Verbindung über das ursprüngliche Zertifikat herstellen kann, wird das neue Zertifikat nicht verwendet.

-   Zweite Stufe: Nachdem alle ATA-Gateways mit der aktualisierten Konfiguration synchronisiert wurden, können Sie das neue Zertifikat aktivieren, an das der ATA Center-Dienst gebunden ist. Wenn Sie das neue Zertifikat aktivieren, wird der ATA Center-Dienst an das Zertifikat gebunden. Die ATA-Gateways können den ATA Center-Dienst nicht ordnungsgemäß gegenseitig authentifizieren und versuchen, das zweite Zertifikat zu authentifizieren. Nach dem Herstellen der Verbindung mit dem ATA Center-Dienst ruft das ATA-Gateway die neueste Konfiguration ab und verfügt über ein einzelnes Zertifikat für ATA Center. (Dies gilt, bis Sie den Vorgang erneut starten.)

> [!NOTE]
> -   Wenn ein ATA-Gateway während der ersten Stufe offline geschaltet war und die aktualisierte Konfiguration nicht abrufen konnte, müssen Sie die JSON-Konfigurationsdatei im ATA-Gateway manuell aktualisieren.
> -   Das verwendete Zertifikat muss von den ATA-Gateways als vertrauenswürdig eingestuft werden.
> -   Das Zertifikat wird auch für die ATA-Konsole verwendet, deshalb sollte es der Adresse der ATA-Konsole entsprechen, um Browserwarnungen zu vermeiden.
> -   Wenn Sie nach dem Aktivieren des neuen Zertifikats ein neues ATA-Gateway bereitstellen möchten, müssen Sie das ATA-Gateway-Setuppaket erneut herunterladen.

1.  Öffnen Sie die ATA-Konsole.

2.  Wählen Sie auf der Symbolleiste die Einstellungsoption und dann **Konfiguration** aus.

    ![Symbol der ATA-Konfigurationseinstellungen](media/ATA-config-icon.JPG)

3.  Wählen Sie **Center** aus.

4.  Wählen Sie unter **Zertifikat** eines der Zertifikate in der Liste aus.

5.  Klicken Sie auf **Speichern**.

6.  Daraufhin wird eine Benachrichtigung über die Anzahl der ATA-Gateways angezeigt, die mit der neuesten Konfiguration synchronisiert wurden.

7.  Nachdem alle ATA-Gateways synchronisiert wurden, klicken Sie auf **Aktivieren**, um das neue Zertifikat zu aktivieren.
    >[!IMPORTANT]
    >Bevor Sie die neue Konfiguration aktivieren, vergewissern Sie sich, dass alle ATA-Gateways mit der neuesten Konfiguration synchronisiert sind. Wird die neue Konfiguration aktiviert, bevor alle ATA-Gateways synchronisiert sind, kann es passieren, dass die ATA-Gateway nicht mehr ordnungsgemäß funktionieren. Ist mindestens eines der ATA-Gateways nicht synchronisiert, erhalten Sie diesen Fehler, wenn Sie auf „Aktivieren“ klicken:
    >
    >    ![Synchronisierungsfehler bei ATA-Gateways](media/ataGW-not-synced.png)

8.  Stellen Sie sicher, dass die Konfiguration aller ATA-Gateways nach Aktivierung der Änderung synchronisiert werden kann.

>[!div class="step-by-step"]
[« IP-Adresse von ATA Center](modifying-ata-config-centerip.md)
[URL der ATA-Konsole »](modifying-ata-config-consoleurl.md)

## <a name="see-also"></a>Weitere Informationen
- [Arbeiten mit der ATA-Konsole](working-with-ata-console.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://aka.ms/ata-forum)



<!--HONumber=Feb17_HO1-->


