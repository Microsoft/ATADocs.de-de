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
ms.openlocfilehash: b9dcd871fecd855a35a530f57c020fba5f3d1347
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93275867"
---
# <a name="change-product-long-portal-configuration---domain-connectivity-password"></a>[!INCLUDE [Product long](includes/product-long.md)]Portal Konfiguration ändern-Domänen Verbindungs Kennwort

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

## <a name="change-the-domain-connectivity-password"></a>Ändern des Domänenverbindungskennworts

Wenn Sie das Domänenverbindungskennwort ändern müssen, stellen Sie sicher, dass das eingegebene Kennwort korrekt ist. Wenn dies nicht der Fall ist, wird der [!INCLUDE [Product long](includes/product-long.md)] Sensor Dienst für alle bereitgestellten Sensoren angehalten.

Wenn Sie vermuten, dass dies der Fall ist, überprüfen Sie die Datei "Microsoft. Tri. Sensor-Errors. log" auf folgende Fehler: `The supplied credential is invalid.`

Gehen Sie folgendermaßen vor, um das Domänen Verbindungs Kennwort im Portal zu aktualisieren [!INCLUDE [Product short](includes/product-short.md)] :

> [!NOTE]
> Dies ist der Benutzername und das Kennwort der lokalen Active Directory-Bereitstellung und nicht aus Azure AD.

1. Öffnen Sie das [!INCLUDE [Product short](includes/product-short.md)] Portal, indem Sie auf die Portal-URL zugreifen.

1. Wählen Sie auf der Symbolleiste die Option Einstellungen, und wählen Sie **Konfiguration** aus.

    ![[! Symbol für das Hinzufügen von [Product Short] (includes/Produkt-Short. MD)] Konfigurationseinstellungen](media/config-menu.png)

1. Wählen Sie **Verzeichnisdienste** aus.

    ![[! INCLUDE [Product Short] (includes/Produkt-Short. MD)] Image des eigenständigen Sensor Kennworts ändern](media/directory-services.png)

1. Ändern Sie das Kennwort unter **Kennwort**.

    > [!NOTE]
    > Geben Sie hier einen Active Directory-Benutzer sowie ein Kennwort ein, nicht für Azure Active Directory.

1. Klicken Sie auf **Speichern**.

1. [!INCLUDE [Product short](includes/product-short.md)]Wählen Sie im Portal die Option **Konfiguration** aus.
1. Wählen Sie unter **System** die Seite **Sensoren** aus, und überprüfen Sie den Status der Sensoren.

## <a name="see-also"></a>Weitere Informationen

- [Integration mit Microsoft Defender for Endpoint](integrate-mde.md)
- [Sehen Sie sich das [!INCLUDE [Product short](includes/product-short.md)] Forum an!](https://aka.ms/MDIcommunity)
