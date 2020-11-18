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
ms.openlocfilehash: fb97959f9cffe0e80cb0d273e061a13e6b809f83
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2020
ms.locfileid: "94847767"
---
# <a name="configure-product-long-to-make-remote-calls-to-sam"></a>Konfigurieren von [!INCLUDE [Product long](includes/product-long.md)] für das Ausführen von Remoteaufrufen an SAM

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
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
