---
title: Konfigurieren von Sam-R zum Aktivieren der Erkennung von Lateral Movement-Pfaden in Microsoft Defender für Identity
description: Erläutert das Konfigurieren von Microsoft Defender für die Identität, um Remote Aufrufe an Sam durchführen zu können.
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
ms.openlocfilehash: 9e1bfe428a466e4870613798e4af116f27d63647
ms.sourcegitcommit: 218ba562a2a109ff456b011004530f503a4e82c6
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/04/2020
ms.locfileid: "93342503"
---
# <a name="configure-product-long-to-make-remote-calls-to-sam"></a>Konfigurieren [!INCLUDE [Product long](includes/product-long.md)] von, um Remote Aufrufe an Sam durchführen

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

[!INCLUDE [Product long](includes/product-long.md)]die Erkennung von [lateral Movement](use-case-lateral-movement-path.md) -Pfaden basiert auf Abfragen, mit denen lokale Administratoren auf bestimmten Computern identifiziert werden. Diese Abfragen werden mithilfe des Sam-R-Protokolls durchgeführt, wobei das Dienst Konto verwendet wird, das [!INCLUDE [Product short](includes/product-short.md)] während der [!INCLUDE [Product short](includes/product-short.md)] Installation  [Schritt 2 erstellt wurde. Verbindung mit AD herstellen](install-step2.md).

## <a name="configure-sam-r-required-permissions"></a>Konfigurieren von für SAM-R erforderliche Berechtigungen

Um sicherzustellen, dass Windows-Clients und-Server Ihr [!INCLUDE [Product short](includes/product-short.md)] Konto Sam-R durchführen können, muss eine Änderung an **Gruppenrichtlinie** vorgenommen werden, um das [!INCLUDE [Product short](includes/product-short.md)] Dienst Konto zusätzlich zu den in der **Netzwerk Zugriffs** Richtlinie aufgeführten konfigurierten Konten hinzuzufügen. Stellen Sie sicher, dass Sie Gruppenrichtlinien auf alle Computer **außer Domänen Controllern** anwenden.

> [!Note]
> Bevor Sie neue Richtlinien wie die zuvor erwähnte erzwingen, ist es wichtig, dass Sie die Sicherheit Ihrer Umgebung gewährleisten können und dass die Änderungen sich nicht auf die Anwendungskompatibilität auswirken. Aktivieren und überprüfen Sie daher zunächst die Kompatibilität vorgeschlagener Änderungen im Überwachungsmodus, bevor Sie Änderungen an Ihrer Produktionsumgebung vornehmen.

1. Finden der Richtlinie:

   - Richtlinienname: Netzwerkzugriff: Clients einschränken, die Remoteaufrufe an SAM ausführen dürfen
   - Speicherort: Computerkonfiguration, Windows-Einstellungen, Sicherheitseinstellungen, lokale Richtlinien, Sicherheitsoptionen

    ![Finden der Richtlinie](media/samr-policy-location.png)

1. Fügen Sie den [!INCLUDE [Product short](includes/product-short.md)] Dienst der Liste genehmigter Konten hinzu, die diese Aktion auf Ihren modernen Windows-Systemen durchführen können.

    ![Hinzufügen des Diensts](media/samr-add-service.png)

3. Der **aatp-Dienst** (der [!INCLUDE [Product short](includes/product-short.md)] während der Installation erstellte Dienst) verfügt jetzt über die erforderlichen Berechtigungen, um Sam-R in der Umgebung auszuführen.

Weitere Informationen zu SAM-R und dieser Gruppenrichtlinie, finden Sie unter [Netzwerkzugriff: Clients einschränken, die Remoteaufrufe an SAM ausführen dürfen](/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).

## <a name="see-also"></a>Weitere Informationen

- [Untersuchen von Angriffen mit lateral Movement-Pfaden mit [!INCLUDE [Product short](includes/product-short.md)]](use-case-lateral-movement-path.md)
- [Sehen Sie sich das [!INCLUDE [Product short](includes/product-short.md)] Forum an!](https://aka.ms/MDIcommunity)
