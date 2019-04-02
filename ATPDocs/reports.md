---
title: Arbeiten mit Azure ATP-Berichten | Microsoft-Dokumentation
description: Beschreibt, wie Sie Berichte in Azure ATP generieren können, um Ihr Netzwerk zu überwachen.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 11/26/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2c2d6b1a-fc8c-4ff7-b07d-64ce6159f84d
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2cee80ba0806882aa61dd0eab413c97039840cfe
ms.sourcegitcommit: b468d9060eb784c16b64a9cc46dbe2d246046cdd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/30/2019
ms.locfileid: "58674553"
---
# <a name="azure-atp-reports"></a>Azure ATP-Berichte

Über den Abschnitt „Azure ATP-Berichte“ im Azure ATP-Portal können Sie Berichte, die Ihnen System- und Entitätsstatusinformationen liefern, entweder planen oder sofort generieren und herunterladen. Mit dem Berichtsfeature können Sie Berichte zur Systemintegrität, zu Sicherheitswarnungen und potenziellen Lateral Movement-Pfaden erstellen, die in Ihrer Umgebung erkannt wurden.


Um auf diese Berichtsseite zuzugreifen, klicken Sie auf das Berichtssymbol auf der Berichtsleiste: ![Berichtssymbol](./media/atp-report-icon.png).
Folgende Berichte stehen zur Verfügung: 

- **Zusammenfassungsbericht**: Der Zusammenfassungsbericht zeigt ein Dashboard des Status im System an. Sie können drei Registerkarten sehen: eine für eine **Zusammenfassung** dazu, was in Ihrem Netzwerk ermittelt wurde, eine mit dem Namen **Offene verdächtige Aktivitäten**, in der die verdächtigen Aktivitäten aufgelistet werden, auf die Sie achten müssen, und eine mit dem Namen **Offene Integritätsprobleme**, in der Integritätsprobleme mit Azure ATP aufgeführt sind, um die Sie sich kümmern sollten. Die aufgeführten verdächtigen Aktivitäten werden nach Typ unterteilt, so auch die Integritätsprobleme. 

- **Änderung sensibler Gruppen**: Dieser Bericht führt jede Änderung an sensiblen Gruppen auf (z. B. Administratoren oder manuell markierte Konten oder Gruppen). Wenn Sie eigenständige Azure ATP-Sensoren verwenden, müssen Sie sicherstellen, dass [Ereignisse von Ihren Domänencontrollern an die eigenständigen Sensoren weitergeleitet werden](configure-event-forwarding.md), damit Sie einen vollständigen Bericht zu Ihren sensiblen Gruppen erhalten. 

- **Kennwörter in Klartext offengelegt**: Einige Dienste verwenden das nicht sichere LDAP-Protokoll, um Kontoanmeldeinformationen als Nur-Text zu versenden. Dies kann sogar bei sensiblen Konten geschehen. Angreifer, die Ihren Netzwerkdatenverkehr überwachen, können diese Anmeldeinformationen abfangen und diese zu böswilligen Zwecken verwenden. In diesem Bericht werden alle Quellcomputer- und Kontokennwörter aufgeführt, die Azure ATP als „als Klartext gesendet“ ermittelt hat. 

- **Lateral Movement-Pfade zu sensiblen Konten**: In diesem Bericht werden die sensiblen Konten aufgeführt, die über Lateral Movement-Pfade zur Verfügung gestellt werden. Weitere Informationen erhalten Sie unter [Lateral Movement-Pfade](use-case-lateral-movement-path.md). Dieser Bericht erfasst potenzielle Lateral Movement-Pfade, die im von Ihnen gewählten Berichtszeitraum erkannt wurden. 

Es gibt zwei Möglichkeiten, einen Bericht zu generieren: entweder bei Bedarf oder durch Planen eines Berichts, der in regelmäßigen Abständen an Ihre E-Mail-Adresse gesendet wird.

So generieren Sie einen Bericht nach Bedarf:

1. Klicken Sie im Azure ATP-Portal in der Menüleiste auf das Berichtsymbol: ![Berichtsymbol](./media/atp-report-icon.png).

2. Legen Sie unter Ihrem ausgewählten Berichtstypen die Datumsangaben **Von** und **Bis** fest (also das Start- und Enddatum), und klicken Sie auf **Herunterladen**. 
 ![Berichte](./media/reports.png)

So legen Sie einen geplanten Bericht fest:
 
1. Klicken Sie auf der Seite **Berichte** auf **Geplante Berichte festlegen** oder auf der Konfigurationsseite des Azure ATP-Portals unter „Benachrichtigungen und Berichte“ auf **Geplante Berichte**.

   ![Planen von Berichten](./media/atp-sched-reports.png)
 
   > [!NOTE]
   > Tägliche Berichte sind standardmäßig so konzipiert, dass sie kurz nach Mitternacht (UTC) gesendet werden. Wählen Sie mit der Zeitauswahloption Ihre eigene Uhrzeit aus. 

2. Klicken Sie auf **Zeitplan** neben dem ausgewählten Berichtstyp zum Festlegen der Häufigkeit und der E-Mail-Adresse für die Zustellung der Berichte. Die ausgewählte Berichtshäufigkeit bestimmt die im Bericht enthaltenen Informationen. Klicken sie auf das Pluszeichen neben dem E-Mail-Adressenfeld, geben Sie die Adresse ein und klicken Sie auf **Speichern**, um E-Mail-Adressen hinzuzufügen.

   ![Häufigkeit des geplanten Berichts und E-Mail-Adresse](./media/sched-report1.png)


## <a name="see-also"></a>Weitere Informationen
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Azure ATP capacity planning (Azure ATP-Kapazitätsplanung)](atp-capacity-planning.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-forwarding.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
