---
# required metadata

title: Ändern der ATA-Konfiguration – Domänenverbindungskennwort | Microsoft Advanced Threat Analytics
description: Beschreibt, wie das Domänenverbindungskennwort auf dem ATA-Gateway geändert wird.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Ändern der ATA-Konfiguration – Domänenverbindungskennwort

>[!div class="step-by-step"]
[« IIS-Zertifikat](modifying-ata-config-iiscert.md)
[Name des Netzwerkadapters für die Erfassung »](modifying-ata-config-nicname.md)

## Ändern des Domänenverbindungskennworts
Wenn Sie Domänenverbindungskennwort ändern, stellen Sie sicher, dass das eingegebene Kennwort korrekt ist. Andernfalls wird der ATA-Dienst auf den ATA-Gateways nicht mehr ausgeführt.

Wenn Sie vermuten, dass dies der Fall ist, prüfen Sie, ob auf dem ATA-Gateway in der Datei „Microsoft.Tri.Gateway-Errors.log“ der folgende Eintrag vorhanden ist:
`The supplied credential is invalid.`

Um dies zu korrigieren, führen Sie die folgenden Schritte zum Ändern des Domänenverbindungskennworts auf dem ATA-Gateway aus:

1.  Öffnen Sie die ATA-Konsole auf dem ATA-Gateway.

2.  Wählen Sie auf der Symbolleiste die Einstellungsoption und dann **Konfiguration** aus.

    ![Symbol der ATA-Konfigurationseinstellungen](media/ATA-config-icon.JPG)

3.  Wählen Sie **ATA-Gateways** aus.

    ![Abbildung – Ändern des Kennworts für ATA-Gateway](media/ATA-GW-change-DC-password.JPG)

4.  Ändern Sie unter **Domänenverbindungseinstellungen** das Kennwort.

5.  Klicken Sie auf **Speichern**.

6.  Überprüfen Sie nach dem Ändern des Kennworts, ob der ATA-Gatewaydienst auf den ATA-Gatewayservern ausgeführt wird.

>[!div class="step-by-step"]
[« IIS-Zertifikat](modifying-ata-config-iiscert.md)
[Name des Netzwerkadapters für die Erfassung »](modifying-ata-config-nicname.md)

## Siehe auch
- [Arbeiten mit der ATA-Konsole](/advanced-threat-analytics/understand/working-with-ata-console)
- [Installieren von ATA](install-ata.md)
- [Unterstützung finden Sie in unserem Forum.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


