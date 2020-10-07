---
title: Sicherheitsbewertungen von ruhenden Entitäten von Azure Advanced Threat Protection
description: Dieser Artikel bietet eine Übersicht über die ruhenden Azure ATP-Entitäten im Bericht zur Bewertung des Identitätssicherheitsstatus sensibler Gruppen.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 08/25/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2fe62047-75ef-4b2e-b4aa-72860e39b4e4
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: db289191d8520a478867c3a2ff3c1b47267e82f1
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2020
ms.locfileid: "90913183"
---
# <a name="security-assessment-dormant-entities-in-sensitive-groups"></a>Sicherheitsbewertung: Ruhende Entitäten in **sensiblen** Gruppen

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

## <a name="what-are-sensitive-dormant-entities"></a>Was sind **sensible** ruhende Entitäten?

Azure ATP ermittelt, ob bestimmte Benutzer **sensibel** sind, und stellt Attribute bereit, die verfügbar sind, wenn diese Benutzer inaktiv, deaktiviert oder abgelaufen sind.

**Sensible** Konten können jedoch auch *inaktiv* (ruhend) werden, wenn sie für einen Zeitraum von 180 Tagen nicht verwendet werden. Ruhende [sensible Entitäten](sensitive-accounts.md) sind Ziele für böswillige Akteure, um Zugriff auf vertrauliche Daten Ihrer Organisation zu erhalten.

## <a name="what-risk-do-dormant-entities-create-in-sensitive-groups"></a>Welches Risiko bergen ruhende Entitäten in **sensiblen Gruppen**?

Organisationen, die ihre ruhenden Benutzerkonten nicht sichern können, lassen quasi die Tür zu ihren sensiblen Daten offen.

Böswillige Akteure suchen ähnlich wie Diebe häufig in jeder Umgebung nach dem einfachsten und lautlosesten Weg. Der einfachste und ruhigste Weg zu Ihrer Organisation ist durch **sensible** Benutzer- und Dienstkonten, die nicht mehr verwendet werden.

Es ist unerheblich, ob es sich bei der Ursache um Mitarbeiterwechsel oder Misswirtschaft von Ressourcen handelt: Wenn Sie diesen Schritt überspringen, bleiben die empfindlichsten Entitäten Ihrer Organisation anfällig und offengelegt.

## <a name="how-do-i-use-this-security-assessment"></a>Wie wird diese Sicherheitsbewertung verwendet?

1. Verwenden Sie die Berichtstabelle, um zu ermitteln, welche Ihrer sensiblen Konten inaktiv sind.
1. Ergreifen Sie entsprechende Maßnahmen für diese Benutzerkonten, indem Sie deren privilegierte Zugriffsrechte entfernen oder das Konto löschen.

> [!NOTE]
> Diese Bewertung wird nahezu in Echtzeit aktualisiert.

## <a name="see-also"></a>Weitere Informationen

- [Verwenden von Aktivitätsfiltern und Erstellen von Aktionsrichtlinien mit Azure ATP in Microsoft Cloud App Security](activities-filtering-mcas.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)