---
title: Arbeiten mit ATA-Berichten | Microsoft-Dokumentation
description: "Beschreibt, wie Sie Berichte In ATA generieren können, um Ihr Netzwerk zu überwachen."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 06/12/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 38ea49b5-cd5e-43e5-bc39-5071f759633b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 4f29dfcc8b18ff755f6c0dcdaa08eaa807b08072
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/30/2017
---
*Gilt für: Advanced Threat Analytics Version 1.8*


# ATA-Berichte
<a id="ata-reports" class="xliff"></a>

Der Abschnitt der ATA-Berichte in der Konsole erlaubt Ihnen, Berichte zu generieren, die Ihnen Informationen zum Systemstatus sowie zur Systemintegrität und einen Bericht über verdächtige Aktivitäten, die in Ihrer Umgebung ermittelt wurden, bereitzustellen.

Um auf diese Berichtsseite zuzugreifen, klicken Sie auf das Berichtssymbol auf der Berichtsleiste: ![Berichtssymbol](./media/ata-report-icon.png).
Die verfügbaren Berichte sind: 
- Zusammenfassungsbericht: Der Zusammenfassungsbericht zeigt ein Dashboard des Status im System an. Sie können drei Registerkarten sehen: eine für eine **Zusammenfassung**, was in Ihrem Netzwerk ermittelt wurde, **Open suspicious activities** (Offene verdächtige Aktivitäten), die die verdächtigen Aktivitäten auflisten, auf die Sie achten müssen und **Open health issues** (Offene Integritätsprobleme), die Integritätsprobleme des ATA-Systems aufführen, um die Sie sich kümmern müssen. Die aufgeführten verdächtigen Aktivitäten werden nach Typ unterteilt, so auch die Integritätsprobleme. 
- Änderungen an sensiblen Gruppen: Dieser Bericht führt jede Änderung an sensiblen Gruppen (z.B. Administratoren) auf.

Es gibt zwei Möglichkeiten, einen Bericht zu generieren: entweder bei Bedarf oder durch Planen eines Berichts, der in regelmäßigen Abständen an Ihre E-Mail-Adresse gesendet wird.

So generieren Sie einen Bericht nach Bedarf:

1. Klicken Sie auf der Menüleiste der ATA-Konsole auf das Berichtsymbol auf der Menüleiste: ![Berichtsymbol](./media/ata-report-icon.png).
2. Legen Sie entweder unter **Zusammenfassung** oder **Änderungen an sensiblen Gruppen** die Daten **From** (Von) und **To** (Bis) fest, und klicken Sie auf **Herunterladen**. 
![Berichte](./media/reports.png)

So legen Sie einen geplanten Bericht fest:
 
1. Klicken Sie auf der Seite **Berichte** auf **Geplante Berichte festlegen** oder auf der Konfigurationsseite der ATA-Konsole unter „Benachrichtigungen und Berichte“ auf **Geplante Berichte**.

   ![Planen von Berichten](./media/ata-sched-reports.png)

2. Klicken Sie auf **Zeitplan** neben **Zusammenfassung** oder auf **Modification to sensitive groups** (Änderungen an sensiblen Gruppen), um die Frequenz und E-Mail-Adresse für die Lieferung der Berichte festzulegen. Klicken Sie anschließend auf das Pluszeichen neben den E-Mail-Adressen, um sie hinzuzufügen, und klicken Sie auf **Speichern**.

   ![Häufigkeit des geplanten Berichts und E-Mail-Adresse](./media/sched-report1.png)


> [!NOTE]
> Geplante Berichte können per E-Mail übermittelt werden und können nur gesendet werden, wenn Sie schon einen E-Mail-Server unter **Konfiguration** konfiguriert haben. Wählen Sie anschließend unter „Benachrichtigungen und Berichte“ **E-Mail-Server** aus.


## Weitere Informationen
<a id="see-also" class="xliff"></a>
- [Voraussetzungen für ATA](ata-prerequisites.md)
- [ATA-Kapazitätsplanung](ata-capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-collection.md#configuring-windows-event-forwarding)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
