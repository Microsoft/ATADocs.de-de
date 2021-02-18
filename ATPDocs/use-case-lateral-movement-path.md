---
title: Verstehen und Verwenden von Lateral Movement-Pfaden mit Microsoft Defender for Identity
description: Dieser Artikel beschreibt die potenziellen Lateral Movement-Pfade (LMPs) von Microsoft Defender for Identity.
ms.date: 10/27/2020
ms.topic: conceptual
ms.openlocfilehash: 60fac487690d5ff71eb2df5d6ee52c15c336941e
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533442"
---
# <a name="microsoft-defender-for-identity-lateral-movement-paths-lmps"></a>Lateral Movement-Pfade (LMPs) für Microsoft Defender for Identity

> [!NOTE]
> Die auf dieser Seite erläuterten [!INCLUDE [Product long](includes/product-long.md)]-Features sind auch über das neue [Portal](https://portal.cloudappsecurity.com) zugänglich.

Lateral Movement bedeutet, dass ein Angreifer nicht sensible Konten benutzt, um über Ihr Netzwerk hinweg Zugriff auf sensible Konten zu erhalten. Lateral Movement wird von Angreifern genutzt, um Zugriff auf sensible Konten und Computer in Ihrem Netzwerk zu erhalten, die gespeicherte Anmeldeinformationen für Konten, Gruppen und Computer gemeinsam nutzen. Sobald ein Angreifer erfolgreich Lateral Moves in Richtung Ihrer wichtigsten Ziele ausführt, kann er das nutzen und sich Zugriff auf Ihre Domänencontroller verschaffen. Lateral Movement-Angriffe werden mithilfe vieler unterschiedlicher Methoden durchgeführt, die im [Handbuch zu verdächtigen Aktivitäten](suspicious-activity-guide.md) beschrieben werden.

Eine wichtige Komponente der [!INCLUDE [Product long](includes/product-long.md)]-Sicherheitserkenntnisse sind Lateral Movement-Pfade (LMPs). [!INCLUDE [Product short](includes/product-short.md)]-LMPs sind visuelle Hilfsmittel, mit denen Sie genau verstehen und bestimmen können, wie Angreifer sich seitlich in Ihrem Netzwerk bewegen können. Der Zweck von Lateral Movements innerhalb der Cyber Kill Chain ist es, über nicht sensible Konten Zugriff auf Ihre sensiblen Konten zu erhalten. Das Kompromittieren Ihrer sensiblen Konten bringt die Angreifer ihrem Hauptziel, dem Kontrollieren der Domäne, einen Schritt näher. Um zu verhindern, dass diese Angriffe Erfolg haben, stellen Ihnen [!INCLUDE [Product short](includes/product-short.md)]-LMPs einfach zu interpretierende, direkte visuelle Anleitungen für Ihre vertraulichen Konten zur Verfügung, bei denen eine Sicherheitsverletzung gravierende Folgen hätte. LMPs helfen Ihnen dabei, solche Risiken zukünftig zu minimieren bzw. ganz zu verhindern, und blockieren den Zugriff für Angreifer, bevor diese Domänendominanz erreichen können.

![Lateral Movement-Pfad (LMP) von [!INCLUDE [Product short](includes/product-short.md)]](media/lmp.png)

Lateral Movement-Angriffe können auf unterschiedliche Weise durchgeführt werden. Einige der von Angreifern am häufigsten verwendeten Methoden sind der Diebstahl von Anmeldeinformationen und Pass-the-Ticket-Angriffe. Bei beiden Methoden werden Ihre nicht sensiblen Konten von den Angreifern für Seitenangriffe genutzt, indem sie nicht sensible Computer ausnutzen, die Anmeldeinformationen gemeinsam mit Konten, Endpunktgruppen und Computern mit sensiblen Konten verwenden.

## <a name="where-can-i-find-defender-for-identity-lmps"></a>Wo finde ich Defender for Identity-LMPs?

Jeder Computer und jedes Benutzerprofil, der bzw. das sich gemäß [!INCLUDE [Product short](includes/product-short.md)]-Erkennung in einem LMP befindet, weist eine Registerkarte für **Lateral Movement-Pfade** auf. Computer und Profile, die keine Registerkarte vorweisen, wurden noch nie innerhalb einer potenziellen LMP ermittelt.

![Registerkarte für Lateral Movement-Pfade (LMPs) von [!INCLUDE [Product short](includes/product-short.md)]](media/lateral-movement-path-tab.png)

Der LMP für jede Entität bietet verschiedene Informationen abhängig von der Vertraulichkeit der Entität:

- Sensible Benutzer: potenzielle LMP(s), die zu diesem Benutzer führen, werden angezeigt.
- Nicht sensible Benutzer und Computer: mit der Entität verknüpfte potenzielle LMP(s) werden angezeigt.

Wenn Sie auf die Registerkarte klicken, zeigt [!INCLUDE [Product short](includes/product-short.md)] immer den neuesten ermittelten LMP an. Jeder potenzielle LMP wird nach der Ermittlung 48 Stunden lang gespeichert. Der LMP-Verlauf ist verfügbar. Klicken Sie auf **Anzeigen einer anderen Datumsangabe**, um ältere LMPs, die in der Vergangenheit ermittelt wurden, anzuzeigen.

![Anzeige der Lateral Movement-Pfade (LMPs) von [!INCLUDE [Product short](includes/product-short.md)]](media/lmp-complete.png)

Ermitteln Sie, wann potenzielle LMPs identifiziert wurden und welche verwandten Entitäten möglicherweise betroffen sind.

## <a name="lmp-discovery"></a>LMP-Ermittlung

Auf der Registerkarte „Aktivitäten“ werden Warnungen angezeigt, wenn neue potenzieller LMP erkannt wurden:

- Sensible Benutzer: Wenn ein neuer Pfad zu einem sensiblen Benutzer identifiziert wird

![[!INCLUDE [Product short](includes/product-short.md)] hat einen potenziellen LMP zu einem vertraulichen Benutzerkonto identifiziert](media/lmp-activities.png)

- Nicht sensible Benutzer und Computer: Wenn diese Entität in einem potenziellen LMP, der zu einem sensiblen Benutzer führt, identifiziert wird.

![[!INCLUDE [Product short](includes/product-short.md)] hat einen potenziellen LMP zu nicht einem vertraulichen Benutzerkonto identifiziert](media/lateral-non-sensitive.png)

## <a name="lmp-related-entities"></a>LMP-verwandte Entitäten

LMP können Sie jetzt direkt bei Ihrem Untersuchungsprozess unterstützen. [!INCLUDE [Product short](includes/product-short.md)]-Beweislisten für Sicherheitswarnungen geben die verwandten Entitäten an, die an jedem potenziellen Lateral Movement-Pfad beteiligt sind. Die Beweislisten können Ihrem Sicherheitsreaktionsteam direkt helfen, die Wichtigkeit der Sicherheitswarnung und/oder der Untersuchung der verwandten Entitäten zu senken oder zu erhöhen. Wenn z.B. eine Pass-the-Ticket-Warnung ausgegeben wird, sind der Quellcomputer, der kompromittierte Benutzer und der Zielcomputer, von dem aus das gestohlene Ticket benutzt wurde, alle Teil des potenziellen Lateral Movement-Pfads, der zu einem sensiblen Benutzer führt. Das Vorhandensein des identifizierten LMP macht das Untersuchen der Warnung und das Überwachen des verdächtigen Benutzers umso wichtiger, um den Angreifer an weiteren Seitenangriffe zu hindern. Nachverfolgbare Beweise werden in LMPs zur Verfügung gestellt, um Ihnen ein leichteres und schnelleres Stoppen von Angreifern zu ermöglichen, die sich durch Ihr Netzwerk bewegen.

## <a name="lateral-movement-paths-to-sensitive-accounts-report"></a>Bericht zu Lateral Movement-Pfaden zu sensiblen Konten

LMP-Daten sind auch im [Bericht zu Lateral Movement-Pfaden zu sensiblen Konten](investigate-lateral-movement-path.md) verfügbar. In diesem Bericht werden die sensiblen Konten auf,gelistet die über Lateral Movement offen gelegt wurden, und umfasst Pfade, die manuell für einen bestimmten Zeitraum ausgewählt wurden oder im Zeitraum für geplante Berichte enthalten sind.  Passen Sie den enthaltenen Datumsbereich über die Kalenderauswahl an.

## <a name="preventative-best-practices"></a>Empfohlene präventive Methoden

Mit Sicherheitserkenntnissen ist es nie zu spät, den nächsten Angriff zu verhindern und Schaden zu beheben. Aus diesem Grund bietet das Untersuchen eines Angriffs, selbst wenn die Domäne bereits eingenommen wurde, ein anderes, jedoch wichtiges Beispiel. In der Regel ist Ihr Domänencontroller während der Untersuchung einer Sicherheitswarnung möglicherweise bereits gefährdet, wie z.B. der Codeausführungen von Remotestandorten, wenn die Warnung ein richtig positives Ereignis ist. Aber LMPs informieren Sie darüber, wo sich der Angreifer Berechtigungen verschafft und welchen Pfad in Ihrem Netzwerk er benutzt hat. Auf diese Weise können LMPs auch wichtige Einblicke in mögliche Ansätze zum Abwehren oder Abschwächen derartiger Angriffe geben.

- Sie können Lateral Movement-Angriffe am besten verhindern, indem Sie sicherstellen, dass sensible Benutzer ihre Administratoranmeldeinformationen nur dann verwenden, wenn sie sich an gehärteten Computern anmelden. Überprüfen Sie in diesem Beispiel, ob der Administrator im Pfad tatsächlich Zugriff auf den gemeinsam genutzten Computer benötigt. Wenn kein Zugriff erforderlich ist, stellen Sie sicher, dass der Administrator sich nicht mit den Administrator-Anmeldeinformationen beim gemeinsam genutzten Computer anmeldet, sondern mit einem anderen Benutzernamen und Kennwort.

- Stellen Sie sicher, dass Ihre Benutzer wirklich Administratorrechte benötigen. Überprüfen Sie im Beispiel, ob alle Benutzer in der geteilten Gruppe tatsächlich Administratorrechte auf dem bereitgestellten Computer erfordern.

- Stellen Sie sicher, dass Personen nur Zugriff auf die Ressourcen haben, die sie benötigen. Im Beispiel verstärkt Ron Harper erheblich Nick Cowleys Reichweite. Ist es erforderlich, dass Ron Harper Mitglied in der Gruppe ist? Können Untergruppen erstellt werden, mit denen sich die Anfälligkeit für Lateral Movement minimieren lässt?

**Tipp**: Wenn Sie keine potenzielle Lateral Movement-Pfadaktivität für eine Entität in den letzten 48 Stunden ermitteln können, klicken Sie auf **Ein anderes Datum anzeigen**, und suchen Sie nach vorherigen potenziellen Lateral Movement-Pfaden. Der **Bericht „LMP zu sensiblen Benutzern“** ist immer verfügbar, wenn LMPs ermittelt wurden und bietet Ihnen Informationen über identifizierte potenzielle Lateral Movement-Pfade zu sensiblen Benutzern.

**Tipp**: Unter [Konfigurieren von SAM-R](install-step8-samr.md) finden Sie Informationen dazu, wie Sie Ihre Clients und Server so einrichten, dass [!INCLUDE [Product short](includes/product-short.md)] das Ausführen derjenigen SAM-R-Vorgänge erlaubt wird, die für die Erkennung von Lateral Movement-Pfaden erforderlich sind.

## <a name="investigating-lmps"></a>Untersuchen von LMPs

Anleitungen zum Identifizieren und Untersuchen mithilfe von Lateral Movement-Pfaden von [!INCLUDE [Product short](includes/product-short.md)] finden Sie unter [Untersuchen von Lateral Movement-Pfaden](investigate-lateral-movement-path.md).

## <a name="see-also"></a>Weitere Informationen

- [Untersuchen von LMPs von [!INCLUDE [Product short](includes/product-short.md)]](investigate-lateral-movement-path.md)
- [Konfigurieren von [!INCLUDE [Product short](includes/product-short.md)] für das Ausführen von Remoteaufrufen an SAM](install-step8-samr.md)
- [Arbeiten mit Sicherheitswarnungen](working-with-suspicious-activities.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
