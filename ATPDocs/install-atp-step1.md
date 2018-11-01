---
title: Installieren von Azure Advanced Threat Protection | Microsoft-Dokumentation
description: Der erste Schritt zur Installation von Azure ATP umfasst das Erstellen der Instanz für Ihre Azure ATP-Bereitstellung.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/4/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 15ee7d0b-9a0c-46b9-bc71-98d0b4619ed0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7a7bdd045a0964c4ed4ccc4ebe2315b3c3465be2
ms.sourcegitcommit: c10a1c5d1e5408b5473a31485346915908688680
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/29/2018
ms.locfileid: "50208101"
---
*Gilt für: Azure Advanced Threat Protection*


# <a name="creating-your-azure-atp-instance-in-the-portal---step-1"></a>Schritt 1: Erstellen einer Azure ATP-Instanz im Portal

> [!div class="step-by-step"]
> [Schritt 2 »](install-atp-step2.md)

Diese Installationsschritte enthalten Anweisungen zum Erstellen und Verwalten Ihrer Azure ATP-Instanz oder Ihres -Arbeitsbereichs. Weitere Informationen zur Azure ATP-Architektur finden Sie unter [Azure ATP architecture (Azure ATP-Architektur)](atp-architecture.md).

In Azure ATP verfügen Sie über eine einzelne Instanz bzw. einen einzelnen Arbeitsbereich, der Ihnen die Verwaltung mehrerer Strukturen von einer einzelnen zentralen Konsole aus hilft. 

> [!NOTE]
> Derzeit werden Azure ATP-Rechenzentren in Europa, Nordamerika/Mittelamerika/Karibik und Asien bereitgestellt.

## <a name="step-1-enter-the-azure-atp-portal"></a>Schritt 1: Öffnen Sie das Azure ATP-Portal

Nachdem Sie überprüft haben, ob Ihr Netzwerk den Anforderungen des Sensors entspricht, können Sie mit der Erstellung des Azure ATP-Arbeitsbereichs fortfahren.

> [!NOTE]
>Damit Sie auf das Verwaltungsportal zugreifen können, müssen Sie ein globaler Administrator, ein Sicherheitsadministrator oder der Mandant sein.


1.  Wechseln Sie ins [Azure ATP-Portal](https://portal.atp.azure.com).

2.  Melden Sie sich mit ihrem Azure Active Directory-Benutzerkonto an.

## <a name="step-2-create-your-workspace"></a>Schritt 2. Erstellen Ihres Arbeitsbereichs

1. Klicken Sie auf **Arbeitsbereich erstellen**.

2. Benennen Sie im Dialogfeld **Neuen Arbeitsbereich erstellen** Ihren Arbeitsbereich, und wählen Sie eine **Geolocation** für Ihr Rechenzentrum aus. Ihr Arbeitsbereich ist standardmäßig der **primäre** Arbeitsbereich. 
 > [!NOTE]
 > Nachdem Sie eine Geolocation festgelegt haben, können Sie sie nicht mehr ändern.
    ![Azure ATP-Arbeitsbereich](media/create-workspace.png)

3. Klicken Sie auf den Link **Zuweisen von Administratorrollen in Azure Active Directory**, um direkt auf das [Azure Active Directory Admin Center](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) zuzugreifen und Ihre Rollengruppen zu verwalten.

 > [!NOTE]
 > Für eine erfolgreiche Anmeldung in Azure ATP müssen Sie sich mit einem Benutzernamen anmelden, der der richtigen Azure ATP-Rolle zugewiesen wurde. Erst dann können Sie auf das Azure ATP-Portal zugreifen. Weitere Informationen zur rollenbasierten Zugriffssteuerung in Azure ATP finden Sie unter [Working with Azure ATP role groups (Arbeiten mit Azure ATP-Rollengruppen)](atp-role-groups.md).

4. Klicken Sie auf den Namen Ihres Arbeitsbereichs, um auf das Azure ATP-Portal zuzugreifen.

    ![Azure ATP-Arbeitsbereiche](media/atp-workspaces.png)

- Es kann nur der primäre Arbeitsbereich bearbeitet werden. Wenn Sie Ihren primären Arbeitsbereich löschen möchten, müssen Sie zunächst die Integrationen deaktivieren. Vorher kann er nicht gelöscht werden.

- Datenaufbewahrung: Zuvor gelöschte Arbeitsbereiche werden nicht auf der Benutzeroberfläche angezeigt. Weitere Informationen zur Datenaufbewahrung in Azure ATP finden Sie unter [Sicherheit und Datenschutz für Azure ATP](atp-privacy-compliance.md).

> [!div class="step-by-step"]
> [« Vor der Installation](atp-prerequisites.md)
> [Schritt 2 »](install-atp-step2.md)



## <a name="see-also"></a>Weitere Informationen
- [Azure ATP sizing tool (Azure ATP-Tool zur Größenanpassung)](http://aka.ms/aatpsizingtool)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
