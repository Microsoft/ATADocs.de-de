---
title: Richtlinie zu personenbezogenen Daten von Azure Advanced Threat Protection | Microsoft-Dokumentation
description: Dieser Artikel stellt Links zu Informationen bereit, wie Sie private Informationen und personenbezogene Daten aus Azure ATP löschen.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 10/04/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 224e629a-0e82-458c-bb03-b67070a9241d
ms.reviewer: ophirp
ms.suite: ems
ms.openlocfilehash: 6758527b61e2b1ab440898ed23aa7d507d8f3b3c
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2019
ms.locfileid: "65196813"
---
# <a name="azure-atp-data-security-and-privacy"></a>Sicherheit und Datenschutz für Azure ATP

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

## <a name="search-for-and-identify-personal-data"></a>Suchen und Identifizieren von personenbezogenen Daten 

In Azure Advanced Threat Protection können Sie identifizierbare personenbezogene Daten über die [Suchleiste](workspace-portal.md#search-bar) des [Azure ATP-Portals](workspace-portal.md) anzeigen. 

Suchen Sie einen bestimmten Benutzer oder Computer, und klicken Sie auf die Entität, um zur [Profilseite](entity-profiles.md) des Benutzers oder Computers geleitet zu werden. Die Profile stellen umfassende Details über die Entität aus Active Directory bereit, einschließlich der Netzwerkaktivität im Zusammenhang mit dieser Entität und des Verlaufs.

Personenbezogene Azure ATP-Daten werden von Active Directory über den Azure ATP-Sensor gesammelt und in einer Back-End-Datenbank gespeichert.

## <a name="update-personal-data"></a>Aktualisieren von personenbezogenen Daten 

Personenbezogene Benutzerdaten von Azure ATP werden vom Benutzerobjekt in Active Directory der Organisation abgeleitet. Aus diesem Grund spiegeln sich die Änderungen am Benutzerprofil im AD-Organisationsverzeichnis in Azure ATP wieder.


## <a name="delete-personal-data"></a>Löschen von personenbezogenen Daten 

Nachdem ein Benutzer aus dem Active Directory der Organisation gelöscht wurde, löscht Azure ATP innerhalb von einem Jahr automatisch das Benutzerprofil und sämtliche zugehörige Netzwerkaktivitäten. Sie können ebenfalls alle Sicherheitswarnungen [löschen](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line), die personenbezogene Daten enthalten. 

## <a name="export-personal-data"></a>Exportieren von personenbezogenen Daten 

In Azure ATP haben Sie die Möglichkeit, Informationen zu Sicherheitswarnung in Excel zu [exportieren](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line). Mit dieser Funktion werden außerdem die personenbezogenen Daten exportiert. 
 
## <a name="audit-personal-data"></a>Überwachen von personenbezogenen Daten

Azure ATP implementiert die Überwachung von Änderungen an personenbezogenen Daten, einschließlich der Löschung und Exportierung von personenbezogenen Datensätzen. Die Aufbewahrungszeit von Überwachungspfaden beträgt 90 Tage. Die Überwachung in Azure ATP ist ein Back-End-Feature, auf das Kunden nicht zugreifen können.
 
## <a name="additional-resources"></a>Zusätzliche Ressourcen

- Informationen zur Vertrauensstellung und Konformität von Azure ATP finden Sie im [Service Trust Portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted) und auf der Website zur [DSGVO-Konformität von Microsoft 365 Enterprise](https://docs.microsoft.com/microsoft-365/compliance/compliance-solutions-overview).
