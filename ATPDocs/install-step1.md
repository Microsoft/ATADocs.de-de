---
title: 'Schnellstart: Erstellen einer Microsoft Defender for Identity-Instanz'
description: In diesem Schnellstart erstellen Sie die Instanz für Ihre Microsoft Defender for Identity-Bereitstellung. Dabei handelt es sich um den ersten Schritt für die Installation von Defender for Identity.
keywords: ''
author: shsagir
ms.author: shsagir
ms.date: 10/26/2020
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 50307054535447326b8b48641afaeec7cfc70551
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93277115"
---
# <a name="quickstart-create-your-product-long-instance"></a>Schnellstart: Erstellen Ihrer [!INCLUDE [Product long](includes/product-long.md)]-Instanz

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

In diesem Schnellstart erstellen Sie Ihre [!INCLUDE [Product long](includes/product-long.md)]-Instanz im [!INCLUDE [Product short](includes/product-short.md)]-Portal. In [!INCLUDE [Product short](includes/product-short.md)] verfügen Sie über eine einzelne Instanz, die zuvor als Arbeitsbereich bezeichnet wurde. Über diese Instanz können Sie mehrere Gesamtstrukturen von einer einzelnen zentralen Konsole aus verwalten.

> [!IMPORTANT]
> Derzeit werden [!INCLUDE [Product short](includes/product-short.md)]-Rechenzentren in Europa, dem Vereinigten Königreich, Nordamerika/Mittelamerika/Karibik und Asien bereitgestellt. Ihre Instanz wird automatisch in dem Rechenzentrum erstellt, das Ihrer Azure Active Directory-Instanz (Azure AD) geografisch am nächsten liegt. Nach der Erstellung können [!INCLUDE [Product short](includes/product-short.md)]-Instanzen nicht verschoben werden.

## <a name="prerequisites"></a>Voraussetzungen

- Eine [[!INCLUDE [Product long](includes/product-long.md)]-Lizenz](technical-faq.md#licensing-and-privacy)
- Damit Sie auf das [!INCLUDE [Product short](includes/product-short.md)]-Portal zugreifen können, müssen Sie [globaler Administrator oder Sicherheitsadministrator auf diesem Mandanten](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#available-roles) sein.
- Lesen Sie den Artikel [[!INCLUDE [Product short](includes/product-short.md)]-Architektur](architecture.md).
- Lesen Sie den Artikel [[!INCLUDE [Product short](includes/product-short.md)]-Voraussetzungen](prerequisites.md).

## <a name="sign-in-to-the-product-short-portal"></a>Anmelden beim [!INCLUDE [Product short](includes/product-short.md)]-Portal

Nachdem Sie überprüft haben, ob Ihr Netzwerk den Anforderungen des Sensors entspricht, können Sie mit der Erstellung der [!INCLUDE [Product short](includes/product-short.md)]-Instanz beginnen.

1. Öffnen Sie [das [!INCLUDE [Product short](includes/product-short.md)]-Portal](https://portal.atp.azure.com).

1. Melden Sie sich mit Ihrem Azure Active Directory-Benutzerkonto an.

\*-GCC High-Kunden müssen das [[!INCLUDE [Product short](includes/product-short.md)]-GCC High](http://portal.atp.azure.us)-Portal verwenden.

## <a name="create-your-instance"></a>Erstellen Ihrer Instanz

1. Klicken Sie auf **Instanz erstellen**.

    ![[!INCLUDE [Product short](includes/product-short.md)]-Instanz erstellen](media/create-instance.png)

1. Ihre [!INCLUDE [Product short](includes/product-short.md)]-Instanz wird automatisch nach dem ursprünglichen Azure AD-Domänennamen benannt und in dem Rechenzentrum erstellt, das Ihrer Azure AD-Instanz geografisch am nächsten liegt.

    ![Azure-Instanz erstellt](media/instance-created.png)

    > [!NOTE]
    > Wenn Sie sich bei [!INCLUDE [Product short](includes/product-short.md)] anmelden möchten, müssen Sie sich mit einem Benutzer anmelden, dem eine [!INCLUDE [Product short](includes/product-short.md)]-Rolle mit Rechten für den Zugriff auf das [!INCLUDE [Product short](includes/product-short.md)]-Portal zugewiesen wurde. Weitere Informationen zur rollenbasierten Zugriffssteuerung in [!INCLUDE [Product short](includes/product-short.md)] finden Sie unter [Arbeiten mit [!INCLUDE [Product short](includes/product-short.md)]-Rollengruppen](role-groups.md).

1. Klicken Sie auf **Konfiguration** , **Rollengruppen verwalten** , und verwenden Sie den Link [Azure AD Admin Center](/azure/active-directory/active-directory-assign-admin-roles-azure-portal), um Ihre Rollengruppen zu verwalten.

    ![Rollengruppen verwalten](media/creation-manage-role-groups.png)

- Datenaufbewahrung: Zuvor gelöschte [!INCLUDE [Product short](includes/product-short.md)]-Instanzen werden nicht auf der Benutzeroberfläche angezeigt. Weitere Informationen zur Datenaufbewahrung in [!INCLUDE [Product short](includes/product-short.md)] finden Sie unter [Sicherheit und Datenschutz in [!INCLUDE [Product short](includes/product-short.md)]](privacy-compliance.md).

## <a name="next-steps"></a>Nächste Schritte

> [!div class="step-by-step"]
> [« Voraussetzungen für Azure ATP](prerequisites.md)
> [Installieren von Azure ATP: Schritt 2 »](install-step2.md)

## <a name="join-the-community"></a>Beitritt zur Community

Haben Sie weitere Fragen, oder möchten Sie mit anderen über [!INCLUDE [Product short](includes/product-short.md)] und damit verbundene Sicherheitsaspekte diskutieren? Treten Sie noch heute der [[!INCLUDE [Product short](includes/product-short.md)]Community](https://aka.ms/MDIcommunity) bei.
