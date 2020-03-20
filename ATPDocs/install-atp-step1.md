---
title: 'Schnellstart: Erstellen einer Azure ATP-Instanz'
description: In diesem Schnellstart erstellen Sie die Instanz für Ihre Azure ATP-Bereitstellung. Dabei handelt es sich um den ersten Schritt für die Installation von Azure ATP.
keywords: ''
author: shsagir
ms.author: shsagir
ms.date: 10/31/2019
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 5638e10a23ae9ddec744d7730283c17be5fab322
ms.sourcegitcommit: 11fff9d4ebf1c50b04f7789a22c80cdbc3e4416a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2020
ms.locfileid: "79413756"
---
# <a name="quickstart-create-your-azure-atp-instance"></a>Schnellstart: Erstellen einer Azure ATP-Instanz

In diesem Schnellstart erstellen Sie eine Azure ATP-Instanz im Azure ATP-Portal. In Azure ATP verfügen Sie über eine einzelne Instanz, die zuvor als Arbeitsbereich bezeichnet wurde. Über diese Instanz können Sie mehrere Gesamtstrukturen von einer einzelnen zentralen Konsole aus verwalten.

> [!IMPORTANT]
> Derzeit werden Azure ATP-Rechenzentren in Europa, Nordamerika/Mittelamerika/Karibik und Asien bereitgestellt. Ihre Instanz wird automatisch in dem Rechenzentrum erstellt, das Ihrer Azure Active Directory-Instanz (Azure AD) geografisch am nächsten liegt. Nach der Erstellung können Azure ATP-Instanzen nicht verschoben werden.

## <a name="prerequisites"></a>Voraussetzungen

- Eine [Azure ATP-Lizenz](atp-technical-faq.md#licensing-and-privacy)
- Damit Sie auf das Azure ATP-Portal zugreifen können, müssen Sie [globaler Administrator oder Sicherheitsadministrator auf diesem Mandanten](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#available-roles) sein.
- Lesen Sie den Artikel [Azure ATP-Architektur](atp-architecture.md).
- Lesen Sie den Artikel [Voraussetzungen für Azure ATP](atp-prerequisites.md). 

## <a name="sign-in-to-the-azure-atp-portal"></a>Melden Sie sich beim Azure ATP-Portal an.

Nachdem Sie überprüft haben, ob Ihr Netzwerk den Anforderungen des Sensors entspricht, können Sie mit der Erstellung der Azure ATP-Instanz beginnen.

1. Navigieren Sie zum [Azure ATP-Portal](https://portal.atp.azure.com)*.

2. Melden Sie sich mit Ihrem Azure Active Directory-Benutzerkonto an.

* GCC High-Kunden müssen das [Azure ATP GCC High](http://portal.atp.azure.us)-Portal verwenden.  

## <a name="create-your-instance"></a>Erstellen Ihrer Instanz

1. Klicken Sie auf **Instanz erstellen**. 

    ![Erstellen Ihrer Azure ATP-Instanz](media/create-instance.png)

2. Ihre Azure ATP-Instanz wird automatisch nach dem ursprünglichen Azure AD-Domänennamen benannt und in dem Rechenzentrum erstellt, das Ihrer Azure AD-Instanz geografisch am nächsten liegt. 

    ![Azure-Instanz erstellt](media/instance-created.png)

    > [!NOTE]
    > Wenn Sie sich bei Azure ATP anmelden möchten, müssen Sie sich mit einem Benutzer anmelden, dem eine Azure ATP-Rolle mit Rechten für den Zugriff auf das Azure ATP-Portal zugewiesen wurde. Weitere Informationen zur rollenbasierten Zugriffssteuerung in Azure ATP finden Sie unter [Working with Azure ATP role groups (Arbeiten mit Azure ATP-Rollengruppen)](atp-role-groups.md).
 
3. Klicken Sie auf **Konfiguration**, **Rollengruppen verwalten**, und verwenden Sie den Link [Azure AD Admin Center](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal), um Ihre Rollengruppen zu verwalten.

    ![Rollengruppen verwalten](media/creation-manage-role-groups.png)

- Datenaufbewahrung: Zuvor gelöschte Azure ATP-Instanzen werden nicht auf der Benutzeroberfläche angezeigt. Weitere Informationen zur Datenaufbewahrung in Azure ATP finden Sie unter [Sicherheit und Datenschutz für Azure ATP](atp-privacy-compliance.md).

## <a name="next-steps"></a>Nächste Schritte

> [!div class="step-by-step"]
> [« Voraussetzungen für Azure ATP](atp-prerequisites.md)
> [Installieren von Azure ATP: Schritt 2 »](install-atp-step2.md)

## <a name="join-the-community"></a>Beitritt zur Community

Haben Sie weitere Fragen, oder möchten Sie mit anderen über Azure ATP und damit verbundene Sicherheitsaspekte diskutieren? Treten Sie noch heute der [Azure ATP-Community](https://aka.ms/azureatpcommunity) bei!

