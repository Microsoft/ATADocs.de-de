---
title: Installieren von Azure Advanced Threat Protection – Schritt 1 | Microsoft-Dokumentation
description: Der erste Schritt zur Installation von Azure ATP umfasst das Erstellen eines Arbeitsbereichs für Ihre Azure ATP-Bereitstellung.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/10/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 15ee7d0b-9a0c-46b9-bc71-98d0b4619ed0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a4c2f03955eddb4615b347fa8a211501546e6f4a
ms.sourcegitcommit: e0209c6db649a1ced8303bb1692596b9a19db60d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
ms.locfileid: "31007269"
---
*Gilt für: Azure Advanced Threat Protection*


# <a name="creating-a-workspace-in-the-azure-atp-workspace-management-portal---step-1"></a>Erstellen eines Arbeitsbereichs im Arbeitsbereich-Verwaltungsportal für Azure ATP – Schritt 1

>[!div class="step-by-step"]
[Schritt 2 »](install-atp-step2.md)

Diese Installationsschritte enthalten Anweisungen zum Erstellen und Verwalten eines Arbeitsbereichs im Arbeitsbereich-Verwaltungsportal für Azure ATP. Weitere Informationen zur Azure ATP-Architektur finden Sie unter [Azure ATP architecture (Azure ATP-Architektur)](atp-architecture.md).

Bei Azure ATP haben Sie die Möglichkeit, mehrere Arbeitsbereiche zu verwalten und zu überwachen. Dies ist besonders hilfreich, wenn Sie einen Demo-Arbeitsbereich und einen Testarbeitsbereich erstellen möchten, in denen Sie vor dem Rollout für Ihre gesamte Organisation einen Proof of Concept für Azure ATP durchführen können. Dies ist auch erforderlich, um Bereitstellungen mit mehreren Gesamtstrukturen zu unterstützen. Ein einzelner Arbeitsbereich kann nur mehrere Domänen aus einer einzelnen Gesamtstruktur überwachen. 

> [!NOTE]
> - Sie können maximal zwei aktive Arbeitsbereiche haben. Nachdem Sie einen Arbeitsbereich gelöscht haben, können Sie den Support kontaktieren, um den Arbeitsbereich erneut zu aktivieren. Sie können maximal drei Arbeitsbereiche löschen. Kontaktieren Sie den Azure ATP-Support, um die Anzahl an gespeicherten bzw. gelöschten Arbeitsbereichen zu erhöhen.
> - Derzeit werden Azure ATP-Rechenzentren in Europa, Nordamerika/Mittelamerika/Karibik und Asien bereitgestellt.

## <a name="step-1-enter-the-workspace-management-portal"></a>Schritt 1: Ins Portal zur Verwaltung von Arbeitsbereichen wechseln

Nachdem Sie überprüft haben, ob Ihr Netzwerk den Anforderungen des Sensors entspricht, können Sie mit der Erstellung des Azure ATP-Arbeitsbereichs fortfahren.

> [!NOTE]
>Damit Sie auf das Portal zur Verwaltung von Arbeitsbereichen zugreifen können, müssen Sie ein globaler Administrator, ein Sicherheitsadministrator oder der Mandant sein.


1.  Wechseln Sie ins [Azure ATP-Arbeitsbereichsportal](https://portal.atp.azure.com).

2.  Melden Sie sich mit ihrem Azure Active Directory-Benutzerkonto an.

## <a name="step-2-create-a-workspace"></a>Schritt 2. Erstellen eines Arbeitsbereichs

1. Klicken Sie auf **Arbeitsbereich erstellen**.

2. Benennen Sie im Dialogfeld **Neuen Arbeitsbereich erstellen** Ihren Arbeitsbereich, entscheiden Sie sich, ob es sich dabei um Ihren primären Arbeitsbereich handelt oder nicht, und wählen Sie eine **Geolocation** für Ihr Rechenzentrum. Sie können nur einen Arbeitsbereich als „Primär“ festlegen. Wenn Sie einen Arbeitsbereich als „Primär“ festlegen, hat dies Konsequenzen für die Integration: Sie können nur für Ihren primären Arbeitsbereich Azure ATP in Windows Defender ATP integrieren. Sie können auch später einen anderen Arbeitsbereich als „Primär“ kennzeichnen. Dafür müssen Sie zuvor jedoch bereits für den aktuellen Arbeitsbereich vorgenommene Integrationen entfernen.
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

- Datenaufbewahrung: Gelöschte Arbeitsbereiche werden nicht auf der Benutzeroberfläche angezeigt. Die Daten werden jedoch gemäß der [Microsoft-Richtlinie zur Datenaufbewahrung](https://www.microsoft.com/trustcenter/privacy/you-own-your-data) aufbewahrt.


>[!div class="step-by-step"]
[« Vor der Installation](configure-port-mirroring.md)
[Schritt 2 »](install-atp-step2.md)


## <a name="see-also"></a>Weitere Informationen
- [Azure ATP sizing tool (Azure ATP-Tool zur Größenanpassung)](http://aka.ms/aatpsizingtool)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)
