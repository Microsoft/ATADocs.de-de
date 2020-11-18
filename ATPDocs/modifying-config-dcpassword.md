---
title: Ändern von Microsoft Defender für Identity config-Domänen Verbindungs Kennwort
description: Hier wird beschrieben, wie das Domänen Verbindungs Kennwort im eigenständigen Microsoft Defender für Identity-Sensor geändert wird.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: ef931c90558ffaea1a24d8682cc8091a845aeea8
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2020
ms.locfileid: "94847410"
---
# <a name="change-product-long-portal-configuration---domain-connectivity-password"></a>[!INCLUDE [Product long](includes/product-long.md)]Portal Konfiguration ändern-Domänen Verbindungs Kennwort

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
