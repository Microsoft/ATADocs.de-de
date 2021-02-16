---
title: Ändern von Microsoft Defender für Identity config-Domänen Verbindungs Kennwort
description: Hier wird beschrieben, wie das Domänen Verbindungs Kennwort im eigenständigen Microsoft Defender für Identity-Sensor geändert wird.
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: 2a82226a4eda3a7db762df4e04728848f7e1958e
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533816"
---
# <a name="change-microsoft-defender-for-identity-portal-configuration---domain-connectivity-password"></a>Ändern der Konfiguration des Microsoft Defender for Identity-Portals: Domänen Verbindungs Kennwort

## <a name="change-the-domain-connectivity-password"></a>Ändern des Domänenverbindungskennworts

Wenn Sie das Domänenverbindungskennwort ändern müssen, stellen Sie sicher, dass das eingegebene Kennwort korrekt ist. Wenn dies nicht der Fall ist, wird der [!INCLUDE [Product long](includes/product-long.md)] Sensor Dienst für alle bereitgestellten Sensoren angehalten.

Wenn Sie vermuten, dass dies der Fall ist, überprüfen Sie die Datei "Microsoft. Tri. Sensor-Errors. log" auf folgende Fehler: `The supplied credential is invalid.`

Gehen Sie folgendermaßen vor, um das Domänen Verbindungs Kennwort im Portal zu aktualisieren [!INCLUDE [Product short](includes/product-short.md)] :

> [!NOTE]
> Dies ist der Benutzername und das Kennwort der lokalen Active Directory-Bereitstellung und nicht aus Azure AD.

1. Öffnen Sie das [!INCLUDE [Product short](includes/product-short.md)] Portal, indem Sie auf die Portal-URL zugreifen.

1. Wählen Sie auf der Symbolleiste die Option Einstellungen, und wählen Sie **Konfiguration** aus.

    ![Symbol für die [!INCLUDE [Product short](includes/product-short.md)]-Konfigurationseinstellungen](media/config-menu.png)

1. Wählen Sie **Verzeichnisdienste** aus.

    ![[! INCLUDE [Product Short] (includes/Produkt-Short. MD)] Image des eigenständigen Sensor Kennworts ändern](media/directory-services.png)

1. Ändern Sie das Kennwort unter **Kennwort**.

    > [!NOTE]
    > Geben Sie hier einen Active Directory-Benutzer sowie ein Kennwort ein, nicht für Azure Active Directory.

1. Klicken Sie auf **Speichern**.

1. Wählen Sie im [!INCLUDE [Product short](includes/product-short.md)]-Portal **Konfiguration** aus.
1. Wählen Sie unter **System** die Seite **Sensoren** aus, und überprüfen Sie den Status der Sensoren.

## <a name="see-also"></a>Weitere Informationen

- [Integration in Microsoft Defender für Endpunkt](integrate-mde.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
