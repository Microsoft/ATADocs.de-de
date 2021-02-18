---
title: Verwenden von Microsoft Defender for Identity-Berichten
description: Beschreibt, wie Sie Berichte in Microsoft Defender for Identity generieren können, um Ihr Netzwerk zu überwachen.
ms.date: 10/27/2020
ms.topic: conceptual
ms.openlocfilehash: 1d09bd832167d960323ed0422a7858e9e512c4e1
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533459"
---
# <a name="microsoft-defender-for-identity-reports"></a>Microsoft Defender for Identity: Berichte

Über den Abschnitt „[!INCLUDE [Product long](includes/product-long.md)]-Berichte“ im [!INCLUDE [Product short](includes/product-short.md)]-Portal können Sie Berichte, die Ihnen System- und Entitätsstatusinformationen liefern, entweder planen oder sofort generieren und herunterladen. Mit dem Berichtsfeature können Sie Berichte zur Systemintegrität, zu Sicherheitswarnungen und potenziellen Lateral Movement-Pfaden erstellen, die in Ihrer Umgebung erkannt wurden.

Um auf diese Berichtsseite zuzugreifen, klicken Sie auf das Berichtssymbol auf der Berichtsleiste: ![Berichtssymbol](media/report-icon.png).
Folgende Berichte stehen zur Verfügung:

- **Zusammenfassungsbericht**: Der Zusammenfassungsbericht zeigt ein Dashboard des Status im System an. Sie können drei Registerkarten sehen: eine für eine **Zusammenfassung** dazu, was in Ihrem Netzwerk ermittelt wurde, eine mit dem Namen **Offene verdächtige Aktivitäten**, in der die verdächtigen Aktivitäten aufgelistet werden, auf die Sie achten müssen, und eine mit dem Namen **Offene Integritätsprobleme**, in der Integritätsprobleme mit [!INCLUDE [Product short](includes/product-short.md)] aufgeführt sind, um die Sie sich kümmern sollten. Die aufgeführten verdächtigen Aktivitäten werden nach Typ unterteilt, so auch die Integritätsprobleme.

- **Änderung sensibler Gruppen**: Dieser Bericht führt jede Änderung an sensiblen Gruppen auf (z. B. Administratoren oder manuell markierte Konten oder Gruppen). Wenn Sie eigenständige [!INCLUDE [Product short](includes/product-short.md)]-Sensoren verwenden, müssen Sie sicherstellen, dass [Ereignisse von Ihren Domänencontrollern an die eigenständigen Sensoren weitergeleitet werden](configure-event-forwarding.md), damit Sie einen vollständigen Bericht zu Ihren sensiblen Gruppen erhalten.

- **Kennwörter in Klartext offengelegt**: Einige Dienste verwenden das nicht sichere LDAP-Protokoll, um Kontoanmeldeinformationen als Nur-Text zu versenden. Dies kann sogar bei sensiblen Konten geschehen. Angreifer, die Ihren Netzwerkdatenverkehr überwachen, können diese Anmeldeinformationen abfangen und diese zu böswilligen Zwecken verwenden. In diesem Bericht werden alle Quellcomputer- und Kontokennwörter aufgeführt, die [!INCLUDE [Product short](includes/product-short.md)] als „als Klartext gesendet“ ermittelt hat.

- **Lateral Movement-Pfade zu sensiblen Konten**: In diesem Bericht werden die sensiblen Konten aufgeführt, die über Lateral Movement-Pfade zur Verfügung gestellt werden. Weitere Informationen erhalten Sie unter [Lateral Movement-Pfade](use-case-lateral-movement-path.md). Dieser Bericht erfasst potenzielle Lateral Movement-Pfade, die im von Ihnen gewählten Berichtszeitraum erkannt wurden.

Es gibt zwei Möglichkeiten, einen Bericht zu generieren: entweder bei Bedarf oder durch Planen eines Berichts, der in regelmäßigen Abständen an Ihre E-Mail-Adresse gesendet wird.

So generieren Sie einen Bericht nach Bedarf:

1. Klicken Sie im [!INCLUDE [Product short](includes/product-short.md)]-Portal in der Menüleiste auf das Berichtsymbol: ![Berichtsymbol](media/report-icon.png).

1. Legen Sie unter Ihrem ausgewählten Berichtstypen die Datumsangaben **Von** und **Bis** fest (also das Start- und Enddatum), und klicken Sie auf **Herunterladen**.
 ![Screenshot: Berichtsdownload](media/reports.png)

So legen Sie einen geplanten Bericht fest:

1. Klicken Sie auf der Seite **Berichte** auf **Geplante Berichte festlegen** oder auf der Konfigurationsseite des [!INCLUDE [Product short](includes/product-short.md)]-Portals unter „Benachrichtigungen und Berichte“ auf **Geplante Berichte**.

    ![Planen von Berichten](media/sched-reports.png)

    > [!NOTE]
    > Tägliche Berichte sind standardmäßig so konzipiert, dass sie kurz nach Mitternacht (UTC) gesendet werden. Wählen Sie mit der Zeitauswahloption Ihre eigene Uhrzeit aus.

1. Klicken Sie auf **Zeitplan** neben dem ausgewählten Berichtstyp zum Festlegen der Häufigkeit und der E-Mail-Adresse für die Zustellung der Berichte. Die ausgewählte Berichtshäufigkeit bestimmt die im Bericht enthaltenen Informationen. Klicken sie auf das Pluszeichen neben dem E-Mail-Adressenfeld, geben Sie die Adresse ein und klicken Sie auf **Speichern**, um E-Mail-Adressen hinzuzufügen.

    ![Häufigkeit des geplanten Berichts und E-Mail-Adresse](media/sched-report1.png)

## <a name="see-also"></a>Weitere Informationen

- [Voraussetzungen für [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md)
- [Kapazitätsplanung für [!INCLUDE [Product short](includes/product-short.md)]](capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-forwarding.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
