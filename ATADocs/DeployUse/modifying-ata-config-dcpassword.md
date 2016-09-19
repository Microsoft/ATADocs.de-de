---
title: "Ändern der ATA-Konfiguration – Domänenverbindungskennwort | Microsoft ATA"
description: "Beschreibt, wie das Domänenverbindungskennwort auf dem ATA-Gateway geändert wird."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 050f1ef0b39d69b64ede53243a7fa2d33d0e4813
ms.openlocfilehash: 7cee457a8959526b25a68c50efea2976bafbef75


---

*Gilt für: Advanced Threat Analytics Version 1.7*



# Ändern der ATA-Konfiguration – Domänenverbindungskennwort

>[!div class="step-by-step"]
[« URL der ATA-Konsole](modifying-ata-config-consoleurl.md)


## Ändern des Domänenverbindungskennworts
Wenn Sie das Domänenverbindungskennwort ändern, stellen Sie sicher, dass das eingegebene Kennwort korrekt ist. Andernfalls wird der ATA-Gateway-Dienst auf den ATA-Gateways nicht mehr ausgeführt.

Wenn Sie vermuten, dass dies der Fall ist, prüfen Sie, ob auf dem ATA-Gateway in der Datei „Microsoft.Tri.Gateway-Errors.log“ der folgende Eintrag vorhanden ist:
`The supplied credential is invalid.`

Um dies zu korrigieren, führen Sie die folgenden Schritte zum Ändern des Domänenverbindungskennworts auf ATA Center aus:

1.  Öffnen Sie die ATA-Konsole auf ATA-Center.

2.  Wählen Sie auf der Symbolleiste die Einstellungsoption und dann **Konfiguration** aus.

    ![Symbol der ATA-Konfigurationseinstellungen](media/ATA-config-icon.JPG)

3.  Wählen Sie **Verzeichnisdienste** aus.

    ![Abbildung – Ändern des Kennworts für ATA-Gateway](media/ATA-GW-change-DC-password.png)

4.  Ändern Sie das Kennwort unter **Kennwort**.

    Wenn ATA Center eine Verbindung mit der Domäne herstellt, verwenden Sie die Schaltfläche **Verbindung testen**, um die Anmeldeinformationen zu überprüfen.

5.  Klicken Sie auf **Speichern**.

6.  Überprüfen Sie nach dem Ändern des Kennworts, ob der ATA-Gatewaydienst auf den ATA-Gatewayservern ausgeführt wird.

>[!div class="step-by-step"]
[« URL der ATA-Konsole](modifying-ata-config-consoleurl.md)

## Weitere Informationen
- [Arbeiten mit der ATA-Konsole](working-with-ata-console.md)
- [Installieren von ATA](install-ata.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Aug16_HO5-->


