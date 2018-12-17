---
title: Installieren von Azure Advanced Threat Protection | Microsoft-Dokumentation
description: Der erste Schritt zur Installation von Azure ATP umfasst das Erstellen der Instanz für Ihre Azure ATP-Bereitstellung.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 12/02/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 15ee7d0b-9a0c-46b9-bc71-98d0b4619ed0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: e027e57e3f23be61139217b532b3b4a721dc9cdd
ms.sourcegitcommit: d1c9c3e69b196f6086a8f100e527553cf0d95aac
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/10/2018
ms.locfileid: "53125148"
---
*Gilt für: Azure Advanced Threat Protection*


# <a name="creating-your-azure-atp-instance-in-the-azure-atp-portal---step-1"></a>Erstellen Ihrer Azure ATP-Instanz im Azure ATP-Portal – Schritt 1

> [!div class="step-by-step"]
> [Schritt 2 »](install-atp-step2.md)

Diese Installationsschritte enthalten Anweisungen zum Erstellen und Verwalten Ihrer Azure ATP-Instanz (bisher als Arbeitsbereich bezeichnet). Weitere Informationen zur Azure ATP-Architektur finden Sie unter [Azure ATP architecture (Azure ATP-Architektur)](atp-architecture.md).

In Azure ATP verfügen Sie über eine einzelne Instanz, die Ihnen die Verwaltung mehrerer Strukturen von einer einzelnen zentralen Konsole aus hilft. 

> [!NOTE]
> Derzeit werden Azure ATP-Rechenzentren in Europa, Nordamerika/Mittelamerika/Karibik und Asien bereitgestellt. Ihre Instanz wird automatisch in dem Rechenzentrum erstellt, das Ihrem AAD geografisch am nächsten liegt. Nach der Erstellung können Azure ATP-Instanzen nicht verschoben werden. 

## <a name="step-1-enter-the-azure-atp-portal"></a>Schritt 1: Öffnen Sie das Azure ATP-Portal

Nachdem Sie überprüft haben, ob Ihr Netzwerk den Anforderungen des Sensors entspricht, können Sie mit der Erstellung der Azure ATP-Instanz fortfahren.

> [!NOTE]
>Damit Sie auf das Azure ATP-Portal zugreifen können, müssen Sie ein globaler Administrator, ein Sicherheitsadministrator oder der Mandant sein.


1.  Wechseln Sie ins [Azure ATP-Portal](https://portal.atp.azure.com).

2.  Melden Sie sich mit ihrem Azure Active Directory-Benutzerkonto an.

## <a name="step-2-create-your-instance"></a>Schritt 2. Erstellen Ihrer Instanz

1. Klicken Sie auf **Instanz erstellen**. 

    ![Erstellen Ihrer Azure ATP-Instanz](media/create-instance.png)

2. Ihre Azure-ATP-Instanz wird automatisch mit dem ursprünglichen AAD-Domänennamen benannt und dem Rechenzentrum zugewiesen, das sich am nächsten zu Ihrem AAD befindet und erstellt wurde. 

    ![Azure-Instanz erstellt](media/instance-created.png)

    > [!NOTE]
    > Um sich bei Azure ATP anzumelden, müssen Sie sich mit einem Benutzer anmelden, dem eine Azure ATP-Rolle mit Rechten für den Zugriff auf das Azure ATP-Portal zugewiesen wurde. Weitere Informationen zur rollenbasierten Zugriffssteuerung in Azure ATP finden Sie unter [Working with Azure ATP role groups (Arbeiten mit Azure ATP-Rollengruppen)](atp-role-groups.md).
 
3. Klicken Sie auf **Konfiguration**, **Rollengruppen verwalten**, und verwenden Sie den Link [Azure AD Admin Center](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal), um Ihre Rollengruppen zu verwalten. .

    ![Rollengruppen verwalten](media/creation-manage-role-groups.png)

- Datenaufbewahrung – Zuvor gelöschte Azure ATP-Instanzen werden nicht auf der Benutzeroberfläche angezeigt. Weitere Informationen zur Datenaufbewahrung in Azure ATP finden Sie unter [Sicherheit und Datenschutz für Azure ATP](atp-privacy-compliance.md).


>[!div class="step-by-step"]
[« Vor der Installation](atp-prerequisites.md)
[Schritt 2 »](install-atp-step2.md)



## <a name="see-also"></a>Weitere Informationen
- [Azure ATP sizing tool (Azure ATP-Tool zur Größenanpassung)](http://aka.ms/aatpsizingtool)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
