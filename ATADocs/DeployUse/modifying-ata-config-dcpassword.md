---
title: "Ändern der ATA-Konfiguration – Domänenverbindungskennwort | Microsoft ATA"
description: "Beschreibt, wie das Domänenverbindungskennwort auf dem ATA-Gateway geändert wird."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: 7b8904bcb379004b2038e6b9a14c87c3914f1e1f


---

# Ändern der ATA-Konfiguration – Domänenverbindungskennwort

>[!div class="step-by-step"]
[« IIS-Zertifikat](modifying-ata-config-iiscert.md)


## Ändern des Domänenverbindungskennworts
Wenn Sie das Domänenverbindungskennwort ändern, stellen Sie sicher, dass das eingegebene Kennwort korrekt ist. Andernfalls wird der ATA-Gateway-Dienst auf den ATA-Gateways nicht mehr ausgeführt.

Wenn Sie vermuten, dass dies der Fall ist, prüfen Sie, ob auf dem ATA-Gateway in der Datei „Microsoft.Tri.Gateway-Errors.log“ der folgende Eintrag vorhanden ist:
`The supplied credential is invalid.`

Um dies zu korrigieren, führen Sie die folgenden Schritte zum Ändern des Domänenverbindungskennworts auf dem ATA-Gateway aus:

1.  Öffnen Sie die ATA-Konsole auf dem ATA-Gateway.

2.  Wählen Sie auf der Symbolleiste die Einstellungsoption und dann **Konfiguration** aus.

    ![Symbol der ATA-Konfigurationseinstellungen](media/ATA-config-icon.JPG)

3.  Wählen Sie **Allgemein** aus.

    ![Abbildung – Ändern des Kennworts für ATA-Gateway](media/ATA-GW-change-DC-password.JPG)

4.  Unter Sie unter **Allgemein** das Kennwort.

5.  Klicken Sie auf **Speichern**.

6.  Überprüfen Sie nach dem Ändern des Kennworts, ob der ATA-Gatewaydienst auf den ATA-Gatewayservern ausgeführt wird.

>[!div class="step-by-step"]
[« IIS-Zertifikat](modifying-ata-config-iiscert.md)

## Weitere Informationen
- [Arbeiten mit der ATA-Konsole](working-with-ata-console.md)
- [Installieren von ATA](install-ata.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO4-->


