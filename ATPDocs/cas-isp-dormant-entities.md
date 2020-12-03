---
title: Sicherheitsbewertungen für inaktive Identitäts Entitäten von Microsoft Defender
description: Dieser Artikel bietet eine Übersicht über die ruhenden Entitäten von Microsoft Defender für die Identität in sensiblen Gruppen Identity Security-statusbewertungen.
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: e96b7af917f898c7ef9f701b7e7ffda1cf001598
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/03/2020
ms.locfileid: "96544197"
---
# <a name="security-assessment-dormant-entities-in-sensitive-groups"></a>Sicherheitsbewertung: Ruhende Entitäten in **sensiblen** Gruppen

## <a name="what-are-sensitive-dormant-entities"></a>Was sind **sensible** ruhende Entitäten?

[!INCLUDE [Product long](includes/product-long.md)] ermittelt, ob bestimmte Benutzer **sensibel** sind, und stellt Attribute bereit, die verfügbar sind, wenn Sie inaktiv, deaktiviert oder abgelaufen sind.

**Sensible** Konten können jedoch auch *inaktiv* (ruhend) werden, wenn sie für einen Zeitraum von 180 Tagen nicht verwendet werden. Ruhende [sensible Entitäten](sensitive-accounts.md) sind Ziele für böswillige Akteure, um Zugriff auf vertrauliche Daten Ihrer Organisation zu erhalten.

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
