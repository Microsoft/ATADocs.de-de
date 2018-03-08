---
title: "Ausschließen von Entitäten von der Erkennung in Azure Advanced Threat Protection | Microsoft-Dokumentation"
description: "Beschreibt, wie Sie verhindern, dass Azure ATP bestimmte Entitätsaktivitäten als verdächtige Aktivitäten erkennt."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: cae3ed45-8fbc-4f25-ba24-3cc407c6ea93
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 60a2fae0ef044993786fb3b7e2d21a3ac27bb9f0
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/21/2018
---
*Gilt für: Azure Advanced Threat Protection*



# <a name="excluding-entities-from-detections"></a>Ausschließen von Entitäten von der Erkennung
Dieser Artikel erläutert, wie Sie Entitäten ausschließen, sodass diese keine Warnungen auslösen. So können Sie unbedenkliche wahr-positive Ergebnisse minimieren, aber gleichzeitig sicherstellen, dass wahr-positive Ergebnisse festgestellt werden. Um zu verhindern, dass Azure ATP Warnungen bei Aktivitäten ausgibt, die bei bestimmten Benutzern zu Ihrem ganz normalen Geschäftsalltag gehören, können Sie bestimmte Entitäten ausschließen, sodass diese keine Warnungen auslösen.

Beispiele: Ein Sicherheitsscanner führt eine DNS-Reconnaissance aus, oder ein Administrator führt remote Skripts auf dem Domänencontroller aus. Beides sind sanktionierte Aktivitäten, die im Rahmen des alltäglichen IT-Betriebs in Ihrer Organisation durchgeführt werden. Weitere Informationen zu Erkennungen in Azure ATP, die Ihnen dabei helfen, zu entscheiden, welche Entitäten ausgeschlossen werden sollen, finden Sie im [Handbuch zu verdächtigen Aktivitäten](suspicious-activity-guide.md).

So schließen Sie Entitäten aus, damit diese keine Warnungen in Azure ATP auslösen:

Es gibt zwei Möglichkeiten, Entitäten ausschließen: in der verdächtigen Aktivität selbst oder über die Registerkarte **Ausschlüsse** auf der Seite **Konfiguration**.

- **In der verdächtigen Aktivität**: Wenn Sie eine Warnung zu einer Aktivität eines Benutzers, eines Computers oder einer IP-Adresse erhalten, der bzw. die diese bestimmte Aktivität ausführen darf und dies möglicherweise häufig tut, klicken Sie in der Zeitachse mit verdächtigen Aktivitäten auf diese Entität, und wählen Sie **Schließen und ausschließen**. <br></br>Dadurch wird der Benutzer, der Computer oder die IP-Adresse der Ausschlussliste für diese verdächtige Aktivität hinzugefügt. Die verdächtige Aktivität wird geschlossen und in der **Zeitachse für verdächtige Aktivitäten** nicht mehr in der Liste der **offenen** Ereignisse aufgeführt.

    ![Ausschließen einer Entität](./media/exclude-in-sa.png)

- **Auf der Konfigurationsseite**: Um Ausschlüsse zu überprüfen oder zu ändern, klicken Sie auf der Seite **Konfiguration** auf **Ausschlüsse**, und wählen Sie die verdächtige Aktivität aus, z.B. **DNS-Reconnaissance**.

    ![Konfiguration von Ausschlüssen](./media/exclusions.png)

So fügen Sie eine Entität aus der Konfiguration **Ausschlüsse** hinzu: Geben Sie den Identitätsnamen ein, und klicken Sie auf das Pluszeichen. Klicken Sie anschließend am unteren Seitenrand auf **Speichern**.

Um eine Entität aus der Konfiguration der **Ausschlüsse** zu entfernen, klicken Sie auf das Minuszeichen neben dem Namen der Entität, und klicken Sie dann unten auf der Seite auf **Speichern**.

Es wird empfohlen, Ausschlüsse erst zu Erkennungen hinzuzufügen, nachdem Sie Warnungen des entsprechenden Typs erhalten haben und entscheiden können, dass diese tatsächlich unbedenklich wahr positiv sind. 

> [!NOTE]
> Zu Ihrem Schutz bieten nicht alle Erkennungen die Möglichkeit, Ausschlüsse festzulegen. 

Einige Erkennungen bieten Tipps, die Sie bei der Entscheidung unterstützen, was Sie ausschließen können. 

Jeder Ausschluss richtet sich nach dem Kontext. In einigen Kontexten können Sie Benutzer festlegen, in anderen Computer oder IP-Adressen. 

Wenn Sie die Möglichkeit haben, eine IP-Adresse oder einen Computer auszuschließen, können Sie eine der beiden Entitäten auswählen – Sie müssen nicht beide angeben.

> [!NOTE]
> Die Seiten für die Konfiguration können nur von Azure ATP-Administratoren bearbeitet werden.


## <a name="see-also"></a>Weitere Informationen

- [Integration in Windows Defender ATP](integrate-wd-atp.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)