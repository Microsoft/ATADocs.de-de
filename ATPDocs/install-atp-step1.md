---
title: Installieren von Azure Advanced Threat Protection – Schritt 1 | Microsoft-Dokumentation
description: Der erste Schritt zur Installation von Azure ATP umfasst das Erstellen der Instanz für Ihre Azure ATP-Bereitstellung.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 9/04/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 15ee7d0b-9a0c-46b9-bc71-98d0b4619ed0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 9ba476c579de3c468ce9c8ca09e8b8bab4fa9e1d
ms.sourcegitcommit: f9400ae27d22607e4146dc9b8a0b9ba6f61fdd38
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/05/2018
ms.locfileid: "43743313"
---
*Gilt für: Azure Advanced Threat Protection*


# <a name="creating-a-workspace-in-the-azure-atp-workspace-management-portal---step-1"></a>Erstellen eines Arbeitsbereichs im Arbeitsbereich-Verwaltungsportal für Azure ATP – Schritt 1

>[!div class="step-by-step"]
[Schritt 2 »](install-atp-step2.md)

Diese Installationsschritte enthalten Anweisungen zum Erstellen und Verwalten Ihrer Azure ATP-Instanz. Weitere Informationen zur Azure ATP-Architektur finden Sie unter [Azure ATP architecture (Azure ATP-Architektur)](atp-architecture.md).

In Azure ATP verfügen Sie über einen einzelnen Arbeitsbereich bzw. eine einzelne Instanz, die Ihnen bei der Verwaltung mehrerer Strukturen von einer einzelnen zentralen Konsole aus hilft. 

> [!NOTE]
> Derzeit werden Azure ATP-Rechenzentren in Europa, Nordamerika/Mittelamerika/Karibik und Asien bereitgestellt.

## <a name="step-1-enter-the-management-portal"></a>Schritt 1: Zugreifen auf das Verwaltungsportal

Nachdem Sie überprüft haben, ob Ihr Netzwerk den Anforderungen des Sensors entspricht, können Sie mit der Erstellung des Azure ATP-Arbeitsbereichs fortfahren.

> [!NOTE]
>Damit Sie auf das Verwaltungsportal zugreifen können, müssen Sie ein globaler Administrator, ein Sicherheitsadministrator oder der Mandant sein.


1.  Wechseln Sie ins [Azure ATP-Portal](https://portal.atp.azure.com).

2.  Melden Sie sich mit ihrem Azure Active Directory-Benutzerkonto an.

## <a name="step-2-create-your-workspace"></a>Schritt 2. Erstellen Ihres Arbeitsbereichs

1. Klicken Sie auf **Arbeitsbereich erstellen**.

2. Benennen Sie im Dialogfeld **Neuen Arbeitsbereich erstellen** Ihren Arbeitsbereich, und wählen Sie eine **Geolocation** für Ihr Rechenzentrum aus. Sie können nur einen Arbeitsbereich als „Primär“ festlegen. Wenn Sie einen Arbeitsbereich als „Primär“ festlegen, hat dies Konsequenzen für die Integration: Sie können nur für Ihren primären Arbeitsbereich Azure ATP in Windows Defender ATP integrieren. Sie können auch später einen anderen Arbeitsbereich als „Primär“ kennzeichnen. Dafür müssen Sie zuvor jedoch bereits für den aktuellen Arbeitsbereich vorgenommene Integrationen entfernen.
 > [!NOTE]
 > Nachdem Sie eine Geolocation festgelegt haben, können Sie sie nicht mehr ändern.
    ![Azure ATP-Arbeitsbereich](media/create-workspace.png)

3. Klicken Sie auf den Link **Zuweisen von Administratorrollen in Azure Active Directory**, um direkt auf das [Azure Active Directory Admin Center](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) zuzugreifen und Ihre Rollengruppen zu verwalten.

 > [!NOTE]
 > Für eine erfolgreiche Anmeldung in Azure ATP müssen Sie sich mit einem Benutzernamen anmelden, der der richtigen Azure ATP-Rolle zugewiesen wurde. Erst dann können Sie auf das Azure ATP-Arbeitsbereichsportal zugreifen. Weitere Informationen zur rollenbasierten Zugriffssteuerung in Azure ATP finden Sie unter [Working with Azure ATP role groups (Arbeiten mit Azure ATP-Rollengruppen)](atp-role-groups.md).

4. Klicken Sie auf den Namen des neuen Arbeitsbereichs, um auf das Azure ATP-Arbeitsbereichsportal für diesen Arbeitsbereich zuzugreifen.

    ![Azure ATP-Arbeitsbereiche](media/atp-workspaces.png)

- Es kann nur der primäre Arbeitsbereich bearbeitet werden. Um Änderungen an anderen Arbeitsbereichen vorzunehmen, können Sie diese löschen und erneut hinzufügen. Wenn Sie den primären Arbeitsbereich löschen möchten, müssen Sie zunächst Integrationen deaktivieren und den Arbeitsbereich auf **Primär** festlegen, bevor er gelöscht werden kann.
- Um einen primären Arbeitsbereich zu bearbeiten, müssen Sie zunächst vorhandene Integrationen im Arbeitsbereich deaktivieren.

- Datenaufbewahrung: Gelöschte Arbeitsbereiche werden nicht auf der Benutzeroberfläche angezeigt. Weitere Informationen zur Datenaufbewahrung in Azure ATP finden Sie unter [Sicherheit und Datenschutz für Azure ATP](atp-privacy-compliance.md).


>[!div class="step-by-step"]
[« Vor der Installation](configure-port-mirroring.md)
[Schritt 2 »](install-atp-step2.md)


## <a name="see-also"></a>Weitere Informationen
- [Azure ATP sizing tool (Azure ATP-Tool zur Größenanpassung)](http://aka.ms/aatpsizingtool)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)
