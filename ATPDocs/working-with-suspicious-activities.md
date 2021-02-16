---
title: Arbeiten mit Sicherheitswarnungen in Microsoft Defender for Identity
description: Dieser Artikel beschreibt, wie Sie von Microsoft Defender for Identity ausgegebene Sicherheitswarnungen überprüfen.
ms.date: 10/27/2020
ms.topic: how-to
ms.openlocfilehash: cb589442143bfd78f13360c076d9f5205c0a21af
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/16/2021
ms.locfileid: "100534428"
---
# <a name="working-with-security-alerts"></a>Arbeiten mit Sicherheitswarnungen

> [!NOTE]
> Die auf dieser Seite erläuterten [!INCLUDE [Product long](includes/product-long.md)]-Features sind auch über das neue [Portal](https://portal.cloudappsecurity.com) zugänglich.

In diesem Artikel werden die Grundlagen der Arbeit mit [!INCLUDE [Product long](includes/product-long.md)]-Sicherheitswarnungen erläutert.

<a name="review-suspicious-activities-on-the-attack-time-line"></a>

## <a name="review-security-alerts-on-the-attack-timeline"></a>Überprüfen von Sicherheitswarnungen auf der Angriffszeitachse 

Nachdem Sie sich beim [!INCLUDE [Product short](includes/product-short.md)]-Portal angemeldet haben, gelangen Sie automatisch zur **Zeitachse für Sicherheitswarnungen**. Sicherheitswarnungen werden in chronologischer Reihenfolge aufgeführt, wobei sich die neueste Warnung oben auf der Zeitachse befindet.

Jede Sicherheitswarnung enthält die folgenden Informationen:

- Die beteiligten Entitäten, einschließlich Benutzer, Computer, Server, Domänencontroller und Ressourcen

- Uhrzeiten und Zeitrahmen der verdächtigen Aktivitäten, die zur Auslösung der Sicherheitswarnung geführt haben.
- Schweregrad der Warnung: Hoch, Mittel oder Niedrig.
- Status: „Offen“, „Aufgelöst“ oder „Unterdrückt“.
- Möglichkeiten:
  - Teilen der Sicherheitswarnung mit anderen Personen in Ihrer Organisation per E-Mail.
  - Herunterladen der Sicherheitswarnung im Excel-Format.

> [!NOTE]
>
> - Wenn Sie mit der Maus auf einen Benutzer oder Computer zeigen, wird ein Miniprofil der Entität angezeigt. Dieses enthält zusätzliche Informationen zur Entität und die Anzahl der Sicherheitswarnungen, mit denen die Entität verknüpft ist.
> - Durch Klicken auf eine Entität gelangen Sie zum Entitätsprofil des Benutzers oder Computers.

![Abbildung der Zeitachse der Sicherheitswarnungen von [!INCLUDE [Product short](includes/product-short.md)]](media/sa-timeline.png)

## <a name="security-alert-categories"></a>Kategorien der Sicherheitswarnungen

[!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnungen werden in die folgenden Kategorien bzw. Phasen unterteilt, ähnlich wie die Phasen in einer typischen „Kill Chain“ eines Cyberangriffs.

- [Warnungen zu Reconnaissance](reconnaissance-alerts.md)
- [Warnungen zu kompromittierten Anmeldeinformationen](compromised-credentials-alerts.md)
- [Lateral Movement-Warnungen](lateral-movement-alerts.md)
- [Warnungen zu Domänendominanz](domain-dominance-alerts.md)
- [Warnungen zu Exfiltration](exfiltration-alerts.md)

## <a name="preview-detections"></a>Vorschau von Erkennungsfunktionen 

Das [!INCLUDE [Product short](includes/product-short.md)]-Forschungsteam arbeitet kontinuierlich daran, neue Erkennungen für neu entdeckte Angriffe zu implementieren. Da es sich bei [!INCLUDE [Product short](includes/product-short.md)] um einen Clouddienst handelt, werden neue Erkennungen schnell veröffentlicht, damit [!INCLUDE [Product short](includes/product-short.md)]-Kunden so schnell wie möglich davon profitieren können.

Diese Erkennungen werden als Vorschauversionen markiert, damit Sie die neuen Erkennungen schneller ermitteln können und wissen, dass sie neu für das Produkt sind. Wenn Sie die Erkennung von Vorschauversionen deaktivieren, werden diese Versionen in der [!INCLUDE [Product short](includes/product-short.md)]-Konsole (sowie auf der Zeitachse oder in den Entitätsprofilen) nicht mehr angezeigt, und es werden keine neuen Warnungen mehr geöffnet.

![Erkennung von Vorschauversionen auf der Zeitachse](media/preview-detection-in-timeline.png)

Die Erkennung von Vorschauversionen ist in [!INCLUDE [Product short](includes/product-short.md)] standardmäßig aktiviert.

Gehen Sie wie folgt vor, um die Erkennung von Vorschauversionen zu deaktivieren:

1. Klicken Sie in der [!INCLUDE [Product short](includes/product-short.md)]-Konsole auf **Konfiguration**.
1. Klicken Sie im Menü auf der linken Seite unter **Vorschauversion** auf **Erkennungen**.
1. Verwenden Sie den Schieberegler, um die Erkennungen für Vorschauversionen zu (de)aktivieren.

![Erkennungen von Vorschauversionen](media/preview-detections.png)

## <a name="filter-security-alerts-list"></a>Filtern der Liste der Sicherheitswarnungen

So filtern Sie die Liste der Sicherheitswarnungen:

1. Wählen Sie auf der linken Seite des Bildschirms im Bereich **Filtern nach** eine der folgenden Optionen aus: **Alle**, **Offen**, **Geschlossen** oder **Unterdrückt**.

1. Um die Liste weiter zu filtern, wählen Sie **Hoch**, **Mittel** oder **Niedrig** aus.

**Schweregrad von verdächtigen Aktivitäten**

- **Niedrig**

    Weist auf Aktivitäten hin, die zu Angriffen durch böswillige Benutzer oder Software führen können, um Zugriff auf Organisationsdaten zu erlangen.

- **Mittel**

    Weist auf Aktivitäten hin, die für bestimmte Identitäten das Risiko schwerwiegenderer Angriffe erhöhen und zu Identitätsdiebstahl oder Berechtigungsausweitung führen können.

- **Hoch**

    Weist auf Aktivitäten hin, die zu Identitätsdiebstahl, Berechtigungsausweitung oder anderen Angriffen mit schwerwiegenden Auswirkungen führen können.

## <a name="managing-security-alerts"></a>Verwalten von Sicherheitswarnungen

Sie können den Status einer Sicherheitswarnung ändern, indem Sie auf den aktuellen Status der Sicherheitswarnung klicken und eine der folgenden Optionen auswählen: **Offen**, **Unterdrückt**, **Aufgelöst** oder **Verworfen**.
Klicken Sie dafür auf die drei Punkte in der oberen rechten Ecke einer bestimmten Warnung, um die Liste der verfügbaren Aktionen anzuzeigen.

![[!INCLUDE [Product short](includes/product-short.md)]-Aktionen für Sicherheitswarnungen](media/sa-actions.png)

**Sicherheitswarnungsstatus**

- **Offen**: Alle neuen Sicherheitswarnungen werden in dieser Liste angezeigt.

- **Auflösen**: Wird verwendet, um Sicherheitswarnungen nachzuverfolgen, die Sie identifiziert, untersucht oder entschärft haben.

- **Unterdrücken**: Durch das Unterdrücken einer Warnung wird diese für den Moment ignoriert. Sie erhalten erst dann wieder eine Warnung, wenn eine neue Instanz vorliegt. Wenn es also eine ähnliche Warnung gibt, wird diese von [!INCLUDE [Product short](includes/product-short.md)] nicht mehr geöffnet. Wenn die Warnung jedoch für sieben Tage angehalten wurde und anschließend erneut auftritt, wird eine neue Warnung geöffnet.

- **Löschen** Wenn Sie eine Warnung verwerfen, wird sie aus dem System und aus der Datenbank gelöscht und kann von Ihnen NICHT mehr wiederhergestellt werden. Nachdem Sie auf „Verwerfen“ geklickt haben, können Sie alle Sicherheitswarnungen für den gleichen Typ löschen.

- **Ausschließen**: Die Möglichkeit, eine Entität davor zu bewahren, mehr bestimmte Warnungstypen auszugeben. Sie können z. B. festlegen, dass [!INCLUDE [Product short](includes/product-short.md)] eine bestimmte Entität (Benutzer oder Computer) ausschließt, sodass für einen bestimmten Aktivitätstyp keine Warnungen mehr ausgegeben werden. Beispiele hierfür sind etwa ein bestimmter Administrator, der Remotecode ausführt, oder eine Sicherheitsüberprüfung, die eine DNS-Reconnaissance durchführt. Zusätzlich zur Möglichkeit, Ausnahmen direkt zur Sicherheitswarnung hinzuzufügen, da sie in der Zeitleiste erkannt wurde, können Sie auch auf die Seite „Konfiguration“ zu **Ausnahmen** wechseln. Für jede Sicherheitswarnung können Sie so manuell ausgeschlossene Entitäten oder Subnetze hinzufügen oder entfernen (z.B. für Pass-the-Ticket).

> [!NOTE]
> Die Konfigurationsseiten können nur von [!INCLUDE [Product short](includes/product-short.md)]-Administratoren bearbeitet werden.

## <a name="see-also"></a>Weitere Informationen

- [Arbeiten mit dem [!INCLUDE [Product short](includes/product-short.md)]-Portal](workspace-portal.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
