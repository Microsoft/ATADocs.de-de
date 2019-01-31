---
title: Installieren von Azure Advanced Threat Protection | Microsoft-Dokumentation
description: Im zweiten Schritt der Installation von Azure ATP konfigurieren Sie die Domänenverbindungseinstellungen in Ihrem Azure ATP-Clouddienst.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 12/30/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ae8a95f0-278c-4a12-ae69-14282364fba1
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: ada659d86088cb9f93eba4aca54dd2553e8fb69a
ms.sourcegitcommit: 19ff0ed88e450506b5725bbcbb0d0bd2f0c5e4bb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/27/2019
ms.locfileid: "55085451"
---
# <a name="install-azure-atp---step-2"></a>Installieren von Azure ATP: Schritt 2

> [!div class="step-by-step"]
> [« Schritt 1](install-atp-step1.md)
> [Schritt 3 »](install-atp-step3.md)

## <a name="provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>Angeben eines Benutzernamens und eines Kennworts, um eine Verbindung mit Ihrer Active Directory-Gesamtstruktur herzustellen

Beim ersten Öffnen des Azure ATP-Portals wird die folgende Anzeige angezeigt:

![Azure ATP-Willkommensseite 1](media/directory-services.png)

> [!IMPORTANT]
> Die Benutzeranmeldeinformationen müssen an dieser Stelle einem Benutzerkonto im lokalen Active Directory zugeordnet sein. 


1.  Geben Sie die folgenden Informationen ein, und klicken Sie anschließend auf **Speichern**.

    |Feld|Kommentare|
    |---------|------------|
    |**Benutzername** (erforderlich)|Geben Sie den schreibgeschützten Active Directory-Benutzernamen ein. Beispiel: **ATPuser**. **Hinweis:** Verwenden Sie **nicht** das UPN-Format für Ihren Benutzernamen.|
    |**Kennwort** (erforderlich)|Geben Sie das Kennwort für den schreibgeschützten Benutzer ein. Beispiel: **Pencil1**.|
    |**Domäne** (erforderlich)|Geben Sie die Domäne für den schreibgeschützten Benutzer ein, z. B. **contoso.com**. **Hinweis:** Es ist wichtig, dass Sie den vollqualifizierten Domänennamen (FQDN) der Domäne eingeben, in der sich das Benutzerkonto befindet. Wenn sich das Konto des Benutzers beispielsweise in der Domäne „corp.contoso.com“ befindet, müssen Sie `corp.contoso.com` und nicht „contoso.com“ eingeben.|

2. Klicken Sie im Azure ATP-Portal auf **Download sensor setup and install the first sensor** (Sensorsetup herunterladen und ersten Sensor installieren), um fortzufahren.


> [!div class="step-by-step"]
> [« Schritt 1](install-atp-step1.md)
> [Schritt 3 »](install-atp-step3.md)


## <a name="see-also"></a>Weitere Informationen
- [Azure ATP sizing tool (Azure ATP-Tool zur Größenanpassung)](http://aka.ms/aatpsizingtool)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)