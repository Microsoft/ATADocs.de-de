---
title: Ändern der Azure Advanced Threat Protection-Konfiguration – Domänenverbindungskennwort
description: Beschreibt, wie das Domänenverbindungskennwort auf dem eigenständigen Azure ATP-Sensor geändert wird.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 02/19/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: e7f065fa-1ad1-4e87-bd80-99cc695efbf5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 77ec242769d15eb3681f9e511709a0e6953878e8
ms.sourcegitcommit: bf5f58317121f1fb0fffc83d8b419cdd7ef27d9a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/05/2020
ms.locfileid: "80669520"
---
# <a name="change-azure-atp-portal-configuration---domain-connectivity-password"></a>Ändern der Konfiguration für das Azure ATP-Portal – Domänenverbindungskennwort

## <a name="change-the-domain-connectivity-password"></a>Ändern des Domänenverbindungskennworts

Wenn Sie das Domänenverbindungskennwort ändern müssen, stellen Sie sicher, dass das eingegebene Kennwort korrekt ist. Wenn dies nicht der Fall ist, wird der Azure ATP-Sensordienst für alle bereitgestellten Sensoren angehalten.

Wenn Sie vermuten, dass dies der Fall ist, überprüfen Sie die Datei „Microsoft.Tri.sensor-Errors.log“ auf folgende Fehler: `The supplied credential is invalid.`

Führen Sie die folgenden Schritte zum Aktualisieren des Domänenverbindungskennworts im Azure ATP-Portal aus:

> [!NOTE]
> Dies ist der Benutzername und das Kennwort der lokalen Active Directory-Bereitstellung und nicht aus Azure AD.

1. Öffnen Sie das Azure ATP-Portal, indem Sie die Portal-URL öffnen.

1. Wählen Sie auf der Symbolleiste die Einstellungsoption und dann **Konfiguration** aus.

    ![Symbol der Azure ATP-Konfigurationseinstellungen](media/atp-config-menu.png)

1. Wählen Sie **Verzeichnisdienste** aus.

    ![Bild der Kennwortänderung für den eigenständigen Azure ATP-Sensor](media/directory-services.png)

1. Ändern Sie das Kennwort unter **Kennwort**.

    > [!NOTE]
    > Geben Sie hier einen Active Directory-Benutzer sowie ein Kennwort ein, nicht für Azure Active Directory.

1. Klicken Sie auf **Speichern**.

1. Wechseln Sie im Azure ATP-Portal unter **Konfigurationen** zur Seite **Sensor**, und prüfen Sie den Status des Sensors.

## <a name="see-also"></a>Weitere Informationen

- [Integration mit Microsoft Defender ATP](integrate-wd-atp.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
