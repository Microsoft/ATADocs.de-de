---
title: Richtlinie für persönliche Daten von Microsoft Defender für Identity
description: Enthält Links zu Informationen zum Löschen von privaten Informationen und persönlichen Daten von Microsoft Defender für die Identität.
ms.date: 10/26/2020
ms.topic: conceptual
ms.openlocfilehash: b8336d4b6508fc9de462dcdbb6bc6389dd2fa0f2
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533397"
---
# <a name="microsoft-defender-for-identity-data-security-and-privacy"></a>Microsoft Defender für Identitätsdaten Sicherheit und Datenschutz

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

## <a name="security-and-privacy-for-defender-for-identity-us-government-gcc-high-customers"></a>Sicherheit und Datenschutz für Defender for Identity US Government gcc High-Kunden

Weitere Informationen zu Kompatibilitäts [!INCLUDE [Product short](includes/product-short.md)] Standards und zum Speicherort von Kundendaten für die US-Regierung gcc High-Kunden finden Sie in der [Beschreibung des Enterprise Mobility + Security für den US Government-Dienst](/enterprise-mobility-security/solutions/ems-govt-service-description).
