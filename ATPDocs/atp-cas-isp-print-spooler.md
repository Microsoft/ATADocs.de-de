---
title: Azure Advanced Threat Protection-Bewertungen des Identitätssicherheitsstatus des Druckspoolers | Microsoft-Dokumentation
description: Dieser Artikel bietet eine Übersicht über die Berichte von Azure ATP zur Bewertung des Identitätssicherheitsstatus des Druckspoolers.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 07/08/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 1a7d9525-8923-4dae-af51-02a68aa61644
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 24077c21a6709d357a0b5b570f0d083fcd21dea8
ms.sourcegitcommit: 9673eb49729a06d3a25d52c0f43c76ac61b9cf89
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/12/2020
ms.locfileid: "75907921"
---
# <a name="security-assessment-domain-controllers-with-print-spooler-service-available"></a>Sicherheitsbewertung: Domänencontroller mit verfügbarem Druckspoolerdienst 

![Druckspoolerdienst deaktivieren](media/atp-cas-isp-print-spooler-1.png)
 
## <a name="what-is-the-print-spooler-service"></a>Was ist der Dienst **Druckspooler**? 

Der Druckspooler ist ein Softwaredienst, der Druckprozesse verwaltet. Der Spooler akzeptiert Druckaufträge von Computern und stellt sicher, dass Druckerressourcen verfügbar sind. Der Spooler plant auch die Reihenfolge, in der Druckaufträge an die Druckwarteschlange gesendet werden. In den Anfangszeiten der PCs mussten Benutzer warten, bis Dateien gedruckt waren, bevor sie andere Aktionen ausführen konnten. Dank moderner Druckspooler beeinträchtigt der Druck heute die gesamte Benutzerproduktivität nur noch minimal.

## <a name="what-risks-does-the-print-spooler-service-on-domain-controllers-introduce"></a>Welche Risiken entstehen durch den Dienst **Druckspooler** auf Domänencontrollern? 

Auf den ersten Blick sind Druckspooler harmlos, aber jeder authentifizierte Benutzer kann eine Remoteverbindung mit dem Druckspoolerdienst eines Domänencontrollers herstellen und ein Update zu neuen Druckaufträge anfordern. Darüber hinaus können Benutzer mit [uneingeschränkter Delegierung](atp-cas-isp-unconstrained-kerberos.md) den Domänencontroller anweisen, Benachrichtigungen an das System zu senden. Diese Aktionen testen die Verbindung und machen die Anmeldeinformationen des Computerkontos des Domänencontrollers verfügbar (**Druckspooler** befindet sich im Besitz von SYSTEM). 

Aufgrund der Möglichkeit, dass diese Informationen offengelegt werden, müssen Domänencontroller und Active Directory-Administratorsysteme den **Druckspoolerdienst** deaktivieren. Hierfür wird die Verwendung eines Gruppenrichtlinienobjekts (GPO) empfohlen. 

Diese Sicherheitsbewertung konzentriert sich zwar auf Domänencontroller, aber potenziell ist jeder Server der Gefahr eines Angriffs dieser Art ausgesetzt.

   > [!NOTE]
   > Untersuchen Sie unbedingt die Einstellungen, Konfigurationen und Abhängigkeiten des **Druckspoolers**, bevor Sie diesen Dienst deaktivieren und aktive Druckworkflows verhindern.

## <a name="how-do-i-use-this-security-assessment"></a>Wie wird diese Sicherheitsbewertung verwendet? 
1. Verwenden Sie die Berichtstabelle, um zu ermitteln, auf welchem Ihrer Domänencontroller der Dienst **Druckspooler** aktiviert ist.   
    <br>![Sicherheitsbewertung: Deaktivierung des Druckspoolerdiensts](media/atp-cas-isp-print-spooler-2.png)
1. Führen Sie auf dem Domänencontroller, der diesem Risiko ausgesetzt ist, entsprechende Maßnahmen durch, und entfernen Sie den Druckspoolerdienst aktiv – entweder manuell oder über ein GPO oder andere Arten von Remotebefehlen.

## <a name="remediation"></a>Wartung

Beheben Sie dieses Problem, indem Sie den Druckspoolerdienst auf allen Servern deaktivieren, für die er nicht erforderlich ist.
  

## <a name="next-steps"></a>Nächste Schritte
- [Azure ATP-Aktivitätsfilter in Cloud App Security](atp-activities-filtering-mcas.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)