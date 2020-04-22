---
title: Arbeiten mit Sicherheitswarnungen in Azure Advanced Threat Protection
description: Beschreibt das Überprüfen von Sicherheitswarnungen, die von Azure ATP ausgegeben werden
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 01/26/2020
ms.topic: article
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: a06004bd-9f77-4e8e-a0e5-4727d6651a0f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 98ea2a517f5cc223086ca448c8b532dd29257d78
ms.sourcegitcommit: 63be53de5b84eabdeb8c006438dab45bd35a4ab7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "79410561"
---
# <a name="working-with-security-alerts"></a>Arbeiten mit Sicherheitswarnungen

> [!NOTE]
> Die auf dieser Seite erläuterten Azure ATP-Features sind auch über das neue [Portal](https://portal.cloudappsecurity.com) zugänglich.

In diesem Artikel werden die Grundlagen der Arbeit mit Azure ATP-Sicherheitswarnungen erläutert.

## <a name="review-security-alerts-on-the-attack-timeline"></a>Überprüfen von Sicherheitswarnungen auf der Angriffszeitachse <a name="review-suspicious-activities-on-the-attack-time-line"></a>

Nachdem Sie sich beim Azure ATP-Portal angemeldet haben, gelangen Sie automatisch zur **Zeitachse für Sicherheitswarnungen**. Sicherheitswarnungen werden in chronologischer Reihenfolge aufgeführt, wobei sich die neueste Warnung oben auf der Zeitachse befindet.

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

![Abbildung der Zeitachse für Azure ATP-Sicherheitswarnungen](media/atp-sa-timeline.png)

## <a name="security-alert-categories"></a>Kategorien der Sicherheitswarnungen

Azure ATP-Sicherheitswarnungen werden in die folgenden Kategorien oder Phasen unterteilt, wie die Phasen in einer typischen „Kill Chain“ eines Cyberangriffs.

- [Warnungen zu Reconnaissance](atp-reconnaissance-alerts.md)
- [Warnungen zu kompromittierten Anmeldeinformationen](atp-compromised-credentials-alerts.md)
- [Lateral Movement-Warnungen](atp-lateral-movement-alerts.md)
- [Warnungen zu Domänendominanz](atp-domain-dominance-alerts.md)
- [Warnungen zu Exfiltration](atp-exfiltration-alerts.md)

## <a name="preview-detections"></a>Vorschau von Erkennungsfunktionen <a name="preview-detections"></a>

Das Azure ATP-Forschungsteam arbeitet kontinuierlich daran, neue Erkennungen für neu entdeckte Angriffe zu implementieren. Da es sich bei Azure ATP um einen Clouddienst handelt, werden neue Erkennungen schnell veröffentlicht, damit Azure ATP-Kunden so schnell wie möglich von diesen profitieren können.

Diese Erkennungen werden als Vorschauversionen markiert, damit Sie die neuen Erkennungen schneller ermitteln können und wissen, dass sie neu für das Produkt sind. Wenn Sie die Erkennungen von Vorschauversionen deaktivieren, werden diese nicht mehr in der Azure ATP-Konsole (und auch nicht auf der Zeitachse oder in den Entitätsprofilen) angezeigt, und es werden keine Warnungen mehr geöffnet.

![Vorschauversion für VPN-Erkennungen](./media/preview-detection-vpn.png)

Erkennungen von Vorschauversionen werden standardmäßig in Azure ATP aktiviert.

Gehen Sie wie folgt vor, um die Erkennung von Vorschauversionen zu deaktivieren:

1. Klicken Sie in der Azure ATP-Konsole auf das Zahnradsymbol für Einstellungen.
2. Klicken Sie im Menü auf der linken Seite unter „Vorschauversion“ auf **Erkennungen**.
3. Verwenden Sie den Schieberegler, um die Erkennungen für Vorschauversionen zu (de)aktivieren.

![Erkennungen von Vorschauversionen](./media/preview-detections.png)

## <a name="filter-security-alerts-list"></a>Filtern der Liste der Sicherheitswarnungen

So filtern Sie die Liste der Sicherheitswarnungen:

1. Wählen Sie auf der linken Seite des Bildschirms im Bereich **Filtern nach** eine der folgenden Optionen aus: **Alle**, **Offen**, **Geschlossen** oder **Unterdrückt**.

2. Um die Liste weiter zu filtern, wählen Sie **Hoch**, **Mittel** oder **Niedrig** aus.

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

![Azure ATP-Aktionen für Sicherheitswarnungen](./media/atp-sa-actions.png)

**Sicherheitswarnungsstatus**

- **Offen**: Alle neuen Sicherheitswarnungen werden in dieser Liste angezeigt.

- **Auflösen**: Wird verwendet, um Sicherheitswarnungen nachzuverfolgen, die Sie identifiziert, untersucht oder entschärft haben.

- **Unterdrücken**: Durch das Unterdrücken einer Warnung wird diese für den Moment ignoriert. Sie erhalten erst dann wieder eine Warnung, wenn eine neue Instanz vorliegt. Wenn es also eine ähnliche Warnung gibt, wird diese von Azure ATP nicht erneut geöffnet. Wenn die Warnung jedoch für sieben Tage angehalten wurde und anschließend erneut auftritt, wird eine neue Warnung geöffnet.

- **Löschen** Wenn Sie eine Warnung verwerfen, wird sie aus dem System und aus der Datenbank gelöscht und kann von Ihnen NICHT mehr wiederhergestellt werden. Nachdem Sie auf „Verwerfen“ geklickt haben, können Sie alle Sicherheitswarnungen für den gleichen Typ löschen.

- **Ausschließen**: Die Möglichkeit, eine Entität davor zu bewahren, mehr bestimmte Warnungstypen auszugeben. Sie können z.B. Azure ATP darauf festlegen, eine bestimmte Entität (Benutzer oder Computer) auszuschließen, sodass diese keine Warnung für einen bestimmten Typ einer Aktivität ausgibt, wie etwa ein bestimmter Administrator, der Remote-Code oder eine Sicherheitsüberprüfung ausführt, die DNS-Reconnaissance durchführt. Zusätzlich zur Möglichkeit, Ausnahmen direkt zur Sicherheitswarnung hinzuzufügen, da sie in der Zeitleiste erkannt wurde, können Sie auch auf die Seite „Konfiguration“ zu **Ausnahmen** wechseln. Für jede Sicherheitswarnung können Sie so manuell ausgeschlossene Entitäten oder Subnetze hinzufügen oder entfernen (z.B. für Pass-the-Ticket).

> [!NOTE]
> Die Seiten für die Konfiguration können nur von Azure ATP-Administratoren bearbeitet werden.

## <a name="see-also"></a>Weitere Informationen

- [Arbeiten mit dem Azure ATP-Portal](workspace-portal.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
