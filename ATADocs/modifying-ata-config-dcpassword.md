---
title: Ändern der Advanced Threat Analytics-Konfiguration – Domänenverbindungskennwort | Microsoft-Dokumentation
description: Beschreibt, wie das Domänenverbindungskennwort auf dem ATA-Gateway geändert wird.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 47bd7e9cdd97d8343202be86954e82e69948afed
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/22/2018
---
*Gilt für: Advanced Threat Analytics Version 1.9*



# <a name="change-ata-configuration---domain-connectivity-password"></a>Ändern der ATA-Konfiguration – Domänenverbindungskennwort



## <a name="change-the-domain-connectivity-password"></a>Ändern des Domänenverbindungskennworts
Wenn Sie das Domänenverbindungskennwort ändern, stellen Sie sicher, dass das eingegebene Kennwort korrekt ist. Andernfalls wird der ATA-Gatewaydienst auf den ATA-Gateways nicht mehr ausgeführt.

Wenn Sie vermuten, dass dies der Fall ist, überprüfen Sie auf dem ATA-Gateway die Datei „Microsoft.Tri.Gateway-Errors.log“ auf folgende Fehler: `The supplied credential is invalid.`

Um dies zu korrigieren, führen Sie die folgenden Schritte zum Ändern des Domänenverbindungskennworts auf ATA Center aus:

1.  Öffnen Sie die ATA-Konsole auf ATA-Center.

2.  Wählen Sie auf der Symbolleiste die Einstellungsoption und dann **Konfiguration** aus.

    ![Symbol der ATA-Konfigurationseinstellungen](media/ATA-config-icon.png)

3.  Wählen Sie **Verzeichnisdienste** aus.

    ![Abbildung – Ändern des Kennworts für ATA-Gateway](media/ATA-GW-change-DC-password.png)

4.  Ändern Sie das Kennwort unter **Kennwort**.

    Wenn ATA Center über Konnektivität mit der Domäne verfügt, verwenden Sie die Schaltfläche **Verbindung testen**, um die Anmeldeinformationen zu überprüfen.

5.  Klicken Sie auf **Speichern**.

6.  Überprüfen Sie nach dem Ändern des Kennworts, ob der ATA-Gatewaydienst auf den ATA-Gatewayservern ausgeführt wird.



## <a name="see-also"></a>Weitere Informationen
- [Arbeiten mit der ATA-Konsole](working-with-ata-console.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
