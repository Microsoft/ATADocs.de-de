---
title: Arbeiten mit Azure ATP-Berichten | Microsoft-Dokumentation
description: Beschreibt, wie Sie Berichte in Azure ATP generieren können, um Ihr Netzwerk zu überwachen.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/27/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 2c2d6b1a-fc8c-4ff7-b07d-64ce6159f84d
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 8d9c7f9208ce76e6c2ca915729b9c64f769ae7bd
ms.sourcegitcommit: 158bf048d549342f2d4689f98ab11f397d9525a2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
ms.locfileid: "30202288"
---
*Gilt für: Azure Advanced Threat Protection*


# <a name="azure-atp-reports"></a>Azure ATP-Berichte

Über den Abschnitt der Azure ATP-Berichte im Arbeitsbereichsportal können Sie Berichte generieren, die Ihnen Informationen zum Systemstatus sowie zur Systemintegrität und einen Bericht über verdächtige Aktivitäten bereitstellen, die in Ihrer Umgebung ermittelt wurden.


Um auf diese Berichtsseite zuzugreifen, klicken Sie auf das Berichtssymbol auf der Berichtsleiste: ![Berichtssymbol](./media/atp-report-icon.png).
Die verfügbaren Berichte sind: 

- **Zusammenfassungsbericht:** Der Zusammenfassungsbericht zeigt ein Dashboard des Status im System an. Sie können drei Registerkarten sehen: eine für eine **Zusammenfassung** dazu, was in Ihrem Netzwerk ermittelt wurde, eine mit dem Namen **Offene verdächtige Aktivitäten**, in der die verdächtigen Aktivitäten aufgelistet werden, auf die Sie achten müssen, und eine mit dem Namen **Offene Integritätsprobleme**, in der Integritätsprobleme mit Azure ATP aufgeführt sind, um die Sie sich kümmern sollten. Die aufgeführten verdächtigen Aktivitäten werden nach Typ unterteilt, so auch die Integritätsprobleme. 

- **Änderung sensibler Gruppen:** Dieser Bericht führt jede Änderung an sensiblen Gruppen auf (z.B. Administratoren oder manuell markierte Konten oder Gruppen). Wenn Sie eigenständige Azure ATP-Sensoren verwenden, müssen Sie sicherstellen, dass [Ereignisse von Ihren Domänencontrollern an eigenständige Sensoren weitergeleitet werden](configure-event-forwarding.md), damit Sie einen vollständigen Bericht zu Ihren sensiblen Gruppen erhalten. 

- **Kennwörter in Klartext offengelegt:** Einige Dienste verwenden das nicht gesicherte LDAP-Protokoll, um Kontoanmeldeinformationen in Nur-Text zu versenden. Dies kann sogar bei sensiblen Konten geschehen. Angreifer, die Ihren Netzwerkdatenverkehr überwachen, können diese Anmeldeinformationen abfangen und diese zu böswilligen Zwecken verwenden. In diesem Bericht werden alle Quellcomputer und Kontokennwörter aufgeführt, die Azure ATP als „als Klartext gesendet“ ermittelt hat. 

- **Lateral Movement-Pfade zu sensiblen Konten:** In diesem Bericht werden die sensiblen Konten aufgeführt, die über Lateral Movement-Pfade zur Verfügung gestellt werden. Weitere Informationen erhalten Sie unter [Lateral Movement-Pfade](use-case-lateral-movement-path.md). Dieser Bericht erfasst Pfade, die in den letzten 60 Tagen erstellt wurden. Im Gegensatz dazu werden im Arbeitsbereichsportal nur Informationen der letzten zwei Tage angezeigt.

Es gibt zwei Möglichkeiten, einen Bericht zu generieren: entweder bei Bedarf oder durch Planen eines Berichts, der in regelmäßigen Abständen an Ihre E-Mail-Adresse gesendet wird.

So generieren Sie einen Bericht nach Bedarf:

1. Klicken Sie im Azure ATP-Arbeitsbereichsportal in der Menüleiste auf das Berichtsymbol: ![Berichtsymbol](./media/atp-report-icon.png).

2. Legen Sie unter einem der ausgewählten Berichttypen die Datumsangaben **Von** und **Bis** fest (also das Start- und Enddatum), und klicken Sie auf **Herunterladen**. 
 ![Berichte](./media/reports.png)

So legen Sie einen geplanten Bericht fest:
 
1. Klicken Sie auf der Seite **Berichte** auf **Geplante Berichte festlegen** oder auf der Konfigurationsseite des Azure ATP-Arbeitsbereichs unter „Benachrichtigungen und Berichte“ auf **Geplante Berichte**.

   ![Planen von Berichten](./media/atp-sched-reports.png)
 
 > [!NOTE]
 > Die tägliche Berichte sind so konzipiert, dass sie kurz nach Mitternacht (UTC) gesendet werden.

2. Klicken Sie neben dem ausgewählten Berichttyp auf **Zeitplan**, um die Häufigkeit und E-Mail-Adresse für die Lieferung der Berichte festzulegen. Klicken Sie anschließend auf das Pluszeichen neben den E-Mail-Adressen, um sie hinzuzufügen, und klicken Sie auf **Speichern**.

   ![Häufigkeit des geplanten Berichts und E-Mail-Adresse](./media/sched-report1.png)


## <a name="see-also"></a>Weitere Informationen
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Azure ATP capacity planning (Azure ATP-Kapazitätsplanung)](atp-capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)