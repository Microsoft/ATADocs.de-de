---
title: Bewertung der Identitäts Sicherheit von Microsoft Defender für Identitäts Druck Spooler
description: Dieser Artikel bietet eine Übersicht über die Status Bewertungsberichte von Microsoft Defender für die Identitäts Sicherheitslage.
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
ms.openlocfilehash: 3ce32384545ea3751966ba9a677348ac70fe266b
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93277506"
---
# <a name="security-assessment-domain-controllers-with-print-spooler-service-available"></a>Sicherheitsbewertung: Domänencontroller mit verfügbarem Druckspoolerdienst

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

![Druckspoolerdienst deaktivieren](media/cas-isp-print-spooler-1.png)

## <a name="what-is-the-print-spooler-service"></a>Was ist der Dienst **Druckspooler** ?

Der Druckspooler ist ein Softwaredienst, der Druckprozesse verwaltet. Der Spooler akzeptiert Druckaufträge von Computern und stellt sicher, dass Druckerressourcen verfügbar sind. Der Spooler plant auch die Reihenfolge, in der Druckaufträge an die Druckwarteschlange gesendet werden. In den Anfangszeiten der PCs mussten Benutzer warten, bis Dateien gedruckt waren, bevor sie andere Aktionen ausführen konnten. Dank moderner Druckspooler beeinträchtigt der Druck heute die gesamte Benutzerproduktivität nur noch minimal.

## <a name="what-risks-does-the-print-spooler-service-on-domain-controllers-introduce"></a>Welche Risiken entstehen durch den Dienst **Druckspooler** auf Domänencontrollern?

Auf den ersten Blick sind Druckspooler harmlos, aber jeder authentifizierte Benutzer kann eine Remoteverbindung mit dem Druckspoolerdienst eines Domänencontrollers herstellen und ein Update zu neuen Druckaufträge anfordern. Benutzer können dem Domänen Controller außerdem mitteilen, dass die Benachrichtigung an das System mit [eingeschränkter Delegierung](cas-isp-unconstrained-kerberos.md)gesendet wird. Diese Aktionen testen die Verbindung und machen die Anmeldeinformationen des Computerkontos des Domänencontrollers verfügbar ( **Druckspooler** befindet sich im Besitz von SYSTEM).

Aufgrund der Möglichkeit, dass diese Informationen offengelegt werden, müssen Domänencontroller und Active Directory-Administratorsysteme den **Druckspoolerdienst** deaktivieren. Hierfür wird die Verwendung eines Gruppenrichtlinienobjekts (GPO) empfohlen.

Diese Sicherheitsbewertung konzentriert sich zwar auf Domänencontroller, aber potenziell ist jeder Server der Gefahr eines Angriffs dieser Art ausgesetzt.

   > [!NOTE]
   > Untersuchen Sie unbedingt die Einstellungen, Konfigurationen und Abhängigkeiten des **Druckspoolers** , bevor Sie diesen Dienst deaktivieren und aktive Druckworkflows verhindern.

## <a name="how-do-i-use-this-security-assessment"></a>Wie wird diese Sicherheitsbewertung verwendet?

1. Verwenden Sie die Berichtstabelle, um zu ermitteln, auf welchem Ihrer Domänencontroller der Dienst **Druckspooler** aktiviert ist.

    ![Sicherheitsbewertung: Deaktivierung des Druckspoolerdiensts](media/cas-isp-print-spooler-2.png)
1. Führen Sie auf dem Domänencontroller, der diesem Risiko ausgesetzt ist, entsprechende Maßnahmen durch, und entfernen Sie den Druckspoolerdienst aktiv – entweder manuell oder über ein GPO oder andere Arten von Remotebefehlen.

> [!NOTE]
> Diese Bewertung wird nahezu in Echtzeit aktualisiert.

## <a name="remediation"></a>Wartung

Beheben Sie dieses Problem, indem Sie den Druckspoolerdienst auf allen Servern deaktivieren, für die er nicht erforderlich ist.

## <a name="next-steps"></a>Nächste Schritte

- [[!INCLUDE [Product short](includes/product-short.md)] Aktivitäten Filtern in Cloud App Security](activities-filtering-mcas.md)
- [Sehen Sie sich das [!INCLUDE [Product short](includes/product-short.md)] Forum an!](https://aka.ms/MDIcommunity)
