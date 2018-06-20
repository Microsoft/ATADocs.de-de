---
title: Ändern der Azure Advanced Threat Protection-Konfiguration – Domänenverbindungskennwort | Microsoft-Dokumentation
description: Beschreibt, wie das Domänenverbindungskennwort auf dem eigenständigen Azure ATP-Sensor geändert wird.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/14/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: e7f065fa-1ad1-4e87-bd80-99cc695efbf5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 369f00b1b33fe509850bc331b0d5b45ae161f91c
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/21/2018
ms.locfileid: "29444826"
---
*Gilt für: Azure Advanced Threat Protection*



# <a name="change-azure-atp-workspace-portal-configuration---domain-connectivity-password"></a>Ändern der Konfiguration für das Azure ATP-Arbeitsbereichsportal – Domänenverbindungskennwort



## <a name="change-the-domain-connectivity-password"></a>Ändern des Domänenverbindungskennworts
Wenn Sie das Domänenverbindungskennwort ändern müssen, stellen Sie sicher, dass das eingegebene Kennwort korrekt ist. Wenn dies nicht der Fall ist, wird der Azure ATP-Sensordienst für alle bereitgestellten Sensoren angehalten.

Wenn Sie vermuten, dass dies der Fall ist, überprüfen Sie auf dem eigenständigen Azure ATP-Sensor die Datei „Microsoft.Tri.sensor-Errors.log“ auf folgende Fehler: `The supplied credential is invalid.`

Führen Sie die folgenden Schritte zum Aktualisieren des Domänenverbindungskennworts im Azure ATP-Arbeitsbereichsportal aus:

> [!NOTE]
> Dies ist der Benutzername und das Kennwort der lokalen Active Directory-Bereitstellung und nicht aus Azure AD.

1.  Öffnen Sie das Azure ATP-Arbeitsbereichsportal, indem Sie die Arbeitsbereichs-URL öffnen.

2.  Wählen Sie auf der Symbolleiste die Einstellungsoption und dann **Konfiguration** aus.

    ![Symbol der Azure ATP-Konfigurationseinstellungen](media/atp-config-menu.png)

3.  Wählen Sie **Verzeichnisdienste** aus.

    ![Bild der Kennwortänderung für den eigenständigen Azure ATP-Sensor](media/directory-services.png)

4.  Ändern Sie das Kennwort unter **Kennwort**.

 > [!NOTE]
 > Geben Sie hier einen Active Directory-Benutzer sowie ein Kennwort ein, nicht für Azure Active Directory.

5.  Klicken Sie auf **Speichern**.

6.  Nachdem Sie das Kennwort geändert haben, überprüfen Sie manuell, ob der eigenständige Azure ATP-Sensordienst auf den eigenständigen Azure ATP-Sensorservern ausgeführt wird.

7. Wechseln Sie im Arbeitsbereichsportal unter **Konfigurationen** zur Seite **Sensor**, und prüfen Sie den Status des Sensors.

## <a name="see-also"></a>Weitere Informationen

- [Integration in Windows Defender ATP](integrate-wd-atp.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)