---
title: Richtlinie für persönliche Daten von Microsoft Defender für Identity
description: Enthält Links zu Informationen zum Löschen von privaten Informationen und persönlichen Daten von Microsoft Defender für die Identität.
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: ophir
ms.suite: ems
ms.openlocfilehash: 648d12d6135e5ab09319580142807f930e595eda
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2020
ms.locfileid: "94846968"
---
# <a name="product-long-data-security-and-privacy"></a>[!INCLUDE [Product long](includes/product-long.md)] Datensicherheit und Datenschutz

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

## <a name="search-for-and-identify-personal-data"></a>Suchen und Identifizieren von personenbezogenen Daten

In [!INCLUDE [Product short](includes/product-short.md)] können Sie mithilfe der [Suchleiste](workspace-portal.md#search-bar)identifizierbare persönliche Daten aus dem [ [!INCLUDE [Product long](includes/product-long.md)] Portal](workspace-portal.md) anzeigen.

Suchen Sie einen bestimmten Benutzer oder Computer, und klicken Sie auf die Entität, um zur [Profilseite](entity-profiles.md) des Benutzers oder Computers geleitet zu werden. Die Profile stellen umfassende Details über die Entität aus Active Directory bereit, einschließlich der Netzwerkaktivität im Zusammenhang mit dieser Entität und des Verlaufs.

[!INCLUDE [Product short](includes/product-short.md)] persönliche Daten werden von Active Directory über den [!INCLUDE [Product short](includes/product-short.md)] Sensor gesammelt und in einer Back-End-Datenbank gespeichert.

## <a name="update-personal-data"></a>Aktualisieren von personenbezogenen Daten

[!INCLUDE [Product short](includes/product-short.md)]personenbezogene Benutzerdaten werden aus dem-Objekt des Benutzers in der Active Directory der Organisation abgeleitet. Daher werden Änderungen, die am Benutzerprofil in der Organisations-AD vorgenommen werden, in widergespiegelt [!INCLUDE [Product short](includes/product-short.md)] .

## <a name="delete-personal-data"></a>Löschen von personenbezogenen Daten

- Nachdem ein Benutzer aus der Active Directory der Organisation gelöscht wurde, [!INCLUDE [Product short](includes/product-short.md)] löscht automatisch das Benutzerprofil und alle zugehörigen Netzwerkaktivitäten innerhalb eines Jahres. Sie können ebenfalls alle Sicherheitswarnungen [löschen](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line), die personenbezogene Daten enthalten.

- Es wird **schreibgeschützter Zugriff** auf den Container mit **gelöschten Objekten** empfohlen. Weitere Informationen dazu, wie die * * Deleted Objects-Container Berechtigung vom Dienst verwendet wird [!INCLUDE [Product short](includes/product-short.md)] , finden Sie in der Empfehlung zu den Container für gelöschte Objekte unter [ [!INCLUDE [Product short](includes/product-short.md)] Voraussetzungen](prerequisites.md#before-you-start).

## <a name="export-personal-data"></a>Exportieren von personenbezogenen Daten

In [!INCLUDE [Product short](includes/product-short.md)] haben Sie die Möglichkeit, Sicherheits Warn Informationen in Excel zu [exportieren](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line) . Mit dieser Funktion werden außerdem die personenbezogenen Daten exportiert.

## <a name="audit-personal-data"></a>Überwachen von personenbezogenen Daten

[!INCLUDE [Product short](includes/product-short.md)] implementiert die Überprüfung persönlicher Datenänderungen, einschließlich des Löschens und Exportierens persönlicher Datensätze. Die Aufbewahrungszeit von Überwachungspfaden beträgt 90 Tage. Die Überwachung in [!INCLUDE [Product short](includes/product-short.md)] ist ein Back-End-Feature, auf das Kunden nicht zugreifen können.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

- Informationen zu [!INCLUDE [Product short](includes/product-short.md)] Vertrauenswürdigkeit und Konformität finden Sie im [Dienst Vertrauensstellungs Portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted) und auf der Microsoft 365 Enterprise dsgvo-Kompatibilitäts [Website](/microsoft-365/compliance/gdpr?view=o365-worldwide&preserve-view=true).

## <a name="security-and-privacy-for-product-short-us-government-gcc-high-customers"></a>Sicherheit und Datenschutz für [!INCLUDE [Product short](includes/product-short.md)] gcc High-Kunden der US-Regierung

Weitere Informationen zu Kompatibilitäts [!INCLUDE [Product short](includes/product-short.md)] Standards und zum Speicherort von Kundendaten für die US-Regierung gcc High-Kunden finden Sie in der [Beschreibung des Enterprise Mobility + Security für den US Government-Dienst](/enterprise-mobility-security/solutions/ems-govt-service-description).
