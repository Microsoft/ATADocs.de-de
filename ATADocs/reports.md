---
title: Arbeiten mit ATA-Berichten
description: Beschreibt, wie Sie Berichte In ATA generieren können, um Ihr Netzwerk zu überwachen.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/27/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 38ea49b5-cd5e-43e5-bc39-5071f759633b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 4565c55a754cbbd650fff0e100e727c9c2720fc7
ms.sourcegitcommit: e844155ea57f73dfe2b47f4c5c1c7f5292ccbf1e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2020
ms.locfileid: "94690396"
---
# <a name="ata-reports"></a>ATA-Berichte

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Der Abschnitt der ATA-Berichte in der Konsole erlaubt Ihnen, Berichte zu generieren, die Ihnen Informationen zum Systemstatus sowie zur Systemintegrität und einen Bericht über verdächtige Aktivitäten, die in Ihrer Umgebung ermittelt wurden, bereitzustellen.

Um auf diese Berichtsseite zuzugreifen, klicken Sie auf das Berichtssymbol auf der Berichtsleiste: ![Berichtssymbol](media/ata-report-icon.png).
Die verfügbaren Berichte sind:

- **Zusammenfassungsbericht**: Der Zusammenfassungsbericht zeigt ein Dashboard des Status im System an. Sie können drei Registerkarten sehen: eine für eine **Zusammenfassung**, was in Ihrem Netzwerk ermittelt wurde, **Open suspicious activities** (Offene verdächtige Aktivitäten), die die verdächtigen Aktivitäten auflisten, auf die Sie achten müssen und **Open health issues** (Offene Integritätsprobleme), die Integritätsprobleme des ATA-Systems aufführen, um die Sie sich kümmern müssen. Die aufgeführten verdächtigen Aktivitäten werden nach Typ unterteilt, so auch die Integritätsprobleme.

- **Änderungen an vertraulichen Gruppen**: Dieser Bericht führt jede Änderung an vertraulichen Gruppen (z.B. Administratoren) auf.

- **Kennwörter in Klartext offengelegt**: Einige Dienste verwenden das nicht sichere LDAP-Protokoll, um Kontoanmeldeinformationen als Nur-Text zu versenden. Dies kann sogar bei sensiblen Konten geschehen. Angreifer, die Ihren Netzwerkdatenverkehr überwachen, können diese Anmeldeinformationen abfangen und diese zu böswilligen Zwecken verwenden. In diesem Bericht werden alle Quellcomputer und Kontokennwörter aufgeführt, die ATA als „als Klartext gesendet“ ermittelt hat.

- **Lateral Movement-Pfade zu sensiblen Konten**: In diesem Bericht werden die sensiblen Konten aufgeführt, die über Lateral Movement-Pfade zur Verfügung gestellt werden. Weitere Informationen finden Sie unter [lateral Movement-Pfade](use-case-lateral-movement-path.md) .

Es gibt zwei Möglichkeiten, einen Bericht zu generieren: entweder bei Bedarf oder durch Planen eines Berichts, der in regelmäßigen Abständen an Ihre E-Mail-Adresse gesendet wird.

So generieren Sie einen Bericht nach Bedarf:

1. Klicken Sie auf der Menüleiste der ATA-Konsole auf das Berichtsymbol auf der Menüleiste: ![Berichtsymbol](media/ata-report-icon.png).

1. Legen Sie unter einem der ausgewählten Berichttypen die Datumsangaben **Von** und **Bis** fest (also das Start- und Enddatum), und klicken Sie auf **Herunterladen**.
 ![Screenshot, der die Auswahl des Berichts Datums Bereichs anzeigt](media/reports.png)

So legen Sie einen geplanten Bericht fest:

1. Klicken Sie auf der Seite **Berichte** auf **Geplante Berichte festlegen** oder auf der Konfigurationsseite der ATA-Konsole unter „Benachrichtigungen und Berichte“ auf **Geplante Berichte**.

    ![Planen von Berichten](media/ata-sched-reports.png)

   > [!NOTE]
   > Die tägliche Berichte sind so konzipiert, dass sie kurz nach Mitternacht (UTC) gesendet werden.

1. Klicken Sie neben dem ausgewählten Berichttyp auf **Zeitplan**, um die Häufigkeit und E-Mail-Adresse für die Lieferung der Berichte festzulegen. Klicken Sie anschließend auf das Pluszeichen neben den E-Mail-Adressen, um sie hinzuzufügen, und klicken Sie auf **Speichern**.

    ![Häufigkeit des geplanten Berichts und E-Mail-Adresse](media/sched-report1.png)

> [!NOTE]
> Geplante Berichte werden per E-Mail übermittelt und können nur gesendet werden, wenn Sie bereits einen E-Mail-Server unter **Konfiguration** konfiguriert haben. Wählen Sie anschließend unter **Benachrichtigungen und Berichte****E-Mail-Server** aus.

## <a name="see-also"></a>Weitere Informationen

- [ATA-Voraussetzungen](ata-prerequisites.md)
- [ATA-Kapazitätsplanung](ata-capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-collection.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
