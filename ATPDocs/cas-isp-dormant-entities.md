---
title: Sicherheitsbewertungen für inaktive Identitäts Entitäten von Microsoft Defender
description: Dieser Artikel bietet eine Übersicht über die ruhenden Entitäten von Microsoft Defender für die Identität in sensiblen Gruppen Identity Security-statusbewertungen.
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: 44d7cc7c7152d95230440eeef45ee42a9e11c55d
ms.sourcegitcommit: f92dca4dc3d8a25b1a06f68ac7a9f8318105bcd8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/17/2021
ms.locfileid: "100630729"
---
# <a name="security-assessment-dormant-entities-in-sensitive-groups"></a>Sicherheitsbewertung: Ruhende Entitäten in **sensiblen** Gruppen

## <a name="what-are-sensitive-dormant-entities"></a>Was sind **sensible** ruhende Entitäten?

[!INCLUDE [Product long](includes/product-long.md)] ermittelt, ob bestimmte Benutzer **sensibel** sind, und stellt Attribute bereit, die verfügbar sind, wenn Sie inaktiv, deaktiviert oder abgelaufen sind.

**Sensible** Konten können jedoch auch *inaktiv* (ruhend) werden, wenn sie für einen Zeitraum von 180 Tagen nicht verwendet werden. Ruhende [sensible Entitäten](manage-sensitive-honeytoken-accounts.md) sind Ziele für böswillige Akteure, um Zugriff auf vertrauliche Daten Ihrer Organisation zu erhalten.

## <a name="what-risk-do-dormant-entities-create-in-sensitive-groups"></a>Welches Risiko bergen ruhende Entitäten in **sensiblen Gruppen**?

Organisationen, die ihre ruhenden Benutzerkonten nicht sichern können, lassen quasi die Tür zu ihren sensiblen Daten offen.

Böswillige Akteure suchen ähnlich wie Diebe häufig in jeder Umgebung nach dem einfachsten und lautlosesten Weg. Ein einfacher und stiller Pfad in Ihrer Organisation ist die Verwendung **vertraulicher Benutzer-** und Dienst Konten, die nicht mehr verwendet werden.

Es ist unerheblich, ob es sich bei der Ursache um Mitarbeiterwechsel oder Misswirtschaft von Ressourcen handelt: Wenn Sie diesen Schritt überspringen, bleiben die empfindlichsten Entitäten Ihrer Organisation anfällig und offengelegt.

## <a name="how-do-i-use-this-security-assessment"></a>Wie wird diese Sicherheitsbewertung verwendet?

1. Verwenden Sie die Berichtstabelle, um zu ermitteln, welche Ihrer sensiblen Konten inaktiv sind.
    ![Wiederherstellen von ruhenden Entitäten in der INI-Gruppe](media/cas-isp-dormant-entities-sensitive-groups-1.png)
1. Ergreifen Sie entsprechende Maßnahmen für diese Benutzerkonten, indem Sie deren privilegierte Zugriffsrechte entfernen oder das Konto löschen.

> [!NOTE]
> Diese Bewertung wird nahezu in Echtzeit aktualisiert.

## <a name="see-also"></a>Weitere Informationen

- [[!INCLUDE [Product short](includes/product-short.md)] Aktivitäten Filtern in Cloud App Security](activities-filtering-mcas.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
