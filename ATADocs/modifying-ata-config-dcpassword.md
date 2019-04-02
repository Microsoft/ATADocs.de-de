---
title: Ändern der Advanced Threat Analytics-Konfiguration – Domänenverbindungskennwort | Microsoft-Dokumentation
description: Beschreibt, wie das Domänenverbindungskennwort auf dem ATA-Gateway geändert wird.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: barbkess
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: f53549db48720b8576e56af4b650e2384a164ca4
ms.sourcegitcommit: b468d9060eb784c16b64a9cc46dbe2d246046cdd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/30/2019
ms.locfileid: "58674162"
---
# <a name="change-ata-configuration---domain-connectivity-password"></a>Ändern der ATA-Konfiguration – Domänenverbindungskennwort

*Gilt für: Advanced Threat Analytics Version 1.9*

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
