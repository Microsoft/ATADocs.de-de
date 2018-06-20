---
title: 'Installieren von Azure Advanced Threat Protection: Schritt 2 | Microsoft-Dokumentation'
description: Im zweiten Schritt der Installation von Azure ATP konfigurieren Sie die Domänenverbindungseinstellungen in Ihrem Azure ATP-Clouddienst.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ae8a95f0-278c-4a12-ae69-14282364fba1
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 11f9d5bf69ffda0843a94c7a2bb31869dc980dce
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/21/2018
ms.locfileid: "29445576"
---
*Gilt für: Azure Advanced Threat Protection*



# <a name="install-azure-atp---step-2"></a>Installieren von Azure ATP: Schritt 2

>[!div class="step-by-step"]
[« Schritt 1](install-atp-step1.md)
[Schritt 3 »](install-atp-step3.md)

## <a name="step-2-provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>Schritt 2. Angeben eines Benutzernamens und eines Kennworts, um eine Verbindung mit Ihrer Active Directory-Gesamtstruktur herzustellen

Beim ersten Öffnen des Azure ATP-Arbeitsbereichsportals wird die folgende Anzeige angezeigt:

![Azure ATP-Willkommensseite 1](media/directory-services.png)

> [!IMPORTANT]
> Die Benutzeranmeldeinformationen müssen an dieser Stelle einem Benutzerkonto im lokalen Active Directory zugeordnet sein. 


1.  Geben Sie die folgenden Informationen ein, und klicken Sie anschließend auf **Speichern**.

    |Feld|Kommentare|
    |---------|------------|
    |**Benutzername** (erforderlich)|Geben Sie den schreibgeschützten Benutzernamen ein, z.B. **ATPuser**.|
    |**Kennwort** (erforderlich)|Geben Sie das Kennwort für den schreibgeschützten Benutzer ein, z. B. **Pencil1**.|
    |**Domäne** (erforderlich)|Geben Sie die Domäne für den schreibgeschützten Benutzer ein, z. B. **contoso.com**. **Hinweis:** Es ist wichtig, dass Sie den vollqualifizierten Domänennamen (FQDN) der Domäne eingeben, in der sich das Benutzerkonto befindet. Wenn sich das Konto des Benutzers beispielsweise in der Domäne „corp.contoso.com“ befindet, müssen Sie `corp.contoso.com` und nicht „contoso.com“ eingeben.|

3. Klicken Sie im Arbeitsbereichsportal auf **Download sensor setup and install the first sensor** (Sensorsetup herunterladen und ersten Sensor installieren), um fortzufahren.


>[!div class="step-by-step"]
[« Schritt 1](install-atp-step1.md)
[Schritt 3 »](install-atp-step3.md)


## <a name="see-also"></a>Weitere Informationen
- [Azure ATP sizing tool (Azure ATP-Tool zur Größenanpassung)](http://aka.ms/aatpsizingtool)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)